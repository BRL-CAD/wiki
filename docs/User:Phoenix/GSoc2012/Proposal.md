# Project title

Implicit to NURBS conversion

# Brief summary

At present, BRL-CAD has implemented lots of geometric primitives in an
implicit form, but when it comes to interactive shaded displays and
conversion to other formats, the disadvantages of implicit primitives
come out. So we need a conversion to NURBS bundary representations. Lots
of primitives have already been implemented as NURBS, but some are not
robust and some still need to be improved. Besides, some are still
missing. This summer, if I'm accepted, I'm going to accomplish the goal
of converting all (if needed) implicit primitives to NURBS, including
fixing the bugs and correcting the errors existing now, and adding new
conversions that have not been implemented yet. Finally, I'd like to
build a converter that can walk a CSG tree and convert the implicit
primitives in the tree altogether to their NURBS form. The original
implementation in BRL-CAD is a good starting point, and I will take the
current routines of BRL-CAD.

# Detailed description

## Introduction

Although I have read a few books on Computer Graphics before, I'm not
very familiar with NURBS/BREP before I started preparing for the
application. These days I have read a lot of materials relevant and read
the codes of BRL-CAD, so now I have a deeper understand of what I'm
going to do in this project, and some patches (See below) related to
this project have been made. As I'm making these patches, I get much
more familiar with what I should do and the techniques (mathematics
knowledge, algorithms, APIs, etc.) I should use in this project.

Below is my detailed proposal for the project. In the first part I'd
like to show what BRL-CAD has already done in the implicit to NURBS
conversion. Then I will tell you detailed things I'm going to do in my
summer. At last, I'd like to show you the schedule and what I have
already done about this project.

## Works already done in BRL-CAD

The conversions of implicit primitives to NURBS in BRL-CAD can be seen
in functions rt_\*_brep() in src/librt/primitives/, and the conversion
of each primitive is done in a separate function. The executable file
csgbrep.exe can call most of them to produce NURBS represtations of many
primitives together for a test.

This work is significantly dependent on the OpenNURBS library as its
basic NURBS support. The data structures to describe NURBS is based on
OpenNURBS, and OpenNURBS provides many useful algorithms for our work.
But OpenNURBS is not perfect, with lots of useful and important
functionality missing, so we still need lots of work to implement the
functionality by hand.

Although lots of work has been done in BRL-CAD already, some bugs still
exist and some work is still located at the mathematical orgin. It may
not work well if the parameters are changed in some occasions. And some
primitives are still not included. The robustness need to be improved
and the missing ones should be added.

For example,

-   The primitives 'sph', 'ell', 'hyp' and 'ehy', after converted to
    brep, always stay centered at the origin even if the centers of the
    implicit primitives are set to a non-origin point.
-   When the implicit primitive 'eto' is converted to brep, its shape
    may change.
-   The primitive 'pipe', cannot work for a wide variety of primitive
    dimensions.

The document /share/brlcad/7.21.0/doc/brep.txt describes the current
routine of brep primitives in BRL-CAD.

## Proposal ideas

As there has been a lot of work done in BRL-CAD already in this field,
so I should continue the work following the current routines and try my
best to make it better.

First of all, I'd like to fix the problems remained in the current
version. Some are listed above, and more are going to be discovered and
added to the list (like extrude, revolve, etc.). Besides, I should
provide the conversion of primitives at locations other than the origin.
As for this, I should deduce the transformation matrices that are needed
to transform the BREP at the origin back to the 3-space location where
the CSG implicit is, including scaling (most already done in BRL-CAD),
rotating, shearing and translating. Matrix transformations are applied
to the control points of the NURBS surfaces to make the changes. These
days I have done some work on this (sph, ell, ehy, hyp) and the results
seem quiet good, but I think it will be more challenging later, as the
primitives gets more complicated. The codes in other primitives that
already work well can be referred to when I need help. In a word, to
determine and apply the transmation matrices for non-origin CSG
primitives is an important part of this project. My background in linear
algebra might offer me great help, I hope.:)

During my coding, I should always keep in mind writing maintainable,
portable and complete code. To keep a good habit of coding is really
important. I will write clear documents in the meantime, and discuss my
opinions with the development team. After the conversion of one
primitive, I will improve its documents immediately, so that the work is
complete.

To test the result of conversions, I am going to replace the implicit
primitives in the CSG tree with the NURBS representation, raytrace the
whole model to see whether it is changed. Once I found some mistakes in
my conversion like overflows, I should modify my code immediately.

But the current routine for testing the conversion is to use
csgbrep.exe, which is quite inconvenient. So I'd like to write a
converter that is easy to use. It can convert arbitrary implicit
primitives to breps, as long as the conversion function has been
implemented. I have already add an option to the brep command in my MGED
to do this. The command followed by an object's name (a CSG implicit
primitive) calls the related rt_\*_brep() function and writes the brep
primitive generated to the current database, and then I can draw it onto
the screen. In such way the test becomes an much easier and convenient
job. This should be done early in the project, because it benefits the
following developing a lot. My present work is still incomplete, but it
can work already.

