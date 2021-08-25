# OpenSCAD Importer Proposal

## Personal Information

-   **Student:** Andrei Ilinca
-   **Email:** andrei.ilinca24@gmail.com
-   **IRC Handle:** andrei_il
-   **Studies:** Second year student at the Faculty of Automatic Control
    and Computers, Polytechnic University of Bucharest, Romania
-   **Github:** [ailinca](https://github.com/ailinca)

## Background

I'm a sophomore at the Faculty of Automatic Control and Computers at the
Polytechnic University of Bucharest. This GSoC is my first opportunity
to work with the open source community and I can say I'm thrilled! Aside
of computer science, I am also interested in math. Since Primary School
I attended contests and got rewarded locally , citywide and national. I
enjoy solving various smart mathematical problems with applications in
all areas of research. When I'm not studying computer science, I enjoy
playing basketball, relaxing outside or taking part in acting classes.

## Project Overview

The project aims for making a OpenSCAD importer for BRL-CAD which would
essentially have the purpose of taking either a \*.csg file or a \*.scad
file (OpenSCAD formats ) and convert it to a .g file (BRL-CAD format).
As easy as that!

The project involves building a parser for .scad files that builds an
AST tree which then can be evaluated, saved and written in the proper
BRL-CAD internal logical structure.

I intend to use some of the OpenSCAD’s parser code in the project , as
it will significantly ease my way up. I’ve discussed with the OpenSCAD
devs and they said that there should be no problem in relicensing some
small bits of code in order to be used in BRL-CAD.

## Implementation Details

After a series of discussions on the mailinglist, this is my perception
the flow of execution:

<http://i.imgur.com/Y13sDjg.png>

Scad-g binary is responsible for taking a .scad as an input, parsing it,
generating the respective BRL-CAD logic (internally) then saving it as a
BRL-CAD database. (.g file) . Since .scad is a programming language,
parsing it will be the greatest challenge. I expect this part to be more
difficult, or at least, as difficult as generating the BRL-CAD
logic/structure associated with the .scad file.

The whole project idea can be broken down in two parts.

-   1\) Parsing the file and generating the BRL-CAD structure internally
    (my understanding is that the structure has to be generated
    “on-the-fly”, in the same time as parsing and since they can’t
    really be split)
-   2\) Changing the internal storing structure to .g format and saving
    it accordingly. Since parsing is already a difficult task, I will
    most likely just print/check that the information is correct, rather
    than storing it properly. This part involves changing what I already
    know that’s correct to the appropriate format. In example, use a
    tree instead of a generic list.

**Why I decided to stick to unknown technology rather than implement my
own mechanisms for parsing code?**

It’s an opportunity to learn, even if I expect having difficulties
wrapping my mind around lexer/parser functionality. There’s no point in
reinventing the wheel in terms of efficiency and it’s obviously not
realistic to expect to dodge learning something by simply redoing it.

Besides, I realized it’s a high chance that implementing a parser by
myself would extend the GSoC timeframe. All in all, it looks like the
best option.

The tools suggested by Clifford Yapp are lemon/re2c, initially, I
couldn’t tell the difference between two parsers, I wouldn’t know if any
was a good fit or not. My research so far hasn’t been, unfortunately due
to school assignments, exhaustive, but what I did find so far is that
BRL-CAD already uses lemon/re2c parser in a few given places. Thus, I
decided to use the above mentioned pair because I have a guarantee that
it can integrate seamlessly into BRL-CAD. I will be performing a much
more in-depth research, focused on lemon/re2c, during the community
bonding period. As a (rather far-fetched) observation, I plan to have
the csg parser built in a manner which facilitates adding .scad rules.

**scad-g structure**

<http://i.imgur.com/HHDlbAn.png>

Looking at 3dm-g file, I believe that my application structure would
involve a main class (ScadModel) having a set of methods to interact
with the parser, or actually parse. From what I’ve read, there are
methods using nextToken() and other helper methods, so I’ve added them
as well.

Another set of methods are the ones needed to build the .g hierarchy, I
believe these will be similar to a certain degree to what’s already
implemented, and there already are several helper methods for the
BuildHierarchy method.

## OpenSCAD formats

The main OpenSCAD file extension is .scad. That stands for every file
that you generate using OpenSCAD. However, there is also another format
that can be used which is the .csg .

Constructive solid geometry (CSG) (formerly called computational binary
solid geometry) is a technique used in solid modeling. Constructive
solid geometry allows a modeler to create a complex surface or object by
using Boolean operators to combine objects. Often CSG presents a model
or surface that appears visually complex, but is actually little more
than cleverly combined or divided objects.

Every .scad file can be exported to a .csg format because .csg are just
an intermediate step in the parsing of the language when generating the
graph. So, a good way to start is by making a .csg -&gt;.g importer and
then adding the extra features of the OpenSCAD format to become a
.scad-&gt;.g importer.

