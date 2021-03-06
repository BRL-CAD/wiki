Abstract: Constructive Solid Geometry(CSG) is a procedural modeling
technique that represents solids as Boolean combinations of more
primitive solids. Boundary Representation (B-REP) represents solids by
their limits. Both of these systems have their own merits. My project
will bring these two systems together by implementing methods for
evaluating Boolean operations on B-REP. The algorithm to be implemented
hinges upon calculating the intersection curves between Bezier patches.

Proposal: I propose to forward the goal of hybrid model support in
BRL-CAD by implementing BREP on BREP CSG evaluation. To this end I
propose an implementation of the BOOLE system detailed in Shankar
Krishnan, Atul Narkhede, Dinesh Manocha (1996) (see link). The Boole
system has a number of merits:

Firstly BOOLE is very robust. It is capable of performing operations on
curved surfaces (such as NURBS and Bezier patches) and outputting
trimmed Bezier patches without approximating using polyhedra. This
prevents data proliferation and yields more useful results as the new
surfaces can still be modified using control points. Note: although the
algorithm is meant for curved surfaces, it is very easily applied to
polyhedral surfaces. The system also uses floating points for arbitrary
precision.

Secondly BOOLE is a realistically implementable solution, as is clear
from the fact that Krishnan et al. details an implementation of the
system. This was done in FORTRAN but will still be an invaluable
reference for me throughout the implementation process. This
implementation is open too.

Finally the BOOLE systems is concerned with efficiency. Not only is the
algorithm already streamlined; the paper also details how to parallelize
the system, which will make for a more lasting solution with today’s
computers.

The BOOLE system's algorithm is as follows:

Data Structures The algorithm requires data stored as trimmed Bezier
patches which are simply Bezier patches together with a closed sequence
of curves defined in the domain of the patch. Note, Bezier patches are a
subset of trimmed Bezier patches. And the paper notes that this
algorithm is easily applied to algebraically defined surfaces. The
structure also maintains adjacency information about the surfaces. It
maintains which patches share a curve, the two patches to which a curve
is attached, and the edges (in counter-clockwise order) to which each
vertex is attached (winged edge storage structure). This adjacency
storage method is easy enough to adapt to whatever fits best with the
current BRL-CAD structures.

Assumptions The algorithm assumes that the surfaces form a manifold;
mathematically this means they are locally homeomorphic to a euclidean
space, which implies that they have a well-defined inside and outside,
so boolean operations are well defined. The algorithm also assumes that
the boolean operations on the these manifolds yield manifolds. To this
end the system uses regularized boolean operations (see algorithm
notes). The paper mentions that it is still possible to generate
non-manifolds from manifolds even with regularized boolean operations;
this is something I will have to look into as a possible bug. The paper
states that given these assumptions it has been shown that there exists
an unambiguous topological representation of the solid.

Step 1 The main part of the algorithm is computing the intersection
curves between the two solids. It is also the most computationally
expensive, and each patch of one solid must be checked with every patch
from the other. However, a lot of pairs have no intersection, so the
algorithm uses two techniques to prune the mn patches. The first uses
bounding boxes (really fast) to eliminate pairs (Bezier patches possess
the convex hull property); the second is more costly (which is why it's
second) and uses linear programming (still polynomial) to find planes
between the patches, which also eliminates the pair.

Step 2 The intersection between the remaining pairs of patches is
computed next. This computation is by far the most difficult (but
interesting) part. It relies on the fact that any space curve can be
projected onto a plane curve with the correct linear transformation (a
result from algebraic geometry). The algorithm first finds a suitable
transformation to obtain the curve in a plane. This makes the
computation of the intersection more manageable, although there are
still some interesting twists. The paper goes into some detail on the
mathematics required for this calculation and cites a number of other
papers that contain more information. This section is a bit lengthy for
inclusion in this proposal.

Step 3 The intersection curves become the trimming curves of our
resultant Bezier patches. The curves partition each of the patches into
pieces that are inside the other manifold and pieces that are outside
the other manifold. We then have all the information needed to
reconstruct the solid.

Algorithm Notes Regularized booleans avoid the problem of manifolds
intersecting in lower-dimensional surfaces, for example unit spheres at
(0,0,0) and (2,0,0) intersect in a point (1,1,1). Regularized booleans
avoid this basically by using the interior of sets instead of the entire
set and then taking the closure.

