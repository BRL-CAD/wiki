# Coding period

### *Week 14*

#### Firm pencils down day: 20/08/2012

-   Adjusted the *doc/docbook/system/mann/en/graph.xml* according to the
    changes made on the subcommands and added a brief documentation for
    the **igraph** command.

### *Week 13*

#### 19/08/2012

-   Added two subcommands for the **graph** command: **show** and
    **positions**.

<!-- -->

-   Removed the previous *graph_objects_positions* and
    *graph_structure* commands.

<!-- -->

-   Renamed the previously named Tcl *graph* procedure into **igraph** -
    this command launches the interactive graph; along with this
    procedure, the *src/tclscripts/graph* was renamed into
    *src/tclscripts/**igraph***, and the file
    *src/tclscripts/graph/graph.tcl* was renamed into
    *src/tclscripts/**igraph/igraph.tcl***.

<!-- -->

-   The **igraph** command works in MGED; when launched in Archer, an
    error message in outputted saying that the command is not available
    yet.

<!-- -->

-   Took care of some command error cases (C and Tcl).

#### 18/08/2012

-   Again tried to integrate the previously mentioned command in
    Archer - Didn't find an example that would suit me. I found commands
    that would have procedures that use C wrapped commands but they were
    either working strictly for Archer or for MGED, not for both.

#### 17/08/2012

-   Introduced a **graph** command and its **show** subcommand.

<!-- -->

-   Tried to get rid of an *"invalid command name "graph" while
    executing "graph show""* error but didn't find a solution - this
    appears when I run my procedure in Archer. When running this
    procedure in MGED, no such error appears and the graph is generated
    correctly.

#### 16/08/2012

-   Enabled error message in MGED for the **graph** command in case the
    Adaptagrams library isn't available.

<!-- -->

-   Started reorganizing the **graph** command in subcommands.

#### 15/08/2012

-   Added a basic brlman documentation for the **graph** command.

#### 14/08/2012

-   Grouped top-level commands under a single **graph** command. Came up
    with an approach on how to tackle the following problem: there would
    exist a C implemented "graph" command and also a Tcl procedure named
    "graph" and when ran in MGED the C one is ran instead of the Tcl
    one. Waiting for a response before committing the changes.

#### 13/08/2012

-   Fixed a bug that appeared when launching Archer due to the
    **graph_objects_positions** command.

<!-- -->

-   Started work on integrating the **graph** command in Archer.
    Encountered some problems due to the fact that there isn't a
    corresponding *ged_graph* C routine that can be used. The procedure
    is simply defined in Tcl.

### *Week 12*

#### 12/08/2012

-   Cleaned up the layout source code that was about to be committed.

<!-- -->

-   Replaced the connection lines that existed between two nodes with
    polylines and added arrows at the end of each connection line.

#### 11/08/2012

-   Finished creating the routines that provide a decent layout for the
    graph.

<!-- -->

-   Added vertices between the nodes.


Here is how the graph for the *share/db/axis.g* database looks like now:

![](/wiki/user/img/Graph_editor_v2.png)

<!-- -->


Commit will be made as soon as the source code is cleaned up.

#### 10/08/2012

-   Continued working on the layout part.

#### 09/08/2012

-   Started research and work for solving the layout issue of a graph.

#### 08/08/2012

-   Added the **decorate_object(struct _ged_dag_data \*, char \*,
    int)** routine in *src/libged/dag.cpp*. This creates a new entry
    into a hash table for each newly detected object and sets the
    entry's value depending on the type of object: *primitive*,
    *combination*, or *something else*.

<!-- -->

-   Used these types to differently colour the rectangles in the graph
    editor.

<!-- -->

-   Introduced a text widget with the name of the object within each
    rectangle.


Here is the window that the **graph** command launches for the
*share/db/axis.g* database:

<!-- -->


![](/wiki/user/img/Graph_editor_v1.png)

#### 06/08/2012

-   Looked for a method to store object's colour and name related
    information within an Adaptagrams graph structure.


This is needed for implementing the decorative routines for each type of
object. Couldn't find a method. Worked on an alternative method to store
this information.

### *Week 11*

#### 05/08/2012

-   Updated the **ged_graph_objects_positions** routine; it now
    passes the objects and positions within the graph to the Tcl field.

<!-- -->

-   Used this command in the *src/tclscripts/graph/GraphEditor.tcl*. The
    objects are now drawn at the specified positions using a Tk Canvas
    widget inside a window.

#### 04/08/2012

-   The **ged_graph_objects_positions** can now be used as a command
    within the Tcl field to retrieve objects' positions within the
    graph.

<!-- -->

-   Made sure that the commands **graph_structure**, and
    **graph_objects_positions** always exist so that the user is
    informed that he/she invoked a valid command, although the
    Adaptagrams library is not available.

#### 01/08/2012

-   Again tried to figure out the logic between the data processed in
    the *C* implementation of a command and the data received in the
    *tcl* file when running this command.

<!-- -->

-   Finally got the idea after having a talk with **starseeker**.

#### 30/07/2012

-   Looked for a pattern to follow in the implementation of *C* commands
    that are to be used in the Tcl land. Found the files that need to be
    modified according to the existence of a new command.

<!-- -->

-   It's not clear to me how the data used in a *tcl* file where a
    command is ran is passed on to this *tcl* file.

### *Week 10*

#### 29/07/2012

Developed a first version of a routine
(*ged_graph_objects_positions*) that returns the positions for each
object from the database. This is supposed to be used by a GUI component
that draws the objects using Tk Canvas inside a window.

#### 28/07/2012

-   Had trouble with a *make distcheck* error.
-   Ran tests for the two commands that were implemented:
    "graph_structure" and "graph".


The name of "graph_structure" might be adjusted. Subcommands need to be
added. So far, there is a view command but what it actually does is
traverse the database and define its corresponding graph. The steps for
this need to be split in smaller routines that would eventually be
called as subcommands.

#### 27/07/2012

-   Managed to pop up the window in MGED by simply running the "graph"
    command.

#### 24/07/2012

-   Worked on popping up a new window when running the *graph* command.
    With starseeker's help I found out that one of my script wasn't
    "loaded". Eventually I tackled this. However, the window still
    doesn't pop up when running the command; it shows up only when
    running *<tcl_script_name> .window1*.

### *Week 9*

#### 22/07/2012

-   Created the command "**graph**". For now, it can be ran in MGED like
    this: "**graph view**" and it calls a routine in src/libged/dag.cpp:
    *ged_graph()*.

<!-- -->

-   Worked on creating a new window when running this command.

There is no commit because the code might need some restructuring.

#### 19/07/2012

-   Implemented the **put_me_in_a_bucket** routine that figures out
    the type of an object, adds its name to a vector and defines a
    corresponding shape in the graph.

#### 18/07/2012

-   Replaced the 3 hash tables (solids, regions, and groups) with 3
    vectors of names (primitives, combimations, and non_geometries).

#### 16-17/07/2012

-   Discussed about modifications for the current src/libged/dag.cpp
    file: use a single hash table that stores the names and IDs of all
    the objects and lists of names for each type of an object:
    primitive, combination, non-geometry.

<!-- -->

-   Worked on the above modification. So far:
    -   created a new master hash table called "objects" with the names
        and IDs of all the objects;
    -   worked on switching from the hash tables to simple lists of
        names for each type of an object.

### *Week 8*

#### 13/07/2012

-   Summarized the progress made so far

<!-- -->

-   Updated the future milestones for this project

<!-- -->

-   Currently figuring out a plan for a user-visible feature in
    Archer/MGED, i.e., a command that would open a window displaying the
    graph corresponding to the displayed geometry.

#### 11/07/2012

-   Allocated space for each *value* of an entry of a hash table outside
    the hash table. In the *value* field of an entry I've just copied
    the pointer to this memory space.

<!-- -->

-   Implemented a method that frees the space allocated for these
    values.

#### 10/07/2012

-   Removed entries from the *solids* hash table whenever an object is
    discovered to be a *region* or a *group*. Switched to working with
    pointers for *bu_hash_tbl* structures. Freed memory for each
    allocation.

#### 09/07/2012

-   Made some small modifications on the *src/libged/dag.cpp* related to
    memory allocation.

<!-- -->

-   Tried to deallocate memory for a certain entry in a hash table but
    didn't find a proper solution to this. In the *hash.c* I've only
    found the function **bu_hash_tbl_free(struct bu_hash_tbl
    \*hsh_tbl)** which is not what I need because I don't want to
    deallocate the memory for the whole table but, instead, just for one
    entry. Need to find out how it's supposed to be done.

### *Week 7*

#### 07/07/2012

-   Introduced id's for each object in the database and finished
    memorizing the data.

<!-- -->

-   Taking into account what hash table it belongs to, each object has
    now a corresponding shape and (if needed) links to the nodes of its
    'subtree' in the graph.

<!-- -->

-   Duplication is now avoided because each shape of the router has a
    corresponding id.


Here's the graphical output for the *share/brlcad/7.22.1/db/axis.g*
(that was put in a .svg file, for now):
![](/wiki/user/img/Graph_link_nodes_no_duplications.png)

<!-- -->


Compared to the one mentioned on *01/07/2012*, one can observe that the
number of nodes has been reduced to a single one in case of
duplications. The links between the nodes are overlapping for now. This
needs to be taken care of.

#### 06/07/2012

-   Continued working on the code that is meant to memorize data related
    to each object in a database into the three below mentioned hash
    tables.

#### 05/07/2012

-   Replaced the **bu_ptbl** structures with **bu_hash_tbl** for the
    three kinds of tables: *regions*, *groups* and *solids*.

<!-- -->

-   Implemented code for adding **bu_hash_entry**s into the hash
    tables. Encountered some problems on this part as well as where I
    have to establish the size of each *lists* field in a hash table.

#### 03/07/2012

-   Found a way to eliminate node duplications depending on their
    names - use the **struct bu_hash_tbl**.

#### 02/07/2012

-   Fixed the representation of solid objects: instead of dashed line
    they are represented by rectangles now.

<!-- -->

-   Introduced a temporary method for positioning the nodes into the
    graph.

<!-- -->

-   Cleaned up the code and committed the changes.

### *Week 6*

#### 01/07/2012

-   Managed to link each COMB node with the nodes of its subtree.


Here's the graphical output (that was put in a .svg file, for now):
![](/wiki/user/img/Graph_link_nodes.png)

<!-- -->


One can observe that for some nodes there are branches that link to
other nodes. As a helper, [here](http://pastebin.mozilla.org/1687225) is
the listed output of what the algorithm is doing in the background.

<!-- -->


The order in which they were outputted is the one in which the directory
was traversed. The alignment is due to a linear function that I used for
the coordinates of the rectangles that represent each node. This needs
to be modified as well as the duplicated nodes and the representation of
solids (here, they appear as a single dash line instead of a rectangle).

#### 30/06/2012

-   Looked for an example that would give me hints on how to find and
    traverse a subtree of a combination in order to create actual links
    between the nodes. Decided that *src/conv/g-dot.c* is a good
    starting point.

<!-- -->

-   Worked on the implementation of a method called *dag_comb* that is
    meant to create links between the COMB node and the ones from its
    subtree. Didn't commit anything because it's not finished and the
    code needs to be cleaned up eventually.

#### 29/06/2012

-   Looked in the *src/tclscripts/geometree* folder with the purpose of
    understanding how the MVC (model, view, controller) pattern is
    applied there.

<!-- -->

-   Been suggested that it would be a good idea to create a graph image
    instead (for now). Therefore, I started working on the connections
    between different nodes in the graph.

#### 25/06/2012

-   Committed my latest changes:

:\#Added special cases for when the Adaptagrams library is found or not
found. Don't add dag.cpp to ged_ignore_files if the library is not
found; i.e., always compile it. -- *src/libged/CMakeLists.txt*

:\#Use the \#define HAVE_ADAPTAGRAMS in the src/libged/dag.cpp file in
order to be compiled regardless of the fact that libavoid exists or no.
Fixed indentation. -- *src/libged/dag.cpp*

:\#Added a compile-time preprocessor \#define HAVE_ADAPTAGRAMGS --
*CMakeLists.txt*

-   Started looking for .tcl files that I could use as examples and from
    which I could get methods for implementing a view. My attemp is to
    print out the hierachy structure build with the *dag.cpp*'s methods
    in a user's window.

### *Week 5*

#### 23/06/2012

-   After accessing the *distcheck-enableall_release.log* file I found
    out that the error wasn't generated because of my changes. There are
    usages of **strcmp** in the *src/conv/g-voxel.c* file that have to
    be replaced by **bu_strcmp**. After making this change, running the
    command

`make distcheck`

ended well.

-   There was a problem caused by the duplicated existence of a variable
    named PARALLEL. It was included by both *libavoid.h* and *common.h*
    so I had to figure out a way in which my program would compile and
    none of these two values would be lost/modified during the
    execution.

#### 22/06/2012

-   Introduced a **HAVE_ADAPTAGRAMS** \#define and wrapped most of the
    code in *src/libged/dag.cpp* in a **\#ifdef** - **\#endif**. Still
    need to add the **\#else** case that would provide a useful note
    stating that the library is unavailable.

<!-- -->

-   Altered the *src/libged/CMakeLists.txt* file correspondingly.

Compilation is ok but the command

`make distcheck`

generates an error. I haven't yet figured out what the problem is.

#### 20/06/2012

-   Found a potential solution that could solve the below issue: I've
    compiled Adaptagrams with the flag **-fPIC**.

<!-- -->

-   Discussed it with one of the mentors (brlcad). I was recommended to
    rather add a compile-time preprocessor define like **HAVE_AVOID**
    and enable linkage against the LIBAVOID_LIBRARY in the
    *src/libged/CMakeLists.txt* file than add the file to
    **ged_ignore_files**.

#### 19/06/2012

-   Currently, BRL-CAD doesn't build because my *src/libged/dag.cpp*
    can't access elements from the avoid library. BRL-CAD built in the
    previous attempts because I added a **main** function inside
    *dag.cpp* for which I would add the line

`BRLCAD_ADDEXEC(dag dag.cpp avoid)`

inside the *CMakeLists.txt* file.

The main function was added just for testing purpose so I didn't commit
it. Without the **main** function, and adding **${AVOID_LIBRARY}** with
the **BRLCAD_ADDLIB** command generates
[this](http://pastebin.mozilla.org/1668038) error.

So far, after doing a little research I came to the conclusion that this
is because the libavoid library is static.

#### 18/06/2012

-   Fixed src/libged/CMakeLists.txt because make distcheck wouldn't
    work.

<!-- -->

-   Added reference to the dag.cpp file for the OLD build system.

### *Week 4*

#### 17/06/2012

-   Implemented methods that are used for adding a rectangle to the
    construction of the graph for each object in the database (please
    see *src/libged/dag.cpp* file).

For this, I have modified my previous implementation, more exactly,
simplified it.

-   Eliminated search for the libavoid library from
    *src/conv/CMakeLists.txt* and added it into the folder
    *src/libged/CMakeLists.txt*.

#### 16/06/2012

Started implementing the model for a directed acyclic graph in the
*src/libged* folder. So far, it contains a structure and a method that
initializes elements of such a structure.

#### 15/06/2012

Looked through the *src/libged*, *src/gtools* and *src/tclscripts*
folders for MVC pattern implementation. Still have doubts about how to
structure the pattern in BRL-CAD.

#### 13/06/2012

Corrected the implementation mentioned below. Had a discussion about the
proper locations for MVC implementation files.

### *Week 3*

#### 10/06/2012

Worked on the C++ implementation of a class that contains methods
similar to the ones in *src/conv/g-dot.c*. This approach remains to be
debated.

#### 08/06/2012

By using the *src/conv/g-dot.c* I generated a .svg file that contains
information about the graph's nodes, i.e., for each node that appears in
a **.dot** file I generated a corresponding one by using libavoid.

The .svg file was generated and opened in a visual mode for checkup
purposes: one rectangle per object in the hierarchy can be observed.

#### 07/06/2012

Managed to run a C++ Adaptagrams example(that uses libavoid) inside
BRL-CAD.

#### 05/06/2012

-   Added helper script *misc/CMake/FindADAPTAGRAMS.cmake* to check for
    libavoid's existence as a system-installed library and mark as
    advanced the set variables.

<!-- -->

-   Modified the cmake check for libavoid in *src/conv/CMakeLists.txt*
    accordingly.

#### 04/06/2012

Added a cmake check in *src/conv/CMakeLists.txt* in order to find the
system-installed version of libavoid. If it doesn't find it, it prints a
status message saying it couldn't find it - no error occurs in either
cases (found or not found).

### *Week 2*

#### 03/06/2012

Compilation of BRL-CAD failed because of some 'set but unused variable'
warnings treated as errors. Commited a fix for one of them.

Started work on checking the existence of the libavoid library as a
system-installed dependecy.

#### 02/06/2012

Started working on a file that would take each element of the tree and
process it with libavoid's methods. As a support example I found the
*src/conv/g-dot.c* file.

Failed attempt to integrate libavoid into BRL-CAD. After further
discussions (03/06/2012) it was established that it's best to do this
after I have the functionality going, somewhere in late July.

#### 01/06/2012

Tried to recompile an *example.cpp* file where the Adaptagrams' library
is used outside its main folder. Previous attempt to do this was
unsuccessful. I Managed to compile it after all.

Looked for a location where I could implement functions that would
traverse a tree and construct a DAG with Adaptagrams' library.

I'm still trying to understand how *librt/db_tree.c* and *db_walk.c*
work in the background.

#### 30/05/2012

Adaptagrams will be used as the library of tools.

I've made a plan that sketches what will happend on each side of the MVC
pattern for this project.

The process behind the, let's call it for now, **'igl**' (Interactive
Graph Layout) command that lauches the GUI is the following:

-   access the geometry's hierarchy by using the **'tree**' command with
    an additional option **'g**' that returns the corresponding DAG.

<!-- -->

-   traverse this graph and construct it with the help of Adaptagram's
    library *libavoid*. Libavoid provides polyline connector routing in
    order to avoid obstacle objects. The result is passed on to the
    Tcl/Tk implementation where it will be outputted (View).

<!-- -->

-   on user action (for example: **'move**' or **'delete**' command is
    called), announce the Controller, apply modifications onto the graph
    by using libavoid.

Remark: other uses of Adaptagram's libraries should/may be added.

#### 28/05/2012

Used Adaptagrams' static libraries as external ones by creating a source
code file that calls methods from these libraries.

### *Week 1*

#### 27/05/2012

Studied Adaptagrams' documentation. Listed strong and weak points of
both graph libraries, GOBLIN and Adaptagrams.

#### 26/05/2012

Compiled Adaptagrams; studied and ran examples provided for libcola and
libavoid.

#### 25/05/2012

1.  Worked on compiling GOBLIN. However, I get a lot of errors. You can
    find them [here](http://pastebin.mozilla.org/1650086). I am assuming
    it's because of the c++ standard and their latest update which was
    made in 2010. Submitted a bug on their sourceforge bug tracker and
    am waiting for a reply.
2.  Meanwhile, I'm having a look at the Adaptagrams' source code.

#### 24/05/2012

Made comparisons between Adaptagrams and GOBLIN.

#### 22/05/2012

Discussed with one of the mentors how to approach the implementation
behind the command that would launch the GUI.

Talked about the possible locations where command-line functionality can
be developed.

As a first step, looked for proper already existent functions in BRL-CAD
that would allow me to ge the directed acyclic graph structure of a
tree.

#### 21/05/2012

Read about [Adaptagrams](http://adaptagrams.sourceforge.net/) library.

# Community bonding period

### General progress

#### 19/05/2012

Studied some aspects of the [GOBLIN](http://goblin2.sourceforge.net/)
graph library.

#### 17/05/2012

Commit access was gained. My first commit was for the
src/libbu/test_booleanize.c file; it included style and formatting
corrections.

#### 16/05/2012

Patch for the file src/libbu/booleanize.c was accepted and applied in
the revision r50566.

#### 15/05/2012

I have modified my first patch, the one meant to create a
test_booleanize.c with unit tests for the file src/libbu/booleanize.c.
At the same time, I found a small bug in the booleanize.c code. The
patch can be found
[here](https://sourceforge.net/tracker/index.php?func=detail&aid=3519874&group_id=105292&atid=640804).

#### 14/05/2012

I have created an alternative patch for the one that is meant to
separate out LIBNMG from LIBRT. This one 'moves' the files from the
src/primitives/nmg location to src/libnmg without being needed an extra
help from someone with commit access.

Here is a [link](http://dl.dropbox.com/u/3425790/separate_nmg.patch.bz2)
to a temporary location for the patch since it exceeds the size limit
provided by Sourceforge.

#### 12/05/2012

I have finished a patch meant to separate out LIBNMG from LIBRT. You can
find the patch
[here](https://sourceforge.net/tracker/?func=detail&aid=3526143&group_id=105292&atid=640804).
Build system modifications have been made in the following files:

-   *src/librt/CMakeLists.txt*
-   *src/librt/Makefile.am*

and the following 2 files have been correspondingly added for libnmg:

-   *src/libnmg/CMakeLists.txt*
-   *src/librt/Makefile.am*

One thing needs to be made by a person with commit access: move the
*src/librt/primitives/nmg* source code into *src/libnmg* and apply the
provided patch.

Reminder: there's also
[this](https://sourceforge.net/tracker/?func=detail&aid=3519874&group_id=105292&atid=640804)
patch that I've made and needs to be reviewed. It contains unit tests
for the *src/libbu/booleanize.c* file and it fixes a small bug that
wouldn't have passed one of the tests.

#### 10/05/2012

I've studied the *src/mged*, *src/librt* and *src/conv* folders, looking
for methods that can be used to access the elements of a CSG tree.

Methods that got my attention:

-   in the *src/librt/db_tree.c* file:

`int db_tree_list(struct bu_vls *vls, const union tree *tp)`

which fills a bu_vls with a representation of a given tree appropriate
for processing by Tcl scripts. Could be useful in constructing the
interactive graph.

`union tree *db_tree_parse(struct bu_vls *vls, const char *str, struct resource *resp)`

which takes a TCL-style string description of a binary tree, as produced
\* by db_tree_list(), and reconstruct the in-memory form of that tree.
Could be useful after the structure of the graph is modified and the CSG
needs to be updated.

### 2. Get commit access

#### 08/05/2012

Worked on the patch for the NMG migration task (create a separate
library LIBNMG outside LIBRT). This time, because BRL-CAD previously
built without errors, things go smoother.

### 1. Compile & install BRL-CAD

#### 28/04/2012

After discussing my problem with one of the mentors and finding the
cause for these errors, BRL-CAD completely built.

#### 27/04/2012

I created my first patch for BRL-CAD by using the virtual machine disk
image so now I want to compile and install BRL-CAD from source (from a
svn checkout).

I've followed the instructions with respect to the dependencies (the
ones from here [Compiling](../../Compiling.md) and from the
**doc/README.Linux**). I've used the command

*cmake -DCMAKE_BUILD_TYPE=Debug -DBRLCAD_BUNDLED_LIBS=Bundled .*

but after using

*make*

, I kept getting these errors <http://pastebin.mozilla.org/1602696>.

Afterwards, I decided to try the command

*cmake -DCMAKE_BUILD_TYPE=Debug .*

but then I encountered another error while running it:
<http://pastebin.mozilla.org/1602697>. I managed to solve the problem by
installing itk3 and itk3-dev. However, while running the make command I
bumped into the previously mentioned *make* errors and this one:
<http://pastebin.mozilla.org/1602700>. The first ones refer to
fontconfig symbols.
