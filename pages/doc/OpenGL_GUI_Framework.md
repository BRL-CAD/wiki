# Initial Project from GSoC 2008

## Abstract

Currently in BRL-CAD there's a redesign process to produce a new
modeling interface, more intuitive and user-friendly, and one of the
parts necessary for this is a front-end GUI in OpenGL. In principle some
3D engine (such as OpenSceneGraph, CrystalSpace and OGRE) should be used
to make the job easier, and by the research done so far OGRE seems the
best suited for the job, so it's the choice for the project unless other
options prove more valuable before starting.

Thus the goal of this project is to implement a framework using this 3D
engine, with the GUI acting as thin client and using network protocols
to communicate with the already existing BRL-CAD back-ends providing the
editing functionality. The framework is to be extended later to provide
the full modeling interface.

## Project Detailed Description

### Benefits

The users of BRL-CAD would be able to use an easier user interface, when
all the pieces for the new modeling application are in place.

### Deliverables

-   The thin client, GUI with OGRE
-   Participation in the implementation of the communication protocols
-   Participation in the implementation of the back-ends

### Plan

-   Prior to the beginning of the coding phase, getting acquainted with
    the development and having things ready to start when the official
    period for coding starts.

<!-- -->

-   The first step (probably 2 weeks) is dedicated to gather more
    information about the architecture, protocols and back-end, produce
    some more detailed plans, and starting with a "Hello world" client.

<!-- -->

-   The following 7 weeks (3-9) should be dedicated to implement the
    functionalities. Milestones include (maybe some of them to be added
    or removed, to be discussed with the mentors and the community in
    general):
    -   Get logging working
    -   Get console working
    -   Being able to communicate with the back-end
    -   Displaying geometries
    -   Displaying various representations (wireframe, polygonal, etc)
    -   Rotating and positioning
    -   Input support (trackball, shift-grips)
    -   Clean cross-platform build system integration

<!-- -->

-   The rest of the time (10-12) would be used as a "buffer" to prepare
    documentation necessary, test that everything is working fine,
    bugfixing and integration; and other possible activities necessary
    to close the project.