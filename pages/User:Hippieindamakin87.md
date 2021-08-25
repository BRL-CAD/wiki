## Suryajith

I am a final year undergraduate at Indian Institute of
Technology,Kanpur, majoring in Mechanical engineering.

### Abstract

I wish to implement a library/routine which computes a B-rep from the
given CSG and further does a B-rep on B-rep evaluation generating a
resultant (new) B-rep. The library evaluates the B-rep using lazy
rational arithmetic such that the tolerances are taken care of with
minimal error. Numerical errors are handled at an algorithm-independent
level, which is an original exact arithmetic that performs only the
necessary precise computations. LiDIA shall be used for the exact
precision math and the data structure support is based on MAPC(C++
library for manipulating algebraically defined points and curves in the
plane).

### Proposal

we assume rational polyhedral solids.Rational polyhedral solids are
polyhedral solids which are represented by their boundaries, in which
the coordinates of the vertices and the coefficients of the defining
face plane equations are all available as rational numbers, regardless
of the way in which these numbers are represented. A rational solid is
always numerically consistent; for instance, each vertex-coordinate
triple satisfies the plane equation of each incident face.

The B-rep is made up of two lists

-   one for edges
-   one for faces.

To be valid, the B-rep must satisfy the following three conditions:

1.  Two distinct edges may neither overlap nor intersect at a point
    which is not a common endpoint.
2.  Two distinct faces may intersect only at edges that are listed in
    the B-rep.
3.  An edge must have an even number of flaps(piece of a face that hangs
    on either side of the edge) incident to it. Useless edges that have
    exactly two incident flaps (of the same maximal face) must be
    deleted from the B-rep.

#### Kernel routines

For some of the lower-level routines, the algorithms based on
floating-point arithmetic are susceptible to failure. These include
sign-evaluation of geometric predicates, orientation of points with
respect to curves, and component classification. We refer to the
resulting set of routines as kernel routines. The efficiency and
reliability of the overall evaluation is governed by these routines.
Some of the efficient algorithms to implement the kernel routines use
exact arithmetic. Kernel routines that shall be used are

-   Multivariate Sturm Sequences
-   Multipolynomial resultants.

<!-- -->

-   **Multivariate Sturm Sequences**

Sturm theorem is a procedure to evaluate distinct real roots of a
polynomial. Given two polynomials(in our case the equations of the
planes/curves),we can define another polynomial which is a combination
of these polynomials(volume polynomial in the case of curves). Here the
calculations can be done by approximating the resultant polynomial as a
univariate sequence in one of the variables and then solving the
sequence with respect to the remaining variables.

-   **Comparision of algebraic points**

A vertex in the patch domain is the common solution of two equations.
This is usually an algebraic number which cannot exactly be represented
using floating-point arithmetic. We represent each real algebraic number
using a small rational rectangle. The rational rectangle is guaranteed
to isolate each common root of the equations. To minimize the expensive
computation, the bounding rectangles are narrowed down to small
rectangles.

-   **Topological information of the algebraic curves**

The intersection curve between two surfaces is typically a high degree
algebraic curve which may have multiple real components. Topological
resolution involves identifying critical points like turning points and
singularities (self intersections and points where the tangent vanishes)
and establishing a unique connectivity between them.

-   **Point classification**

Classifying a component with respect to a solid amounts to classifying a
point with respect to the trimmed domain. It is usually done using the
ray shooting (like a point in a polygon problem).

#### B-rep computation

-   For each pair of patches:
    -   Generate an intersection curve in the domains of the patches by
        substituting the parametric representation of each patch into
        the implicit representation of the other patch. Each
        intersection curve is represented as the zero set of a bivariate
        polynomial.
    -   Resolve the topology of the intersection curves (i.e. determine
        their structure in the patch domain).
    -   Intersect the intersection curve with the trimming boundary,
        determining the position of each intersection point in the
        domain of both patches (point inversion).
    -   Determine the curve correspondence, that is, how the individual
        portions of the algebraic plane curve in one patch domain relate
        to those in the other domain.
    -   Clip the intersection curves in each domain so that only the
        portions inside the trimmed regions of both patches are
        maintained.

<!-- -->

-   For each patch:
    -   Merge intersection curves from the patch/patch intersections to
        form patch/solid intersection curves.
    -   Partition the patch into different components based on the
        trimming curves.
    -   Classify partitions as to whether they are inside or outside of
        the other solid by classifying a point contained in each
        partition.
    -   Based on the Boolean operation, choose the correct components
        from each solid to build the ﬁnal solid, updating all
        topological information.

#### Challenges of the B-rep evaluation

**Exact data structures and algorithms:** MAPC provides routines for
handling polynomials (K_POLYs), algebraic plane curves (K_CURVEs), and
both 1D points (K_POINT1Ds) and 2D points (K_POINT2Ds) with algebraic
coordinates. It includes routines for determining the topology of
algebraic plane curves over a limited domain and intersecting two
algebraic plane curves.

