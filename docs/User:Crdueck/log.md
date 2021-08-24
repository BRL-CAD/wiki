This page will contain a log of my progress throughout my project.

## 30/04/2012:

after having some difficulty compiling BRLCAD from the SVN source due to
issues with missing libs, I completed my first successful build. The
issue was with the unorthodox naming scheme my distro uses for the lib32
and lib64 directories, and so CMake was unable to find them.

I am now looking for some bugfixes to tackle so I can gain commit
access.

## 09/05/2012:

while looking through the BUGS file, I found that the bug regarding
drawing with an attached X session crashing MGED in command line mode
unreproducible. Perhaps it was indirectly fixed in a previous patch.

As well, I've been working through the Introduction to MGED and am
comfortable using it to draw and analyze all primitive shapes as well as
using booleans to combine primitives into more complicated shapes.

## 21/05/2012:

one of my patches, adding a function to librt/primitives/ell.c that
computes the surface area of an ellipsoid, was accepted a few days ago
and a patch for libbu/lex.c is pending review. Although I dont yet have
commit access, the first official day of coding is tommorrow, so I hope
to begin producing patches related to my project and have commit access
by the end of the week.

## 22/05/2012:

added a patch to the tracker for a centroid function for ell. The
function is very simple as the central point of an ell is already stored
in the rt_ell_internal struct.

## 24/05/2012:

the next step in my goals for this week is to try to integrate the newly
written functions for ell into MGED's analyze command, as well as clean
up some of the documentation regarding ell

## 28/05/2012:

wrote centroid, volume and surface area functions for the tor primitive.
like ell, the centroid is stored as a point in the rt_tor_internal
struct, and the formulas for surface area and volume use radii values
found in the internal struct as well.

## 29/05/2012:

first day with commit access, committed the tor functions written
yesterday with some slight mishaps which resulted in a chance to learn
how to revert commits with svn.

Worked on a bug where MGED crashes when running "joint holds" or "joint
solve" with a joint file loaded due to a NULL pointer being accessed as
an array, although neither command works properly yet, an error message
is now printed instead of crashing.

finally, tested the libbu/lex.c patch with the "joint list" command. the
output is identical to the pre-patch version so there's some assurance
that the patch hasnt introduced any parsing errors. plan to commit that
patch tomorrow

## 30/05/2012:

the previous test for the bu_lex routine was a bit off the mark. the
section of code that I rewrote dealt with skipping past initial comments
in a joint file which could be C or Bash style, and the test file used
originally only contained Bash comments. After adding some C comments
and testing again, I found there was an error in the code. Some
adjustments were made and the bu_lex routine is now working properly.

Also, i've been looking into the funtabs MGED uses to store its commands
as I'll be needing to modify them to make use of the new primitive
functions in MGED's analyze command. the funtab in src/mged/animedit.c
is a good example.

## 02/06/2012:

looking into adding new primitive functions to MGED, reading source code
in include/raytrace.h, librt/primitives/table.c and
librt/primitives/obj_\*.c. commited changes to the rt_functab in
raytrace.h, adding function pointers for the new functions and made
changes to the func_tab array in librt/primitives/table.c as well

## 05/06/2012:

added a general volume function for tgc that determines if a general tgc
is a rec, rcc, tec, or trc and computes the volume.

## 06/06/2012:

added a general centroid function for tgc. the function handles rec, rcc
and trc, but the formula for tec still needs to be determined. Also
continued working on integrating the new callback functions into the
rt_functab interface so they can be used in libged/analyze.c

## 07/06/2012:

fixed math error in rt_ell_surf_area(). made changes to
analyze_ell() in libged/analyze.c to make use of the new callback
functions and tested the new functions against the old implementation to
ensure correctness.

updated analyze_tor() to include the new callbacks for tor

added rt_tgc_surf_area() to primitives/tgc.c and updated
analyze_tgc() to include the new callbacks for tgc.

tested the analyze command for tgc, tor and ell against the old
implementation and tested corner cases for ells with zero vector axis.

## 12/06/2012:

working on rt_arb_volume(), this primitive is more difficult to deal
with than the previous ones. I've found a formula that will calculate
the volume of an arb with an arbitrary amount of vectors, the tricky bit
is that it requires the area of each face on the arb. Its been difficult
to find a method to calculate the area of the faces from the given
vertices of the arb.

also, there is already an implementation of rt_arb_centroid() which is
used in a few places throughout libged/analyze.c and primitive/arb8.c.
Unfortunately the function signature of the current implementation does
not match the signature of the previous centroid functions i've written,
so it doesnt currently fit into the rt_functab interface i've been
using. It will take some work to ensure that it can be called from the
rt_functab and also not cause problems in any of the places its already
being used.

