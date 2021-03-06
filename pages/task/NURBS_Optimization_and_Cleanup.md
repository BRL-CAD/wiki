BRL-CAD has support implemented for NURBS boundary representation
geometry. Technically, this is our second attempt, which was
considerably more successful than our first! We now have comprehensive
import support (via step-g and 3dm-g) and robust ray tracing. Our
implementation leverages the OpenNURBS API (from the Rhino3D folks) and
implements many of the most useful portions of the API that they
removed. Our rendering support was based on research in 2006 that
demonstrated that you could indeed perform exceptionally fast NURBS
ray-tracing. We started, however, by focusing on just getting it to work
correctly and robustly before shifting gears towards optimization and
cleanup. Now is time for the latter two.

One of the main objectives of this project is to improve performance.
One glaring optimization point currently is a slow ray tracing "prep"
but even ray tracing "shot" could be significantly improved. Profile and
go to town while ensuring you don't break anything.

The other objective is to clean up the code. We extended the OpenNURBS
API but in an unclean non-reusable way. Ideally, our mods and extensions
to the OpenNURBS API should be consolidated together, refactored, and
made into a proper overlay so that our binding layer is easier to debug,
develop, and maintain. We made a couple direct edits to OpenNURBS that
are a pain to reapply every time we update their sources -- those should
be extricated and reworked too.

# References

-   src/other/opennurbs
    -   the "mostly unmodified" OpenNURBS library resides here
-   src/librt/primitives/brep
-   src/librt/opennurbs_ext.\*
-   include/brep.h
-   src/proc-db/csgbrep.cpp
    -   creates a NURBS version of most of our primitives
-   src/proc-db/brep\*
    -   various example tools that use the OpenNURBS API

# Requirements

-   Strong familiarity with C/C++
-   Basic familiarity with refactoring, testing, and rendering