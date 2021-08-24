# Personal Information

-   Name: Bogolin Simion Vlad
-   E-mail address: vladbogolin@gmail.com
-   IRC username: vladbogo

## Background info

I am a third year student at Polytechnic University of Bucharest,
studying computer science and engineering. The main areas that I am
interested in are: algorithms, computer graphics and operating systems.

### Skills

My skills consist in a strong background in algorithms and data
structures. As it comes to programming languages I prefer C/C++ and
Java, in which I also have more experience (about 2 years in Java and
more than 6 years with C).

-   Other programming languages I have experienced: Python, Haskell,
    Scheme, Bash Scripting, Matlab, Assembly language, Clips, Prolog.
-   Versioning tools: I am quite familiar with Git ( I have developed a
    team project using it: Ants) and SVN ( currently developing a school
    project using it: File-sharing system).

### Projects

-   Labirinth: it's a game in which the character is trapped in a maze
    and he has to find the portal that takes him out.
    -   Required skill: C++, OpenGL, GLUT, data structures and
        algorithms.

<!-- -->

-   SpaceEscape: a game in which the character is placed in a spaceship
    and he has to run away from enemies. Unfortunately, he has driven
    his spaceship in an asteroids field and needs to get out by avoiding
    or destroying the asteroids.
    -   Required skills: C++, OpenGL, GLUT, data structures and
        algorithms.

<!-- -->

-   Ants: a Java team projects based on ants game from AIChallenge,
    developed using Git. Ants is a multiplayer game in which every
    player is given a small colony of ants. The objective is to destroy
    all enemy ants.
    -   Required skills: graph algorithms(BFS), data structures and
        Mini-Max algorithm.

<!-- -->

-   Other projects: Below you can find a link to a git repository where
    you can find some of my past projects. Unfortunately, the README and
    the comments for them are in romanian because some of them were
    school projects, but if needed I can provide further information.
    -   <https://bitbucket.org/vladbogo>

# Patches

In order to make a better idea about the project I have made a first
patch:

-   Adding a text display manager. The code can be found at the
    following link:
    -   <http://sourceforge.net/p/brlcad/patches/163/>

This was a first step in order to understand the code. In order to
implement it the first step was to see how libdm works and how are
display managers related to mged. After, inspecting mged/attach.c and
modifying it, it was possible to select the new display manager (txt).
All I had to do after this, was to make the callback functions from
libdm print a particular message.

# Project Information

## Project Title

Code refactoring: eliminate display manager related sources from mged
folder.

## Brief project summary

This project aims to eliminate all display manager related sources in
the mged folder. BRL-CAD’s main interaction with display managers is
done using libdm library. However there still are some dm related
sources in mged which makes understanding and finding dm related
features harder. Because of this, after talking on IRC I consider this a
good project for Google Summer Of Code that will help BRL-CAD. During
this refactoring, I will try to optimize the code as much as possible so
that there can be an improvement in functionality too.

One of the biggest problems I have identified is the fact that in some
cases there is a strong dependency between display manager related files
and mged. This is a sensitive matter and requires a lot of discussions
on IRC in order to decide which feature goes where.

## Description

### Basic steps

The first step in order to complete this project would be to identify
all display manager features that need to be refactored. Secondly, I
plan to use a easy to hard approach. During first step I will identify
the “easier” tasks and then start working on them. With every step, I
will increase the difficulty until the project is finished. Finally, all
dms files from mged must be refactored.

### Approaches

In order to make a good project I plan to do as following: I will start
with small functions that are easier to move than I will continue with
more and more complex functions. I think that in this way I will be able
to be more productive and I will identify problems that will appear
easier. I think that in this project there will be a lot of unexpected
problems but I am sure that I will be able to complete it. Next I will
make a brief summary of what needs to be changed and explain how I will
approach every task.

The display manager sources in the mged folder have the following
structure:

-   mged_dm.h - Header file for communication with the display manager.
    One of the most difficult task will be to decide what has to be
    moved and what not, because here are defined both: mged and also dm
    features.

<!-- -->

