## Personal Info

Hello, my name is Chris. I'm a first year mathematics student at the
University of Waterloo (Canada) with a strong interest in computer
science and programming.

## Contact Info

email: crdueck@uwaterloo.ca

irc: crdueck (find me on freenode, I'll be in \#brlcad)

## Programming Experience

I have experience with C (as well as Scheme and Python), and would be
more than happy to have an opportunity to learn some C++ while working
on my project.

Most of my experience so far has come from school assignments,
[projecteuler.net](https://projecteuler.net) (programming challenges
with a mathematical twist, check it out if you haven't heard of it
before), and small personal pet projects.

I have knowledge of data structures and algorithms from my courses at
school.

I have a solid foundation in basic university level mathematics (one of
my primary reasons for wanting to participate in GSoC is to further my
mathematical knowledge in the subject of computer generated models)

## Project Summary

##### Primitive Volume and Centroid Fuctions

Currently, most primitives in BRLCAD do not have volume, centroid, or
surface area functions. My goal is to implement volume and centroid
functions for many of these primitives.

The primitives I have chosen are mostly simple solids of revolution or
other simple shapes and thus it will be easy to construct explicit
formulas for their volumes and centroids.

As well, I will be refactoring major sections of mged's analyze command
so that it makes use of the functions I will be adding. I also plan on
cleaning up the comments found in the source code that I will be working
on throughout my project.

## Proposal

My primary references for this project will be found in
src/librt/primitives. I will be adding the new callback functions to the
existing source code for each primitive. The relevant parameters that I
will use for computing the volume and centroids will come from the
rb_\*_internal struct. I will make use of the existing API functions
to manipulate this struct and its parameters as much as possible. Using
my knowledge of solids of revolution, I will then derive formulas for
the volume and centroid for each primitive and implement these as
readably, concisely and efficiently as possible.

My reasoning behind choosing to implement both a volume and centroid for
some of the primitives as opposed to just one function for all
primitives is that I believe it will be easier to implement the second
function after I've already spent time becoming familiar with the
primitive through my work in implementing the first. In this way I can
implement twice the number of new functions for the cost of becoming
acquainted with one new primitive.

I plan to test my new functions using mged's analyze command (as this is
how the volume and centroid information will primarily be presented to
the user. However, separate mged commands could be created to
specifically display either the volume or centroid of a primitive. This
is outside the scope of my project, but a potential focus for after
GSoC). To this end, I will be rewriting substantial portions of
libged/analyze.c in order to make use of my newly added functions. There
are many opportunities for refactoring in the analyze_{primitive}
functions and some opportunities to write new analyze_\* functions
(there is currently no analyze_pipe). My work will make the source code
for analyze considerably clearer and more concise.

I will develop a series of test cases for each primitive using analyze
to ensure that my functions are working as expected. This will include
verifying that my volume/centroid functions are returning correct
values, and verifying that the other outputs of analyze are correct as
well.

While I am working on the source code for a primitive, I will take time
to clean up the comments and move them from the \*.c source code file to
the appropriate \*.h API header file. I will make changes to the
formatting if needed, check for typos and other such documentation
related tasks. This is a simple task that will not detract from my main
focus of implementing volume and centroid functions.

During the summer I expect to devote much of my time to fulfilling this
project. I have no major prior engagements and will be able to spend a
full 40+ hours per week on my commitments to BRLCAD. During this time I
will make a strong effort to remain in close contact with my mentor,
providing updates on my progress, as well as any obstacles I come across
or questions I may have related to the project. I will be active on the
\#brlcad channel and mailing list in an effort to hopefully contribute
to the growth of BRLCAD outside the scope of my project.

## Deliverables

-   Volume and centroid functions for the following:
    -   ell (and sph)
    -   tor
    -   rec
    -   rcc
    -   hyp
    -   arb8
    -   arbn
    -   pipe

<!-- -->

-   Improved documentation for each .{c,cpp} file in:
    -   ell
    -   tor
    -   rec
    -   tgc
    -   hyp
    -   arb8
    -   arbn
    -   pipe

<!-- -->

-   Refactored analyze_\* functions in libged/analyze.c for:
    -   ell
    -   tor
    -   tgc
    -   hyp
    -   arb
    -   pipe

## Revised Deliverables

-   Volume, surface area and centroid functions for the following:
    -   ell (and sph)
    -   tor
    -   tgc and derivatives (rcc, rec, trc, tec)
    -   arb8
    -   bot
    -   epa
    -   eto
    -   part
    -   rpc
    -   sketch (only surface area)

