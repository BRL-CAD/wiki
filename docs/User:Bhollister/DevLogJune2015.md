__FORCETOC__

------------------------------------------------------------------------

# Monday, June 1, 2015: ***Start of Week 2 (of 14)***

-   dissertation work

# Tuesday, June 2, 2015

-   dissertation work

# Wednesday, June 3, 2015

-   dissertation defense @ 12:45-2pm PDT

# Thursday, June 4, 2015

-   added callable nmg_mrsv stub, see:
    <https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/ff812753027d4119a590d9d0096f9dbb279163b0>
-   successfully defended PhD dissertation yesterday
-   minor additions / editing / proof-reading of dissertation before
    ProQuest submittal deadline of June 11th
-   todo: add remaining CONSTRUCTION routine stubs
-   todo: determine how to pass nmg model verts, etc. from command line
    (mged) to function stubs

# Friday, June 5, 2015

-   received a few pointers on NMG, and a document link in weekly mtg
-   dissertation editing

# Saturday, June 6, 2015

-   dissertation editing

# Sunday, June 7, 2015

-   dissertation editing

# Monday, June 8, 2015: ***Start of Week 3 (of 14)***

-   [commit \#1 for
    today](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/a6679978dd1f3864f280e938e92c5e7bcfeb2283):
    added remaining NMG construction command stubs
-   [commit \#2 for
    today](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/433bf2330d4455b2c6cb12eb42fb14a27b26a542):
    nmg_mrsv command now accepts a model file name and checks the
    database; removed nmg_mm since make cmd covers that functionality
-   [commit \#3 for
    today](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/027fdbc55d93e1f46a04ea627ea9c3906ae7e1f6):
    fixed format spacing for nmg_mrsv.c

# Tuesday, June 9, 2015

-   final dissertation edits
-   submitted final dissertation to ProQuest
-   delivered signatures, etc. for degree
-   took online surveys for degree
-   note \#1: (todo) need to talk to mentors about cmd line interface;
    some **construction** routines in "Combinatorial Solid Geometry,
    Boundary Representations, and Non-Manifold Geometry," are likely too
    low-level. for instance, does it make sense to specify 'vertexuse' /
    'edgeuse' at the cmd line?? possibly only routines that require user
    specified \*new\* vertices and edges will be implemented... also, we
    may not want to implement some of the api functions that only create
    empty shells / regions for new models. models can already be created
    using the cmd *make*.
-   note \#2: **construction** routines don't require passing particular
    instances of existing geometry. this makes their impl likely easier
    than **destruction** routines in terms of specifying geometry at
    the CLI.

# Wednesday, June 10, 2015

-   [commit \#1 for
    today](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/7afdc98ac418922dbcd3cbd800a7974a46a39e97?diff=split):
    added call to internal api for "Make Region, Shell, Vertex"
-   tried various testing with creating nmg geometry, but was not fully
    able to create nmg test cases with primitives. need to retry using
    "facetize" command again or another route
-   need to determine if we need a higher-level CLI than internal NMG
    access API functions; some of this is already implemented in
    nmg_simplify, nmg_fix_normals, make, etc.

# Thursday, June 11, 2015

-   [commit \#1 for
    today](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/98885604a90091a2eb9d230f7af57feab4384e60):
    added impl for nmg_mm; small fix for return code from nmg_mrsv CLI
    libged function
-   friday todo: implement nmg_mmr()
-   friday todo: implment nmg_msv() - figure out how to specify region
    and pass that to CLI from MGED display (or archer)

# Friday, June 12, 2015

-   need to attend graduation ceremonies practice for a few hours
    (starts @ 1 PM PDT, but need to pick up gown, etc.)
-   [commit \#1 for
    today](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/0a00c24701c90e292154bc53e06e107ae8f462e4):
    added impl for nmg_mmr for CLI. almost identical to ged_nmg_mm,
    but region is created for the new model.
