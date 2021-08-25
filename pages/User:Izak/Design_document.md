## INTRODUCTION

## PROJECT SUMMARY

In our world today , we observe that all solid objects are simply
combinations of basic ones like cubes,spheres,cones,etc and we
frequently have to manipulate objects which have surfaces such as
gadgets and devices . With the explosion in ubiquitous technology,
Computer-aided design (CAD) software help us create digital content in
adverts and movies as well as visualize some solid objects like perfume
bottles and shampoo before they are actually manufactured. In this
project, we propose that BRL-CAD, which aspires to be the best CAD
software, should incorporate a heart, a symbol of love, into its core
functionality as one of its basic solid objects in order to increase its
customer base and differentiate itself amongst its competitors. Indeed,
this heart structure ( also called a heart primitive ) shall be used by
those producing cartoons and designing electronic cards, gifts and
presents during celebrations such as birthdays, weddings,family
reunions, anniversaries and Valentine's day which deeply appeals to many
individuals,families and communities.So during the summer, this heart
primitive will be included into the raytrace library as a set of
routines with corresponding support added to other parts of the source
code.

## PROJECT PLAN

Here, I give a detailed description of how the heart primitive for the
BRL-CAD software will be implemented.

-   Firstly, the constants defined in the include/ headers like
    raytrace.h and rtgeom.h will be edited.
-   Secondly, hrt.c (the heart primitive code), a set of callback
    functions, will be written and added to the
    src/librt/primitives/hrt/ directory.
-   Lastly, associated support for the heart primitive will be added to
    other parts of the BRL-CAD package.

A. Editing include/ headers .

1.raytrace.h

raytrace.h, a header file located in include/ which contains all the
data structures and manifest constants necessary for interacting with
the BRL-CAD ray-trace library , will be edited to serve the hrt.c file
when included as follows;

-   For a chosen (by consensus with mentors) integer K , define ID_HRT
    and comment.
-   Define ID_HEART after the /\*- ADD_BELOW_HERE-\*/ comment which
    is after the ID_CONSTRAINT.
-   ID_MAX_SOLID and ID_MAXIMUM constants will be incremented.

2.rtgeom.h

rtgeom.h, a header file located in /include/ which contains details of
the internal forms used by librt routines for different solids, will be
modified as follows;

-   Add ID_HRT internal section by writing struct rt_heart_internal
    structure .
-   Write macro RT_HEART_CK_MAGIC(_p) BU_CKMAG(_p,
    RT_HEART_INTERNAL_MAGIC, "rt_heart_internal")

3.db.h and/or db5.h

db.h and/or db5.h,header files located in /include/ which define the
internal database format, will be edited as follows;

-   Add heart solid record \#define HRT K to db.h
-   In db.h , write hrt_rec structure containing pad, name , id , etc.
-   Edit db5.h for minor type brlcad heart define K , for a chosen
    integer K .

4\. magic.h

magic.h, the header file in which magic numbers repose serves the
BRL-CAD utilities and ray tracing libraries. This file will be edited as
follows;

-   Add the RT_HRT_INTERNAL_MAGIC define .

B. Writing src/librt/primitives/hrt/hrt.c .

Ray tracing

A parametric surface can be created first. Starting from a volume of
revolution defined by Euler angles φ (rotation around the z-axis) and θ
(angle to the z-axis) and distance r defined below by

0° ≤ φ &lt; 360°

0° ≤ θ &lt; 180°

r(φ, θ) = 1 + 6 sin^2 (φ)(1 - θ/π) (θ/π)^2

At φ=0° and φ=180° the cross section is an unit circle.

At φ=90° and φ=270° the cross section is 1+6(1-θ/π)(θ/π)^2, which
describes a lobe towards θ=135° .

The surface equations can be rewritten as follows ;

x(φ, θ) = cos(φ) sin(θ) r(φ, θ) = cos(φ) sin(θ) + 6 cos(φ) sin(θ)
sin^2(φ) (1 - θ/π) (θ/π)^2 .

y(φ, θ) = sin(φ) sin(θ) r(φ, θ) = sin(φ) sin(θ) + 6 sin(φ) sin(θ)
sin(φ)^2 (1 - θ/π) (θ/π)^2

z(φ, θ) = cos(θ) r(φ, θ) = cos(θ) + 6 cos(θ) sin^2(φ) (1 - θ/π) (θ/π)^2

and can be written using patch coordinates as

x(u, v) = cos(2πu) sin(πv) + 6 cos(2πu) sin(πv) sin^2(2πu) (1 - v) v^2

y(u, v) = sin(2πu) sin(πv) + 6 sin(2πu) sin(πv) sin(2πu)^2 (1 - v) v^2

z(u, v) = cos(πv) + 6 cos(πv) sin(2πu)^2 (1 - v) v2

Note: r(u,v) = 1 + 6 sin^2(2πu) (1 - v) v^2 and 0 &lt; u,v &lt; 1 .