The most important differences between the 2 formats are the facts that
the CSG files do not contain expressions (so if ,in a .scad file we
would use a for loop with 3 incrementations, in the .csg we would have
to write each incrementation ) and modules (roughly comparable to macros
or functions in other languages).

Here we have a .scad file that generates a door stopper and uses the
OpenSCAD specific language.

<http://i.imgur.com/BX0II3U.png>

After exporting the .scad file to CSG, we can see that the 3D graph
generated is the same but the code format altered , resembling a clearer
geometry hierarchy.

<http://i.imgur.com/86jvLIM.png>

## BRL-CAD format

After application period ended, I was left with the impression that I
put a lot of effort into looking on what I have to parse and how could I
do it, but not that much in the end-goal/format. Afterwards, I read
about the directed acyclic graph (dag) that BRL-CAD uses to store its
information. The direct acyclic graph is, in fact, a tree. As suggested,
I've looked in the intaval converter files to get a better idea of the
importing process structure (reading external format and writing .g file
parts) and I believe I could reproduce the given example in order to
accomplish the tasks I've proposed.

My understanding so far is that there’s not an exact 1:1 match between
csg and .g/dag formats so the whole conversion process is going to be
best effort. This is probably a part where I will be needing a lot of
community guidance because maybe there’s not an exact correspondent but
rather a “ close enough” one.

## Project Deliverables

-   **May 25 (coding begins)** - I intend to start working right away on
    the class design, conceptual decisions and other implementation
    issues that might occur. The transition from the Community Bonding
    period should be effortless.
-   **June 26 (Midterm Evaluation)** - +/- 1 week. Have a fully (or at
    least successfully resembling) implemented .csg importer integrated
    in the present BRL-CAD conversion toolchain, tested and documented
    as needed.
-   **August 21 (Final Evaluation)** - Having an integrated .scad
    importer that can work with a variety of OpenSCAD files but missing
    some features (probably the special variables or the list
    comprehension)
-   **August 28 (Final Results Announced)** - Added the rest of the
    OpenSCAD cheatsheet components , making the necessary tests and
    verifications, fix bugs or other issues that may have occurred
-   **Until October 1st (school Starting)** - Stick around for
    maintenance, helping others with the I little I’ve learned, fix any
    minor tasks involving my project

It’s worth mentioning that my ultimate goal is to deliver functional
features, so having a functional csg will be a priority until it’s
succesfully done.

## Technical expertise

C was the first programming language I studied and it's the one I
currently use the most for academic purposes and contests. During my
first year summer break, I picked up Java, as I was keen to write code
that has a visual representation (swing). I did so by writing an app
which tracks how you spend your money and outputs some relevant
diagrams.

I'm glad I did as in the first semester of this academic year, I had a
course on C++. While C++ seems more difficult than Java, I believe that
my understanding of OOP concepts is good and that this project is a
great occasion to further improve upon it, especially the class design
part.

## Timeline

-   During the whole program, I expect to work an average of 45-50 hours
    per week, with less during mentioned circumstances and more when
    needed to catch up.

<!-- -->

-   This is an important aspect, which I can’t really avoid. In the
    first 2 weeks and a half (May 30 - June 19) I will have my summer
    exam session, so I believe I will be able to work an estimated
    amount of 5 - 10 hours per week (depending on how difficult the
    exams seem to me, it can fluctuate, but it won’t be below that).

<!-- -->

-   I intend to use my personal [wiki
    page](Andrei.ilinca24/logs.md) as a host for my work
    this summer.

<!-- -->

-   I will also log my progress (as much as I can) daily, so we can keep
    track of the evolution of the project and make adjustments to the
    timeline (if needed). I think I will be away for about a week
    somewhere in the middle of the summer (probably August, not sure
    yet) so I won’t be able to do any kind of work for the project in
    that period.

## Community bonding period

There are a few unknown variables I haven’t been able to break down and
evaluate until this point, I intend to use the community bonding period
(and the fluency period as well !) to figure this out. For once, I have
never actually written a parser before, so while I do believe I got a
decent theoretical grasp of principles, additional questions may pop up.

As a simple TO-DO list:

-   1\) figure out if there is any major difference between .csg and
    .scad, except of expressions and modules
-   2\) figure out what parser to use (if it’s yacc/bison or re2c or any
    other, I’ll get involved and research what benefits does each offer)
-   3\) figure out how to use it, have a very simple demo set up within
    BRL-CAD build hooks.

## Actual coding

-   **Week 1 (May 25)** -design the class at a conceptual level, have an
    (almost complete) UML diagram with the agreed upon design; begin csg
    parsing / interpreting
-   **Week 2-3 (June 1)** - minimal implementations detail, in example.
    parsing and interpret mechanisms for group, difference
-   **Week 4 (June 15)** - finishing group, difference
    parsing/implementation, code cleanup, tests
