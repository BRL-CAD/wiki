[category:Code examples](category:Code_examples.md) This is a
simple example program that shows how to walk a geometry database while
performing some operation on geometry as it is encountered. In this
particular example, we iterate just over regions and simply count them:

    #include "common.h"
    #include "raytrace.h"

    int incr_region(
        struct db_tree_state *tsp,
        struct db_full_path *pathp,
        const struct rt_comb_internal *combp,
        void *data)
    {
      int *counter = (int*)data;
      bu_log("...incrementing...\n");
      (*counter)++;
      return 0;
    }

    int main(int argc, char *argv[]){

      struct db_i *dbip;
      int counter = 0;
      struct db_tree_state state = rt_initial_tree_state;

      if (argc < 2) {
        bu_exit(0, "need more, db.g obj\n");
      }

      dbip = db_open(argv[1], "r");
      if (dbip == NULL) {
        bu_exit(1, "Unable to open %s\n", argv[1]);
      }

      if (db_dirbuild(dbip) < 0) {
        db_close(dbip);
        bu_exit(1, "Unable to load %s\n", argv[1]);
      }

      bu_log("Database title is:\n%s\n", dbip->dbi_title);
    //bu_log("Units: %s\n", bu_units_string(dbip->dbi_local2base));

      if (db_lookup(dbip, argv[2], 1) == NULL) {
        db_close(dbip);
        bu_exit(1, "Unable to find %s\n", argv[2]);
      }

      state.ts_dbip = dbip;
      state.ts_resp = &rt_uniresource;
      rt_init_resource( &rt_uniresource, 0, NULL );

      db_walk_tree(dbip, 1, (const char **)argv+2, 1, &state, incr_region, NULL, NULL, &counter);

      bu_log("counter is %d\n", counter);
      return 0;
    }

If we compile this program and run it on a sample geometry database, we
get the following:

    # you may need to replace /usr/brlcad with the path to where BRL-CAD is installed on your system
    $ gcc -o db_walk_tree_example -I/usr/brlcad/include -I/usr/brlcad/include/brlcad db_walk_tree_example.c -L/usr/brlcad/lib -lrt -lbu

    $ ./db_walk_tree_example db/ktank.g tank
    Database title is:
    Keith's Tank

    ...incrementing...
    <... trimmed output ...>
    ...incrementing...
    counter is 83