## 14,15,16/06/2012:

implemented rt_arb_volume() and tested analyze_arb() using the new
function. the volume function works, but it has to declare a new bn_tol
struct that could easily be passed from its calling function
analyze_arb(). Unfortunately due to the strict function signature
imposed by the rt_functab interface, I'm unable to change to type, or
number of inputs to the function.

This is annoying because the current implementation for
rt_arb_centroid() has an extra input that must be removed, but its
value is required to calculate the centroid and so must be found from
scratch, using more struct declarations, and extra function calls.
rt_arb_surf_area() also suffers from a similar problem. Having the
option of changing the number of inputs each function takes per
primitive would greatly reduce the amount of repeated or unnessecary
code needed, and the functions themselves would be much cleaner.

while it was not as much an issue as with arb, the callback functions
for tgc could also benefit from extra inputs. i have a feeling this will
be a recurring problem as the geometric shapes of the primitives become
more complicated (i chose to work on the primitives in order of most
geometrically simple to more complicated).

## 18/06/2012:

implemented volume, surface area and centroid functions for rpc. tested
the new functions and updated analyze_rpc() to use the new callbacks.

## 19/06/2012:

found some errors in rt_tgc_centroid(). the centroid was being
calculated from the origin instead of from the center of the the base of
the tgc. also made some improvements using the VJOIN1 macro i learned of
while writing rt_rpc_centroid().

found an equation for the volume of a epa while investigating formulas
for the arc length of a hyperbolic/parabolic segment, and then wrote
rt_epa_volume().

Unfortunately, the formulas regarding hyperbolas involve integrals
containing non-elementary functions such as the elliptical integral.
I'll see if its possible to simplify these as they are needed to
calculate the surface areas of tec, rec, eta, ehy, and rhc.

## 21/06/2012:

while working with the rt_arb_centroid function, i noticed that it's
algorithm is incorrect. for example, it reports the centroid of an arb6
consisting of \[(2,0,0),(0,2,0),(0,0,2),(-2,0,0),(0,-2,0),(0,0,-2)\] to
be (0,-0.33...,0) (as opposed to the correct (0,0,0)). this is because
the arb6 is stored as an arb8 with some duplicate points, but the
ordering of the points is not consistent with what rt_arb_centroid
expects and so in calculating the centroid some duplicate points are
used and a unique point may be completely ignored.

this lead me to take a look at rt_arb_get_cgtype() (which is called
before rt_arb_centroid()), as the comments suggest that this function
re-orders the points of the arb into "GIFT standard". the function did
not modify the arb in any way, but the code was difficult to read, could
be improved by simplifying some vector operations with existing macros,
and had some kludgy sections so i decided to clean it up as much as
possible. I then tested it against many different kinds of arbs until
the output was correct for all cases.

i plan on fixing the errors in rt_arb_centroid() tommorrow.

## 23/06/2012:

while i didn't work on rt_arb_centroid(), i may have found the cause
of the errors i had found, more on that later.

rewrote analyze_face() in libged/analyze.c to use a much more efficient
and elegant algorithm for calculating the area of the face of an arb. 20
lines of hard to read and difficult to maintain code was reduced to 4
lines of vector macros, so there is significant improvement in that
regard.

while testing the changes, i was getting some strange results from some
of the arbs i was using to compare between the old implementation and
the new one. this was because some of the arbs were malformed, and were
not regular polyhedrons. in particular, the arb6 i was using as an
example in my last log was not a well-formed polyhedron and so that
could be the cause of the centroid error.

## 25/06/2012:

implemented volume, centroid and surface area functions for eto. the
surface area function uses an approximate formula for the circumference
of an ellipse. updated the rt_functab interface to use the new
callbacks and wrote a new analyze_eto function in libged/analyze.c.

also, using the formula for the circumference of an ellipse i was able
to update rt_tgc_surf_area() to include the REC case.

## 27/06/2012:

started working on an analyze function for arbn. This is a particularly
difficult primitive as it can have an arbitrary number of faces, and the
primitive is stored as an array of plane equations representing the
faces. Finding the vertices of the arbn is required to begin computing
its volume and surface area, but fortunately this has already been
solved and is implemented in a few functions in primitives/arbn.c such
as rt_arbn_tess().

