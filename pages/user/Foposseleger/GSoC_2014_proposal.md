# Convert Bot to Pipe GSoC Project Proposal

## Personal Information

## Background Information

Name: Leger Foposse Nyah

IRC: leger

email: foposseleger@gmail.com

## Brief Background Information

I am a first year Post graduate student in Computer Science at the
University of Yaounde I, Yaounde Cameroon. From my background in
Computer Science at the undergraduate level. I worked on various Java
SE/Java EE Projects, implemented a simulation program for an elevator in
C/C++ which was used for diagnostic purposes. Also, I wrote a 2D game in
C++ as part of my pet projects. I am excited to work this year with
BRL-CAD since my cousin worked on this great software last year. I am
willing to put in 40+ hours weekly to implement the converter for Bot to
Pipe; together with my experience in Maths and Algorithms during my
undergraduate years.

## Programming Background

C/C++(Very Good):

-   Implemented an Elevator simulation program for diagnostic purposes.

<!-- -->

-   Implemented a 2D Game(Pet project)

Java(Excellent) J2EE,SE :

-   Restaurant management system developed for our University(5000+
    Lines)

<!-- -->

-   Implemented a Binary Search Trees together with associated
    optimizations and graphical interface to simulate the nodes.( 4000+
    lines)

<!-- -->

-   Implemented a Dental simulation program used for Dentists in our
    local hospitals. ( J2EE, 10000+ lines)

## Project Information

Convert BOT to PIPE Project

This project seeks to convert the BOT surface primitive to pipe to
facilitate the the conversion of the "Bag of triangles" solid to native
BRL-CAD geometry.

## Brief Summary

BRL-CAD uses the “Bag o’ Triangles” (BoT) primitive object for
representing triangle mesh objects. BoT primitives are used for
importing component positions from other CAD softwares like Pro-E and
Cadio. This designs imported during vulnerability analysis use
intermediate formats like STL. This is imported to BRL-CAD through the
pipe primitve. This project seeks to implement an accurate Bot to pipe
converter which eliminates lags in models for line routing.

## Introduction

In aircraft design, component positions are constantly in flux leading
to laggin in models of line routine. However, during vulnerability
analysis component positions may miss the correct positions. So during
import to BRL-CAD, overlapping issues have to be resolved guaranteeing
precision and accuracy. This is done by using intermediate formats like
STL.

Due to limitations in the STL format, BRL-CAD employs BoT primitive
objects in the importation of design from other high end CAD softwares
maintaining precision and correctness. With the BoT primitive, many
object could be analysed per file for many files which is an option
already supported by BRL-CAD. Also, BoT supports over 3 Bot mesh modes
which is highly advantageous over single mode supported by STL.

Furthermore, with the numerous advantages of BoT over STL, like single
and double precision, BoT solids have a fundamental problem of
inefficient editing. This project seeks to implement the import of
designs into BRL-CAD using the pipe primitive most likely from the
intermediate STL format.

## Detailed Description

I believe the computational geometry problem of approximating triangular
meshes describing pipes and pipe T- and Y-joints, using solid geometry
pipe structures instead.

`The original programs obviously model the lines and flows using data structures similar to pipes, not as triangular meshes. [Fluid analysis often requires some sort of finite element cell meshing, but I bet they are formed as needed, from the original pipe structures, instead of always describing the pipes as meshes.`

BRL-CAD has a pipe primitive, which takes a list of vertices the pipe
axis passes through, with inner radius, outer radius, and bend radius
for each vertex also specified. Note that there have been reports
(crashes) when the primitive is used, so I'm not certain how reliable or
well-tested the primitive is.

This problem shares certain interesting properties with another of my
favourites, angular momentum cancellation for nanocluster simulation.

The Bot to Pipe converter problem has a symmetry "axis", with a point
cloud surrounding that axis -- except that the "axis" itself is a vague
concept, and may even branch (T and Y joints) in this case. In many
ways, the pipe case is easier, since the mesh provides the vertex
connectivity graph.

# Unravelling Meshes

I'd start by unraveling the meshes.

Look at the triangular mesh connectivity graph. Given a specific vertex,
the circuit with the shortest 3D circumference (sum of Cartesian edge
lengths) containing that vertex, such that you cannot
short-circuit/bypass any of the vertices in the circuit, is a cross
section of the cylinder the mesh approximates at that point. (The
circuit obviously has to have more vertices than the maximum number of
sides in the vertex mesh polygons; otherwise you're just looking at a
single polygon.)

Such polygons are the shortest ones containing that vertex, that circle
the cylinder/pipe axis (the vertex mesh approximates) at that point.
Also a relatively straightforward way to analyse the mesh to obtain the
roughly-cross-sectional polygons would be:

-   determine the order of those polygons from the connectivity graph.

The above will give a stack of not-exactly-flat-but-close,
almost-circular polygons, forming the approximate cross sections of the
pipe. (The inner mesh will correspond to the pipe inner surface, and
outer mesh to outer surface. Because the 'pipe' primitive can only
describe pipes with symmetric walls, I'll assume the cross sections are
coaxial/concentric.)