-   dm-generic.c - Source for generic features. Even though it’s
    basically just one function, moving this will be one of the most
    problematic tasks because there is a strong dependency between
    dm-generic.c and other mged sources (scroll.c, menu.c, etc.). In
    order to solve these dependencies I plan to create a new header file
    that deals with them.

<!-- -->

-   dm-DMNAME.c - Source for defining routines for a particular display
    manager. Dealing with just a particular dm, the dependencies between
    these files and other mged sources, are lower than in the generic
    case. I will try to solve this by adding functions to struct dm from
    libdm.

<!-- -->

-   other sources: doevent.c which is the X event handling routine.

### Features

In order to make the project code more readable there should be a
maximum organization when it comes to writing code. As I saw, BRL-CAD
tries to have specialised libraries for every feature it provides which
makes the code more organized. This project will add a plus of
organization to BRL-CAD’s actual code.

#### Refactoring particular display managers

BRL-CAD’s library for display managers is libdm. DM is the primary means
with which BRL-CAD interacts with geometry. Basically, libdm is a set of
callback functions. In order to make a complete refactor of mged-dm I
plan to add new functions to struct dm, and make a different
implementation for every display manager. If there are any functions
that are not common to all of the dm’s I will choose between adding the
function to struct dm ori creating another header file. In order to take
the best decision I will consult with my mentor. I consider that the key
of this project is a good communication between me and the community.

First of all, I will start with the init_dm function that are declared
in attach.c (the initialization is made when the dm is attached). As I
saw that this functions are common to all dm’s, so I will add a new
callback function to the actual implementation (struct dm - dm.h).
Another function that will be dealt in the same way is fb_open. The
framebuffer must be opened so that the display manager could be used.
This should be also part of struct dm being needed for every graphical
display manager.

Other functions that will be dealt in the same way are the event
handlers. But sure there are some functions that are not present in all
dm’s. In this case, I will either add a new entry in struct dm and leave
it null for the dm’s that do not support it, or I will try a different
approach, that includes different headers depending on which dm is used.

A important thing I must keep in mind while refactoring is the fact that
BRL-CAD is cross-platform and I should modify existing libraries in an
appropriate way.

## Testing

In order to make a good project writing code is just not enough so I
will highly focus on testing especially on this project where the actual
success is measured in maintaining functionality after refactoring. A
lot of test must be done after every stage of the project. Also, it may
be a good idea to make some cross-platform tests (Linux and Windows),
because being cross-platform is one of the main features of BRL-CAD.

Testing will try to focus on every key aspect of every function. Another
key aspect in testing is that all display managers must be tested. There
cannot be done any presumption such that “if it’s working using ogl it
should also work using X”.

Testing will also use the dm command which provides a means to interact
with the dm at a lower level.

## Documentation

During my work on this proposal a lot of documentation had to be read.
Even though there are not any particular algorithms, I will describe how
I approached this project.

Working on the first proposal, I experienced a lot of difficulties in
navigating through the code. I kept constantly forgetting that there are
also dm features implemented in mged folder. At first it took me a while
to find out that there are display manager functions in mged. I remember
that I was focusing on “X_dm_init” declared in attach.c and I couldn’t
find it’s definition. Finally, after using ack-grep I was able to find
it.

## Deliverables

Because of the complexity of this project it can be divided in various
ways. First off all I must say that in order to reflect the progress I
will make frequently commits so that every change can be tracked (so
that the progress can be seen at every step). I consider that the
success of this project consists in being organized and make a lot of
commits so that it can be really easy to revert in case something goes
wrong.

As it comes to measurable specific goals the primary ones are to have
the whole code moved and not to lose any of the functionalities. This
primary goals can be divided in subgoals according to the steps
described above:

-   refactor every particular dm
-   refactor dm-generic.c

# Schedule

This is a rough plan that I am I sure I will be able to follow. I hope
that every feature will be ready before the scheduled time. After
researching, I am sure that this is a realist schedule that I definitely
can follow. In the schedule below I have also included time for
unexpected delays or some breaks but I haven’t explicitly mention that.
As planned the project has to be ready with at least 2 weeks before the
final deadline and I will make any necessary efforts for this to happen.

