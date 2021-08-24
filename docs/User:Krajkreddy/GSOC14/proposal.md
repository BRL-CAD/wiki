# Personnel Information

|                   |                           |
|-------------------|---------------------------|
| **Name**          | K. Raj Koushik Reddy      |
| **Email Address** | <kraj.reddy@lnmiit.ac.in> |
| **IRC(nick)**     | raj12lnm                  |
| **github**        | raj12lnm                  |
| **Time Zone**     | UTC +0530                 |

# Project Information

## Project Title

Python Geometry : Python Bindings for BRL-CAD Geometry

## Brief summary of Project

This project aims to wrap BRL-CAD's primitives in python. BRL-CAD in
python is an ongoing effort to wrap BRL-CAD functionality in python
\[1\]. Further this project aims at completing the primitives wrapping.
With each wrap tests and examples will be added to ensure agility and
efficiency. There are total 20 primitives left to be wrapped. This
include the brlcad primitive BOT, DSP, EBM, GRIP, ARS, BOT, CLINE, DSP,
EBM, GRIP, HALF, HF, METABALL, NURB, PG, SUBMODEL and PNTS.

## Detailed project description

### Introduction

The python-bindings allows for easy and simple access to the BRL-CAD
APIs for geometry construction and manipulation. These bindings work by
parsing the header files for the installed version of BRL-CAD, then
construct a standard library of abstractions around the bindings.

### BRL-CAD in Python, A brief Summary

BRL-CAD python is an ongoing effort to use the brl-cad APIs in python.
There are several advantage of binding BRL-CAD APIs in python. Premiere
among them is to easily modify certain functionalities. To use the
advantage of a strong Object-Oriented version of python and its
scripting way, which makes it easier for developers to make quick
changes. Python-brlcad uses ctypes to wrap the BRL_CAD libraries. This
could have been done by hard-coding the loading of the libraries in
python files, which would have meant tight coupling to the BRL-CAD
version they wrap. Instead of doing that, a dynamic wrapper generator
*ctypesgen* is used which reads the BRL-CAD headers (\*.h), and generate
the ctypes wrapper code which is then written into a python file.

### BRL-CAD current Status of Primitives

Currently some BRL-CAD primitives have been wrapped in python-brlcad.
This include ARBN, ARB, EHY, ELL, ELL, EPA, ETO, EXTRUDE, HYP, PIPE,
PARTICLE, REVOLVE, RHC, RPC, SKETCH, TGC, REC, TOR, COMBINATION and VOL.
This project will extend the list to add all the primitives in
python-brlcad. Implementation details of these is added at \[4\]

### Goal of this Project

-   This project aims at wrapping all the primitives in python.
-   Also tests and examples of all the primitives will be added as part
    of the project.

## Sample Codes and Tools

I have already wrapped vol primitive in python. This has been merged by
Csaba in his repository. Details can be found at \[2\].

## Importance of the Project

This project will complete the primitive wrappings for python. Thus
marking an important completion for development of python-brlcad
project.

## Time availability

Coding period GSOC time line falls in my holidays. My University exams
finishes on 15th May 2014 and my joining date at Sapient Nitro (the
software company where I have been recruited) will fall in mid-
September or October. Thus I will be free completely. I can spend around
40-45 hours a week.

## Deliverables

-   Wrapping of the primitives.
-   Writing tests of the primitives.
-   Writing examples of to create reasonable primitives.
-   Updating the wiki page with details of each primitive.

## Development Schedule

**Note :- Whenever a primitive or a ctype adaptor is implemented, this
includes writting the tests and the code simultaneously.**

-   **Community Bonding Period**
    -   Implement travis for automated code checking on github.
    -   Ask for other cleaning works from the mentors, if required.

<!-- -->

-   **Week 1 (19 May)**
    -   ARS
    -   SUPERELL
    -   BINUNIF

<!-- -->

-   **Week 2 (26 May)**
    -   HALF
    -   Metaball
    -   Submodal