After I finish doing something on the implemented conversions, I'd like
to add more new conversions from implicit primitives to NURBS. For
example, the conversions of implicit primitives like ars, half, part,
grip, superell, metaball and so on are still missing now. Study the
current code as examples may be of great help. Implementation of
conversions of different primitives still have lots of things in common,
like creating a curve and rotate or extrude it, creating surfaces, etc.
And the comments in librt/primitives can tell me the concrete algorithms
I should use to deal with that kind of primitives. Math books as well as
materials online or in the library can offer me theoretical assistance.
By the way, I should really learn more about the classes and functions
in OpenNURBS, which provides basic support for our NURBS representation,
with abundant APIs provided. I need to get full use of the library of
OpenNURBS to implement my own methods, like bezier curves, surfaces,
etc. As well as the others, the new implemented conversions should not
be only for primitives located at the origin, and I should try my best
to make the result as robust as possible. So as well as writing new
code, the test is also very important, as I have mentioned above.

Finally, after finish all the rt_\*_brep() functions for all
primitives that would be included in a model, I am going to write a
conversion function which walks the CSG tree and converts the implicit
primitives in it to NURBS. The tree structure is duplicated, but the
implicit primitives are replaced by the brep primitives. The conversion
function may be available in a command in MGED, using an object or the
whole model as its parameter. As there is already a command named "brep"
in MGED, I'd like to follow it and add new options to it. The MGED
command can be like this:

` brep `*`obj`*` [`*`brepname`*`]`

or

` brep -t `*`root`*` [`*`suffix`*`] // -t means it deals with a tree`

The former converts an implicit primitive to brep, and the latter can
convert primitives in a CSG tree together. brepname and suffix are
optional. When brepname is not specified, the name of the generated brep
would be objname_brep (or objname.brep like what csgbrep.exe does).
When the suffix is not specified, the names of the generated breps would
be originalname_brep (or .brep). Of course, the specific details should
not be decided now, and lots of discussion are needed when I develop
this feature.

The deliverables and detailed schedule of my summer is as below.

# Deliverables

-   The remained problems with implemented conversions like ehy, hyp,
    revolve, sph, ell, tor, extrude, pipe, etc. are fixed. Patches will
    be updated promptly. (Some have been done now, verification needed.)
-   Conversions of non-orgin located primitives are implemented (if they
    have not been implemented now)
-   The missing conversions of implicit primitives are implemented.
-   At last a converter working for a whole CSG tree is built (The user
    interface of my work).

# Development schedule

-   \- May 21 (\~4 weeks)
    -   Study materials on NURBS/BREP etc
    -   Read the codes in librt/primitives
    -   Get familiar to OpenNURBS
    -   Fix some bugs and make patches
    -   Implement a method for convenient testing

<!-- -->

-   May 21 - June 10 (\~3 weeks)
    -   Modify implemented conversions if not finished
        -   pipe
        -   sph, ell, tor, hyp
        -   eto, extrude, revolve, etc.

<!-- -->

-   June 11 - June 18 (\~1 week)
    -   Final examination week in our school

<!-- -->

-   June 19 - July 1 (\~2 weeks)
    -   Still work on existing conversions
    -   Work on non-origin primitives
        -   Deduce transformation matrices
        -   Apply the transformation
        -   Test the results and write documents

<!-- -->

-   July 1 - July 29 (\~4 weeks)
    -   Add new conversions to missing primitives
        -   Test whether it works well
        -   Write clear documents
        -   From easy ones to hard ones
    -   July 1 - July 8 (1 week)
        -   rec
        -   ars
        -   half
        -   ell1
    -   July 8 - July 15 (1 week)
        -   metaball
        -   pnts
        -   part
        -   grip
    -   July 15 - July 22 (1 week)
        -   superell
        -   cline
    -   July 22 - July 29 (1 week)
        -   hf
        -   other missing primitives

<!-- -->

-   July 29 - August 13 (\~2 week)
    -   Write a convert for whole
        -   Write a function to walk the tree
        -   Add a command to MGED
        -   Discussions and documents
    -   Test the work and fix bugs

<!-- -->

-   August 13 - August 20 (\~1 week)
    -   Pencil down data
        -   Improve documentation
        -   Evaluations

<!-- -->

-   Post-GSoc
    -   Further involvement with BRL-CAD :)

# Time availability

I will have lots of free time during my summer vacation, so time is not
a problem. I can work about 8 hours a day and 7 days a week. I'll have
the final exams during June 11 to June 18, which takes about a week.

# Things I have done now (Patches)

I have made patches related to the project I'm applying. The original
revision(48890) of functions rt_ell_brep(), rt_ehy_brep() and
rt_hyp_brep() cannot deal with objects centered at a non-origin point.
I add rotation, translation and shearing matrices and apply them to do
the transformation. They work quiet well in my tests. I hope it's a good
start point for my work. This patch can be seen on
<https://sourceforge.net/tracker/?func=detail&aid=3513288&group_id=105292&atid=640804>
.

I also add an option to the 'brep' command in MGED which can call
functions rt_\*_brep() to convert an implicit primitive to brep. So I
can test the conversion function in MGED, which is a much more
convenient way then csgbrep. I also share it as a patch on
<https://sourceforge.net/tracker/?func=detail&aid=3515194&group_id=105292&atid=640804>
.

# Why BRL-CAD

I'm really interested in computer graphics, and BRL-CAD is an excellent
open-source CAD software. I think working for BRL-CAD is an interesting
and meaningful experience, and I can learn much from it.

# Why me

I'm good at mathematics, and this project needs lots of math knowledge.
I'm also good at programming in C++. And I have made some patches on the
functions I'm going to deal with in this project, which makes me
confident that I can do a good job in this project.

# My opinions to GSoC

I think I will get lots of practice if I participate in this project,
and I hope to continue work for BRL-CAD, because once I start I cannot
stop myself. I am really interested in working for BRL-CAD, and I found
open source is such an interesting place.