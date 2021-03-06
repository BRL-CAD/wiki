This project involves implementing a new cross-platform display manager
for BRL-CAD's LIBDM display manager library using an API toolkit such as
OGRE or Qt that abstract platform-specific implementation detail.

BRL-CAD's primary means to interact graphically with geometry is
provided by ***display managers***, which handle drawing geometric
wireframes, text, (sometimes) shaded triangle mesh geometry, and other
visualization elements. It's the 3D graphics window. Currently BRL-CAD
has specific display managers for X11 Opengl (ogl), Windows OpenGL
(wgl), and raw X11 (X), in addition to a variety of other special
purpose and experimental display managers. Consequentially, our existing
display managers are all platform-specific and a burden to maintain.

Either OGRE or Qt could be utilized to implement a new display manager
interface

The steps for this task would be:

1.  Review current display manager code to identify features a new
    display manager needs to support
2.  Get OGRE or Qt running and embedded within a Tk window (this will be
    necessary for Archer/MGED to use the display manager). Bear in mind
    that one of the primary goals is to use this display manager on
    multiple platforms.
3.  Identify how to perform the basic operations needed for a display
    manager, including
    -   line drawing
    -   text display
    -   keyboard and mouse input integration between OGRE or Qt and Tk
    -   embedding a framebuffer window (see overlay/interlay/underlay
        settings in the MGED raytrace control panel)
4.  Writing routines to perform tasks needed (the display manager
    functionality) and hooking it into libdm
5.  Testing (ideally cross platform) -- load a .g model and display it
    in the display manager

A good proposal for this task would demonstrate a good understanding of
what approaches would be taken to embed OGRE or Qt into Tk and what
functionality would be utilized to perform wireframe drawing, text
drawing, etc.

# References

-   src/libdm
-   include/dm\*.h

<!-- -->

-   <http://www.ogre3d.org/>
    -   OGRE is a cross platform, open source 3D graphics engine that
        provides the features needed to implement a display manager for
        BRL-CAD, while abstracting many of the low level platform
        specific details. OGRE has the added benefit of having built-in
        support for scene graph management allowing for accelerated 3D
        windows.

<!-- -->

-   <http://qt.nokia.com/>
    -   Qt is a cross-platform application and UI framework of interest
        for new GUI development work in BRL-CAD. It similarly has
        support for creating OpenGL-based display contexts that could
        serve as the implementation detail for a new display manager. Qt
        has the added benefit of being able to use drawing canvases not
        reliant upon OpenGL or hardware acceleration.

# Requirements

-   Familiarity with C and C++
-   (optional) Familiarity with OGRE
-   (optional) Familiarity with Qt

# Past Efforts

[GSoC12](../user/Mesut/Reports.md)