<!-- -->

-   Refactored/new analyze_\* functions in libged/analyze.c for:
    -   ell
    -   tor
    -   tgc
    -   arb8
    -   arbn
    -   bot
    -   epa
    -   eto
    -   part
    -   rpc
    -   sketch
    -   ars

## Timeline

-   Present - May 21
    -   compile BRLCAD from SVN source, ensure build environment is
        working
    -   become familiar with submitting patches to SVN
    -   become familiar with source code in librt/primitives and
        libged/analyze.c
    -   get comfortable with using mged to generate and test primitives
    -   participate with the BRLCAD community on irc, mailing list etc

<!-- -->

-   Week 1 (May 22nd to 27th)
    -   implement a volume and centroid function for ell
    -   rewrite sections of analyze_ell
    -   test implementation for correctness

<!-- -->

-   Week 2 (May 28th to June 3rd)
    -   implement a volume and centroid function for tor
    -   rewrite sections of analyze_tor
    -   test implementation for correctness

<!-- -->

-   Week 3 (June 4th to 10th)
    -   implement a volume and centroid function for rec and rcc
    -   rewrite sections of analyze_tgc
    -   test implementation for correctness

<!-- -->

-   Week 4/5 (June 11th to 24th)
    -   implement a volume and centroid function for arb8 and arbn
    -   rewrite sections of analyze_arb
    -   test implementation for correctness

<!-- -->

-   Week 6 (June 25th to July 1st)
    -   move comments from each of the primitives visited so far to the
        appropriate header files

<!-- -->

-   Week 7 (July 2nd to 8th)
    -   time to review code, more testing

<!-- -->

-   Week 8 (July 9th to 15th)
    -   prepare midterm evaluation
    -   discuss with my mentor which primitives I have chosen to
        implement surface area functions for

<!-- -->

-   Week 9/10 (July 16th to 22nd)
    -   implement a volume and centroid function for pipe (lin_pipe and
        bend_pipe)
    -   write analyze_pipe
    -   test implementation for correctness

<!-- -->

-   Week 11/12 (July 23rd to August 5th)
    -   implement surface area functions for chosen primitives
    -   \~to be updated with list of primitives\~
    -   test implementations for correctness

<!-- -->

-   Week 13 (August 6th to 12th)
    -   move comments from additional primitives to the appropriate
        header files

<!-- -->

-   Week 14/15 (August 13th to 26th)
    -   final testing, code review to ensure all functions are working
        as expected
    -   prepare final evaluation

## Revised Timeline

starting from july 13th

-   Week 8/9 (July 13th to 22nd)
    -   continue work on an area function for the sketch primitive
    -   finish bezier approximation function using circular arcs
    -   implement a tesselation algorithm for the sketch primitive for
        use in rt_sketch_tess() and rt_sketch_surf_area()

## Me & GSoC

I want to participate in GSoC 2012 for many reasons. Firstly, to develop
a stronger understanding of how mathematics is implemented through
programming in the real world. My courses at school consist of a lot of
theory, and I haven't seen much of the application side of things yet.
When searching for a potential organization to apply to, I knew I wanted
to work on mathematics related software, and BRLCAD caught my eye right
away.

I also hope to greatly expand my programming skills in a real world
development setting. I feel that I can improve myself as a programmer by
leaps and bounds this summer by working with the devs at BRLCAD. This is
also a great chance to get involved with the open-source community. As
an avid user of open-source software, contributing back to an
open-source project has been something I have wished to pursue for a
while now, but am just recently confident enough in my skills to be able
to meaningfully contribute.

If accepted, I plan on continuing my involvement with BRLCAD after GSoC
ends, moving on to more challenging tasks. In particular
[this](http://brlcad.org/wiki/General_Tree_Walker) project interests me
as I have a good deal of experience working with trees from my Data
Structures course at school. Having already invested some time
familiarizing myself with BRLCAD's source library, I'm considering
completing some of my proposed goals this summer even if my application
is unsuccessful.

## My Patches

As a warm up to gain knowledge about the internals of BRLCAD, I decided
to implement a volume function for a simple primitive. After some
discussion on \#brlcad, I chose a ell for its simplicity. You can find
my patch notes
[here](https://sourceforge.net/tracker/?func=detail&aid=3513421&group_id=105292&atid=640804).

After gaining some familiarity with how primitives are handled, I
decided to implement a surface area function for ell as well. Patch
notes can be found
[here](https://sourceforge.net/tracker/?func=detail&aid=3515075&group_id=105292&atid=640804).

If you have any comments on these patches please let me know :)