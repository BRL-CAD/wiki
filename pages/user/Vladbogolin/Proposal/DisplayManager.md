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

<!-- -->

-   Versioning tools: I am quite familiar with Git (I have developed a
    team project using it: Ants) and SVN (currently developing a school
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
libdm print a particular message. While working at the second patch, I
have discovered an improvement that can be done, but unfortunately I
didn't have time to implement it because of my exams period. Now, in
order to select the txt dm, I have added an if clause. This is not the
best approach. A better approach would be to create a init function
(attach.c) in which the open method that returns the struct dm needs to
be called.

-   Refactor X_open_dm from dm-generic.c. The code can be found at the
    following link:
    -   <https://sourceforge.net/p/brlcad/patches/179/>

In order to remove the \#ifdef from dm-generic.c, I have added a new
callback function dm_open in struct_dm. Also, I have created a new
function dm_select (defined in dm-generic.c) which selects the dm. At
the moment, it only selects X dm. The function returns the primary dm
struct (dm_X) and then there is necessary to call the open method from
struct_dm. To refactor all dm’s it is necessary just to add the open
function to struct dm(now it’s NULL) and to call it in mged/dm-\*.c.

-   Eliminated some warnings from brep.cpp. The code can be found at the
    following link:
    -   <https://sourceforge.net/p/brlcad/patches/184/>

# Project Information

## Project Title

New Cross-Platform 3D Display Manager

## Brief project summary

The purpose of this project is to create a new cross-platform 3D display
manager. A display manager is the primary means with which BRL-CAD
interacts graphically with geometry. The framework used in
implementation will be Qt. The project will be structured as an
extension to BRL-CAD's libdm library.

## Description

### Basic steps

Even though the purpose of this project is to create a new display
manager interface, this cannot be done without being careful about all
the features that a DM should support in order to maintain previous
functionalities. So this is one of the most important things I plan to
have in mind while implementing the new DM (for features to be supported
see "Features"). After this, I can start working effectively and the
next step would be to embed Qt in Tk window (for more information see
Embed Qt in Tk windows).

When all this is done, I can start working on the actual operations that
need to be supported. Finally, last step would be testing.

### Concepts

Implementing a display manager is strongly related to a lot of concepts
that BRL-CAD uses. In order to make a better image about the whole
project I decided to make a short list of concepts that are related to
display manager and to point out in some case some relevant source code.

#### Display Manager

A display manager is a tool that is used for starting a new session of a
graphical server. For BRL-CAD the DM is the primary means with which it
interacts with geometry. DM-s are implemented as a library: libdm.
Display managers can be controlled using dm objects (dm-obj.c)

#### Framebuffer

A framebuffer is a video device that displays from a memory buffer
containing a complete frame of data. Contrary to the previous
solution(vector displays) where only the vertices of the graphics
primitives were stored, in a framebuffer there is at least one bit for
each pixel. In order to emulate the functions of a framebuffer for
compatibility reasons a virtual framebuffer can be created. In BRL-CAD
there is a generic framebuffer library: libfb and also a framebuffer
server: fbserv which actually opens the framebuffer. Also, in order to
control the fb a framebuffer object (fb_obj.c) can be used. Another
useful tool when it comes to framebuffer is fbhelp which displays info
about framebuffer devices available to libfb, gives details about
choices of frame buffers and gives detailed info about any option the
currently device may have.

#### Qt

Qt is a cross-platform application framework used for developing
applications with a graphical user interface using C++. Besides having
one of the best GUI designer tools, another major advantage is C++ that
gives the possibility to work with lots of libraries including STL. I
must say that I do not experienced Qt before, but during the application
process I had looked over some small applications in order to get used
to it.

#### Tcl/Tk

Tk is a library of basic elements for building a graphical user
interface. It is actually an extension for Tcl scripting language having
the following characteristics: platform-independent, customizable,
configurable.

#### Raytracing

Ray tracing is a technique for generating an image by tracing the path
of light through pixels in an image plane and simulating the effects of
its encounters with virtual objects. Raytracing isn’t particularly
related to this entire project, it’s only related to the “embedding a
framebuffer window”. In BRL-CAD raytracing is implemented as rt which
does the actual raytrace. There is also a raytrace library (librt -
library for raytracing a mged database).

## Features

### Actual features

Because the display manager is the primary way with which BRL-CAD
interacts with geometry, a new display manager should provide all of the
basic necessary features. In order to maintain all of the necessary
features, I will make a step by step implementation of struct dm
functions and other mged-dm functions (such that dm_init, fb_open).

### Embed Qt in Tk windows

-   Step 1: Open

In order to maintain functionality the new DM should be embedded in Tk
windows. To do this it is necessary to make all the initializations of
the new display manager that uses Qt but to make it in such a way that
can be integrated in Tk. In order words, a new Tk_window should be
created and also geometry attributes for the window should be specified.
Then, the window must be mapped. Meanwhile, Qt/ogl context must be
created. As the window is created and the DM initialized, it is ready to
be fired up. This should be one of the first steps that must be
implemented.

-   Step 2: Init

The initialization of the DM consists on adding an event handler that
executes when an event occurs and on defining the behaviour of the dm
when a command is executed (a command that involves the dm such as
“set”). The initialization step is done when mged attaches the dm.

-   Step 3: Open framebuffer

In order to have a functional display manager, a framebuffer needs to be
opened in order to be used.

-   Important aspects:
    -   One of the most important things that should be considered while
        doing this is the fact that the DM should be cross-platform. As
        I recently experienced (on my Operating Systems course) this
        could be quite tricky but I will try to consider all things that
        might be problematic from the beginning. This will be solved
        probably using macros for things that need to be different
        accordingly to a specific OS.
    -   Step 2 and 3 are routines specific to MGED’s use of LIBDM.

### Basic operations

#### Drawing

Drawing is one of the most important operations. Without this operation
a new display manager would be useless. When it comes to drawing there
should be done some several steps in order to actually draw. First step
is to initialize the environment for the draw operation (drawBegin),
then do the actual drawing and finally flush the output buffer(drawEnd).

##### Line Drawing

After doing all the above steps, drawing a line shouldn’t be so
difficult. As I saw in the existing code, the line is drawn using each
display manager particular way. So this means that drawing a line needs
to call the Qt appropriate function with the actual values.

##### Text Drawing

Text drawing should be done in the same way Line Drawing is done. As I
researched in Qt a string can be drawn inside a rectangle or from a
point.

#### Keyboard and mouse integration

When it comes to keyboard and mouse, Qt deals with them in a quite
simple way: using events so handling mouse and keyboard in Qt is not a
problem. As I seen in the actual code, mouse is at the moment
generically handled, the implementation being the same for all display
manager (mged/dm-generic.c). If it will be possible I will try to
maintain this genericity, but in the case I cannot find any solution
even after discussing with my mentor that can deal with mouse and Qt in
a generic way, I will write a Qt specific implementation.

As it comes to testing, there should be performed different tasks to see
if the new DM responds correct (for example: responding correctly to
shift grip keys).

#### Embedding a framebuffer window

Embedding a framebuffer window (overlay, interlay, underlay) is strongly
related to raytracing. Actually, in this case there is another BRL-CAD
program that mget lunches (rt) that does the actual raytrace. Also a
framebuffer refresh is necessary to perform this action. Doing this in
Qt should be very similar. When this feature is called, the actual
raytrace must be done and the framebuffer used by Qt has to be
refreshed.

## Testing

In order to make a good project, writing code is just not enough so I
will highly focus on testing. First of all I plan to do a step by step
test, meaning that after every new feature is implemented, I will test
it. After the project is implemented (hopefully with at least 2-3 weeks
before the deadline) I will focus just on testing.

One of the top features of the display manager is to be cross-platform,
so I will test it on multiple platforms. At the moment I have installed
two Linux distribution (32 and 64 bits), and also Windows (7 32-bits and
8 64-bits) so testing can be done on this four platforms. If, after
consulting with my mentor, we decide that there is a particular
distribution on which I should test the DM, there would be absolutely no
problem testing on it.

Testing will consist mostly in creating and loading different models in
the new display manager, but as I said before after every new feature
implemented I will write new tests. I will also make a comparison
between the model loaded in the new display manager and the model loaded
in the other dm’s.

## Documentation and links on algorithms

During my work on this proposal a lot of documentation had to be read.
Even though there are not any particular algorithms, I will describe how
I approached this project and give some useful links to documentation.

First of all, I started by reading the manpages and the documentation
from brlcad.org which helped me make a better idea on how things work.
After reading about display manager, framebuffers I started working on a
patch in which I created a debug dm. The most difficult thing I had to
overcome during this step was to navigate between sources, but in the
end I succeeded to understand how a DM works for BRL-CAD.

The most useful tool that I used in order to find relevant code was
ack-grep which really made things easier. It was the first time I used
it but, I am strongly recommending it. If you know what you search then
ack-grep is the answer to find all keypoints where you need to look. On
the other hand, there was the community which responded to all of my
questions I’ve put on IRC.

Links:

<http://brlcad.org/w/images/c/cf/Introduction_to_MGED.pdf> - very
usefull in order to get an idea about mged

<http://en.wikipedia.org/wiki/Framebuffer>

<http://ecomputernotes.com/computer-graphics/basic-of-computer-graphics/what-is-frame-buffer>

<https://en.wikipedia.org/wiki/Ray_tracing_%28graphics%29>

## Deliverables

The project can be divided in at least 5 parts, so all of this can be
considered a specific measurable goal (one for every feature
implemented). In order to reflect the progress I will make frequently
commits so that every change can be tracked.

I will primarily work on linux and at the end of each phase I will test
the code also on Windows and make the necessary changes.

Finally, I will focus just on testing so that there would be a
functional display manager at the end.

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
    will start working effectively and writing code.

<!-- -->

-   Week 2-3 (24 June - 8 July): During this time I plan that Qt will be
    embedded in Tk. This time includes at least one day for testing.

<!-- -->

-   Week 4 (8 July - 15 July): This week is reserved on implementing the
    drawing line functionality. At the end of this period, the drawing
    line functionality should be implemented and tested.

<!-- -->

-   Week 5 (15 July - 22 July): This week is reserved on implementing
    the drawing text functionality.

<!-- -->

-   Week 6 (22 July - 29 July): Preparing mid-term evaluation and after
    finishing it probably about 2 days of vacation.

<!-- -->

-   Week 7 - 9 (29 July - 19 August): Implementing the keyboard and
    mouse integration between Qt and Tk.

<!-- -->

-   Week 10 - 12 (5 August - 9 September): Embedding a framebuffer
    window.

<!-- -->

-   Week 13 - 14 (9 September - 27 September): Final testing and
    submitting the final application.

At the end of each time slice the particular functionality should be
implemented and tested.

# Time availability

I can say without any doubt that I can fulfil the minimum required time
of 40 hours / week. As I understood after talking with the community
this is quite a complex project so if it will be necessary I could work
more. This project is really interesting to me so I will invest as much
time as it needs in order to finalize it.

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
(except I had a small idea from the name CAD), after looking on the Idea
page, I found a project that was suited for me and which contained one
of my favorite interests: computer graphics.

Finally, after reading the description page I knew I had found the
perfect way to spend my summer.

# Why me?

First of all, I am really enthusiastic to work to an open source
project. Until now, I have worked on small projects so I am really eager
to start working on a large project. Also, I think that this is a great
opportunity to learn new things that will help me in my future career,
so this makes me even more enthusiastic about the project.

Least but not last, I must say that I consider that I have all the
necessary skills in order to complete this project. I do not back away
from difficult tasks and I am fully committed to finishing the project.
I also plan to be an active developer in BRL-CAD after GSoC is over.

Finally, I want to thank you for taking time to read my proposal. I hope
we will collaborate during this summer but also after GSoC.

Also, I want to mention that this is my preferred project (New
Cross-Platform 3D Display Manager)

Simion Vlad Bogolin