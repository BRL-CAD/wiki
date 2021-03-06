An important part of working with geometry is being able to select
subsets of larger models to work on. An example of this is BRL-CAD's
search command, which can identify subsets of geometry based on filters
of geometry type, name, depth in tree hierarchy, and other criteria. In
addition, search can combine multiple criteria to match only geometry
satisfying multiple criteria.

For this task, geometry selection refers specifically to the selection
of geometric subsets that satisfy geometric location criteria such as
"within this volume" or "projected area onto this plain is within this
rectangle", typical operations for graphical selection of geometry in a
window. Rather than implementing this logic at the graphical level, the
goal would be to program a C API that would accept as arguments a list
of geometry paths and geometric filtering criteria. This function should
not be aware of the client modeling application's view state directly -
any such information should be passed into the function as part of the
filtering criteria. The target product would be a C api in librt
(possibly an extension of the existing search code filter types, if that
proves appropriate) and a command line utility (either new search
options or a select command) that exercised them. Graphical integration
is a separate topic, and would require this task to be completed first.

A proposal for this task should outline candidate selection criteria to
implement and an implementation strategy - issues to consider include
how to specify filters with geometric criteria on the command line, how
to handle view information, and mechanisms to test using implicit
geometry (for example, the projected rectangle case above may require an
approximation using bounding box volumes if the unevaluated primitive
doesn't contain enough information to project an area onto a plain
without raytracing or format conversion.)

# References

-   src/libged
-   src/mged
-   include/ged.h
-   src/libtclcad

# Requirements

-   Familiarity with C
-   Good grasp of geometry (projections onto plains, etc.)