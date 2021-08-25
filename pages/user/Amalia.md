#### CONIC CURVE SUPPORT FOR LibreCAD

#### INTRODUCTION

## Personal Information

Name: Ngassa Amalia Finjap

Email: ngassafinjap@gmail.com

IRC Nick: amalia237

Github : Ngassa

Google+ Handles: Ngassa Amalia

Time Zone: UTC + 01:00

Brief Background Information: I am Ngassa Amalia, a senior year
management science major from the Catholic University Institute of Buea,
Cameroon who's interested in participating in Google Summer of Code
under LibreCAD. I am ready to work for for over 40+ hours on my project
during the summer holidays and will do everything to meet my project
goals on nights and weekends even when my tests and examinations come
up.

#### PROJECT DESCRIPTION

## Project Title: Conic Curve Support for LibreCAD

## Brief Project Summary

It has been observed that designers start from using small shapes called
primitive to attain more complex ones. This project aims at building
conic curve support into the LibreCAD software package by implementing
the hyperbola and parabola primitives entity types. This will enable
users of the LibreCAD software to use conics in modeling the Dulles
Airport Tower in Virginia, process just as in the . Hyperbolas in
particular can be used in preliminary sketches of beautiful butterflies,
nuclear cooling towers, hyperbolic shadows on the wall, hyperbolodial
gears in skew shafts and buildings while parabolas can be used by
architects to design rainbows, suspension bridges, roller coasters and
much more. During this Summer of Code period, I'll be incorporating
these two primitives into LibreCAD by defining necessary classes and
implementing member functions within interface and implementation files
(lc_hyperbola.h, lc_parabola.h and lc_hyperbola.cpp,
lc_parabola.cpp) in librecad/src/lib/engine/ and librecad/src/actions/.

## Detailed Project Summary

Here, I give more detailed information on how I intend to build conic
curve support into the LibreCAD software package. From my recent studies
of the ellipse and circle primitives (rs_circle.\* and rs_ellipse.\*)
in librecad/src/lib/engine/, I observe that for each primitive type is
designed as a class with data members which are attributes of that
primitive and member functions implementations which define properties
of the primitive. In LibreCAD, the framework of engine (math) support
for ellipses can be applied readily to hyperbola/parabola, so only minor
extension is needed to get those features. This is primarily because
LibreCAD equation solvers can solve quartic equations.

# Hyperbola

The equation of the hyperbola is (x-x0)^2/a^2 – (y-y0)^2/b^2 = 1.

The hyperbola will be defines as a class with data members ;