Production Notes The final product of my proposal will be a library to
be added into the BRL-CAD codebase implementing the BOOLE system as
described above. I am fairly certain that I will be able to use the
B-REP structures as they are in the BRL-CAD codebase. Although as I
understand these are presently undergoing rewriting, my project may
involve some work on these if it makes sense with the project goals.
Also should my project finish ahead of schedule, I intend to begin
implementing the CSG primitives in BRL-CAD as B-REP objects. The most
challenging part of this project is computing the intersection curve
between two patches. Thus I intend to code this part first, and
anticipate that it will take 4 weeks. After this I anticipate spending
the next 4 weeks developing the remainder of the system, that is, making
it compatible with all of the BRL-CAD structuresand setting up the other
parts of the algorithm. These include the pruning methods to optimize
the patch intersection computations and the methods needed to reassemble
the B-REP from intersection curves. The final task is making sure that
the outputs are all compatible with BRL-CAD. I anticipate about 1 week
for each task. This leaves me with about 4 weeks at the end to debug
everything and possibly if everything is running fine work on some
related tasks.

About Myself: I am presently a third year math and computer science
major at The University of Chicago. I have taken numererous classes on
C/C++ programming and consider myself very comfortable with the two
languages. I am also very comfortable with funtional programming
languages, particularly Scheme and Lisp. Although these will be less
handy for the BRL-CAD project. This project has very interesting
mathematical underpinnings and as such piques my mathematical curiosity.
There are also a number of interesting challanges to be overcome in
implementing such a system. This project is one of the few in the GSoC
pool that really interests both the Mathematician and the Programmer in
me. Over the past 2 summers I have worked at Fermi National Laborartory
writing a simulation of a liquid argon neutrino detector that was being
built there. And as a researcher at The University of Chicago doing
research on genetic programming. My experience in the later involved
writing a working implementation of my research topic using Lisp and
Python.

My dedication: If selected to join the brlcad team over the second as
part of google summer of code, I would treat that as a full time job and
feel obligated to work at least 40 hours a week on it. I have select
brlcad because it's a project I feel I could be very passionate about
working on, therefore I'm certain I will wind up spending more than
those 40 hours a week at times when my project has particularly
interesting hurdles for me to overcome.

Timeline and deliverables: Step 1, Leveraging ON_Nurb: .5-1 weeks My
planned solution will use the openNurbs solution the first step will be
to make sure that these are all setup in the most logical way to be used
in the intersection algorithms. This will include writing a few helper
functions. I don't expect this to be a long step at all, it just has the
potential to save me a lot of headaches down the road. Deliverables:
Helper functions for ON_Nurb objects.

Step 2, Intersection (CPU solution): \~3 weeks With a bit of setup I'll
be ready to get right into the meat of the task, intersecting two
ON_Nurb objects together. It will take 2 ON_Nurbs, and return the path
along which they intersect. This will allow us to easily form
intersections and unions. The main worry with this algorithm is that the
error will get out of hand. Prior solutions have either lacked the
accuracy that is required for our solution, or used calculations that
are far too expensive for our purposes. This will be the main hurdle of
the project. Deliverables: Intersection Algorithm for ON_Nurb objects.

Step 3, restitching \~2 weeks After we can take two ON_Nurbs objects
and intersect them succesfully to get the paths, we need to able to take
these and restitch them properly into the resultant ON_Nurbs. This
doesn't have the same algorithmic challenges that the previous step has
but will really be a matter of bookkeeping. Delivarables: Restitching
algorithm, leaving us with a functional intersection algorithm.

Step 4. testing, tweaking 1 week This isn't so much a step with set
deliverables as a time that I'm sure I'll need just to tweek everything
with the algorithm and make sure it's all running well and working
together.

Step 5 GPU solution \~3 weeks: In
<http://www.uni-weimar.de/cms/fileadmin/medien/vr/documents/publications/Ray_Casting_of_Trimmed_NURBS_Surfaces_on_the_GPU.pdf>
a speed up in this algorithm was acheived by leveraging GPUs. This would
be an ambitious thing to implement. Furthermore I don't have any
experience programming GPUs. However this would be a very nice feature
to have since this task parallellizes so well we would get a substantial
speed boost. Deliverables: A functional GPU version of the above
algorithm which would be much faster.

This leaves me with 4 weeks of unallocated time which I'm told is a good
amount of time to leave in the GSoC period for random things that might
arise and for integration of my implementation into the trunk.

Patch (from last year) :
<http://sourceforge.net/tracker/index.php?func=detail&aid=1944674&group_id=105292&atid=640804>

