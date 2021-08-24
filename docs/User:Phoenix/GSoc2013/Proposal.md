# Project title

NURBS Intersection

# Brief summary

BRL-CAD currently has a routine to compute the intersection curves of
two NURBS surfaces, and in general cases it works well, but to get a
more robust one, I still need lots of work on it this summer. Lots of
tests and verification are needed, and maybe a TDD (Test Driven
Development) can be used in this step. To get the SSI working in all
cases, no matter what the input is like is very important, otherwise it
would be useless.

In this summer, if there is enough time, I would like to finish the
remaining parts of evaluating NURBS, and finally offer a routine to
convert CSG combination objects to evaluated NURBS objects. The work
includes partitioning a surface, and building the new NURBS geometry. If
there's still some time remaining, I will tried to do more tests and
verification to make the implementation better.

# Detailed description

## Introduction

NURBS surface-surface intersection is still a high-priority project in
BRL-CAD. NURBS is a dominant geometric representation format in CADs, so
we need to have enough support for it in BRL-CAD. Currently most objects
in BRL-CAD are modeled in CSG, when converted to NURBS representations,
the primitives are first converted to NURBS primitives, which BRL-CAD
supports, but the next step is missing - evaluate the boolean operations
on NURBS primitives, and then get an evaluated NURBS combination as the
original CSG combination object. Currently BRL-CAD only gives \`\`CSG
tree + unevaluated NURBS primitives", so we need NURBS intersections and
evaluations. This has the potential to become the premiere free open
source implementation of NURBS Boolean evaluation, but only if it's
exceptionally robust to all inputs.

Below is my detailed proposal for this summer's project. In the first
part, I'd like to mention the current status of this project left off
last summer. Then I list my plan of this summer, dividing into several
parts. At last, I'd like to show you the schedule and what I have
already done this year about this project.

## The current status of NURBS intersections & evaluations

Last year I spent about a month on NURBS intersections after I almost
finished the Implicit to NURBS conversion project. I implemented a
surface-surface intersection routine, using the sub-division method
referred in a paper \[1\]. Now it can give us the intersection curves of
two NURBS surfaces in both 3D spaces and 2D uv spaces. If the two inputs
are in good condition, the result is quite reasonable (For detailed
information, please see my last year's development log, there will be
some convincing figures). But when the two surfaces have some coincides
(some degenerated cases as described in \[2\]), the implementation still
has problems, because it first calculates the intersection of surfaces'
bounding boxes, and then use polylines to approximate the curves,
however, in this case, we should get a surface, not some curves. And for
some strange shaped surfaces, the accuracy of the output may be not
ideal. (max_dis can be inputted manually to get a better result, but
it's a burden for users)

And I also tried to calculate boolean operations on NURBS. I just focus
on the union of two spheres, which is a well-conditioning problem, and
tried to get a evaluated model which can pass the IsValid check offered
by openNURBS, but failed. So this part only have many lines of code
written, but cannot work yet.

## Computing P/P, P/C, P/S, C/C, C/S intersections

Last year I implemented the SSI directly using the algorithm in \[1\],
but the functionality to compute P/P, P/C, P/S, C/C, C/S intersections
is missing (P: point, C: curve, S: surface). (See \[3\] for all the
classifications of intersection problems)

This are basis of SSI, and can be used in dealing with some degenerated
issues in SSI. So I'd like to implement this in the very beginning of my
schedule. Like the surface-surface intersection, the subdivision
algorithm can be a good candidate in these intersection problems, as
BRL-CAD already has the functionality of generating curve trees and
surface trees (see src/libbrep/opennurbs_ext.cpp). So for example, in
the C/C cases, we can generate the curve trees of the two curves,
calculating the intersections of the bounding boxes, and get the
intersection point with triangular approximations. In C/S cases, the
intersections should be between curve trees and surface trees.

The paper \[3\] is good reference on defining intersection problems, but
its calculations are based on numerical analysis, which I think can be
easily suffered from floating point precision and accuracy (for high
dimension problems like C/C, C/S and S/S), so I would like to use the
subdivision method instead, which already proves good functionality in
the SSI implemented. As for P/C and P/S, the get_closest_point()
functions in libbrep which are used for brep raytracing, can be used to
first get the closest point on a surface (curve) from a given point, and
then we can compute the distance and compare it with a given tolerance
to decide whether there is an intersection or not. And P/P is the most
direct one - we can compute their distance, and compare it with the
tolerance, but a point can have an area with uncertainty, so is the
result intersection point, which is discussed in the later part "Keeping
track of the uncertainty intransitivity".

Just like SSI, lots of tests and verification are needed in all these
intersection problems. Some corner cases need to be considered as well.
For example, two curves can touch at the endpoints, and a curve can have
some part residing on the surface (that is, the intersection is a curve
instead of a point, which is the general case). I should try to make the
implementation as robust as possible, and it SHOULD work in all cases
regardless of the input. Otherwise, the robustness of SSI can be
affected, if it has some part based on lower dimensional intersection
routines.

## Calculating surface-surface intersection curves

The function calculating NURBS surface-surface intersection curves is in
/src/libbrep/opennurbs_ext.cpp:

int surface_surface_intersection(const ON_Surface\* surfA,

`                const ON_Surface* surfB,`
`                ON_SimpleArray<ON_NurbsCurve*> &intersect3d,`
`                ON_SimpleArray<ON_NurbsCurve*> &intersect_uv2d,`
`                ON_SimpleArray<ON_NurbsCurve*> &intersect_st2d,`
`                double max_dis,`
`                double)`

Some improvements are still needed:

1\) If we detect there are many intersection points that seems to form a
surface, not just curves, that it seems that these may exist an
intersection 'surface'. But finding out this is quite confusing, because
that may be some cases where two surfaces have many intersection curves
that are very close to each other, but they don't have anywhere
coincide. (The paper \[2\] considers such degenerate overlap issues in
Part 4.3 Robustness issues)

2\) There should be some detection related to the two surfaces when
merging polylines (the 3rd step of SSI), not just using the max_dis
parameter. In some cases, there may be two segments that should be in
one intersection curve have bigger distance than two segments that
exists in two nearby intersection curves, but we tend to merge the
latter two segments instead of the former, without that detection.
(Actually, I think max_dis_2dA and max_dis_2dB should be used when
merging segments, that is, we merge curves in 2D parameter spaces.)

3\) Detecting loops. Note: only loops in the 2D uv space is of interest,
those in 3D space is just for displaying, not very useful in the later
evaluation process. A loop in the 3D space may not be a loop in the 2D
space.

4\) We should test more cases and find more problems in the intersection
routine, and fix them to get better performance. A test driven
development scheme can be adopted here.

5\) Fit the curves into lower order ones. At least linear and quadratic
fittings in 2D space are needed, as many primitives in BRL-CAD has
quadratic surfaces.

6\) Some code re-factoring is needed, and comments should be added to
make the code more readable.

The goal of this part is to get a robust routine of SSI that can work in
all cases, so the most important parts are test, validation and
verification. Until after the routine is proved to pass strict tests can
we move to the next step.

For more detailed in tests and verification, see the part below: More on
tests and verification.

Besides, I'd like to emphasis a little on consistency. Preserving the
solidity property after an evaluation is of paramount importance. The
paper \[4\] can give some note on guaranteeing consistency.

P.S. The next two parts focus on the rest steps in evaluating NURBS,
which should be done after the SSI is satisfying. This will not happen
too early in my schedule, but I think they should appear in my proposal
as I already have some clear ideas on this, and ready to do this in my
project.

## Reporting the intersections (API designing)

OpenNURBS originally provides us with ON_X_EVENT and ON_SSX_EVENT
classes which are going to report the intersection results (ON_X_EVENT
for C/C and C/S, ON_SSX_EVENT for S/S). The functionality of
ON_SSX_EVENT is still not complete, and P/P, P/C and P/S intersections
should also be supported. But openNURBS gives us a good framework for
designing the API of reporting intersections.

So I'm going to add some extensions. Once the intersection function is
called and run successfully, an array of ON_X_EVENTs (or
ON_SSX_EVENTs for SSI, ON_PX_EVENTs something like that for point
related intersections) will be returned to the caller. It includes the
intersection points (curves) in 3D spaces and parametric spaces,
checking the validity of the results, the type of the intersections
(transverse, tangent, overlap, etc.), a powerful dumping function (show
the result in text) and lots of other useful features.

The related openNURBS code is in src/other/openNURBS/opennurbs_x.h and
opennurbs_x.cpp.

The newer version of openNURBS has removed the code related to
ON_X_EVENT. So I'd like to put all this code in libbrep (move the
existed one in openNURBS to libbrep, and add the extensions to libbrep),
so that we won't need to worry about conflicts with the newer openNURBS.

## Keeping track of the uncertainty intransitivity

Uncertainty intransitivity can be introduced by the limited precision of
floating point representations, and the tolerance used during
intersections. Paper \[5\] and \[6\] suggests an interval arithmetic
based approach for tracking the uncertainty intransitivity and improve
robustness. A 3D point is not just the coordinates, but three intervals
one for each axis, or the coordinates together with a diameter resulting
in a sphere volume. A curve and a surface is represented by interval
based CVs and interval weights. Although the interval arithmetic
approach is hard to applied directly to BRL-CAD, we can get some ideas
on how to keep track of the the area of uncertainty around points
(curves, surfaces) during the computation of intersections, and maybe
report it to the users (e.g in ON_PX_EVENTs, we not only gives an
intersection point if there is an intersection, but also the uncertainty
area around that point, for example, a diameter or something like that).

Again, verification is needed for this issue. Actually, as Sean says,
the uncertainty intransitivity is coincidentally also the MAIN failing
of most boolean evaluation implementations, so we need to give it a high
priority.

## Split the surfaces and generate new trimmed sub-surfaces using intersection curves

The code in the function split_trimmed_face in
src/librt/primitives/brep/brep.cpp currently works on this, but it's
just a scratched draft worked out last summer. (I think there should be
an independent file containing the NURBS evaluating code)

The paper \[2\] gives us a good direction on how to do this. We get
intersection curves in 2D uv spaces in the first part, and a NURBS
surface in a 2D uv space is much simpler than in the 3D space. Trimming
curves are also 2D curves. As the paper suggests, we can use the
non-intersecting chains to partitioning a simple polygon (just like what
we need to do in the 2D space: the intersection curves are polylines,
and the outer loop of a surface will always be a polygon). There has
been some drafted code already in BRL-CAD, but they don't work well.
Further study of this algorithm and better implementation are needed
this summer.

Note that inner loops should be considered, as is not mentioned in the
paper.

And curve-curve intersection is needed in this part when we need the
intersection of intersection curves and trimming curves, but it's not
difficult because they are all polylines. Actually, the paper suggests a
fast routine using Seidel's algorithm for fast polygon triangulation to
calculate this, as intersection curves are always close curves in
spaces.

And I have a small question here: as far as I'm concerned, in this step,
we just use trimming curves to define the border of a new partitioned
face (the trimming curves will play a role in the final ON_Brep
object), but the ON_Surface as well as ON_BrepFace is still the
original one, is that enough to describe the result of splitting?

## Computation of the new solid model

Currently nothing have been done on this. It's the last step -
performing inside/outside tests to determine whether a trimmed surface
should appear in the final evaluated model or not. But inside/outside
tests are time-consuming (described later), and the paper \[2\] suggests
using connectivity graphs, which can reduce the number of inside/outside
tests to only two per operation.

A connectivity graph is an undirected graph describing the neighborhood
information between the patches constituting the solid, representing the
topology of the solid model. Each patch of a solid is associated with a
vertex, and an edge exists in the graph iff the relative patches are
neighboring patches. And when we compute the new model, we construct a
new connectivity graph whose vertices are connected components of the
old graph and there is an edge between two components if they lie on
either side of the intersection curve. From the construction it is clear
that if one vertex lies inside the other solid all its neighbors lie
outside and vice versa. Therefore performing exactly one inside/outside
test is sufficient to determine the containment classification of each
component.

As for how to perform inside/outside tests - we use curve-surface
intersection - computing the number of intersections of a semi-infinite
ray emanating from a point with the solid, and if the number is odd, the
point is inside the solid, otherwise it's outside.

Operations include: union, difference, intersection. (Focus on one
first, maybe intersection)

Finally we generate the ON_Brep object. Lots of elements should be
added - edges, curves, trims, etc. and the ON_Brep::IsValid() will
check. Read the code in IsValid() functions will help us know what a
valid ON_Brep shbuld look like. The code in add_elements() in
/src/librt/primitives/brep/brep.cpp has some basic routine but is far
from complete.

As Cliff suggests, the code in src/librt/test_bot2nurbs.cpp may help
illustrate how the structures can be built up. The brep structural
assembly itself (curves/edges/surfaces/faces/etc.) may be helpful.

## More on tests and verification

A test driven development can be useful in SSI - the basic scheme has
already been done but problems still exist. Write a test program (like
the ones in src/proc-db), find the problems and fix them, and then more
tests and modifications, until it's good enough. Test cases will be
updated from time to time to find the bugs, and a regression test is
needed, to avoid the modification affecting something we don't expect.

Many corner cases that are easily to be neglected should be carefully
considered:

1\) two surfaces touching at one point

2\) two surfaces have somewhere coinciding

3\) the measurements of the two surfaces differs greatly

4\) ...

Making sure the SSI handles any possible topology and geometry correctly
is very hard, so the tests and verification cannot be over emphasized.
The test program should be written in the very beginning, maybe in the
community bonding period before all coding starts (or even during the
application process).

As for the evaluation part, at first, we can have some basic tests -
e.g. two spheres have some part intersecting, an arb8 and a sph, etc.

If the evaluation on basic primitives is satisfying, more complicate
tests should be performed. Finally, we should test on the /share/db/\*.g
files, and tried to convert the big models (m35, havoc) into evaluated
NURBS models.

Besides, the brep command in MGED should be extended, to support
evaluations of NURBS objects (Don't forget the manual page). Maybe this
command can also be migrated into archer. The conversion script
(conversion.sh) should also be modified to generate evaluated NURBS.

# Links

\[1\] Adarsh Krishnamurthy, Rahul Khardekar, Sara McMains, Kirk Haller,
and Gershon Elber. 2008. Performing efficient NURBS modeling operations
on the GPU. In Proceedings of the 2008 ACM symposium on Solid and
physical modeling (SPM '08). ACM, New York, NY, USA, 257-268.
DOI=10.1145/1364901.1364937 <http://doi.acm.org/10.1145/1364901.1364937>

\[2\] S. Krishnan, A. Narkhede, and D. Manocha. BOOLE: A System to
Compute Boolean Combinations of Sculptured Solids. Technical Report
TR95-008. Department of Computer Science, University of North Carolina,
1995. <http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.38.88>

\[3\]
<http://web.mit.edu/hyperbook/Patrikalakis-Maekawa-Cho/node55.html>

\[4\] <http://www.math.uiuc.edu/~nmd/temp/hass3.pdf>

\[5\]
<http://www.sciencedirect.com/science/article/pii/0010448596000139>

\[6\]
<http://www.sciencedirect.com/science/article/pii/0010448596000140>

# Deliverables

-   A ROBUST NURBS surface-surface intersection routine
-   Other intersection supports: P/P, P/C, P/S, C/C, and C/S
-   NURBS evaluation support
-   CSG model to evaluated NURBS conversion

# Development schedule

-   \- June 17 (\~4 weeks)
    -   Study the papers on this topic
    -   Discuss with other developers
    -   Some code clean up in the current SSI routine
    -   Write a test program to test SSI
-   June 17 - June 23 (1 week)
    -   Lower dimension intersections
        -   P/P, P/C, P/S
        -   With the support of openNURBS
    -   Tests and documentations
-   June 24 - July 7 (2 weeks)
    -   Intersections regarding curves
        -   C/C, C/S
        -   Subdivision - curve trees, surface trees
    -   Tests and documentations
-   July 7 - Aug. 4 (4 weeks)
    -   TDD on SSI
        -   Test the SSI
        -   Find the problems
        -   Fix the bugs
        -   Find more bugs and fix them
        -   Degenerated cases
    -   Try to get the code faster
        -   Fit the curve to a lower order if possible
    -   Documentations
        -   Comment in code
        -   Write some extra document on SSI (algorithms, problems,
            TODOs...)
    -   Mid-term evaluation in July 29 - Aug. 2
-   Aug. 5 - Aug. 18 (2 weeks)
    -   Finish the surface partitioning
        -   Polygon partitioning
        -   Curve-curve intersection
    -   Tests
        -   Trims may intersect
-   Aug. 19 - Aug. 25 (1 week)
    -   Add connectivity graph support
        -   Generate connectivity graphs for objects
        -   Design proper data structures for the graph
-   Aug. 26 - Sept. 1 (1 week)
    -   Inside-outside tests
        -   Curve-surface intersection
        -   BFS of the graph to determine inside/outside
-   Sept. 2 - Sept. 8 (1 week)
    -   Generate valid ON_Brep objects
        -   Read code in IsValid() functions
        -   Add elements (trim, edge, etc.)
        -   Try to pass the validation
    -   Extend the brep command in MGED
-   Sept. 9 - Sept. 15
    -   Robustness Issues
        -   Deal with the degenerated cases
        -   All 3 steps should be modified
    -   Tests
        -   Fix bugs
        -   Improve performance
-   Sept. 16 - Sept. 22 (1 week)
    -   Pencils down
        -   Code clean up
        -   Documentation (wiki pages)
-   Sept. 23 - Sept. 27 (1 week)
    -   Final evaluation
    -   Submit code to Google

# Time availability

I can offer 40+ hours per week on the project. The semester ends at the
late June, and the next semester begins at the beginning of September.

# Why BRL-CAD

I have spent one summer with BRL-CAD last year, and got familiar with
it, and I also love this open source CAD system. I can learn a lot and
enjoy my programming with BRL-CAD.

# Why me

I finished my project successfully with BRL-CAD in last year's GSoC. And
this year's topic is also related to NURBS, and I'm quite familiar with
it. This project had a good beginning by me last summer.

# Things I have done this year

-   Add a test program in librt to test the functionality of SSI.
    (Commit revision 55252)
    -   Some improvement (Commit revision 55270, 55275)
    -   See:
        <http://svn.code.sf.net/p/brlcad/code/brlcad/trunk/src/librt/tests/test_ssi.cpp>
-   Some improvements (bug fixing) of the SSI routine
    -   Detecting loops separately in 2D space and 3D space. (Commit
        revision 55312)
-   Use openNURBS APIs for SSI, and move some code from openNURBS to
    libbrep (Commit revision 55322)
    -   Extend the ON_SSX_EVENT::Dump() functionality.
    -   Use max_dis_2dA and max_dis_2dB for merging polyline
        segments. (Commit revision 55433)
    -   Use and ON_Intersect() overload for SSI, and change the return
        value for consistency with other ON_Intersect()s, and some
        modifications to the ON_SSX_EVENT so that it can be consistent
        to both the current version of openNURBS in BRL-CAD and the
        newest version of openNURBS. (Commit revision 55439)
    -   Fix return value of ON_Intersect (SSI) - returns the number of
        intersection events (consistent with openNURBS), and add comment
        to brep.h. Remove the uncessary check of OPENNURBS_PLUS_INC_,
        and reduce debugging messages. (Commit revision 55550)
-   A test geometry for SSI - using arb8. (Commit revision 55552)