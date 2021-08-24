## SoC

### Further OpenGL Geometry Editor GUI development

#### Log

##### 2009-06-10

-   Set up g3d's cmake to pull in Qt4
-   Began work on experimental Qt Ogre widget

##### 2009-06-11

-   Cleanup

##### 2009-06-17

-   Moved RBGui/OIS initialization into OgreGLWidget, where it will
    remain until they can be completely purged.
-   Repaired numerous bugs in said initialization introduced by the
    unusual initialization times/procedures of the OgreGLWidget.
-   Found
    [evidence](http://sourceforge.net/tracker/index.php?func=detail&aid=2583123&group_id=2997&atid=302997)
    that a SVN version of Ogre will be necessary for the desired
    wrapping until their next release is made.

Currently very close to having old g3d running within a logical Qt
Application and an actual Qt window.

##### 2009-06-18

-   Configured a secondary FreeBSD machine for development
-   Improved ability of CMake package-finding scripts to locate libbu
    and libged when pkg-config is unavailable or providing inaccurate or
    insufficient information

##### 2009-06-20

-   [Fixed](https://sourceforge.net/tracker/?func=detail&aid=2809665&group_id=2997&atid=302997)
    Ogre bug leading to X error on shutdown
-   Began process of purging RBGui, as its Ogre backend appears to be
    incompatible with the version of Ogre required for embedding in Qt
-   Began multipart checkin of Ogre SVN, patched for clean shutdown when
    embedded in Qt
-   Successfully tested complete Qt Ogre widget startup/shutdown

##### 2009-06-21

-   Finished the (surprisingly painful) multipart checkin of Ogre SVN.

##### 2009-06-23

-   Moved Ogre code from a QGLWidget-derived class to a
    QGraphicsScene-derived class to allow integration of Qt widgets
-   Added experimental resize handling
-   Attempted to test Qt widget integration, only to find Ogre's
    rendering call preventing Qt widgets from being visible. Posted [a
    request for
    help](http://www.ogre3d.org/forums/viewtopic.php?f=2&t=50841) on the
    Ogre forums.
-   Researched OpenGL state-saving as a possible solution to the Ogre/Qt
    conflict.

##### 2009-06-24

-   Further research into Ogre/Qt conflict:
    -   Looked into what appears to be [the standard
        way](http://www.ogre3d.org/forums/viewtopic.php?p=296902) to do
        raw OpenGL calls in an Ogre context. Not resorting to this yet
        because it would require interacting with Qt on a significantly
        lower level than that enabled by the current GraphicsScene
        approach.
    -   Obtained [an OpenGL call
        tracer](http://www.opengl.org/sdk/tools/BuGLe/) for possible use
        working out how Qt manages to reset things after a frame.

##### 2009-06-25

-   Dug around in the Qt code looking for reset hints. Nothing found
    that does the job yet.

##### 2009-06-28

-   Further Qt digging; identified a possible approach based on
    modifying Qt (undesirable), and the potential for an Ogre-centric
    solution, if certain functionality provided by the Qt-centric
    solution can be replaced.

##### 2009-06-29/30

-   Final research and experimentation in the hopes of replicating Qt's
    reset mechanisms. Found something very promising with QPainter::load
    and QPainter::save, but unless I am misusing them they proved
    insufficient to prevent Ogre from hiding Qt. No other content of
    QGraphics(Scene\|View)::render seems to be able to do the trick,
    unfortunately. Barring unexpected discoveries, further attempts will
    focus on pure Qt-in-Ogre. (Addendum: Qt modifications will also be
    tested.)

##### 2009-07-05

-   Attempted to resolve Ogre/Qt conflict by duplicating initialization
    code in (QGraphicsView\|QGraphicsScene)::render in a variety of ways
    after the call to drawBackground. No visible effect.

##### 2009-07-06

-   Experimented with various permutations of rendering Ogre via a
    QGLWidget, QGraphicsScene, and QGraphicsView to no avail.

##### 2009-07-08

-   Isolated Ogre/Qt experiments from g3d and added them to the build
    system as a separate target entitled "ogretest" (can be build with
    "make ogretest").

##### 2009-07-09

-   Identified and removed an accidental call to Ogre code that
    performed a buffer swap in ogretest. Unfortunately, its removal
    appears to have had no effect upon the Ogre/Qt conflict.
-   Found and successfully tested QCoreApplication::processEvents, which
    appears Qt to function with an external mainloop, significantly
    simplifying the matter of putting Qt under Ogre's control.
-   Made a first attempt at the as-yet-untested QtRenderListener, which
    is intended to allow Qt to do everything it needs to, including
    rendering its widgets to the shared OpenGL context, without being
    interfered with by Ogre. It tries to achieve this by explicitly
    stepping Qt after the completion of an Ogre render queue, and within
    a prepared OpenGL state.
-   Began reworking ogretest.cxx to allow the QtRenderListener to be
    tested, by moving significant portions of OgreScene into the main
    function.

##### 2009-07-10

-   Completed and began debugging test code for operating Qt on Ogre's
    terms. Widgets are not yet rendered correctly, but there is some
    evidence that adjustments to this approach, perhaps in the details
    of resetting OpenGL state in QtRenderListener::renderQueueEnded,
    still have potential. Initial attempts resulted in a black window
    with the dark grey of the configured Ogre background color present
    in a rectangle in the lower left corner. Disabling Ogre buffer swap
    (as Qt almost certainly performs its own bufferswap when stepped,
    although I'm not at all certain swapping buffers at the point at
    which Qt is stepped (which is much earlier than when Ogre normally
    swaps buffers, although it ostensibly occurs at the end of the
    render queue, of whose significance I am uncertain) is safe in Ogre,
    particularly considering that OpenGL state is
    saved/restored/otherwise twiddled across the swap) replaced this
    rectangle with one of white, the color which Qt draws as a
    background to its widgets by default. If this is in fact the source
    of the white, then it may be that getting that rectangle realigned
    with (i.e. filling) the context will result in visible
    widgets—although then the opaque white background will need to be
    removed.

##### 2009-07-11

-   Experimented with disabling portions of the OpenGL state reset in
    QtRenderListener to solve presumed alignment issues, identifying
    interesting effects observed yesterday as unrelated to Qt.
-   Observed the alignment issue dissapear and reappear across multiple
    runs of an unmodified test binary. Perhaps this is some side effect
    of an absence of special handling for the resizes enforced by my
    (tiling) window manager?
-   Attempted to contact the author of the Ogre native render system
    code on which the current effort is founded for advice and further
    information.

##### 2008-07-12

-   Original native render system author had nothing to offer. Started
    [a new
    thread](http://www.ogre3d.org/forums/viewtopic.php?f=2&t=51199) on
    the Ogre forums with more detailed information in the hopes of
    hooking in someone more knowledgable.

##### 2008-07-14

-   In light of the incredible resistance of the Ogre/Qt conflict to
    solution, I discussed alternatives with mentors and decided to
    attempt rendering Qt atop, rather than into, Ogre's heavily defended
    context.
    -   First attempt used a QDialog for testing. No luck until a call
        to QDialog::show() is applied to the QDialog, which leads to
        apparent initial success tempered by the realization that the
        QDialog is being rendered as, surprisingly, a popup dialog—that
        is, a separate top-level window. It turns out this is documented
        behavior; I must assume that its use in the model renderer
        example from the Qt blog using the GraphicsView system is an
        exception to this rule. Thus, previous experiments' use of it
        was likely not invalid.
    -   Second attempt used a simpler widget, the QPushButton. Again no
        initial results, but the removal of code giving the OgreGLWidget
        an initial size of 1024x768 on a hunch that it was leading to
        some form of subtle conflict with my window manager lead to the
        widget becoming visible within the OgreGLContext as desired.
        Thus, this attempt was a success.
        -   Further experimentation showed that a call to
            QPushButton::show(), in this case left over from the
            symbol's original role as a QDialog, was necessary for it to
            appear, although I don't recall seeing such calls in the
            original model renderer (quite possibly they were hidden
            elsewhere; it had quite a bit of widget initialization
            code). Earlier failed attempts to get Ogre and Qt to
            cooperate will bear repetition with this call added, as
            ideal results may still be attainable through its use.

##### 2008-07-17

-   Verified support for more advanced Qt functionality within
    OgreGLWidget
-   Successfully integrated support for Qt Designer's output files into
    the build system
-   Using Qt Designer, assembled a simple GUI based on the original G3D
    GUI as designed by mafm
-   Wrapped Qt Designer output to allow functionality to be attached to
    GUI signals
-   Created a new "Console" widget that includes an auto-hiding output
    window, and successfully used Qt Designer to place it in the GUI
-   Added timer code to ensure that the OgreGLWidget is redrawn
    frequently
-   Encountered a heisenbug in which garbage is scribbled all over areas
    of the GUI intended to be transparent; I conjecture that this
    relates to the drawing of Qt widgets on top of, rather than into,
    the OpenGL context, and that drawing Qt directly into the
    OgreGLWidget would resolve the issue.
-   Tweaked the GUI layout to make aforementioned bug unobtrusive when
    it manifests to allow an attractive and usable GUI to be implemented
    without relying upon a fix for the bug manifesting in short order.

##### 2009-08-03

Much has happened since last log. In summary, OpenGL embedding is now
functional, and after some work the GUI has been restored to original
G3D functionality and can be seen following.
![](img/G3d-2009-08-03.png)

#### Abstract

I propose to continue the development of the OpenGL Geometry Editor GUI
effort began during Summer of Code 2008 through modifying the existing
application to take advantage of the Qt application and UI framework and
then taking advantage of the wide array of development tools, widgets,
and libraries offered by the framework to rapidly flesh out the front
end, with the ultimate goal of preparing a powerful and intuitive CSG
modeling GUI ready for connection to the geometry service.

#### Content

BRL-CAD is unparalleled in power and maturity in the small world of
open-source CAD, and has a feature-set capable of competing successfully
with commercial CAD products. However, the suite has until recently, as
an in-house tool, been targeted almost exclusively at small population
of trained experts. As such, the current standard modeler, mged, is
highly unintuitive, requiring extensive perusal of documentation before
even relatively straightforward modeling tasks can be completed
reliably. To make BRL-CAD a useful and attractive toolset for a wider
audience, it is therefore critical to implement a more intuitive GUI
without sacrificing the power offered by mged.

As a well-recognized need, this project was first addressed in a [2008
Summer of Code
project](OpenGL_GUI_Framework#Initial_Project_from_GSoC_2008.md)
which produced the beginnings of a working prototype based upon
[Ogre](http://www.ogre3d.org/) and
[RBGui](http://www.rightbraingames.com/tech/). While it provides an
attractive beginning, it lacks any actual editing interface, and suffers
from limited potential for direct growth as a result of the selection of
RBGui, which is unmaintained (to the extent that I found it unbuildable
on Linux without numerous modifications), has a limited selection of
widgets, has no design tools or other development aids, and lacks much
of the higher-level functionality that can be found elsewhere. To remedy
this, I propose to within the existing codebase swap out RBGui with
[Qt](http://www.qtsoftware.com/), an extremely
[powerful](http://doc.trolltech.com/4.5/examples.html),
[well-documented](http://doc.trolltech.com/4.5/index.html), and
[widely-used](http://www.qtsoftware.com/qt-in-use) application and UI
framework, and is well supported on [all remotely popular
platforms](http://doc.trolltech.com/4.5/supported-platforms.html), and
popular itself to the extent that up to date binaries for it exist in
most package management systems, offsetting the admitted problem
presented by the notoriously slow build process of the framework.
Additionally, a wide variety of [development
tools](http://www.qtsoftware.com/products/developer-tools) exist, which
have the potential to accelerate prototyping immensely compared to the
hand-coded measures necessary in the current implementation. Although Qt
is traditionally rendered in software, making it seem an odd choice for
use within an OpenGL context as RBGui is currently used, Qt recently
gained [support](http://doc.trolltech.com/4.5/demos-boxes.html) for this
type of use.

Once I have successfully integrated Qt with Ogre and substituted it for
all uses of RBGui, I will work to continue the efforts made last year to
develop it into a complete geometry editor frontend based upon the
[Ideal Operating Environment](http://brlcad.org/design/gui/) concept
around which the work up to this point has been based. In particular, I
will work to construct a framework for the rapid prototyping of a highly
usable GUI composed of actions accessible through multiple routes,
including the command line and multiple GUI methods, and leveraging it
to form an interface with functions to perform and display a variety of
common basic editing operations. Support for actually performing these
operations will be implemented through stubs wrapping libged
functionality, to be replaced with use of the geometry service as soon
as it is practical. This will allow a degree of actual functionality
sufficient to test the GUI design in practice, allowing for meaningful
early analysis of the effectiveness of design decisions, which will
support the direct evolution of the interface towards the greatest
possible usability. Although the scope of functionality to be
implemented will be inevitably limited by the time allowed for the
Summer of Code, I hope to continue on with this project after the
Summer's completion, as I believe strongly in the importance of such an
interface to BRL-CAD's success, and the benefits such success has to
offer to a diverse audience; as the sole example of high-quality open
CAD software, bringing an accessible BRL-CAD into reality would not only
benefit current users of such technology, but help make CAD accessible
to those unable to afford the expensive licenses typically required for
commercial options, potentially opening up a whole new world of open
community-oriented design projects, paralleling with real-world products
the massive success of open software.

To achieve these goals I will take advantage of my existing familiarity
with both the BRL-CAD internals and the modeling interface (and power
thereof) offered by mged, as well as experience with the popular
[Blender](http://www.blender.org/) modeling and 3D graphics toolkit, the
familiarity with C, C++, and many similar languages I've developed
through years of self-motivated programming, and the familiarity with
build systems, command line interaction paradigms, and diverse user
interface designs conferred by regular use of Unix-based systems for
both software development and everday tasks. Additionally, I will take
advantage of my familiarity with the community, a result of my presence
on IRC for most of the past year under the nick "Ralith," to engage with
the current primary users of BRL-CAD for immediate feedback on my
prototypes, in the interest of creating a tool that is not only
attractive to new users, but powerful and intuitive to long-time users
of the system as well.

#### Milestones

1.  Integrate existing work with a Qt OpenGL context
2.  Replace all use of RBGUI with Qt. RBGUI and Mocha removed as
    dependencies.
3.  Present a clean, consistent, and appealing look in all GUI states
4.  Design and implement system for handling popup command line
    instructions
5.  Parallel all relevant current GUI features in the popup command line
6.  Implement mged-style wireframe rendering of a limited subset of
    primitives

#### Timeline

April 20 through May 22:
Determine best approach for Qt/Ogre integration

Become familiar with Qt development tools and techniques

Become familiar with the relevant libged/geometry service API

Discuss design issues with mentor

<!-- -->

May 23 through May 30
Modify g3d to render to a Qt OpenGL context

Render Qt widgets into the context

<!-- -->

May 31 through June 20
Replace existing GUI elements with Qt widgets

Adapt Qt widget appearance/functionality to g3d's needs

<!-- -->

June 21 through July 11
Generalize actions such that both the command line and multiple GUI
widgets can trigger a single implementation

Implement easily extensible noun/verb based popup command line system

Implement command line control over existing functionality

<!-- -->

July 11 through July 25
Implement editing framework (loading of geometry, 3D cursor, connection
to libged or geometry service

<!-- -->

July 26 through August 2
Implement mged-style rendering of a limited subset of primitives

<!-- -->

August 2 through August 10
Review usability and intuitiveness of interface, taking comments from
community and making optimizations

<!-- -->

August 11 through August 17
Clean up/document existing code and fix bugs. Implement no new
functionality.
