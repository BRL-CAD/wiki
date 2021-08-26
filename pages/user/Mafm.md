# Personal Information

-   Name: **Manuel A. Fernandez Montecelo**
-   E-mail/GoogleTalk: **manuel.montezelo**
-   IRC nickname (freenode network): **mafm**
-   SourceForge username:
    **[mafm](https://sourceforge.net/users/mafm/)**

# GSoC (Google Summer of Code) 2008

-   Project: [OpenGL GUI Framework](/wiki/OpenGL_GUI_Framework.md)
-   Example for interaction:
    <http://brlcad.org/design/gui/ioe_proto_final.mov> , recommended by
    [Sean](/wiki/user/Sean.md)
-   Another example in the form of a real program: wmii (Plan9 window
    manager) ( <http://www.suckless.org/wiki/wmii> ), recommended by
    [Sean](/wiki/user/Sean.md)

# Milestones

Milestones include (maybe some of them to be added or removed, to be
discussed with the mentors and the community in general):

-   Get logging working
-   Get console working
-   Being able to communicate with the back-end
-   Displaying geometries
-   Displaying various representations (wireframe, polygonal, etc)
-   Rotating and positioning
-   Input support (trackball, shift-grips)
-   Clean cross-platform build system integration

# ToDo

## To finish GSoC

    [2008-07-25 17:01:58]
    <brlcad> okay, so requirements
    <brlcad> hooking in to the back-end in *some* fashion is definitely one to do so
    you can display real stuff
    <brlcad> libged has enough for that to be doable now, but your app isn't
    supposed to talk to libged directly, it's a bad coupling
    <mafm> so I could introduce a class simulating network layer?
    <brlcad> *delete* *delete* *delete*  .. heh, yes
    <brlcad> doesn't even have to simulate it, on the app side it could be a network
    layer using libpkg, but then you'll need to stuf in a server layer that
    minimally hooks into libged too
    <brlcad> you could do it without the network communication, but the danger there
    will be that it really needs to avoid polluting any data types across into the
    front end
    <mafm> yes, I mean that the app could call this layer, and this layer bind
    directly to libged
    <mafm> and when the network libs are complete, to use them instead
    <mafm> but the rest of the front-end wouldn't be affected
    <brlcad> okay, so that sounds like the start of a plan


    <brlcad> the other bit I'd like to get a better feel for before gsoc ends is
    rbgui customization
    <brlcad> i.e. how easy it is to 1) customize the appearance (theme it or
    otherwise change how it looks) and 2) add a new control widget (e.g. say you
    want a rotating progress indicator)
    <brlcad> if that's a huge deal, then rbgui probably isn't a good framework to go
    with since the design requirements require a lot of custom interactions and
    appearance
    <brlcad> somewhere in there is how layout can be controlled too
    <mafm> rotating progress indicator?
    <mafm> the camera coordinates at the moment?
    <brlcad> finally, the last item making sure input controls are "done" .. not
    just 90% -- I can redo the entire build system really easily if needed, I can
    redo the libged binding easily, can work on logging/console, etc .. but there's
    a higher 'expense' to follow how input control works so that part should be near
    "done" for the two styles
    <mafm> I have been working in something like that (as a window with components,
    not a new widget), but I scraped it because in IOE it doesn't seem to be place
    for smallish, floating windows
    <brlcad> that's because it shouldn't be a smallish floating "window" .. it
    should be a control that can go onto a given context
    <brlcad> just as an example, say you wanted to draw a simple spinner progress
    indicator, like http://www.tmssoftware.com/Images/acp.png down on one of the
    buttons or on the top status bar or elsewhere
    <brlcad> i'm not saying do that particular control, but need to be able to
    evaluate how hard it is to write new controls (so maybe try that one)
    <mafm> contexts are minimum half of the window size?
    <brlcad> i have a fairly straight-forward sense for how hard that is roughly
    with cegui, for example
    <brlcad> little to no idea how hard that will be for rbgui
    <brlcad> hm? minimum half? (no)
    <mafm> in example in IOE, when dragging parts of the greeting card
    <mafm> one context was the sheet for the card, another half was the things to
    put in there (would be like primitives in our case)
    <mafm> IIRC :D
    <brlcad> yeah, that was a separate (temporary) context/panel
    <brlcad> how much space those take up is content-specific and
    application-specific
    <brlcad> but yeah, could hold primitives in our case


    <brlcad> the last bit I'd add would be to actually do a binary release
    <brlcad> for at least one platform
    <brlcad> for developers
    <brlcad> (to check it out)
    [2008-07-25 17:44:33]