**Point inversion:** A point in the domain of a patch P1 determines, via
the parameterization, a point P in 3-space. If P is in the intersection
of P1 with another patch P2 , it may be necessary to ﬁnd the inverse
image of under the parameterization of P2 . This process is point
inversion.

**Curve correspondance:** Curve correspondence refers to ﬁnding the
orientation of a curve in one patch domain, relative to the same curve
represented in the domain of another patch.

#### Proposed approach

For the conversion of CSG to B-rep, the implementation approach shall be
similar the one followed by [D.Manocha et
al](http://www.cs.unc.edu/~geom/CSG/boole.html).The basic kernel
operations shall be implemented using exact arithmetic using lazy
evaluation for the operations like solving for the roots using
Multivariate Sturm Sequence (with the approximations as mentioned above
and this makes it less robust than ESOLID but faster than it) and the
comparision of algebraic points. The afore mentioned processes shall be
implemented in C++ .To get the work done faster i prefer to tweak the
BOOLE souce files.The operations such as point classification can be
done using simplified computation and the operations point inversion and
curve correspondance.LiDIA shall be used for the exact precision math
and the data structure support is based on MAPC(C++ library for
manipulating algebraically defined points and curves in the plane).

Efficient geometric modelling needs to be both

-   robust
-   computationally economic

I am aiming at balancing both the factors in this proposed approach.

#### Deliverables

-   Efficient routines for B-rep on B-rep evaluation.
-   Optimised routines for CSG to B-rep conversion.
-   B-rep generation of the exisiting implicit primitives.
-   Documentation

#### Timeline

1.  Literature study and mathematical analysis.(Pre-GSOC)
2.  Implementation of the data structures for the surfaces ,curves and
    points.(\~2 weeks)
3.  Implementation of the lazy evaluation based exact arithmetic
    approach for the kernel routines(the solutions to the sturm
    sequences and comparision of the geometric points).(\~2 weeks)
4.  Optimisation of other kernel routines which already use
    floating-point arithnmetic.(\~1 week)
5.  Implementation of the boundary evaluation over the kernel
    routines(\~4 weeks)
6.  Generic routines to covert the CSG representation to B-rep
    representation.( \~2.5 weeks)
7.  Implementation of the routines that generate a BREP for all of our
    implicit primitives.(Post-GSOC)

#### References

-   John Keyser, Tim Culver, Mark Foskey, Shankar Krishnan, Dinesh
    Manocha

ESOLID-A System for Exact Boundary Evaluation. Proceedings of the ACM
Conference on Solid Modeling, June 17-21, 2002.

-   John Keyser, Tim Culver, Dinesh Manocha, Shankar Krishnan.

Efficient and Exact Manipulation of Algebraic Points and Curves. Special
Issue of Computer Aided Design on Robustness. 2000.

-   John Keyser, Shankar Krishnan, Dinesh Manocha.

Efficient and Accurate B-rep Generation of Low Degree Sculptured Solids
Using Exact Arithmetic: I -- Representations Computer Aided Geometric
Design. Vol 16, No. 9. pp. 841-859. October, 1999.

-   John Keyser, Shankar Krishnan, Dinesh Manocha.

Efficient and Accurate B-rep Generation of Low Degree Sculptured Solids
Using Exact Arithmetic: II -- Computation Computer Aided Geometric
Design. Vol 16, No. 9. pp. 861-882. October, 1999.

-   John Keyser, Tim Culver, Dinesh Manocha, Shankar Krishnan.

MAPC: A library for Efficient and Exact Manipulation of Algebraic Points
and Curves. Proceedings of Fifteenth Annual Symposium on Computational
Geometry, pp. 360-369, 1999.

-   Shiaofen Fang , Beat Brüderlin, Robustness in Geometric Modeling -
    Tolerance-Based Methods, Proceedings of the International Workshop
    on Computational Geometry - Methods, Algorithms and Applications,
    p.85-101, March 21-22, 1991

<!-- -->

-   Mohand Ourabah Benouamer, Dominique Michelucci, Bernard Peroche:
    Error-free boundary evaluation based on a lazy rational arithmetic:
    a detailed implementation. Computer-Aided Design 26(6):
    403-416 (1994)

#### Notes

Incase of any licencing issues with respect to either of the dependant
libraries,NTL along with GMP(or LiDIA with ) shall be used extensively
for the datastructures and the computation.

#### Personal profile

[<http://suryajith.tp2p.com/>](http://suryajith.tp2p.com/)

------------------------------------------------------------------------

IRC nick:hippieindamakin8

------------------------------------------------------------------------

I am sure that I would make a good candidate as I bring a very strong
sense of work ethic to each of my endeavors. My project basically
requires a very good command of Geometric Modelling which I can safely
say that I have good level of expertise in. Additionally a good
theoretical know how of Computational Geometry can prove invaluable to
this project which I am very thorough in. Lastly the wide repoirtoire of
Geometric Data Structures and applied mathematical methods at my
disposal can greatly aid me in quick solutions to whatever obstacles I
may encounter during the Project.