These can be simplified and even approximated using Taylor series
expansions of sine and cosine .These functions are continuously
differentiable over their domains.

I intend to compute the normal vector (ray) using the cross product of
the partial derivatives of the coordinate functions. That is,

∂ux(u,v) = ∂x(u,v)/∂u = -2π sin(2πu) sin(πv) (1 + 6 v^2 - 18 v^2
cos^2(2πu) - 6 v^3 + 18 v^3 cos(2πu)) ---------------------(i)

∂vx(u,v) = ∂x(u,v)/∂v = π cos(2πu) cos(πv) + 6π cos(2πu)cos(πv)
sin^2(2πu) (1-v) v^2 - 6 cos(2πu) sin(πv) sin^2(2πu) v^2 + 12 cos(2πu)
sin(πv) sin^2(2πu) (1-v) v --------(ii)

∂uy(u,v) = ∂y(u,v)/∂u = 2πcos(2πu)sin(πv) + 48
π^2cos^2(2πu)sin(πv)sin(2πu)(1 – v)v^2 ------------------------------
(iii)

∂vy(u,v) = ∂y(u,v)/∂v = - πcos(πv)cos(2πu) – 6πsin^3(2πu)cos(πv)(1 –
v)v^2 + 6sin^3(2πu)sin(πv)(2 – 3v)v -------------------- (iv)

∂uz(u,v) = ∂z(u,v)/∂u = cos(πv)( 1 + 12πsin(4πu)(1 – v)v^2)
------------- (v)

∂vz(u,v) = ∂z(u,v)/∂v = - πsin(πv)( 1 + 6sin^2(2πu)( 1 – v)v^2) +
6sin^2(2πu)cos(πv)(2 – 3v)v ------------------- (vi)

where the vectors tu(u,v) = &lt;∂ux(u,v) , ∂uy(u,v) , ∂uz(u,v)&gt; and
tv(u, v) = &lt;∂vx(u,v) , ∂vy(u,v) , ∂vz(u,v)&gt; are tangents to the
surface of the heart . Thus, we obtain the vector perpendicular to the
tangent ( which is the normal to the surface of the heart ) which is
N(u, v) = p(u, v) / \|\| p(u, v) \|\| where p(u, v) = tu(u,v) X tv(u,v).
The normal to the surface N(u,v) is the ray touching the heart from a
particular point in 3D.

Rendering

Here, I discuss how I intend to do visualization (geometric
representation and analysis). I intend to do this by finding the
intersection points between the line (light ray ) and the heart. We
simply will write a line-heart test which tells us if a point on the
heart surface intersects with the line. The points of intersection are
those that satisfy the line equation and the equation for the surface of
the heart at the same coordinates x, y, z. Here , we equate the heart
equation and the equation of the line given below by X = o + dL where d
&gt; 0 , X = (x,y,z) is in R^3 and L is the direction of the line. To
search for points that are on the line and on the heart means combining
the equations and solving for d. When equations are combined , expanded
and rearranged , we get a quadratic equation ad^2 + bd + c = 0 which can
be solved using the quadratic formula. d = -b + sqrt(b^2 - 4 \* a \* c)
/ 2\*a and d = -b - sqrt(b^2 - 4\*a\*c) / 2\*a. If the value of b^2 -
4\*a\*c is less than zero, then it is clear that no solutions exist,
that is, the line misses the heart. If it is zero, then exactly one
solution exists, that is, the line just touches the heart at one point.
If it is greater than zero, two solutions exist, and thus the line
touches the heart in two points (the entry and exit point).

C. Additional support to other files.

1\. table.c

table.c , a file located in the src/librt/primitives directory ,contains
tables for the BRL-CAD Package ray-tracing library ( librt ). The
following will be done to accommodate the heart primitive in table.c;

-   Declare a raytrace interface for the heart by
    RT_DECLARE_INTERFACE(hrt) .
-   Edit the rt_functab\[\] array , which indexes the different
    callback functions in hrt.c, by providing an entry for the heart
    primitive. That is, add RT_FUNCTAB_MAGIC, "ID_HRT",
    "hrt",rt_heart_\*, et cetera .
-   Edit the idmap\[\] array which maps database objects to internal
    ones by adding ID_HRT .
-   Edit the rt_id_solid() function which determines the appropriate
    function subscripts by adding a case for the ID_HRT .

2\. mirror.c

mirror.c, a file in src/librt/primitives which contains routines to
mirror objects about some axis, will be hacked to support
src/librt/primitives/hrt.c by doing the following.

-   Write RT_DECLARE_MIRROR(hrt) .
-   Edit rt_mirror() function by adding case ID_HRT .

3\. db_scan.c

db_scan.c,a file in src/librt/,will be edited as follows;

-   Add the ID_HRT case to db_scan() function .

4\. Makefile.am

-   Edit librt_nil_la_SOURCES by adding primitives/hrt/hrt.c