## About building system

    [2008-07-01 20:30:08]
    <brlcad> should work on improving/finishing that build system integration some more too ;)
    [2008-07-01 20:31:28]
    <brlcad> saving users the need to hunt/download is only a small piece of the reason for including the deps, it should build them if it doesn't find a suitable system version
    [2008-07-01 20:32:04]
    <brlcad> also, your cmake files presently assume pkg-config, that shouldn't be assumed
    [2008-07-01 20:32:13]
    <brlcad> (nor required)

    [2008-07-01 20:34:38]
    <mafm> I'm no expert in building systems, but that could take weeks :S
    [2008-07-01 20:35:39]
    <mafm> "but" is alias to "but I think" and "because of that" at the same time :)

    [2008-07-01 20:35:45]
    <brlcad> I don't think anyone here would call themselves a cmake expert :)
    [2008-07-01 20:37:03]
    <brlcad> it is something that needs to happen earlier rather than later given this tool is intended to become pretty fundamental eventually
    [2008-07-01 20:37:37]
    <brlcad> minimally document the need somewhere (TODO), but poke on it when you can

    [2008-07-01 20:37:56]
    <mafm> but I could spend much time with it and miss the milestones with gsoc

    [2008-07-01 20:39:14]
    <brlcad> i understand, that doesn't change the pressing need for it ..
    [2008-07-01 20:39:23]
    <brlcad> the longer it's ignored, the harder it will be for whomever does try it
    [2008-07-01 20:39:57]
    <brlcad> it's part of coding complete
    [2008-07-01 20:40:22]
    <brlcad> if the build doesn't work cleanly, it's not really usable yet to most of our devs

    [2008-07-01 20:40:45]
    <mafm> I see

    [2008-07-01 20:41:47]
    <brlcad> e.g. I can't imagine bob readily being willing to futz with three different build systems plus pkg-config, cmake, and scons
    [2008-07-01 20:42:29]
    <brlcad> we're used to *zero* effort unless you want to change away from defaults
    [2008-07-01 20:43:49]
    <brlcad> it's not top-priority in front of the milestone tasks, but it's probably #2 or #3 to have a default-functioning build system regardless of system deps

    [2008-07-01 20:44:22]
    <mafm> that's fine, but I don't think that it's in the scope of the project to rework whatever building system the dependencies decide to use

    [2008-07-01 20:44:38]
    <brlcad> so at least document it is what I'm saying, maybe work on it if you take a break from coding

    [2008-07-01 20:44:41]
    <mafm> especially being an experimental project

    [2008-07-01 20:45:38]
    <brlcad> fyi, I don't see this as an experiement -- a prototype, sure .. but one with an exceptionally high probability of becoming the foundation for a new GUI
    [2008-07-01 20:46:26]
    <brlcad> you'd have to mess up in several big ways for it to be wasted effort :)

    [2008-07-01 20:47:36]
    <mafm> it seems to me that you're relaying on somebody with a weak knowledge of building for such a foundation :P

    [2008-07-01 20:48:15]
    <brlcad> not relying, just don't want you to blow it off entirely as not your problem
    [2008-07-01 20:50:02]
    <brlcad> wasn't saying drop what you're doing to work on it, just keep it in mind and poke on it when you can .. and document where things are at

# Log

## August

August 24:

-   Submitting final evaluation survey, and sending e-mail to the
    developer mailing list with the summary about the work done and
    future.
-   Screenshot:
    <http://brlcad.org/~mafm/g3d-screenshots/brlcad_rbgui_20080824-1.png>

August 20:

-   (In trunk) Bug fixing: not using argv\[0\] when argc&lt;1, it tends
    to be crashy ;) (it happened to me when trying to use the library).
    I did some minor normalization in other commands, initializing the
    result and so on, hopefully I didn't introduce new bugs due to poor
    understanding of the way it works.
-   (In trunk) Remove '\#if GED_USE_RUN_RT', Sean did the same
    yesterday in libged but not here, so now it won't compile.
-   Fixing the commands in g3d using libged -- finally they are using
    the library correctly and libged is not crashing improperly.

August 19:

-   Fixing libged commands, now they at least give some result and
    mostly work.
