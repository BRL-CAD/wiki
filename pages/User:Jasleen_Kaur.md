Name: Jasleen Kaur

Email Address: jasleen.7956@gmail.com

IRC Username: jasleen

Brief Background Information:

An open source programmer with background of C/C++ .

1\) I am familiar with Qt and I am working for the LibreCAD
organisation, which uses Qt framework.

2\) My Interest is in Computer Graphics, Data Structures.

3\) I recently added 6 new features in LibreCAD

`  `[`http://forum.librecad.org/New-Features-for-LC-2-1-td5707958.html#a5707970`](http://forum.librecad.org/New-Features-for-LC-2-1-td5707958.html#a5707970)

4\) Final year B.Tech student of Information and Technology at Guru
Nanak Dev Engineering College, Ludhiana, India.

Phone number: +91 887 240 9561

Project Information:

Project Title: Cross-Platform 3D Display Manager.

Brief summary:

This project's main goal is to make a Cross Platform Display Manager.
Currently, their are canvas specific Display Managers (wgl, ogl, ps,
plot, tk, rtgl, X). To make a cross platform Display Manager, I am using
Qt framework. Qt is used to make a cross platform applications. Based on
Qt's QCanvas, a cross platform Display Manager will be made. This
Display manager will work on any window system. dm-qt.c will be my new
cross platform Display Manager's C file, which will based Qt's canvas,
which is a cross platform canvas. Its header will be
/src/include/dm-qt.c . I will hook this cross platform Display manager
in Cmake file (/src/libdm/CMakeLists.txt).

Detailed description:

1\) In a cross platform display manager, I will use Qt classes. Qt's
QCanvas, Qt OpenGL, QPixmap, QObject, QPalette, QPainter, QFrame,
QTransform, QMouseEvent,QKeyEvent etc will be used. QPainter class has
functions like drawPoint(), drawLine(), drawPixmap().

2\) I will hook this cross platform Display manager in Cmake file
(/src/libdm/CMakeLists.txt). Cmake utility generates a makefile which
will compile this C code.

3\) For Keyboard and mouse Integration,the QWidget::setEnable() function
can be used to enable or disable mouse and keyboard events for a widget.
The event handlers Widget::keyPressEvent(), Widget::keyReleaseEvent(),
QGraphicsItem::keyPressEvent() and QGraphicsItem::keyReleaseEvent()
receive key events.

4\) To get Qt running with Tk window (MGED/Archer), I will use a
binding(suggested by developers) to integrate Qt with Tk/Tcl (if
necessary). Otherwise, I will create an integration between them in my
code myself.

5\) Testing: I will create a new database file (.g), where I will
examine the working of operations by performing these operations on Qt's
canvas which will work on any platform.

6\) Documentation: It will obvious the part of my project. I will
deliver this project with a complete Developer's Documentation. So that
if anyone wants to involve in it, can easily get involved. This
documentation will contain all its workflow. For documentation I will
use Doxygen or latex or any software suggested by developers.

7\) Maintenance: I will be active on IRC, mailing list and will continue
my contribution. I will contribute even after GSoC overs. I will take
care of all bugs/issues related to my project and also contribute my
time to solve others bugs/issues too.

Framework I intend to use: Qt is a cross-platform application framework
that is widely used for developing application software with a graphical
user interface (GUI) (in which cases Qt is classified as a widget
toolkit), and also used for developing non-GUI programs such as
command-line tools and consoles for servers.http://qt-project.org/

Deliverables: Fully functional, thoroughly tested, cross platform
Display manager.

Milestones:

1\) Revision of Existing code. an routines of libdm. Exploring
<http://diyhpl.us/~bryan/papers2/cad/brlcad/doc/html/manuals/libdm/index.html>
2) Making a patch to show my ability of programming. 3) Create dm-qt.c
(src/libdm/) and its header dm-qt.h in (src/include/). First by copying
the exiting code ok dm-tk.c to dm-qt.c files. 4) Code using Qt classes
in dm-qt.c 5) Run Qt with Tk windows (both MGED and Archer). Here the
GUI will remain as it is, but all the routines will be set using in Qt
classes. 6) Performing basic operations: drawing line,text, point, Input
from keyboard, mouse to test its functionality. 7) Remove redundancy of
code( if exist). 8) Testing by uploading same .g file on my display
manager by working on different OS. 9) Making a patch of my work. 10)
Submitting it to Google. 11) Maintenance (future work).