Also, If the mesh is very coarse, it will not model a pipe, but a
twisted polygonal rod. If such data is prevalent in practice, I'd also
consider a completely different approach:

-   sweeping the meshes with spheres \[or cylinders, in practice\]. It
    will be a lot slower approach, although there are lots of
    mathematical tricks which can be employed to make it faster. Here,
    the sphere centers and radiuses form a set of intermediate data, to
    which the pipe parameters are fitted to.)

At joints, the mesh gets silly so I'll model everywhere else first, and
then extrapolate the joint properties last, using the mesh vertices as
helpful point cloud data only. (For example, for a T or Y joint, all
three legs of the joint tend to be straight. The point closest to all
three axis vectors is most likely the joint point.

-   Using Leg Information

Another option is to use the leg information to construct a prototype
joint, and compare the joint prototype to the mesh data, adjusting the
parameters to obtain the best fit.)

Any small-scale features at joints like the nooks used in old sewers
near tight bends, causing turbulence in the flow, keeping the bend clean
from debris -- are always lost, but that should not matter here anyway:
the 'pipe' primitive cannot model them anyway.

Overall, I think it's quite achievable to implement the triangular mesh
to pipe conversion -- either as a BRL-CAD command, or as an external
utility. A lot of work, but good results are certainly achievable.

## Deliverables

-   Implement a vertex reduction Algorithm based on user defined
    tolerances.
-   Implement options for allowing automatic generation of fluid
    components and option for automatic boolean operation in line and
    fluid regions.
-   Methods for calculate inner and outer diameters for BoT solid
    primitives.
-   Implement methods for determine pipe start and end points, solid
    bend radius.
-   Computing pipe solids for line model intersections.

## Development Schedule

Community Bonding period (April 21st to May 19th)( 3 weeks )

-   Acquaint myself with necessary version control svn for BRL-CAD.
-   Read appropriate documentation and programming regulations of
    BRL-CAD project.
-   Research additional information on BoT solid and pipe primitives and
    sharpen m y programming skills.
-   Work on BRL-CAD's tickets and bugs and earn commit privileges.

Pre mid-term work period (May 19th to June 20th) (2 weeks)

-   Determine BoT inner and outer diameters
-   Determine BoT inner and outer diameters

Week 3 - 4(2 weeks)

-   negotiate line models that have T or Y shaped intersections creating
    pipe solids for each leg

Week 5 - 6(2 weeks)

-   Implement the vertex reduction algorithm based on user defined
    tolerances (angular tolerance to define a straight segment)

Mid-term evaluation week (June 23rd to June 27th) (1 week)

-   Report work done within the pre mid-term work period.
-   Fill and submit mid-term evaluation form.

Post mid-term work period (June 30th to August 11th) (2 weeks)

-   Accurately utilize the pipe solid bend radius attribute to limit the
    number of vertices necessary to create a bend

Week 10 - 11(2 weeks)

-   Implement options allowing the automatic generation of a fluid
    component (fuel or hydraulic fluid within the line)

Week 12 - 14 (2 weeks)

-   Implement options that allow for automatic Boolean operations into
    both line and fluid Regions

Pencils down week (Aug 11th to Fri 15th) (1 week)

-   Final testing, debugging and removing memory leaks within code.
-   Documenting the BoT to Type Conveter for BRL-CAD.

Final evaluation week (Aug 18th to Aug 22nd ) (1 week)

-   Report work done within the post mid-term work period.
-   Fill and submit Final evaluation form.
-   Final submission of project code to Google.

Google Summer Of Code Aftermath period

-   Continue speeding-up several aspects of BoT to pipe converter.

## Time Availability

I'll be available to offer at least 40 hours a week for this project.
During periods of examinations, I will code less during weekdays and
make sure to catch up during the weekends. When I have events to
organise within GDG Bandjoun, I'll take a few hours of during the day to
do so and cover up for these lapses by pushing code at night. I'll also
regularly communicate the progress with my mentors by chatting on IRC,
writing on the mailing list and updating my diary.

## Why BRL-CAD ?

First of all, I really believe that software can change the world by
providing new technologies and that software should be free. I choose
BRL-CAD because it is a not-for-profit technology organization which
offers me the opportunity to assist the BRL-CAD organization with tools
for computer Aided design and computer graphics. Working with BRL-CAD
also helps me contribute over the long-term and gain status within the
hacker community based on my mathematical/Computing background and
academic interests. Although I have not contributed before to open
source ,I see implementing the BoT to Pipe Converter as a long-awaited
opportunity to make the world a better place and a jump-start to my
continued contribution to open source software through BRL-CAD.

## Why Me ?

I am passionate about working with BRL-CAD because I have always enjoyed
computing and Mathematical problems. Since my project has to do with BoT
to Pipe Converter, I am enthused to work on an efficient and precise
solution to this problem. My capacity to excellently communicate in
English and French will enable me easily interact with mentors on a
regular basis on the mailing list and IRC. With a deep knowledge of
mathematics from my post graduate and undergraduate experiences, a
deeply ingrained fact-finding habit and professional experience
developing software in C/C++, Java,although I have not contributed to
open source before, I believe I have the relevant experience to
implement the Bot to Pipe converter despite my new experience to CAD.

## Anything Else?