-   Using program-wide data structures for libged, instead of on-demand
    ones for testing until now.

August 18:

-   Official "Pencils down" date.
-   I was trying to get my commands using libged working, but no luck so
    far and no tangible code worth to commit.

August 17:

-   Adding a couple of new commands using libged, but still not properly
    working (I don't know if it's my fault or libged's)

August 15:

-   Moving Command base class to a separate file
-   Preparing CMake files for using BRL-CAD library
-   Adding a new command to start to use libged (more to come, but I'm
    having some issues)

August 11/12:

-   Preparing binary package so more people can test it. Unfortunately
    they're only for GNU/Linux amd64, since my personal laptop got
    screwed and I cannot install new systems in the computer at work.
    The packages are in: <http://brlcad.org/~mafm/g3d-packages/> , some
    other libs are necessary in order to get it running: libfreeimage,
    libCg etc; easily available from your favourite distro or the
    Intertubes.

August 8:

-   Working in the camera control window, fixing some of the remaining
    problems
-   Revisiting part of the code, removing some comments not applicable
    anymore and doing a bit of cleanup.
-   Starting to prepare a binary package.

August 7:

-   Perfecting the taskbar, now it works much more closely to the Ideal
    Operation Environment (IOE, see my wiki page for the video) that we
    take as ideal interaction model
-   Enhancing custom widget with a label and the numerical progress
    (useful at least when testing)
-   Several other minor changes related with this.

August 6:

-   After a few days of weekend and relax visiting friends and family,
    came back to work.
-   Adding methods to CameraMode to retrieve the relative rotations, so
    (in example) they can be shown in windows
-   Continued working with the custom widget. It's not easy since it
    seems that some of the brush methods don't work (in example to draw
    lines), so I changed the strategy to use a kind of slider instead of
    a "pie" to represent the rotation.

August 1:

-   Creating icons for camera control buttons
-   Enhancing camera modes by adding bindings for actions in the camera
    control window, and binding actions in camera control window with
    camera modes -- some previous code needed some modifications to get
    this working fine.

## July

July 31:

-   Working in the custom window and camera control, commiting code even
    if it doesn't work very well.

July 30:

-   Saving the state of camera rotations before dragging, so they
    continue to rotate from the current position instead of starting
    from scratch (for both Blender and MGED modes).
-   Working in creating a new window to control the camera, including
    the creation of a custom Widget (as requested by Sean, to test how
    easy it is to achieve that with RBGui), but results not ready to
    commit yet because there are lots of glitches (images not showing in
    buttons when they should, etc).

July 29:

-   Fixing day :)
    -   Fixing the problems with zooming in orthographic mode with
        minimum hassle, using some of the capabilities of OGRE (instead
        of previous trials modifying view matrices and so on). It works
        as expected with all current camera/input modes.
    -   Fixing the problems with panning when controlled by keyboard
        (currently for Blender Camera mode only).
    -   Fixing the problems with panning when controlled by mouse
        (currently for MGED/Shift-grips Camera mode only). In the end it
        was very simple, but only once we got the relative dimensions of
        the camera and we're working in orthogonal projection mode.

July 28:

-   Adding support for different projections:
    orthogonal(orthographic)/perspective. Putting the control of
    Perspective/Orthogonal projection types in the CameraManager, so
    it's independent of the Camera/Input Modes (MGED, Blender, etc).
-   When in orthogonal projection mode there's no concept of zooming,
    every object is projected with real size on the screen; so I started
    to look into how to emulate this by using view matrices and things
    like that.

July 25:

-   Screenshot:
    <http://brlcad.org/~mafm/g3d-screenshots/brlcad_rbgui_20080725-1.png>
-   Working on perfecting MGED (Shift-grips) mode
-   Talking with Sean for quite a long time about mid-term evaluation,
    some new goals (making binary release, working in making some widget
    control) and stressing some things (more polishing), etc -- main
    things reflected in ToDo section

July 23:

-   Commits for MGED (Shift-grips) mode:
    -   Scale commands seem to work fine
    -   Implementing basic translation, although not working as well as
        desired yet
-   Adding Axis enumerator to base CameraMode class, useful for some of
    the modes (Shift-grips at least) and other minor changes to adapt
    better to the new mode

July 22:

-   Continued working in Shift-grips/MGED camera mode, I almost have the
    "Normal View" working.