a small change had to be made to make the code suitable for the analyze
command. rt_arbn_tess() uses an arbn_pt data structure that holds a
point_t and an array of the planes which intersect at the point. for
the purposes of the analyze function, the opposite is needed (an
arbn_face data structure which stores its defining plane_t and an
array of the point_t that form the vertices of the face as well as
other information relevant to the face). the adjustment was not overly
difficult to make.

the issue of memory allocation must be considered here for the first
time in my project, as the arbn has an arbitrary amount of faces and so
the array of arbn_face structs must be allocated at runtime. this is a
simple matter as the number of faces is stored as
rt_arb_internal.neqn, however allocating memory for the array of
point_t that represent the vertices of each face required more thought.
I reasoned that the maximum number of vertices on a face must be (\#
faces - 1) as that would be the case of all planes but one intersecting
with a single plane, which of course cannot intersect itself.

having discovered all the faces with their respective vertices
simplified the problem down to the case of finding the area of a general
3D polygon with n-many vertices, for which there exists an efficient
algorithm.

however, there is still one issue to solve. the points for a face aren't
discovered in order, so the algorithm used to calculate surface area
doesn't work properly as it needs to walk the edges of the polygon in
order. i've looked into methods to sort an array of 3D points into a
convex hull, in particular Graham's scan looks promising.

## 28/06/2012:

more progress on the analyze function for arbn. I wasted a great deal of
time looking into how to implement Graham's scan, or other convex hull
algorithms before i realized that it was not needed.

