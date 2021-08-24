## **Wrapping BRLCAD primitives in python**

### **Abstract**

BRL-CAD is an open source solid modeling system that includes
interactive geometry editing, ray-tracing for rendering and geometric
analysis, geometry libraries for application developers and a lot more.
BRL-CAD has various geometric primitive objects it uses for modelling
complicated solids. This project aims to wrap BRL-CAD functionality in
python.

### **Introduction**

Python BRLCAD is an ongoing project that aims to enable using BRLCAD
APIs in python. It mainly focuses on wrapping BRLCADs primitives in
python. These bindings parse the header files of the primitives from the
installed version of BRLCAD, and uses them to construct a standard
library of abstractions around the bindings. These python-bindings
warrant simple and non-complicated access to the BRLCAD primitives for
geometry construction and manipulation. This project uses ctypes to wrap
the BRLCAD libraries. The main motivation behind python wrappers was to
enable faster iterations and avoid the pain of with pointers and
data-type casting

By loose coupling these bindings, we enable these bindings to interact
with the bleeding edge version (and most other versions) of BRLCAD. We
do this by using a dynamic wrapper generator ctypesgen which parses
BRLCAD’s primitive header files (\*.h) and generates the ctypes wrapper
code and then writes it into a python file.

### **Past Work**

Python BRL-CAD was last worked upon in the summer of 2014 as a GSoC
project. During this project, more primitives were added to the
repository. Some test cases were written and close to no documentation
was done.

### Issues in the current project

-   Fixing the current project. There are certain issues in the current
    version of python BRL-CAD, they are :
-   Outdated and non-maintained codebase (4 Years old)
-   Incomplete installation scripts
-   Support for only python2.7
-   No support for OS-X
-   Non-exhaustive tests for primitives
-   Unwrapped primitives
-   Close to no documentation

### Goals

-   Extending support to python3.x
-   Create robust installation scripts for Windows, Linux and OS-X
-   Introduce bindings for 16 new primitives
    -   annot
    -   brep
    -   datum
    -   dsp
    -   ehy
    -   eto
    -   extrude
    -   hf
    -   hrt
    -   joint
    -   nmg
    -   pnts
    -   poly
    -   rec
    -   revolve
    -   rhc
-   Documenting the project. Documentation would be done for :
    -   Installing and setting up python BRL-CAD
    -   How python BRL-CAD works? (ctypesgen interactions)
    -   How to build wrappings for primitives in python
    -   How to and when to use python BRL-CAD
    -   List of future tasks for the project

### Deliverables

Over the course of GSoC ‘18, I will be submitting three deliverables.
These deliverables would be followed as strictly as possible with minor
updates during the community bonding period. The 3 deliverables are :

-   First Deliverable
    -   Python bindings for 5 primitives (annot, ehy, hrt, nmg, poly)
    -   Tests for these 5 primitives
    -   Documentation on installation and using python BRL-CAD
    -   Documentation of primitives

<!-- -->

-   Second Deliverable
    -   Python bindings for 5 primitives (brep, datum, eto, hf, rhc)
    -   Tests for these 5 primitives
    -   Documentation on how to build wrappings for primitives in python
    -   Documentation of primitives
    -   Partially completed tasks of future possible tasks

<!-- -->

-   Final Deliverable
    -   Python bindings for 6 primitives (extrude, joint, pnts, rec,
        revolve)
    -   Tests for these 6 primitives
    -   Contribution guidelines for python BRL-CAD
    -   Documentation of primitives
    -   List of future possible tasks
    -   Updates on the wiki

### Timeline

Tentative timeline of the project over the summer of 2018.

-   Community Bonding Period :
    -   Get familiarized with different file types and constructs
    -   Contact active contributors and ask them about possible doubts.
    -   Log everything under ‘python BRL-CAD Development'
    -   Would help in fixing prior errors
    -   Fix installation scripts to extend support for OSX (Start)

<!-- -->

-   Week 1 (May 14 - May 20) :
    -   Primitive Completed : annot
    -   Make final changes to the outdated code (if any remaining)
    -   Setup a platform for my : Daily logs

<!-- -->

-   Week 2 (May 21 - May 27) :
    -   Primitives Completed : ehy, nmg (first half)
    -   Documentation of primitives constructed so far
    -   Write test cases for previously created primitives

<!-- -->

-   Week 3 (May 28 - June 3) :
    -   Primitives Completed : hrt, nmg (second half)
    -   Documentation : Installation and usage of python BRL-CAD (V1)

<!-- -->

-   Week 4 (June 4 - June 10) :
    -   Primitives Completed : poly
    -   Documentation : Installation and usage of python BRL-CAD (Final)
    -   Final tests for 5 primitives : annot, ehy, hrt, nmg, poly

#### First Deliverable

-   Week 5 (June 11 - June 17) :
    -   Primitives Completed : brep, dsp
    -   Start chalking out possible future tasks (Weak Document)
    -   Complete support for porting to OSX

<!-- -->

-   Week 6 (June 18 - June 24) :
    -   Primitives Completed : datum, eto
    -   Documentation of primitives constructed so far

<!-- -->

-   Week 7 (June 25 - July 1) :
    -   Primitives Completed : hf
    -   Documentation : Building wrappers for primitives in python (V1)

<!-- -->

-   Week 8 (July 2 - July 8) :
    -   Primitives Completed : rhc
    -   Final tests for 6 primitives : dsp, brep, datum, eto, hf, rhc
    -   Documentation : Building wrappers for primitives in python
        (Final)

#### Second Deliverable

-   Week 9 (July 9 - July 15) :
    -   Primitives Completed : extrude
    -   Start porting to OS-X

<!-- -->

-   Week 10 (July 16 - July 22) :
    -   Primitives Completed : joint, pts
    -   Contribution guidelines for python BRL-CAD (V1)
    -   Finish porting to OS-X

<!-- -->

-   Week 11 (July 23 - July 29) :
    -   Primitives Completed : rec
    -   Updates on the wiki page
    -   Contribution guidelines for python BRL-CAD (Final)

<!-- -->

-   Week 12 (July 30 - Aug 5) :
    -   Primitives Completed : revolve
    -   Documentation of primitives
    -   Test for 5 primitives : extrude, joint, pnts, rec, revolve
    -   Final documentation updates

#### Final Deliverable

### Who am I?

I'm Jaipal, a final year student pursuing my Bachelors in Computer
Science with coupled with an MS by research in Computational
Linguistics. I'm a massive python fanboy and love running. I have been
contributing to open source since 2015. My Open-source contributions
include work with organization like like Mozilla, Plone, and Apertium.
Other than contributing, I also volunteer and take part in local FOSS
workshops organized by Drupal and Mozilla. I was selected to work with
Apertium as a part of Google Summer of Code 2016.