-   Fixing some missing things when finishing functions, or properly fix
    badly typed functions, etc (in blender Camera mode)
-   Adding button to show and cycle camera mode in the topbar, and
    adding a command too to cycle mode.

July 21:

-   Adding missing functionality to Blender camera mode: zoom in/out
    with mouse scroll (discovered by Dawn Thomas <homovulgaris>)
-   Separating camera modes (classes) in different files, as suggested
    by Sean.
-   Adding auto-completion functionality for the console and command
    overlay
-   Enhancing PolygonMode command so less typing is needed, minor
    rearrangements to prepare for next changes, and to avoid warnings

July 18:

-   Starting to work in Shift-grips camera bindings.

July 17:

-   Completing Blender camera mode, and factoring out more functionality
    in the base class (now basically the different modes act only on
    input, defining the bindings, as Sean had suggested).
-   Some commits correspond to work of yesterday.

July 16:

-   Changing private Observer/Listener pattern implementation in
    CameraManager by the one already existing in the project
-   Setting limits to orbital camera mode, so it doesn't cause strange
    artifacts when verticalRotation is greater than PI/2 (or smaller
    than -PI/2).
-   More work done but sourceforge's SVN has been unavailable due
    scheduled downtime -- some commits delayed for next day.

July 15:

-   Commited first serious code for handling camera, instead of the old
    hacks. It's the orbital mode, which it's very similar to the
    trackball mode (rotates around central the point of the scene,
    changing zoom distance and horizontal/vertical rotation), but it
    happens that I understand this well so it goes first.
-   Thinking about how the other modes would be implemented, by
    extending the actions of the current camera mode.

July 14:

-   Still working in camera implementation, but unfortunately not much
    since I got sidetracked by job interviews.
-   In the meanwhile, after talking with developers, scraped the idea of
    having a window for camera control, since: 1) it doesn't seem to fit
    into the "ideal operating environment" to have a small window
    present just for this, and 2) the basic camera modes should mimic
    what BRL-CAD uses already know, so no much point in making a visible
    interface for controlling it. There might be place for something in
    the top-panel showing camera mode and so on, maybe.

July 11:

-   Started to work in proper Camera controls implementation.

July 10:

-   Adding methods for basic camera manipulation. I'm waiting for
    confirmation from other devels, but I think that the proper thing to
    do is to create one or several camera modes with better and more
    complete functionality, encapsulated in a proper way.
-   Adding GeometryConversion class, and modifying the "create geometry"
    command so we can create at least sample tetrahedrons.
-   Screenshot after a few days:
    <http://brlcad.org/~mafm/g3d-screenshots/brlcad_rbgui_20080710-1.png>

July 9:

-   Trying to get manually-made geometries displayed in the window, with
    no successful results in the whole day. As I figured out later, it's
    not enough to create them as vertices list inside ManualObject, but
    it has to be created with indices so it can be made a Mesh, and then
    instantiate an Entity and add it to the SceneManager. And nowhere
    where they clearly tell you this. Pheeeeew.

July 8:

-   Using another approach for building 'src/other': creating the rules
    in a way that if some of the external libraries fails to build, the
    whole process stops (suggestion of Dawn Thomas). Hopefully I got it
    right this time...
-   Trying to create geometries, which in fact I think I do, but I can't
    visualize them...

July 3:

-   Continued working on automatic compilation of external dependencies
    (Ogre remained with some problems). Finally got all of them working
    smoothly in my system; but this will only happen for certain systems
    -- probably only GNU/Linux and at most FreeBSD; and some manual
    intervention for MacOSX.
-   Writing instructions about building, so hopefully with both of these
    issues "resolved" we will get more people willing test it.

July 2:

-   Working on automatic compilation of external dependencies
    (src/other, like Ogre or RBGui). This includes:
    -   To create a Makefile in there with rules to automatically
        compile/install those libraries
    -   Creating CMake files in Mocha (so SCons is not needed)
    -   Modifying CMake files for RBGui so no ".svn" files are installed
        in the system
    -   Creating pkg-config files from CMake files in Mocha and RBGui so
        no static external files are needed (and as a consequence now it
        uses CMake variables for choosing the destination of the
        installed files, in example).
-   This work should mean a step forward in the desired direction, but
    it's not very well tested and most certainly it won't work right
    away for non-modern-Unix systems.

July 1:

