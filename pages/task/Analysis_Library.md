BRL-CAD contains a number of tools for analytical raytracing, including
nirt, rtarea, rtweight, rtcheck, and g_qa. These separate tools can
often contain overlapping functionality, and other tools may want to
utilize techniques only available in a single tool.

libanalyze is a BRL-CAD library intended to provide a unified, organized
API for analytical raytracing functionality. A proposal on this topic
should review the functionality provided by the above tools, outline an
API that would encapsulate and expose the core functionality, and
specify testing procedures to ensure correctness of the results
(analysis accuracy is very important for BRL-CAD, so checking the
results is key). It may not be practical to actually implement all the
libanalyze routines needed to provide full coverage of all the tools'
functionality, so a student should identify core useful procedures (for
example, g_qa uses three axis aligned grids of rays while rtcheck uses
one grid that fires from the "view plane" in MGED - a logical API for
this would be to use librt's ray bundle abilities (or enhance them if it
can't produce the grid shapes currently) and provide a function that
takes as arguments a view plane, mins and maxes within the view plane,
and grid density of rays.)

# References

-   src/rt/viewarea.c
-   src/rt/viewweight.c
-   src/rt/viewcheck.c
-   src/gtools/gqa.c
-   src/nirt
-   src/libanalyze
    -   the design of this library's API must be carefully considered
-   include/raytrace.h

# Requirements

-   Familiarity with C