Schedule:

May 1 - May 26: (Getting familiar and making patch ) I am making patches
to show them my ability to code. Interacting with developers on IRC,
Mailing List. Discussions with developers to innovate this idea with
more useful features. Link to Patches: \[1\]
<https://sourceforge.net/p/brlcad/patches/181/>

May 27 - June 2: (Explore existing code) Till now I explored exiting
code with the help of this link
<http://diyhpl.us/~bryan/papers2/cad/brlcad/doc/html/manuals/libdm/index.html>
Now I know what routines are working for Display Manger and its
dependencies. My cross platform Display Manager will use many of these
dependencies like options.c, query.c, rect.c, scale.c, axes.c, etc and
will add more according to new features to be implemented. If I get
selected( by God's will). I will dig more deeply into code and start
working for it. And If In case I am not selected, I will continue my
contribution to BrlCad.

June 3 - June 9: ( Use Qt classes) Create a new file dm-qt.c and run
exiting code to that file. Modify that code to Qt to test its Qt's
working. I will start implementing desired code using Qt classes. Will
use existing features to implement in Qt and add more features there.

June 10 - June 22: ( Qt running with Tk window- MGED) I will create an
option in Mged window, like Modes &gt; Display Manager &gt; (Qt Display
manger) Code of Mged is in src/mged/. Here its GUI will remain as it is
( in Tk ), but Tk will use this cross platform Display manager( made
using Qt framework)

June 22 - July 10: (Input from mouse/keyboard - MGED) I will use Qt
classes QMouseEvent and QKeyEvent to take input from MGED. Integrate Qt
and Tk to take input from Tk window(Mged)

July 11 - July 15: ( Qt running with Tk window- Archer) Similarly I will
add option to Archer (code in src/archer/).

July 15 - August 2: (Input from mouse/keyboard - Archer) I will use Qt
classes QMouseEvent and QKeyEvent to take input from Archer. And mid
term evaluation of my work.

August 2 - August 12: ( Examine the code by performing Different
Operations ) I will perform different operation to check its working.
Operation like drawing point, text, line or mouse/ keyboard input,
drag-drop functionality etc, will be tested. I am using Linux (Ubuntu),
so I will first test all operations on Ubuntu. I will keep log of every
thing with me to include its information in documentation.

August 12 - September 1: (Testing and improvement) By loading any
database (.g) file into new display manager. Testing will done on
different platforms.

September 1 - September 22: (Documentation) I will start writing
developers documentation. I will deliver my project with a good
developers documentation so that if some wants to involve in it, then
he/she can easily get involved.

Sept. 23 - Sept. 27: ( Final evaluation and Submit code to Google) Final
review of code. After solving issues or bugs, I will finally upload my
project to Google-melange's site.

Future work: Maintainability of its code.

Future scope: Cross platform display manager with more features and good
functionality. This Display manager will work with both Tk Windows
(MGED/Archer)

Time Availability: I will be available 40 hours / week. If needed, can
spend more. No restriction of time.

Why BRL-CAD?

Working with 3D-CAD would really provide a good experience. This will
helpful in understanding Computer Graphics more practically. BRL-CAD is
an old CAD sotware. Therefore, it is developing from many years by great
develops. It follows computational graphics well. I am an Active
contributor in LibreCAD, but unfortunately LibreCAD is not in GSoC this
year. Finding this organisation on the organisation list, inspires me to
start contribution to this organisation too.

Why me?

Programming is my passion. It would be great, if I could get such
responsible work. This work is of my interest. I know all its workflow.
It would undoubtedly improve my programming skills. I will take it as my
responsibility to finish this project on a positive node. I am very
excited to take this project. I have already been working with CAD
programs, I have also improved LibreCAD code. I know how the display
manager works and I feel I am the right candidate for this project.
Founding my interest in this project, rather than waiting for this event
to start, I already started working on it.

\[Blog\] <http://jasleen7956.wordpress.com/>

\[Github\] <https://github.com/jasleenkaur>