-   Moving basic window creation, operations and settings to base class,
    so we abstract and protect a bit more the code from the GUI
    libraries that we're using underneath. Other general enhancements:
    making public-accesable attributes read-only (const) in the Observer
    events, decoupling a bit more functionality of the Console from the
    widgets implementing it, etc.
-   Adding a couple of commands (quit, set log level); enhancing the
    command display (help), and the flexibility to show information
    about commands themselves.
-   Improvements to Logger class: checks when setting new level so it's
    a correct one, made it a ObserverSubject so other classes can attach
    and receive interesting events (e.g. the Console, to show also the
    log messages in there).
-   Substituted private Listener implementations for the more general
    Observer pattern, so we'll \[hopefully\] have less hassles when
    adding/modifying code in the future. The update() operation in the
    Observer is event-based, and the events are subclassed and
    identified by RTTI -- so we only need to create new types of events
    and program the reaction to them by the observers, no need to touch
    the rest of the code.

## June

June 30:

-   Working to create the Command Interpreter (to use in conjunction
    with console-like windows), still a work in progress.

June 27:

-   Mostly revisiting the code created so far (and commiting minor
    enhancements and fixes here and there), testing the features and
    preparing a bit the next steps (loading geometry and so on).

June 26:

-   Creating buttons in the top toolbar to quit the application and
    toggle visibility of console and command overlay.
-   Enhancing usability and consistency of Command and Console, such as
    focusing the prompt and closing command overlay automatically with
    each command entered.
-   Disabling keyboard and mouse grabbing in X11, so it doesn't disturb
    the user too much in the case of program hangs and the like (OIS
    defaults are really annoying).
-   Fix of many small glitches, doxygen documentation, cleanups and
    renamings for consistency.
-   Starting to look into Ogre geometries.
-   Screenshot of the Day:
    <http://brlcad.org/~mafm/g3d-screenshots/brlcad_rbgui_20080626-1.png>

June 25:

-   Usability enhancements to CommandOverlay and Console, such as
    sharing history and commands of CommandOverlay being reflected in
    the Console panel. Screenshot:
    <http://brlcad.org/~mafm/g3d-screenshots/brlcad_rbgui_20080625-1.png>
-   Spent half the afternoon investigating and fixing a problem with
    Ogre Singleton intantiations. It turns out that their implementation
    allows you to create objects from classes which are Singletons, and
    that kinds of cause weird problems.

June 24:

-   Working on the implementation and redesign of many things in the GUI
    front (see screenshot for visual reference:
    <http://brlcad.org/~mafm/g3d-screenshots/brlcad_rbgui_20080624-1.png>
    ):
    -   New Window Manager class, to act as high level decision-maker
        about layout; and things like taking into account created
        windows (and deciding which ones to show in taskbar), so I think
        that "assimilates" the Taskbar class too, and thus I removed it
        as separate class.
    -   New panel in the top, which will be used for context operations,
        setting fullscreen modes and things like that.
    -   Created new Command Overlay, separated from Console (but
        probably would collaborate and share a common history, etc)
-   Working "toggle Fullscreen" functionality
-   Making Application and GuiWindowManager classes a Singleton, so they
    can be accessed from elsewhere without having to pass pointers
    around all the time (it's needed for the "toggle fullscreen"
    functionality, in example).

June 23:

-   Watching again the video about "ideal interaction", for inspiration
    and to create a list of ideas to implement. I would like to have a
    chat about this though, to see the differences that we need to apply
    to our program.
-   Starting to implement a taskbar, to mimic the interaction shown with
    the video. Screenshot:
    <http://brlcad.org/~mafm/g3d-screenshots/brlcad_rbgui_20080623-1.png>

June 20:

