# Project Title

Survey of CSG Algorithms

# Personal Information

Name: Nyah Watad Check. Email: check.nyah@gmail.com. IRC Nick: Ch3ck,
Ch3ck_.

## Background Information

I am a third year Computer Engineering student of the University of Buea
and one of the two first GSoC participants in Francophone Africa; worked
with BRL-CAD in GSoC 2013, participated in the Google Doc Camp where I
documented the BRL-CAD, OpenMRS and GNome projects. Participated as an
X.org Evoc participant with X.org in 2014. I participated in as a Mentor
in the 2014 Google Code-In for BRL-CAD.

## Programming Background

-   X.org Evoc Participant, X.org, July – October 2014
    -   Added Shatter Support to the X server project using Xephyr.
    -   Clip Impedance layer to Xephyr and ran unit tests like Xts
        fixing bugs

<!-- -->

-   Google Summer of Code Participant, BRL-CAD, April - September 2013
    -   Implemented a pull routine to reverse the effects of a push on
        Geometry.
    -   Integrated command into MGED interface. (C, XML, 500+ lines of
        code)
    -   Tested the polynomial and matrix math routines, improving the
        speeds of the inverse matrix and matrix determinant routines by
        over 10%. (C, 300+ lines of code)
    -   Integrated the xpush routine which pushes objects having more
        than a single matrix transformation into the push which pushes
        object matrix transformations to leaf nodes. ( C, 1000 lines of
        code.)

<!-- -->

-   Book Sprint Participant, Google Doc Camp, October 2013
    -   Participated in creating a contributors guide to BRL-CAD which
        will encourage a greater number of contributors to working on
        the BRL-CAD project.

<!-- -->

-   SKILLS
    -   Languages: C(Excellent), Java( Excellent ), C++( Beginner),
        Bash(Excellent), SQL(Proficient)
    -   Tools: Secure Shell, subversion, Git, Linux, Netbeans, gdb,
        valgrind.

# Synopsis/ Proejct Summary

This project aims at performing a comparison studies of 2D and 3D CSG
algorithms, looking at the efficiency and robustness vis a vis the
current implementations in OpenSCAD. Constructive Solid Geometry being
one of the primary modeling techniques in the CAD industry is a major
part of OpenSCAD. This involves studying the Clipper and CGAL library
implementations in OpenSCAD and coming up with improvements on existing
implementations.

# Detailed Project Description

## Introduction

Constructive Solid Geometry is a technique used in Solid modeling which
allows a modeler to create a complex surface using Boolean operators to
combine objects. This is often referred to as procedural modeling and
can be performed on polygonal meshes. Here, the simplest solid objects
used for representation are called primitives which are used to
construct more complex objects using allowable Boolean operators such as
union, intersection, difference and well as geometric transformations on
those sets of objects.

OpenSCAD uses the Clipper Library to implement CSG in 2D and CGAL
libraries to model 3D surfaces. My objective in this study is to look at
the CSG Algorithms implemented by OpenSCAD and do a comparative study
with other CSG algorithms, performing and algorithmic analysis and
implement prototypes which can be useful in the OpenSCAD framework. This
entails studying 4 main research papers together with various
implementations of the algorithms associated with them and implementing
the most efficient on the OpenSCAD platform.

## CSG Algorithm for OpenSCAD(Current Implementation)

OpenSCAD is a parametric CSG based modelling software; which means
objects are manipulated by editing the CSG descriptions of objects being
rendered. It employs two different mechanisms for processing CSG
descriptions. It uses the OpenCSG library for visualization during
editing and the CGAL library for export created a meshed BREP output.
However, the OpenCSG Library uses the Goldfeather and SCS algorithms to
evaluate the 2D images of a CSG object from the given perspective. This
is beneficial because of its speed and ability to render complex images
within a short time.

However, CGAL employs the Nef Polyhedra for evaluating boolean
operations on CSGs. It is robust and is able to handle non manifold
input but proves incredibly slow in practice and not very suitable for
time critical applications . There are also overflow issues that arise
with using large size polyhedra. The used of BSP tree proves more
efficient for CSG evaluations than CGAL's Nef based polyhedra . Below
describes the use of BSP based algorithm for CSG evaluations than CGAL's
Nef-based Polyhedra system.

## BSP Tree based Implementation of Boolean Operations

