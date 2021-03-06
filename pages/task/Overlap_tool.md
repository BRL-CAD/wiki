One of the recurring problems when editing BRL-CAD geometry is detection
and elimination of overlaps - that is, geometric errors where two solid
objects claim to occupy the same 3 dimensional volume. Often, one of the
jobs of a modeler working on a large model is to identify and fix what
can be a multitude of small overlaps.

The task for the summer would be to develop a Tcl/Tk based graphical
tool that helps to view and address overlap problems in a model.
Roughly, the steps are:

1.  Run the overlap checker
2.  Review the results and make appropriate changes
3.  Re-run the checker to confirm the changes

When resolving the overlap, it is very useful to see what is overlapping
- a wireframe visualization of the individual overlapping components
would be a virtual must for any tool proposal. The tool should assist
with identifying optimal subtractions (subtracting one big geometry tree
from another to clear overlaps is usually a bad idea). It should also
allow the modeler to editing the geometry and quickly re-test that
particular overlapping combination.

# References

-   src/tclscripts/mged
-   src/tclscripts/archer
-   mged
    -   there is an existing overlap tool here (on the Tools menu)
    -   it sucks, but look at it.
-   archer
    -   has nothing, ideal place to put the new interface

# Requirements

-   Familiarity with C
-   Familiarity with Tcl/Tk