<!-- -->

-   **Week 3 (2 Jun)**
    -   EBM
    -   BOT
    -   PNTS

<!-- -->

-   **Week 4 (9 Jun)**
    -   SUBMODEL
    -   ANNOTATION
    -   HRT

<!-- -->

-   **Week 5 (16 Jun)**
    -   HF
    -   POLY
    -   GRIP
    -   CONTRAINTS

<!-- -->

-   **Week 6 (23Jun)**
    -   DSP
    -   Also do code cleaning for the mid-term evaluation.
    -   Write a mid-term wiki entry regarding the experience.

<!-- -->

-   **Mid Term evaluation**

<!-- -->

-   **Week 7 (30Jun)**
    -   Understand BREP.
    -   Create simple examples.
    -   Get hold of OpenNurbsLibrary
    -   Create dummy examples to wrap constructors of C++ classes and
        find the methods to be employed.

<!-- -->

-   **Week 8 & 9 (7 Jul, 14 Jul)**
    -   Wrap the BREP constructors to be able to create simple BREPs
        -   ON_BrepVertex
        -   ON_NurbsSurface
        -   ON_BrepFace
        -   ON_BrepLoop
        -   ON_2dPoint
        -   ON_BrepEdge
        -   ON_BrepTrim

<!-- -->

-   **Week 10 & 11 (21 Jul, 28 Jul)**
    -   Wrap the ON_Brep primitive.
    -   Wrap the BREP primitive using the above.
    -   Improve the above to accomodate examples.

<!-- -->

-   **Week 12 (4 Aug)**
    -   Create BREP examples for python.
    -   Use the wrapped BREP constructors.
    -   Create a wiki page for using BREP in python-brlcad.

<!-- -->

-   **Week 13 \[Pencil Down\] (11 Aug)**
    -   Run all the tests again. (of course a script ;), Just to be 100
        % sure)
    -   Code Cleaning.
    -   Write Project Summary.
    -   Make Blog Entry Regarding Experience.
    -   Make a group of all the diffs to submit to Google Melange

<!-- -->

-   **Week 14 (18 Aug)**
    -   Submit Final Evaluation and Code to the Melange Home

## My preparation for the Project

-   My preparation for this project began by looking at the development
    – logs of previous students..
-   Further I contacted few of them (Kesha and Mohit from GSOC 2013) who
    gave insights on choosing a project.
-   Later I introduced myself on the list and asked for help regarding
    projects
-   Then I asked for some work on python repository. Csaba (javampire on
    \#IRC) helped me with that.
-   I got hold of the CVS system used by python-brlcad (git) and brlcad
    (svn) main repository, installed working environment (Pycharm)
-   I successfully submitted a pull request (with VOL primitive) which
    was merged in the repository. \[2\]

## Why BRL-CAD?

BRL-CAD as an organization has well documented procedures. It has a
defined structure for GSOC students. I tried with other organizations
but found BRL-CAD as more welcoming for students with intermediate
skills.

## Why me?

I will not say that I am a advanced level software developer but I can
assure of my agility. I am a quick learner. I like to explore and learn.
I have good communication skills. I have demonstrated my skills during
the preparation of my porposal. I have submitted my pull request for the
code (VOL primitive) and which was successfully merged by one of the
mentors.

## References

\[1\] <https://github.com/kanzure/python-brlcad>

\[2\] <https://github.com/ncsaba/python-brlcad/pull/1>

\[3\] <http://brlcad.org/wiki/BRL-CAD_Primitives>

\[4\]
<http://brlcad.org/wiki/User:Krajkreddy/GSOC14/proposal/primitives_details>

\[5\] <http://sourceforge.net/p/brlcad/mailman/message/31785283/>

\[6\]
<http://sourceforge.net/p/brlcad/mailman/brlcad-devel/thread/CACb7qUDk5pJ6yWsbxJOwUb0cvH1hsqB0RBditd3n%2BU1xPQ2fjg%40mail.gmail.com/#msg32107236>