-   [commit \#2 for
    today](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/5961a0e291b4927291a8bfe939ddb99309715613):
    added preliminary nmg_msv CLI command. command accepts model name
    and adds shell / vertex to the first region encountered via
    BU_LIST_FIRST. the command also performs NMG_CK_REGION. if a
    model doesn't have a region, then this check causes MGED to log a
    bad pointer error and crash. TODO: may need to find a way to specify
    region to CLI and handle error w/o crash.

# Saturday, June 13, 2015

-   relatives visiting thru Thursday

# Sunday, June 14, 2015

-   graduation ceremonies attendance (most of the day)

------------------------------------------------------------------------

# ***End of Spring Term @ UCSC; Now GSoC Full-time!***

------------------------------------------------------------------------

# Monday, June 15, 2015: ***Start of Week 4 (of 14)***

-   added nmg_me imp for CLI. not committed to github yet due to merge
    conflicts?? todo: fix this tomorrow!
-   read thru
    [some-thoughts-about-nmg-primitve](http://t3550.cad-brlcad-development.cadtalk.us/some-thoughts-about-the-nmg-primitive-t3550.html)
-   concerning
    [some-thoughts-about-nmg-primitve](http://t3550.cad-brlcad-development.cadtalk.us/some-thoughts-about-the-nmg-primitive-t3550.html),
    not sure if shells or regions will be specified or used on CLI.
-   todo: need to find problem with nmg_msv CLI. appears that it is not
    adding new shell to nmg data structure
-   todo: fix nmg_me CLI to allow for setting vertex coords (current
    impl only adds vertexuses via nmg_mvvu)

# Tuesday, June 16, 2015

-   [commit \#1
    yesterday](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/3f6102f573a09058c2c1e5c47ceed6227057082f):
    added nmg_me to CLI. can't currently set vertex coord but the
    vertexuses are added properly.
-   [commit \#1 for
    today](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/afeb00de7c1d5038d5eb33d59e47df5fdd0b8143):
    adding CLI version of nmg_me. command takes two vertex coords and
    the name of the model. the first region / shell are used. also,
    updating comment in ged_nmg_msv.
-   [commit \#2 for
    today](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/f0a04b7981a1d7ce85524c921a781a7a38678145):
    added ged_nmg_mvvu. routine takes first region / shell as parent
    structure in model to add vertex / vertexuse. note that a NULL
    pointer is added to the vertexuse struct. although possibly not
    clear, ged_nmg_mvu can be used to set a specific vertex instance
    for the vertexuse, i.e. a \*new\* vertexuse.
-   [commit \#3 for
    today](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/e82d939a47b4b888ce80cdec3452c8739e43fdff):
    ged_nmg_mvu impl prelim. need to find vertex with coordinates
    given on CLI. Use the parent struct of the found vertex as upptr.
    Here, this is a shell. TODO: the point of this routine is to
    re-assign a vertexuse to an \*existing\* vertex. Right now, this
    routine finds a shell with the specified vertex and replaces the
    vertexuse in that shell. we need to find a vertexuse \*not\* in a
    shell, such as an edge, and reassign it a \*new\* vertexuse. CLI
    doesn't use vertex id, so coord may be non-unique to multiple
    vertices in nmg model. IMPORTANTLY: crashing on curr_vg =
    curr_s-&gt;vu_p-&gt;v_p-&gt;vg_p; Need to fix.
-   todo: need to fix nasty white spacing issues in submitted code
    revisions!

# Wednesday, June 17, 2015

-   last day of relatives' visit. taking day off. will work some
    saturday as makeup.

# Thursday, June 18, 2015

-   [commit \#1 for
    today](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/bd3738b720ae18df38440a178e7c41efd0744fd0?diff=split):
    added ged_nmg_ml. calls nmg_ml directly with the first
    encountered region / shell in model. if shell doesn't have the
    required edgeuses / edges, then program throws and error.
-   [commit \#2 for
    today](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/3e1b8791315bd1d20d82192c956af609510b140f?diff=split):
    added ged_nmg_meonvu. user can specify a vertex coord on CLI.
    routine searches for the first encountered vertexuse that uses a
    vertex instance (coord). note: this is not what the internal api
    function is meant to do. it uses a \*vertexuse\*. todo: pass a
    \*vertexuse\* if possible from the CLI, or find another way to
    define similar construction routine that is more suitable for
    the CLI. once the vertexuse / vertex / geom is found, an "empty"
    edge with the same topological vertex(use?) is inserted into the
    model.
-   found how to properly traverse model with BU_LIST_PNEXT macro.
    todo: need to update ged_nmg_mvu to reflect this correction.

# Friday, June 19, 2015

-   received direction by mentors to add single top-level nmg CLI
    command
-   todo: move all other nmg commands as private subcommands callable
    only via single top-level CLI command
-   todo: extend nmg \*construction\* routines dev time into week 5.
    week 5 / 6 of schedule was originally allocated for \*destruction\*
    routines, but these are fewer and simpler than the \*construction\*
    subcommands for nmg; todo: update project schedule
-   todo: provide a straight-forward method to create a simple
    primitive, such as a cube using the \*new\* nmg CLI

# Saturday, June 20, 2015

-   n/a

# Sunday, June 21, 2015

-   n/a

# Monday, June 22, 2015: ***Start of Week 5 (of 14)***

-   [commit \#1 for
    today](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/c36b98e4097a44262926d55b634fbc821065e9fc?diff=split):
    added top-level nmg command stub (only usage info reported).
-   todo: will pass on CLI paramaters to appropriate subcommand
-   todo: need to add remaining destruction and manipulation subcommands
    to current stub

# Tuesday, June 23, 2015

-   [commit \#1 for
    today](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/fce10d06fa65aa5c44ddb90634ecdaec62a4bd73?diff=split):
    added subcommand handling for construction routines
-   [commit \#2 for
    today](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/b4d9a32189720b14e298988373de91ed12333efd?diff=split):
    added convenience construction and destruction stubs
-   should be able to submit patch for nmg command stub...after adding
    manipulation routines tomorrow

# Wednesday, June 24, 2015

-   investigated uses of internal nmg api. found /src/proc-db/nmgmodel.c
-   todo: need to find proper uses of internal api in order to provide
    best interface to nmg via CLI (checking with mentors)
-   suggested scaling back proposal to nmg work only (in line with
    original brlcad gsoc suggestions from wiki)

non-brlcad time expenditures...

-   birthday today, so only half-day work. will work the weekend if
    possible.
-   spent some time updating resume + applying for positions

# Thursday, June 25, 2015

-   updated project schedule to reflect NMG \*only\* work. approval by
    mentor in IRC.
-   nmgmodel.c compiles to src/proc-db/nmgmodel in the build directory
-   todo: need to further investigate /src/proc-db/nmgmodel.c as model
    for new CLI

non-brlcad time expenditures...

-   spent some time updating resume + applying for positions

# Friday, June 26, 2015

-   added patch <https://sourceforge.net/p/brlcad/patches/387/>
-   todo: for weekend, add subcommands to add faces with variable number
    of verts on commandline

# Saturday, June 27, 2015

-   n/a

# Sunday, June 28, 2015

-   n/a

# Monday, June 29, 2015: ***Start of Week 6 (of 14)***

-   updated patch 387: <https://sourceforge.net/p/brlcad/patches/387/>
-   [commit \#1 for
    today](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/35b56cfd9b07c04b9fddf2f542b8bd0d2f1200fe?diff=split):
    added extern function prototypes to fix build on some configurations
-   traced thru src/proc-db/nmgmodel.c; todo: will use that approach to
    add high-level command to add manifold quad faces to nmg model this
    week.

# Tuesday, June 30, 2015

-   [commit \#1 for
    today](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/20a5379fb8282a4731ddac283c5976d18fa0dc08?diff=split):
    added ged_nmg_cmface impl. some issues with null model when
    filling out vertices.
-   updated patch <https://sourceforge.net/p/brlcad/patches/387/> with
    UNUSED macro
-   todo: need to check patch with -DBRLCAD_ENABLE_STRICT=YES and
    resubmit fix if needed