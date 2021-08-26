Project proposal for [Visualizing Constructive Solid
Geometry](/wiki/Visualizing_Constructive_Solid_Geometry_%28CSG%29),
GSoC 2012

# Personal information

## About me

-   Name: Cristina Precup
-   E-mail address: cp.cristina.pre.cup@gmail.com
-   IRC username: cristina


I am in my third year as a student of Software Engineering at the
Babeș-Bolyai University (Cluj-Napoca, Romania).

## Background information

-   A successful attendance in the GSoC 2011 during which I worked on
    the “Netgen: Constructive Solid Geometry in 2D” project for the TU
    Wien organization. The goal was to create an extension for the
    Netgen mesh generator that would allow the user to construct complex
    2d shapes starting from some basic shapes, just by applying boolean
    operations over them. Apart from the implementation of geometric
    construction, there was also needed a parser for the input file
    format defined. The programming language used was C++ and for the
    geometric part the Open Cascade library. More information can be
    found on my [wiki
    page](http://www.iue.tuwien.ac.at/cse/wiki2011/doku.php?id=wiki:blog:cristina)


Tags: C/C++, OpenCascade, Netgen, Doxygen

-   Internship at National Instruments where I’ve developed an
    application that would process images in order to classify the
    objects in it and reconstruct a LabView schema


Tags: C++, OpenCV, LabView

-   For my thesis I am working on a scientific computing project
    developed in C++ as well. Staying in touch with the TU Wien
    organization made the possibility of developing my thesis in
    collaboration with the administrator of the organization.


Tags: C++, Qt, ViennaGrid, ViennaSHE

------------------------------------------------------------------------

# Project information

## Project title

Visualizing Constructive Solid Geometry (CSG)

## Brief project summary

BRL-CAD already offers the possibility of generating geometry
hierarchies corresponding to *.g* databases but this can be eventually
interpreted just by images. However, the purpose of this project is to
provide more than this: an interactive graph editor that allows the user
to modify the .g database just by interacting with its displayed graph.

A hierarchy in Constructive Solid Geometry is shaped as a tree. But this
is nothing but a directed acyclic graph and thus an automatic graph
layout API would be useful for representing the structure of the .g
databases.

The visual layout will be built with interactive **Tcl/Tk** widgets and
will make use of graph algorithms to alter the graph structure as well
as the .g geometry structure as the user modifies the visualized graph.

In the end, this graph based visualization should be part of **mged**
and/or **archer**.

## Detailed project description

In my opinion, this interactive graph editor would be very useful for
the user. It would provide the ability to modify the .g geometry in a
more intuitive, fast and user-friendly way. Moreover, construction flaws
could be discovered by the representation of the CSG tree and imediately
alter it.

Firstly, I'd extract the corresponding BRL-CAD's geometry hierarchy.
After some familiarization with the part of the source code that
concerns me, I've got an idea of where I should try to get this
information from. There is this file,

*`brlcad/src/mged/bool_rewrite.c`*

which has methods that might be useful in accessing the boolean tree.

Secondly, I intend to format this data structure such that it can be fed
to a graph layout API. Here I'm thinking of using the tool **GOBLIN**.
It's a C++ class library which will help me in handling the boolean tree
represented internally as a graph. Two of the file formats that it can
import are Dimacs and Steinlib so I could format the geometry's boolean
tree into one of these file formats. In this way, afterwards I could
handle the graph. Another method of formatting the boolean tree would be
to build the graph from scratch and then feed it to GOBLIN.

My Tcl/Tk lack of knowledge can be enriched within the next step in an
effective way: GOBLIN has its GUI **GOBLET** that, among other things,
it can be used to edit graphs. This could help me understand how the C++
data can be graphically represented with Tcl/Tk (the editor code for
GOBLIN is written in the Tcl/Tk scripting language).

Further on, the output of the graph generator GOBLIN has to be used in
the interactive visual layout. This will be implemented in Tcl/Tk and
implies two phases:

1.  implement it as a stand-alone application
2.  hook it into mged and/or archer -&gt; this needs advanced knowledge
    in using capabilities of mged/archer for their widgets

(A second approach was discussed about the implementation of the visual
layout by using Qt. I chose to work with Tcl/Tk because althought I have
to learn the capabilities of mged/archer, I can use them eventually in
developing the graph editor.)

Actions of the user upon the boolean tree represented graphically
include changing the location of a node in the graph, excluding nodes
from the graph.

Remarks:

-   To this part are to be added other actions available for the user.
-   Mockups are to be included in a future version of the proposal.

## Links to any code or algorithms I intend to use

-   GOBLIN graph library:

:\# project page: <http://goblin2.sourceforge.net/>

:\# source code repository: <http://sourceforge.net/projects/goblin2/>

-   BRL-CAD mged/archer:


source code repository: <http://sourceforge.net/projects/brlcad/>

## Deliverables

1.  Feed the geometry hierarchy to GOBLIT
2.  Create the interactive visual layout for the boolean trees
3.  Eventually, hook it into mged/archer

## Development schedule

1.  April 23 - May 20 (community bonding period)
    -   Decide how to extract the data about the geometry hierarchy
    -   Further study of the way in which I will represent the C++ data
        into Tcl/Tk graphics
    -   Further study of potential user actions for the interactive
        graph visualization tool
    -   Clarify the approach followed, the implementation needed to be
        done, and the future tasks
2.  May 21 - June 03 (coding period start)
    -   Extract BRL-CAD's geometry hierarchy
3.  June 04 - June 17
    -   Format the data extracted so that it can be fed to GOBLIT
        (either by implementing from scratch or using one of the two
        file formats Dimacs or Steinlib)
4.  June 18 - June 24
    -   wrap graph algorithms of GOBLIN needed for handling the boolean
        tree
    -   start representing the C++ data into Tcl/Tk graphics
5.  June 25 - July 12
    -   continue representing the transition from C++ data to Tcl/Tk
        graphics
    -   start working on the interactive capabilities of the visual
        layout
6.  July 13 - July 26
    -   continue working on the interactive side of the project
    -   study the hooking into mged/archer
7.  July 27 - August 17
    -   integrate the application into mged/archer
    -   bugs tracking: make sure that the work is flawless by testing
        and carefully checking if there are any errors
    -   document the source code
8.  August 18 - August 24
    -   buffer for unexpected delay

## Describe time availability

I will dedicate 40 hours/week, but will be capable of expanding this
limit.

### Known commitments

Between June 11 and July 1 I will have my exams session. Although this
represents an interval of three weeks, I have to take only three exams.
Therefore, I will still have time available for maintaining the pace of
the development.

Apart from this, sometime during my summer holiday (not necessarily
during GSoC) I will have to participate in a three week internship (I
have been in the same situation in the previous year, GSoC + a three
week internship and I tackled the situation just fine). The problem with
my university is that it won’t accept a GSoC participation as an
internship so I need to participate in one separately. However, I will
still consider GSoC as a primary focus because it is the most exciting
thing for me. During these three weeks I could work up to 30 hours/week
but, as I explained above, when in need I can invest a larger number of
hours dedicated to work (this would be in order to compensate the ones
lost during the internship).

## Why BRL-CAD?

I chose BRL-CAD because I think it's great to work on such a powerful
Open Source modelling system.

## Why you?

The reason why I want to apply for the "Visualizing CSG" project is
because I enjoyed working on the previous GSoC project which contributed
in forming a CSG background. I am aware that it's not the type of
knowledge mostly needed for this project but I hope that my C++
experience along with the desire to learn new interesting things (such
as work with Tcl/Tk, GOBLIN, see how mged/archer are implemented) will
suite the requirements for it.

# Development progress

Information regarding my general progress can be found
[here](Cprecup/GSoC2012_progress.md).

**Midterm overview of milestones**


*Summary:*

-   Studied the two potential graph libraries: **Adaptagrams** and
    **GOBLIN**. Adaptagrams was eventually chosen to work with.

:\* Integrated the Adaptagrams' **libavoid** library into BRL-CAD (see
the files: *misc/CMake/FindADAPTAGRAMS.cmake*,
*src/libged/CMakeLists.txt*, and *src/libged/Makefile.am*) -- gained
knowledge in working with cmake configurations and in how they are set
inside BRL-CAD.

:\* Worked on the *model* part of this project. It can be found in the
*src/libged/dag.cpp* file. The accomplished goals so far are:

:\*\* traverse a geometry

:\*\* identify its objects based on their type: solid / comb

:\*\* for each such object, add a shape (Avoid::ShapeRef) to the graph
(internally, by attaching it to a router (Avoid::Router))

:\*\* there are 3 hash table structures corresponding to each type of
objects (solid, regions and groups (the last two are subtypes of comb))

:\*\* depending on the type of object do one of these things:

:\*\*\* for a solid: add a rectangle to the graph

:\*\*\* for a comb: add a rectangle along with connections between this
shape and the ones belonging to its "subtree"

:\*\* assign IDs to each object. This helped in avoiding node
duplications which rose when an object was first considered a solid and
then, later, a comb.


*Updated goals for the next period:*

-   Milestone 1: create a user-visible feature in Archer/MGED, i.e., a
    command (possibly, called "**igl**") that opens a window showing the
    graph for the currently displayed geometry.
-   Milestone 2: align the graph's nodes and structure it.
-   Milestone 3: work on the interactive capabilities of the visual
    layout: commands such as **delete** and **move** for nodes.
-   Milestone 4: track bugs; make tests. Document the source code.