5.mged/sedit.h

-   Add necessary defines for ECMD_HEART_\* .

6\. mged/tedit.c

-   Add case ID_HRT to the writesolid() function which writes numerical
    parameters of a solid to a file.
-   Add case ID_HRT to the readsolid() function which reads numerical
    parameters of a solid from a file.

## DELIVERABLES

Pre mid term evaluation period

-   Edit include/ header files like raytrace.h, rtgeom.h, magic.h and
    db.h /db5.h

<!-- -->

-   Write src/librt/primitives/hrt/hrt.c

Post mid term evaluation period

-   Add support to other files in BRL-CAD like primitives/table.c,
    primitives/mirror.c, src/librt/db_scan.c, mged/tedit.c,
    mged/sedit.h and Makefile.am .

## DEVELOPMENT SCHEDULE AND TIMELINE

June 17th to July 26th : Work period (Pre-mid term evaluation)

(1 week)

-   Edit include/ header files like raytrace.h, rtgeom.h, magic.h and
    db.h /db5.h .

(1 week)

-   Write hrt_specific structure .

<!-- -->

-   Write rt_hrt_prep() function to determine if system is dealing
    with a valid heart .

<!-- -->

-   Write rt_hrt_print() function to display some properties of the
    heart .

<!-- -->

-   Write rt_hrt_shot() function to intersect a ray with a hrt .

<!-- -->

-   Testing and debugging functions in hrt.c

(1 week)

-   Write rt_hrt_norm() function to return the normal, entry and exit
    points of a ray .

<!-- -->

-   Write rt_hrt_curve() function to return th curvature of the heart
    .

<!-- -->

-   Write rt_hrt_uv() function to return the polar cooordinates of a
    point hit by a ray .

<!-- -->

-   Write rt_hrt_free() function .

<!-- -->

-   Testing and debugging routines in hrt.c.

(1 week)

-   Write rt_hrt_plot() function .

<!-- -->

-   Write rt_hrt_import() function from database format to internal
    format .

<!-- -->

-   Write rt_hrt_export5() function to export from internal format to
    external format .

<!-- -->

-   Testing and debugging routines in hrt.c.

(1 week)

-   Write rt_hrt_tess() function .

<!-- -->

-   Write rt_hrt_describe() function to present the heart in
    human-readable format.

<!-- -->

-   Write rt_hrt_params() function .

<!-- -->

-   Testing and debugging routines in hrt.c

(1 week)

-   Submission of hrt.c to mentors for final review .

<!-- -->

-   Final corrections of hrt.c .

June 29th to August 2nd : Mid-term evaluation

(1 week)

-   Submission of preliminary hrt.c to Google .

Aug 5th to Sept 13th : Work period (Post mid-term evaluation)

(2 weeks)

-   Edit the table to support librt in table.c .

<!-- -->

-   Edit mirror.c to help mirror objects across some axis.

(2 weeks)

-   Write database interaction support in db_scan.c .

<!-- -->

-   Edit Makefile.am to include hrt support .

(2 weeks)

-   Create necessary support for heart primitive in src/mged/?edit.?
    files .

Sep 16th to Sep 27th: Testing and Documentation period

(1 week)

-   Final testing and debugging of src/librt/primitives/hrt/hrt.c code .

<!-- -->

-   Documenting heart primitive in BRL-CAD .

<!-- -->

-   Final review of hrt.c by BRL-CAD mentors .

<!-- -->

-   Final corrections of hrt.c .

(1 week)

-   Final submission of hrt.c code to Google.

## POSSIBLE DEVIATIONS

As proposed in the project proposal - www.brlcad.org/wiki/User:Izak, the
sextic equation of the heart can be used alongside differential calculus
to add the heart primitive to the BRL-CAD package. A possible deviation
from this approach will be to implement a pseudoprimitive that is, a
primitive created using other primitives but usable as a CSG primitive
e.g. a ell created using a sph. We could use a metaball to create a
heart by mapping the heart's properties like lobe size and aspect ratio
as metaball properties.

## DIFFICULTIES ENCOUNTERED

## FUTURE DIRECTIONS

Determining which points are inside / outside the heart . Computing the
surface of intersection between the heart and other BRL-CAD primitives.

## RESOURCES USED

-   Taubin, G. "An Accurate Algorithm for Rasterizing Algebraic Curves."
    In Second ACM/IEEE Symposium on Solid Modeling and Applications
    Proceedings. 221-230, May 1993.
-   Nordstrand, T. "Heart." <http://jalape.no/math/hearttxt>.
-   "A Generalization of Algebraic Surface drawing" by James F. Blinn.
-   Wolfram mathworld's sextic
    equation:<http://mathworld.wolfram.com/HeartSurface.html>
-   Solving sextic equations by division , Raghavendra G. Kulkarni.
-   Solving sextic equations by decomposition , Raghavendra G. Kulkarni.