Progress: Initial Commit:
<https://sourceforge.net/tracker/?func=detail&aid=2805742&group_id=105292&atid=640804>

June 13th - June 15th -Implemented:

`   -PointInTriangle`
`   -SegmentSegmentIntersect`
`   -SegmentTriangleIntersect`
`   -TriangleTriangleIntersect`

June 15th - June 16th: Worked on making my code conform to all HACKING
guidelines

June 16th: Wrote tests and fixed bugs in PointInTriangle Wrote tests for
SegmentSegmentIntersect (thus far there don't seem to be any bugs)
Question to look into: Cross products are creating a great deal of
floating point inaccuracy is this to be expected or can I mitigate it in
some way?

June 18th: Fixed numerous bugs both in my code and in test code. Tests
are now very rigorous using rotations to generate large numbers of tests
(these are nice becuase intersection is invariant under rotation so I
still know the answer) At this point it seems that all of the low level
functions are very robust.

June 19th,22nd: Implemented the function MeshMeshIntersect. The final
goal of all of these functions, it doesn't handle degenerate cases yet.
Next Steps: test the function very rigorously, since this function uses
all of the lower level stuff it serves as a very good integrative test.
Also these tests are closer to the sort of thing that it will actually
be called on.

June 25th: Added integrative tests and tracked down a number of small
bugs. MeshMeshIntersect now works perfectly on a nice (meaning not
degenerate test case). Learned an important less about ON_SimpleArrays,
nesting them cause them to segfault on initialization. Use
ON_ClassArray&lt;ON_SimpleArray<T> &gt; instead.

The only thing left that's need to actually perform CSG on meshes is
implementing accounting systems to keep track of the curves and insert
them as trimming curves.

June 30th: The accounting system to keep track of the CSG meshes is
proving to be a tricky problem. The main problem is reconstructing the
mesh and figure out which triangle are internal. And which are external.
The approach I'm taking toward doing this is to record this information
by the direction that the edges we return are pointing. At the end any
face with it's normal pointing the same way as it's superface will be
part of the external mesh, and any face with it's normally pointing the
opposite way will be part of the internal. So the problem becomes
maintaining the edge direction correctly. I believe that I've got most
of the algorithm worked out but, there are still one or two pathological
cases that I don't account for.

Status July 7th: I've spent the last few days going over the algorithm.
To reiterate the challenge at hand is this. Given a triangle from a mesh
intersection we need to figure out whether it was inside of the other
mesh (internal) or (outside). Now to aid in this we have the following
condition on the lines we get out of the intersection are oriented
anti-parallel to the normal of the two intersecting faces. Now there are
5 different types of faces we can get out, note that as of now faces are
exclusively triangles:

Type 1: Faces which have intersections but in which every line of
intersection transverses the triangle in this case the correct thing to
do is to load all of the segments from the intersection, and the
segments from the edge of the triangle and use them to make closed
paths. These closed paths lie along the boundaries between internal and
external triangles. Furthermore if a path's normal is parallel to the
original triangle's it's external, anti-parallel indicates internal. We
then need to triangulate these paths to get the triangles.

Type 2: Faces which have intersections but have exclusively internal
edges. This is the case that arises if a corner is poking through the
triangle but doesn't hit any of the edges. In this case the first step
is the same as the above we make the segments into paths, now one of
these paths is going the be the edge of the triangle and then there can
also be arbitrarily many internal paths. The paths can never cross one
another, so the must be either inside one another or completely
distinct. To solve this we arrange the paths in a tree, where path B is
decedent of path A if B is contained in A. Thus the outer edge is the
root of the tree. Then each path we triangulate will be the path and all
its children.

Type 3: Faces which have intersections of both types, internal and
transverse. Again we arrange as paths and then can arrange the same tree
we had from type 2.

Type 4: Faces which have no intersections but are attached to faces
which do have intersections. After we have gotten the answers for all of
the above types. We get the connectivity of the faces. If a face is
connected to an internal face (through a path which doesn't use external
faces) then it is also internal. (Same of course with external.) Thus we
can just get all the connected components for them.

Type 5: Faces which have no intersections and aren't attached to any
faces that do. This occurs when we have one surface completely enclosed
in another. (e.g Two concentric spheres) Then the only way to figure out
which is inside the other is to do a direct test. The easiest test is
simply whether a single point is inside or outside the the other mesh.
To determine this for a point P, we simply choose some point in the
distance Q, and count the intersections of PQ and the triangles of the
other mesh. An even number indicates external, an odd internal.

July 28th: Spent last week starting to add support for intersection
between paramtric surface. We've decided upon an entirely numeric
solution, since algebraic one's are both substantially more complex and
prohibitively slow. Utility Functions:

`   -Closest Value: returns the closest point in a given interval to a given `
`       -value used when we step off the edge of a surface.`
`   -Push: very useful function that updates parameters move a point in a `
`       -surface along an xyz vector.`
`   -Step: walks a specified stepsize along the intersection between 2 surfaces.`
`   -Jiggle: Given 2 points on different surfaces, that are close to equal, `
`       -tries to find closer ones. Used both to mitigate inaccuracy due to `
`       -stepsize, and to find starting points.`
`   -WalkIntersection: Given a starting points walks, the full intersection `
`       -curve of the two surfaces and returns the resulting Bezier trim Curve.`
`   -GetStartPoints: divides up the surface and uses bounding box methods to `
`       -hone in on starting points, has the huge disadvantage that it finds `
`       -much more than 1 starting point per curve.`
`    -SurfaceSurfaceIntersect: Puts together all the other functions to find `
`       -starting points, walk them and eliminate duplicate starting points, `
`       -getting just the intersection curves.`

Aug 19th: Have since added a number of functions to round out the
functionality of csg system Classes:

`   -Face_X_Event: `
`        -analogous to the ON_X_EVENT (which records curve on curve`
`        -intersections and curve on surface intersections) but for BrepFace on`
`        -BrepFace intersections.`

Methods:

`   -Face_X_Event::Face_X_Event(): `
`       -on blank constructor to just make a new`
`       -blank instance and one to fill in the values, really nothing to tricky`
`       -going on here.`
`   -Face_X_Event::Render_Curves(): `
`       -The intersection between 2 Faces is a subset of the intersection`
`       -between the underlying surfaces depending on what the trim loops look`
`       -like.`
`   -Face_X_Event::Get_ON_X_Events(): `
`       -Intersects the 2 new curves with all of the trims in the Face loading`
`       -the result into the x field in the class.`

Functions

`   -SplitTrim: `
`       -takes a trim and splits it at a given parameter using`
`       -ON_Curve::Split(). It then replaces the reference in the m_trim_index`
`       -array to the original trim with references to the left and the right`
`       -side of the split.`
`   -ShatterLoop: `
`       -takes a trimming loop of a face and records its constituent trims and`
`       -an array. Then it destroys the loop.`
`   -Compare_X_Parameter: `
`       -compares ON_X_EVENTS by the parameter of the first curve at which they`
`       -occurred, used to be passed in to`
`       -ON_SimpleArray`<ON_X_EVENT>`.Quicksort(), and`
`       -ON_SimpleArray`<ON_X_EVENT>`.BinarySearch()`
`   -Curve_Compare_start: `
`       -Compares 2 curves by starting point, used in`
`       -ON_SimpleArray<ON_Curve*>.QuickSort() and`
`       -ON_SimpleArray<ON_Curve*>.BinarySearch()`
`   -Curve_Compare_end: `
`       -same as above yet for endpoints.`
`   -SetCurveCurveIntersectionDir: `
`       -Same purpose as ON_SetCurveCurveIntersectionDir, which is actually`
`       -unimplemented. Sets the dir flags in an intersection event which is`
`       -very important for what we're doing.`
`   -MakeLoops: `
`       -Creates trim loops out of trims by matching them end to end.`
`   -IsClosed: `
`       -Checks an ON_2dPointArray to see if it's closed, ie start and end`
`       -within some tolerance of one another, and atleast one other point`
`       -outside that tolerance.`
`   -GetStartPointsInternal: `
`       -finds starting intersection points between surfaces that are internal`
`       -to both surfaces.`
`   -GetStartPointsEdges: `
`       -finds starting intersection points between surfaces that are one the`
`       -edges.`
`   -FaceFaceIntersect: `
`       -SurfaceSurfaceIntersect has been renamed to FaceFaceIntersect same`
`       -functionality but it records results in Face_X_Events thus it needs to`
`       -know where to find the faces.`
`   -BrepBrepIntersect: `
`       -handles the work of intersecting 2 breps, intersects all the possible`
`       -face pairs. Gets the results as Face_X_Events, renders the curves and`
`       -shatters the loops. Then reconstructs the trims.`

Aug 26: New function CurveCurveIntersect to replace the
ON_Curve::IntersectCurve which doesn't actually exist.