I already have knowledge that the set of vertices are all members of the
convex hull forming the polygon, and Graham's scan is intended to take a
large number of points as input, and exclude those which do not form the
convex hull, returning the shortest "path" that encircles all the
points. The problem now is now simply to sort the array of points into
counter-clockwise order, using the knowledge that all the points are
necessarily co-planar. I found this relevant Stack Overflow question:
[1](http://stackoverflow.com/questions/6880899/sort-a-set-of-3-d-points-in-clockwise-counter-clockwise-order)

i implemented a suitable qsort helper function and confirmed that the
array of points had been sorted into counter-clockwise order. now the
surface area algorithm works as intended, although this needs to be
double-checked.

one unfortunate problem in all of this is that i doubt it will be
possible/worthwhile to seperate the implementation of the analyze
command into a surface area, centroid and volume function. The
computation of the volume relies on the surface area of each face, and
so without being able to pass an array of surface area values to the
volume function using the rt_functab interface, it seems extremely
redundant to calculate the surface area for each face once in the
surface area function, and then recalculate it again for use in the
volume function. the very expensive discovery of all the vertices would
have to be duplicated as well. unless the functab is updated to allow
more flexibility in the inputs of the callback functions, it does not
make sense to seperate the analyze_arbn function.

## 30/06/2012:

made a few changes to clean up the analyze_arbn function. not much more
can be done except possibly using the current print_faces_table() from
libged/analyze.c to print information about an arbn face but it would
take some fiddling to get it to work as print_faces_table() seems to
have been made specifically for regular arb.

started working on an analyze_bot command. much of the process for
computing surface area, volume and centroids is very similar to the arbn
so it seemed a suitable next step. the data for a bot is stored rather
strangely, and much of my time writing the function was spent wrestling
with array indexes into the fields of the rt_bot_internal. for
instance, the field which stores the various vertices that make up the
bot is an array of fastf_t instead of an array of point_t, which makes
accessing an entire vector instead of just one of its components more
difficult than need be.

regardless, once the indexing was figured out the rest of the function
was straight forward after working with arbn, and I finished the day by
committing a very rough version of the analyze_bot command which
correctly computed the total surface area and volume of a bot. i tested
for correctness by creating an identical arb4 and comparing the results
to analyze_arb.

## 01/07/2012:

factored a section of analyze_bot() into a new analyze_bot_face()
function. fixed uninitialized variables in both analyze_bot and
analyze_arbn and moved the calculations for surface area and volume for
both analyze_bot and analyze_arbn into the same for loop for each
respective function, as they had previously been in separate loops with
the exact same conditions.

## 02/07/2012:

took today to review all the new functions that have been added over the
course of the project. made a few minor changes, gave variables more
appropriate names, unrolled a very short for loop, added comments and
restructured an if/else tree into a much more readable form.

one major change was a improvement to rt_arb_volume() which had
previously used an inefficient formula to calculate the area of a
triangular base. it now uses a simple cross product of the legs of the
triangle to determine area, a technique that had been recently used in
analyze_bot(). the new implementation actually returns a very slightly
different value than the old one but since the new implemtation follows
directly from a simple mathematical formula I'm convinced that the old
values were slightly off.

modified print_volume_table() to display "COULD NOT DETERMINE" if a
surface area or volume value is negative. now every primitive that can
be analyzed uses print_volume_table() for consistency.

## 03/07/2012:

analyze_bot() and analyze_arbn() now use the print_faces_table
function from libged/analyze.c to display per-face information such as
the plane equation, the area, and the vertices that make up the face.

## 05/07/2012:

removed some unessecary functions from libged/analyze.c. factored a
section of rt_bot_tess() into a new rt_bot_centroid function and
added it to the rt_functab interface. added new rt_part_volume() and
rt_part_surf_area() functions for the particle primitive, updated the
rt_functab interface to include them and wrote a new analyze_part
function.

## 08/07/2012:

familiarized myself with relevant topics for creating non-polygonal
tesselation of a sketch, such as delaunay triangulation, approximation
of bezier curves, and the source code for the sketch primitive. Lots of
good ideas have been suggested on the mailing list regarding how to
tesselate a sketch in order to calculate its area for an analyze_sketch
function, but also provide the option to export sketches as polygonal
representations and other uses.

## 13/07/2012:

added sketch_tess.cpp to primitives/sketch. this file currently
contains functions to approximate a bezier curve by a set of circular
arcs using the algorithm detailed here:
<http://itc.ktu.lt/itc354/Riskus354.pdf>

progress was slow at first, as I'm lacking experience working with C++
or the openNURBS library, but quickly improved as I became more
comfortable working with the API which provided many useful functions.

## 17/07/2012:

the last few days have been spent working on the contents of
sketch_tess.cpp. I've written rt_sketch_surf_area() which is working
well for sketchs containing only line_segs and carc_segs. The Bezier
approximation still needs some work however.

I discovered that the approx_bezier() function which is responsible for
converting a bezier segment into a std::vector<ON_Carc> approximation
had an error, and was producing 249 carc_segs (the algorithm I was
using as a guideline produced 6-9 given the same tolerance). After
fixing the error the number of carc_segs produced for the segment
dropped to a reasonable 12.

I was able to decrease this further by using the point of maximum
deviation from the approximation biarc as the splitting point instead of
the first point of deviation greater than tolerance.

I found another relevant paper here:
<http://home.zcu.cz/~byrtus/Articles/G1ArcSplineApproximationOfQuadraticBezierCurves.pdf>
which, among other things, has provided a simple formula to check if a
bezier curve segment has monotone curvature over its domain. I can use
this to avoid calculating inflection points, which is a good thing
because implementing a robust algorithm to determine the inflection
point of a bezier curve has proven difficult.

## 18/07/2012:

the current functions to determine the inflection point of a bezier
curve, and to find the point of maximum deviation from an approximating
curve at which to subdivide the bezier curve use an iterative method
which involves walking the curve at fixed intervals (originally 10 steps
per curve). This worked, but wasnt very robust.

a solution for the inflection point function was to use the value of the
curvature to determine the step size. Inflection points occur at 0
curvature, therefore as one approaches a point of inflection, the
curvature value -&gt; 0. Using the curvature value as the stepping size
(with hardcoded maximum/minimum stepping size to avoid weirdness when
the curvature is very large or very small) allows for a very precise
method to find the point of inflection.

hopefully a similar approach can be used for finding the point of
maximum deviation.

## 19/07/2012:

the fixed step size problem in approx_bezier was solved similarly, with
the value of 1 - \|crv\| used instead of \|crv\| to determine the step
size so the step size is small when the curvature value is large (more
likely to deviate from the approximating arc).

also, added an explanation for the maximum and minimum step values as
well as rewriting them as macros and fixed some calculation errors in
rt_sketch_surf_area().

## 26/07/2012:

did some code reduction in libged/analyze.c. Pulled common code from
analyze_bot_face(), analyze_arbn_face(), and analyze_arb8_face()
into a new analyze_poly_face() function.

updated analyze_arb8(), analyze_arbn(), and analyze_bot() to populate
a poly_face struct with the required info (vertices, face normal, and
label) and calling analyze_poly_face() to do the analyzing.

## 31/07/2012:

added a new analyze_ars() function to libged/analyze.c. The function
uses a method similar to the one used by rt_ars_tess() to find
triangular faces on the ars, then populates a poly_face and passes it
to analyze_poly_face().

## 03/08/2012:

updated the table interface in libged/analyze.c to allow for tables with
arbitrary number of rows. Some primitives like arbn can have an
arbitrary number of faces and so the table needs to be dynamically
generated to display all the various face information.