Bernstein et all\[1\] presented an exact and more efficient method for
evaluating 3D polyhedra already supported by OpenSCAD. Results from
tests showed for a BSP tree implementation which 16-28X faster at
performing iterative computations than CGAL's Nef polyhedra . The use of
a BSP-tree based boolean algorithm allows the explicit handling of all
geometric degeneracies without treating a large number of cases. There
are also efficient CSG to BSP algorithms which could be used for easy
representations in both formats.

BSP trees afford an alternative to B-rep algorithms that avoid their
concomitant case explosion by explicitly handling all degenerate
configurations of geometry. They have demonstrated to have suitable
performance for interactive volumetric sculpting.

-   Numeric Substrates

In this system, a plane is a quadruple of floating point numbers
interpreted as coefficients of a plane equation.

-   -   Concidence: Two planes p, q are coincident if and only if the
        determinant of all 2x2 minors are 0
    -   coincident orientation: if p and q are coincident and Pa.Qa,
        Pb.Qb, Pc.Qc, Pd.Qd are non negative.

<!-- -->

-   -   Point Validity: if a point A(p,q,r) is valid if i'ts determinant
        is non zero

` Pa Pb Pc`
` Qa Qb Qc`
` Ra  Rb Rc`

-   -   Orientation: Given a point A(p, q, r) is valid and it lies
        behind, on, or in-front of the plane S if and only iff the
        following expression is negative, zero or positive

`                            Pa Pb Pc  Pd`
`Pa Pb Pc                    Qa Qb Qc Qd`
`Qa Qb Qc       *            Ra Rb Rc Rd`
`Ra Rb Rc                    Sa Sb Sc  Sd`

These predicates are implemented as static filtered floating-point
predicates in the style of shewchuk, but deviations will be done to
support double precision.

-   Geometric Substrates

In the preceding step, we defined planes as primitives, points as
triples of planes and 4 predicates operating on these plans; now we
define a convex polygon type for a constructor and splitting routine.

-   -   Convex polygon: This is a plane of support, s with a bounding
        plane {Bi} I £ Z. This vertices given by Vi = (s, Bi-1, Bi).

<!-- -->

-   -   Construction of a Convex Polygon from a Plane: Given a plane h,
        this operation constructs a convex polygon representing h
        clipped by a very large box. The output polygon serves as a
        stand in for the infinite extent plane. A consistent axis
        aligned “very large box” is used for all calls to the
        constructor and consists of volume spaced bounded by planes X+,
        X-, Y+, y- , Z+, Z-.

<!-- -->

-   -   Splitting a Convex Polygon by a Plane: Since polygon splitting
        may be viewed as two successive and complementarty instances of
        polygon clipping. The algorithm below similar to the
        Sutherland-Hodgman style polygon clippers, rather than deciding
        if and when to insert a crossing point to the output stream, we
        decide if and when to insert the splitting plane into the output
        stream.

## Algorithm

If s is concident with h

` if s is similarly oriented to h`
`     Return (s, {Bi}i e Zn)`
` Else `
`    Return nothing`

Else

`  For I e Zn(in order)`
`     Output planes as specified by table lookup using:`
`      o(s, bi-2, bi-1, h)`
`      o(s, bi-1, bi, h);`
`      o(s, bi, bi+1, h)`
`   Return (s, output)`
`                 Algorithm: Clip(s, {bi}i e Zn) by h`

The Above algorithm works in interoperability between input and output
that is between the Point-based polygon soup and the Plane-based
Representation working with Boolean operations.

# Sample Algorithms/Links

-   Gilbert Bernstein and Don Fussell: Fast, Exact, Linear Booleans
-   Sebastian Steuer: Methods for Polygonalization of a Constructive
    Solid Geometry Description in Web-based Rendering Environments

<!-- -->

-   MEPP: Exact and Efficient Booleans for Polyhedra
-   Cork - by Gilbert Bernstein
-   CGAL: <http://www.cgal.org/>
-   <http://liris.cnrs.fr/mepp/>

# Testing and Verification

Test would be written to verify and test the robustness of the BSP-tree
based algorithm for CSG evaluations. This could apply Octoball tests
from single operations between sizable meshes to Random Boxes tests and
Sculpt Bunny depending on the efficiency. Also, the heat sink test which
has proven to have a worst case performance of O(n2) in the size of
input can be applied to the aforementioned implementation. Unit tests
will be developed to handle different aspects of the BSP-tree
evaluations and appropriate documentation attached for later works on
the system. Also, any bugs coming up during this process will be fixed
and documentation of this work done during development since OpenSCAD is
actively developed and this will keep other developers informed on any
changes taking place in the CSG module for OpenSCAD.