-   center
-   majorP ( a in equation above)
-   ratio ( of minor radius to major radius)
-   angle1
-   angle2
-   reversed ( whether it's reversed or not )

Dongxu Li already started implementing the hyperbola primitive in
lc_hyperbola.\*. In the lc_hyperbola.h interface file, the Hyperbola
Data and Hyperpola Entity classes are defined and their data members,
corresponding accessor and mutator functions as well as other predicate
functions are declared. In the lc_hyperbola.cpp implementation file,
the member functions of the above classes are implemented. However, I
think functions like the following still have to be implemented (and of
course much more)

-   Computing the direction of tangents at some points
-   Create a hyperbola from equation
-   Scale a hyperbola
-   Rotate a hyperbola
-   Move a hyperbola
-   Draw a hyperbola
-   Determine if a point is on the hyperbola
-   etc still have to be implemented.

I am ready to follow Dongxu Li's instructions to do any clean-up and
modifications to the hyperbola primitive which he started implementing.

# Parabola

The equation of the parabola with vertex (x0, y0) which opens downwards
is (y-y0)^2 = 4a(x-x0)

The parabola will be defined as a class with data members ;

-   vertex,
-   focus,
-   latus rectum,
-   flag for direction in which parabola opens up. Or the rotate
    functions will come in handy to replace this data member.

The parabola with vertex (x0, y0) which opens upwards is given by the
equation (x - xo)^2 = 4a(y – yo). To implement the parabola primitive,
we define Parabola Data and Parabola Entity classes with their data
members and declare their corresponding geometric member functions in
lc_parabola.h. In the lc_parabola.cpp implementation file, I'll be
implementing the geometric member functions of the aforementioned
Parabola classes. The geometric member functions to be implemented
include;

-   Computing the position vector of the focus.
-   Compute focal length
-   Create a parabola from equation
-   Find the tangential points and directions from a given point
-   Rotate a parabola
-   Scale a parabola
-   Mirror a parabola against a given axis
-   Draw a parabola
-   And much more

## Links to some Pictures

1\. <http://www.pleacher.com/mp/mlessons/calculus/apphyper.html>

2\. <http://britton.disted.camosun.bc.ca/jbconics.htm>

3\.
<http://www.thecoastercritic.com/2010/04/intimidator-carowinds-roller-coaster-reviews.html>

4\. <https://mschrist.wikispaces.com/Art>

5\.
<http://en.wikipedia.org/wiki/Parabola#/media/File:Parabola-antipodera.gif>

## References

-   <http://mathworld.wolfram.com/Hyperbola.html>
-   <http://mathworld.wolfram.com/Parabola.html>
-   <http://en.wikipedia.org/wiki/Parabola>
-   <http://en.wikipedia.org/wiki/Parallel_curve>

#### PROJECT TIMELINE

## Deliverables

Pre Mid-term evaluation goals

1\. Define the Hyperbola Data and Entity classes.

2\. Declare the geometric member functions.

3\. Write the lc_hyperbola.cpp file.

Post Mid-term evaluation goals

4\. Define the parabola Data and Entity classes.

5\. Declare the geometric member functions.

6\. Write the lc_parabola.cpp file.

## Development schedule

# Community Bonding Period ( April 27th - May 24th )

-   Study LibreCAD's manuals and documentation.
-   Study LibreCAD's code base to understand project more.
-   Refine my project proposal based on updated knowledge.
-   Write patches and remove bugs.
-   Discuss with other developers and LibreCAD mentors on project
    orientations.
-   Brush up my C++, Qt Creator and git development skills.

# Pre Mid-term Evaluation Work Period ( May 25th - June 25th )

Week 1 (May 25th - May 29th)

-   Defining the Hyperbola Data class
-   Defining the Hyperbola Entity class

Week 2 (June 1st - June 5th)

-   Computing the direction of tangents at some points
-   Create a hyperbola from equation

Week 3 (June 8th - June 12th)

-   Scale a hyperbola
-   Rotate a hyperbola

Week 4 (June 15th - June 19th)

-   Move a hyperbola
-   Draw a hyperbola

Week 5 (June 22nd - June 26th)

-   Determine if a point is on the hyperbola
-   Return the equation of the hyperbola as LC_Quadratic to aid in
    finding intersection points between any LC_Quadratic object and a
    hyperbola.

Week 6 : Mid-term Evaluation Week ( June 29th - July 3rd )

-   Offset function to compute the direction and distance of an offset
-   Fill mid-term evaluation form.

# Post Mid-term Evaluation Work Period ( July 6th - August 20th )

Week 7 (July 6th - July 10th)

-   Computing the position vector of the focus of the parabola
-   Compute the area occupied by the parabola

Week 8 (July 13th - July 17th)

-   Return the equation of the parabola as LC_Quadratic to aid the
    finding of intersection points between any LC_Quadratic object and
    the parabola.
-   Compute focal length of parabola

Week 9 (July 20th - July 24th)

-   Create a parabola from equation
-   Find the tangential points and directions from a given point on the
    parabola

Week 10 (July 27th - July 31st)

-   Rotate a parabola
-   Scale a parabola

Week 11 (August 3rd - August 7th) Mirror a parabola against a given axis
Draw a parabola

Week 12 & 13 - Pencils down Period ( August 10th - August 21st )

-   Offset member function to compute the direction and distance of
    offset
-   Continue integrating conics into other aspects of LibreCAD.
-   Testing and debugging of librecad/src/lib/engine/{lc_hyperbola.\* &
    lc_parabola.\*} code.
-   Documenting conic curve primitives in LibreCAD.
-   Producing animated videos of conics from LibreCAD.

Final Evaluation Week ( August 24th - August 28th )

-   Fill Final evaluation form
-   Submit code to Google

## Time availability

I'll be available to start and finish my Google Summer of Code project
from May 25th through August 25th 2015 wherein I'll work 40+ hours
weekly. To compensate for examination periods in school, I'll work
harder during nights and weekends to make sure I meet the goals of my
project.

#### ABOUT MYSELF

## Why LibreCAD ?

First off, the very word “Libre” in LibreCAD is a word I like because I
love the french language. I chose LibreCAD because it's an open source
community-driven initiative and is aligned with my dream of serving
within a game-manufacturing software company.This dream will become
materialized with sustained contributing to LibreCAD and learning about
Computer Aided Design erstwhile.

## Why Me ?

I got introduced to computers (my dad literally imposed that on my
siblings and I) when I attended the LUKMEF computer training in Limbe,
Cameroon. After that I got interested in computer programming in C/C++
and the Organizers of the Google Developer Group Buea helped orientate
me on how to learn programming. I've used Linux OSes especially Ubuntu
since 2013 and would really be happy to get introduced to open source
development through LibreCAD through the Google Summer of Code 2015
program. In November 2014, I helped set up FATE Automated Testing System
in ffmpeg,the open source multimedia framework , on the Fedora 20
platform and submitted the results to fate.ffmpeg.org. If I am selected
for the program, I will make sure I communicate my progress on a daily
basis by chatting on IRC and writing on the mailing lists.

## Anything Else

I believe that software development is about passion and not about what
students major in while at University. Selecting me will really pass
across a message that gender and race doesn't matter in open source
development with LibreCAD and would encourage more students ( especially
girls ) who aren't Computer Science/Engineering majors to get interested
in Computer programming.

# DEVELOPMENT SCHEDULE

-   My development is kind of my Google Summer of Code Log
    Book. Anyone can view it [here](Development_logs.md).
