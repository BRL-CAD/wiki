year is 2019

# Before Bonding Period

-   Create a Simple Qt Ui for a CAD software (no functionalities)
-   Built from sources and run
-   Learnt some Tcl/Tk
-   Studied a CoreInterfaces
-   Studied and made modifications to RT^3 Qt project

# Bonding Period

## May 21

-   Completed the [Checklist](/wiki/Summer_of_Code/Checklist)

# Coding Period

## May 27 - May 31

-   I am trying to understand how things are happening in BRL-CAD.
    Things aren't very easily understandable. So I am doing things like
    breaking and studying the function call stack to understand what
    happens underneath. I need to do this because I believe I should
    implement displaying of geometry first since the existing thing in
    RT^3 project (ray tracing) is not sufficient even for development.
-   Now understand how different DMs display Vlists using OpenGL or
    Window system methods.
-   I'm studying Vlist creation.

## June 1

-   Vlist obtained for a single solid in RT^3 project

## June 2

-   Added QOpenGLWidget to the application. Line creation is not
    straight-forward like in the earlier OpenGL version which existing
    OpenGL DMs use in BRL-CAD. glBegin and glEnd are have been
    deprecated and now removed in QOpenGLWidget. Studying the new
    method.
-   Added the deprecated component QGLWidget instead of QOpenGLWidget
    since the later doesn't support the methods used in BRL-CAD.
-   Studied OpenGL API

## June 3

-   Implemented displaying an object on the QGLWidget using wireframes

## June 4

-   Experimented with some keyboard controls to move around in the scene

## June 5

-   Abandoning ft_plot, need to implement Facetize.
-   Obtained NonManifoldGeometrys for a db.

## June 6

-   Working on trying to use Facetize for DM.

## June 8-14

-   No implementations, following qt tutorials.

## June 15

-   Laptop broke
-   I learnt some AutoCAD during the days my laptop wasn't working.

## June 23

-   Started a new project QtNewGUI rather than doing the QtGUI as per
    Daniel's suggestion.
-   Started creating toolbox. (still can't work in my laptop well)

## June 24

-   Got laptop repaired.
-   Added GraphicsViewOpenGL and placed it as the central widget.

## June 25

-   Opening DB, displaying geometry names in Objects list.
-   Tried to configure BRL-CAD for windows (either of VS or Clion)
    failed.

## June 26

-   Geometry is displayed in QtNewGUI graphics screen now.
-   Tried to configure BRL-CAD for windows (either of VS or Clion)
    failed.

## June 27

-   Saving database to a file.
-   Tried to configure BRL-CAD for windows (either of VS or Clion)
    failed.
