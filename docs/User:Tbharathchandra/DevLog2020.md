# Coummunity Bonding Period

-   Setup the Development Log
-   Explore and analyze different key-value datastores.
-   Discuss with Mentors and finalize the perfect datastore.

## May 16

-   Downloaded and installed Hiredis (v0.14.1) on my machine
-   hiredis.prf is created for auto-detection of hiredis

## May 17

-   Exploring hiredis and redis

## May 18

-   Created pcache.h which contains the core methods to connect and
    communicate with the server.

## May 19

-   Written some functionality of the PCache class.
-   Testing and resolving different degenerate cases in PCache.

## May 20

-   Added somemore functionality for PCache class.

## May 21

-   Testing of PCache class and added required guards ENABLE_HIREDIS
-   Pushed the code into repo and results show a success.

## May 22

-   Understanding the layout of preference dialog.

## May 23

-   Created the required GUI, which takes the IP address and port number
    and connects to the Redis server.
-   Pushed the code to the repo and checks ran successfully.

## May 24-30

-   Exploring Redis commands

## May 31

-   Added authentication functionality to PCache class
-   Added required GUI in preferences to take password.

# Phase 1

## June 1

-   Added prepending functions
-   Added print function

## June 2

-   Experimented with the referencing style of CGALCache and GeomCache.

## June 4

-   PCSettings class is added
-   Added command-line option to decs

## June 5

-   Integrated PCSettings with CLI and GUI version.

## June 6

-   fixed build issue

## June 7

-   Added FindHiredis.cmake and added to CMakeLists.txt
-   Fixed few typo errors.

## June 8

-   Testing authentication

## June 9

-   Testing command-line options

## June 10-12

-   Learning about boost serialization library

## June 13

-   worked on Serialization implementatio outside OpenSCAD

## June 14

-   Created and placed connect and disconnect functionality in Main
    window and OpenSCAD.

## June 19

-   Created SCADSerializations.h file to store all serialization
    definitions
-   created cache_entry structs in pcache.

## June 20

-   Worked with boost serialization in non-intrusive and split mode.
-   checking it's compatibility in OpenSCAD env through small tests
    outside OpenSCAD.

## June 21

-   Completed writing all serialization definitions

## June 22

-   Completed Insert and get methods for CGAL and Geometry

## June 23

-   Resolved error with header files
-   Added Guards around cache_enry serialization definitions
-   Made some modifications to the smartCacheInsert method and
    encountered a critical error.

## June 24

-   Resolved problem related to serializing a pointer to derived class
    of boost serialization
-   Ran 1st test on the complete project, it is partially successful
-   Geometries are inserted perfectly into Redis but raised a
    segmentation fault which to be addressed.

## June 25

-   Geometry cache is inserting into Redis by preview action
-   Segmentation fault of yesterday still prevails

## June 26

-   Testing has done in the case of CGAl Cache, CGAL is successfully
    inserting into Redis while previewing and crashes in case of Render
    action.
-   Found the cause for segfault, in the process to resolve it

## June 27

-   Resolved the segfault by starting the connection on render thread
    while rendering. no change in the case of the preview.

## June 28

-   worked on crash due to lazy union
-   identified the reason behind the crash.

## June 29

-   Analyzed the options for resolving the crash

## June 30

-   After discussing with mentor, we decided to continue working on the
    reconstruction of object from redis and try to resolve the issue in
    parallel.

# Phase 2

## July 4-8

-   Resolved segmentation fault related to rendering on a different
    thread

## July 9-13

-   Resolved the crash which is happening when previewing the second
    script

## July 14-16

-   Resolved the repeating authentication bug

## July 17

-   Adding a new test app to CTest of OpenSCAD

## July 18

-   Completed the python test script and added it to tests/CMakList.txt
-   failed to run the test on local machine
-   test failed by running on travis and other tools most probably
    because of lack of hiredis lib

## July 19

-   fixed the problem discussed yesterday, by changing the args in
    add_cmd_test in tests/cmakelists.txt and changing the export path
    in python script.
-   ran Travis along by starting Redis-server, macOS doesn't offer that
    service and no huge time difference is observed in the other two
    builds.
-   need to add hiredis dependency to Travis check to complete.

## July 20-26

-   placed pcachepngtest_CSG into heavy config due to variety of
    reasons
-   discussed with teepee about things that can be done
-   started by adding clear Redis cache feature under the same
    design=&gt;flush caches
-   Added a new option for openscad for logging debug messages into an
    external file
-   Added another test for persistent cache which tests the cache hit
    behavior

# Phase 3

## Aug 2

-   Added debug-output option to openscad

## Aug 3

-   added testcase using debug-output option

## Aug 4

-   Added a section in WIP wikibook about persistent cache

## Aug 5

-   Designed local cache feature set

## Aug 6

-   Completed writing insert, get, gethash and contains methods.
-   Resolved build issues on CI checks

## Aug 7

-   Resolved issues with lcache and completed setting up it's working in
    GeometryEvaluator
-   Resolved the crash issue which is arising when trying to flush
    cache.

## Aug 8

-   Resolved the crash which occurs when lazy-union is enabled.

## Aug 9

-   Added local cache to cmd line options renamed --persistent-cache
    option as --option with args like --option=file for enabling local
    cache and --option=redis,127.0.0.1,6379,foobared for enabling redis
    cache.
-   encountered a seg fault

## Aug 10

-   resolved the segfault crash.
-   updated WIP in progress page.

## Aug 13-18

-   In search of eviction implementation

## Aug 19

-   Facing build errors with Circle CI builds which are disabled because
    of some reason
-   Decided to upstream to remove the boosty dependency in platformutils

## Aug 20

-   Updated tests/cmakelist.txt to include the changes made to --cache
    option and corrected few things dropped because merging