-   Finished commiting OGRE (lots of hours spent seeking mime-types to
    meet SVN hooks' requirements), and also commiting Mocha and RBGui
    and brief, rudimentary building instructions.

June 19:

-   Starting to commit 3rd party libraries needed for all this to work:
    OGRE and OIS. Only OIS could be commited, at last.

June 18:

-   Sidetracked by work and bureaucracy, couldn't do almost anything.

June 17:

-   Preparing and uploading RBGui files (theme, shaders, images, fonts),
    OGRE config files are to be generated on the fly (they contain paths
    depending on installation options).
-   Getting the current code to compile with CMake in a clean fashion
    (without hardcoded system, in example). I think that it's a good
    base and a very important step.

June 16:

-   Take wmii (Plan9 window manager) (
    <http://www.suckless.org/wiki/wmii> ) as a guide when designing the
    console (recommended by [Sean](Sean.md))
-   Trying to get the project to build with CMake

June 14:

-   Creating Logging functionality.
-   Starting to look into putting data files in place, creating a proper
    build system and all that.

June 13:

-   Looking into ideas to implement the User Interface.

June 12:

-   More work in the Console, getting lines to wrap instead of being
    cut; and fixing RBGui (with several hours of reasearch involved) so
    autorepeat does use an initial delay and you can actually write
    individual characters (instead of 'aaaaaaaa' when you press the key
    for only 200ms). See the screenshot of the day:
    <http://brlcad.org/~mafm/g3d-screenshots/brlcad_rbgui_20080612-1.png>
-   A bit of work reorganizing code, making Doxygen documentation,
    removing leaks (even if the objects only are to be removed when the
    application closes anyway) and the like.
-   I wrote to RBGui guys to know if they're interested in patches to
    support at least my platform (Debian GNU/Linux, amd64 -- but at
    least Linux and POSIX systems by extension) instead of having to
    maintain private patches.
-   I need ideas and directions about what things to implement (e.g. how
    to implement console window, if I should use logging from libbu or
    making my own method, for a start).

June 11:

-   Today I continued working in the Console, now at least the history
    functionality and the way to create and position windows it is
    basically stable (can be changed easily, but I mean that it's not a
    hack-ish/example-ish application). Screenshot:
    <http://brlcad.org/~mafm/g3d-screenshots/brlcad_rbgui_20080611-1.png>
-   OIS (the input library) is giving problems with auto-repeat, a
    problem that already had several years ago: it disables auto-repeat
    from X, so the rest of the applications in that DISPLAY that
    capability, and if the application crashes before OIS restores it,
    you have to reset it by hand. This looks unacceptable to me, but I
    haven't devised any solution yet.

June 10:

-   Mostly working in the Console window & functionality, still quite a
    lot of work to be finished.

June 9:

-   Still working in the example application, but now it looks much
    better -- documented, code style, reorganizing things, making cursor
    visible (wasn't there in the POSIX version at least)... Screenshot:
    <http://brlcad.org/~mafm/g3d-screenshots/brlcad_rbgui_20080609-1.png>

June 8:

-   Getting RBGui sample application to work, reading "administrative"
    information of rt^3 module and in general preparing for submitting
    the code.
-   Commiting first patches, it's basically the example application
    coming with RBGui.

June 6:

-   Patching and recompiling other branches needed of some of the
    components, RBGui doesn't work with the most recent stable versions
    of OGRE right away.
-   Investigating a bit about other GUIs, updates on the considered
    GUIs, etc; with no interesting results: things are basically the
    same as when making the application.

June 5:

-   Compiling OGRE and OIS (input system, needed for most applications
    using OGRE), since latest stable versions are not available in
    Debian. No big hassles.
-   Compiling Mocha, a library needed by RBGui with misc utilities (3D
    math and the like) -- found a source RPM with minor patches for
    GNU/Linux systems, again no big problems.
-   Compiling RBGui... this one is not so easy. Some CMake config files
    have to be modified, at least for my 64 bit system; and it's not in
    sync with OGRE (it seems to use some special function) so it doesn't
    compile successfully, yet.
-   Thought: I'm starting to be a bit worried about RBGui... by the time
    of the application they had very recent releases adding support for
    \[at least\] GNU/Linux systems, apart from Windows. Now, even if
    there seems to be people porting it to MacOS X too, the developers
    seem are mostly silent and inactive. In general, it seems that this
    complicates the ease of installation for BRL-CAD users, and thus
    RBGui seems less convenient now than a while ago...

June 4:

-   Misc. preparations: compiling up-to-date BRL-CAD, re-enabling
    subscriptions to mailing lists, and checking the tools to use (OGRE,
    RBGui). Not a very productive day, but not so bad to be the 1st day
    after weeks of overworking and travelling... and at least it's a
    start!

June 3:

-   Back to Lisbon, at last. Hopefully tomorrow I'll start coding!

## May

May 26:

-   SoC program starts :)
-   Due to some personal problems and exam dates (as already noted when
    submitting the application) I couldn't start coding or submitting
    patches to get commit access, note sure if I'll be able to start
    before June 5th or so.