# Deliverables

-   A paper containing the CSG Algorithm survey and it's relation to
    OpenSCAD
-   Prototype implementations integrated with OpenSCAD on the more
    efficient and robust CSG Algorithms.
-   An Evaluation of how more advanced modeling techniques could be
    realised with each algorithm.

# Development Schedule/Timeline

This is a tentative plan which will be modified and developed as GSoC
proceeds.

-   May 17 – June 06( 3 weeks)
    -   Study papers on this topic
    -   Discuss with developers on implementation specifics and further
        clarifications on CSG Algorithms supported by OpenSCAD.

<!-- -->

-   May 24 – June 13 ( 3 weeks)
    -   Check current implementation of the BSP tree algorithm for
        evaluating CSGs and porting to OpenSCAD.
    -   Implement the BSP-tree representations in OpenSCAD or optimize
        current implementation.
    -   Testing, debugging and documentation.

<!-- -->

-   June 14 – June 20( 1 week)
    -   Unit tests for BSP-tree routines
    -   Testing degenerate cases.

<!-- -->

-   June 21 – July 4 ( 2 Weeks) Mid Term Evaluations
    -   Add functionality for CSG to BSP-tree conversion
    -   Testing for robustness and degenerate cases.

<!-- -->

-   July 5 – July 11( 1 week)
    -   Implement testing suite for BSP tree implementation of the
        Bernstein algorithm.
    -   Adding documentation to OpenSCAD framework

<!-- -->

-   July 12 – July 25 ( 2 weeks)

<!-- -->

-   -   Implement and test subroutines for Numeric substrates.
    -   Testing and debugging.

<!-- -->

-   -   July 26 – August 8 ( 2 Weeks)
    -   Add functionality for Geometric Substrates together with sub
        routines.
    -   Testing and debugging of Convex polygon constructor for clipped
        plane

<!-- -->

-   August 9 – August 22( 2 Weeks)
    -   Inside-out tests, address robustness issues with modules and
        improve performance of libraries.
    -   Write paper on Comparison of CSG based algorithms in relation to
        OpenSCAD Implementations.
    -   Check code for memory leaks and performance analysis, with unit
        tests added for implemented modules.

<!-- -->

-   August 23 – August 29( 2 weeks)
    -   Pencils Down, Code clean up.
    -   Review documentation and Finalize paper writing.
    -   Final evaluation, Submission of code to melange.

# Time availability

I would be able to offer over 40 hours on the project. However, since
the project would start during our second Semester; I would be coding
mostly during the nights up to late June or early July when our semester
ends. Also, to meet up with the demands of the project, I would be
coding during weekends and regularly informing my mentors on the status
of the project and regularly updating my logs in this respect.

# Why BRL-CAD

After participating in GsoC 2013 with BRL-CAD, I fell in love with CAD
and will love to spend my summer contributing code to improve BRL-CAD
software.

# Why Me

First of all hailing from Africa with lack of computing infrastructure
posed a lot of great challenges to ascend to hackerdom especially with
the scarcity of good programmers and lack of Internet access. Working
with BRL-CAD in 2013 taught me a great deal especially working with the
brightest researchers in this field. I believe my participation in GSoC
this year would not only give me a great learning experience but also
heighten my ambition of being a great Computer Science researcher in
Africa. I see this project as both an intellectual challenge to impact
change through open source software.

# Contributions

## Past Coding Work

-   GSoC 2013:
    -   <http://www.google-melange.com/gsoc/project/code_samples/google/gsoc2013/ch3ck/5721450489053184>

<!-- -->

-   Xorg Evoc 2014
    -   <https://github.com/Ch3ck/xorg-xserverhttps://github.com/Ch3ck/xorg-xserver>

<!-- -->

-   Other Projects
    -   <https://github.com/Ch3ck/SAMS>
    -   <https://github.com/openmrs/openmrs-core>

## Current OpenSCAD work

Here are my current and ongoing contributions on OpenSCAD

-   Rework AbstractFunction::evaluate to virtual function only fixing
    calls
    -   <https://github.com/openscad/openscad/pull/1285>