-   **Week 5 (June 22)** - implement parse and interpret for square and
    circle, sphere and cube, tests,code, cleanup.
-   **Week 6 (June 29)** - implement parse and interpret for the rest of
    csg primitives (polygon, text, cylinder and polyhedron), tests, code
    cleanup.

MID-term Evaluations

-   **Week 7 (July 6)** - extend .csg parser, implement parse and
    interpret for variable declarations and include, tests, code cleanup
-   **Week 8 (July 13)** - implement parse and interpret
    transformations, ideally all, at worst mainstream transformations
    (translate, rotate, scale, resize, mirror, multmatrix, color,
    offset, hull, minkowski )
-   **Week 9 (July 20)** - implement the parse and interpret method for
    mathematical functions (no boolean ops) and modifier characters.
-   **Week 10 (August 3)** - work on saving the current structure to a
    .g file (BuildHierarchy)
-   **Week 11 (August 10)** - probably the week off
-   **Week 12 (August 17)** - finishing saving file implementation to
    .g, performing tests (BuildHierarchy)
-   **Week 13 (August 24)** - safe backup for the implementation of
    BuildHierarchy, otherwise cleanup, further polishing and writing
    final report.
-   **Week 14 (August 31)** - upstreaming, fixing any issues encountered
    when merged into BRL-CAD

Final Evaluation

## Why BRL-CAD?

Well, honestly, I never used BRL-CAD before or any other CAD software
for that matter. My professional/personal path never met the
need/curiosity to use such a tool before. I have heard of BRL-CAD and
its interactive solid geometry editing(at a presentation, described
below) but I never really got to use it. In fact, I had never used
Photoshop or any other "graphic" program until BRL-CAD.

I know it doesn't sound like a promising start but bear with me.

Recently (since I started college), I heard about the open source
concept. At first, I was puzzled. "Why would someone work for free? How
can they ..uhm .. exist?" I did some research and understood the whole
process a bit more. I didn't actually write any patch, the one I
submitted a few days ago is the first, but the prospect of being able to
showcase my work, to have other people use something that I did (which
never happens throughout my academic endeavours) made me realise that
it's worth investing time and effort in. I learned about git, svn,
sourceforge and Linux bash from friends who graduated or are going to
graduate this year. I kept asking them questions about open source and
this is how I learned of GSoC.

It was difficult to pick an organisation from the list of accepted orgs
as I kept asking myself "Why would the respective org need me?", "How
can I know I can do what I propose?" There was a presentation held at
our university about students that previously participated in GSoC and
that's where I first heard of BRL-CAD. BRL-CAD was not my first choice
as based on the students' presentation I believed it was simply too
difficult for me, at the current level.

I felt really panicked and confused as no matter how much effort I put
in there was little progress. So, I took the decision to change ... and
I landed on BRL-CAD page, looking for a project that maybe I can
understand. What made me stay on BRL-CAD's GSoC page and the aspects
that attracted me the most in the idea of working for this org in the
first place were the friendly getting-started guides and the detailed
explanation about BRL-CAD's intentions for this GSoC. As I mentioned in
the introductory mail, I feel more motivated investing time and effort
knowing the situation. Above that, and it might seem ordinary to you, I
really appreciated the support that I've got since and the feedback from
you guys, it has proven to be very useful.

Regarding the project I've chosen , the OpenSCAD Importer was not my
first choice, as the link on the project ideas page seemed broken at
that time (I believe it still is). Though , after the feedback received
from mentors (which lead to a better, actually - a basic understanding
of what it involves), I've decided that this project would be an useful
feature to work on for the BRL-CAD community and also a very good way to
improve my desired coding skills, bonus points to making my first major
open source contribution.

## Why me?

Because I really like programming and I really believe that, by working
on this project, both BRL-CAD and myself will have some valuable
benefits (I’m planning to continue my collaboration with BRL-CAD for as
long as needed in order to deliver the fully working, documented and
implemented OpenSCAD importer) .

Because I’m very excited to take part in such an extensive project and
my motivation towards making a good impression and learning some real
world skills is genuine. On that note, I believe you can be certain of
my dedication and strive to achieve the necessary abilities to complete
the project tasks.

So far, I hope I fulfilled the [Acceptance
guidelines](/wiki/Summer_of_Code/Acceptance.md) and also followed the
[Application
guidelines](/wiki/Summer_of_Code/Application_Guidelines.md).  Here is
a [link](https://sourceforge.net/p/brlcad/patches/329/) to my first
ever open source patch and, hopefully, not the last for BRL-CAD ,
regarding the importer logic and also following the HACKING guide.

As a last note, to be honest, I don’t have any really amazing reason to
showcase (like previous industry experience on CAD, previous GSoCs etc)
but … that’s a reason in itself.

Thank you for taking the time to review my proposal!

I’m looking forward to working with you this summer!