-   Week 1 (17 June - 24 June): Look even more on the code to see
    everything that I might have missed during the application period. I
    plan to look until the official starting date but I do not know if I
    will have time because this period overlaps with my exams period so
    I will be busy. If I will consider that everything is understood, I
    will start working effectively and writing code. Understanding the
    code it’s the biggest problem in this project so I won’t skip this
    step until I am certain that everything is clear.

<!-- -->

-   Week 2 (24 June - 1 July): At least at this time I will be already
    working. I will start with dm-plot and dm-ps because the files
    contain small functions that should not be very hard to refactor.

<!-- -->

-   Week 3-4 (1 July - 15 July): Start working at rctg-dm. In order to
    be sure I will finish, I scheduled 2 weeks time for this task for
    any unexpected problems.

<!-- -->

-   Week 5 (15 July - 22 July): Start working at ogl dm. These next
    task, I consider I can finish in one week because I already did the
    rctg display so I already know the workflow.

<!-- -->

-   Week 6 (22 July - 29 July): Preparing mid-term evaluation

<!-- -->

-   Week 7 (29 July - 5 August): However if there are a lot of
    unexpected problems with ogl I scheduled just to be sure one more
    week. Finishing working at ogl dm if there still is some work to do.
    In this week there will also be a short break.

<!-- -->

-   Week 8 (5 August - 12 August): Start working at wgl dm. After
    dealing with ogl I think one week is enough.

<!-- -->

-   Week 9 (12 August - 19 August): Start working at X dm and
    successfully refactor it.

<!-- -->

-   Week 10 (5 August - 12 August): Start working at tk dm and
    successfully refactor it.

<!-- -->

-   Week 11 - 12 (5 August - 9 September): Start working at generic-dm
    and finish the project.

<!-- -->

-   Week 13 - 14 (9 September - 27 September): Final testing and
    submitting the final application.

# Time availability

I can say without any doubt that I can fulfil the minimum required time
of 40 hours / week and if necessary I can work extra. This project is
really interesting to me so I will invest as much time as it need in
order to finalized it.

## Known commitments

-   Exams: my exam period ends on 14 June so it does not overlap with
    the official schedule, but I must say that until then I won't be
    able to start working 100%.

<!-- -->

-   Vacations: I plan to take about a week (not necessary continuous
    time) of vacation during the summer. Probably there will be some
    free days after my exams period also. I don't think this is a
    problem because I plan to take this vacation accordingly to my
    progress on the project and after consulting with my mentor.

# Why BRL-CAD?

First of all, I must say that I am really interested in open-source
programming. From the first year in college when I had my first
encounter with open-source, step-by-step I understood the role of
open-source. I consider open source a very good way to be on, in order
to boost your knowledge. Another major advantage is the community which
helps you overcome a lot of problems that appear on the way. Actually,
this is one of the top things I like about BRL-CAD: the community.
During my short time spend on IRC, every time I encountered a problem
someone answered and gave me enough details in order to overcome it.

Secondly, even though at first I haven't known about what BRL-CAD does
(except I had a small idea from the name CAD), after talking on IRC I
decided to apply for this project. I think that after finishing it, I
will improve a lot my programming skills and I will learn to write
efficient code.

# Why me?

First of all, I am really enthusiastic to work to an open source
project. Until now, I have worked on small projects so I am really eager
to start working on a large project. Also, I think that this is a great
opportunity to learn new things that will help me, so this makes me even
more enthusiastic about the project.

Least but not last, I must say that I consider that I have all the
necessary skills in order to complete this project. I do not back away
from difficult tasks and I am fully committed to finishing the project.
I also plan to be an active developer in BRL-CAD after GSoC is over.

Moreover, after finishing this project I will know every display manager
internal used by mged which will make me eager to contribute more. I
consider that this is one project that will help me improve my
programming skills. I expect to encounter a lot of problems (in my
opinion, in every projects it’s impossible to consider all the aspects
that may appear, especially in code refactoring) but this makes me even
more enthusiastic about the project.

Finally, I want to thank you for taking time to read my proposal. I hope
we will collaborate during this summer but also after GSoC.

Also, I want to mention that New Cross-Platform 3D Display Manager is my
preferred project.

Simion Vlad Bogolin