BRL-CAD has recently implemented support for raytracing of NURBS
surfaces, but beyond basic operations such as rotation and translation
it has no ability to edit them. This project would implement support for
editing NURBS curves and surfaces in the new Archer modeling interface.

Note that editing NURBS in Archer should not assume OpenGL surface
representations of NURBS are available. Editing should be possible using
wireframe representations of key features, and be mappable to more
sophisticated OpenGL based visualization once it appears.

Main tasks would be:

1.  Identifying key editing operations (see next) and mapping those
    operations to openNURBS calls (or identifying that the equivalent
    routine doesn't exist in openNURBS and will need to be implemented)
2.  Implementing librt/libbrep/libged logic to allow those calls to be
    made
3.  Implementing appropriate graphical controls and interface logic in
    Archer (other primitive editing support code in Archer will provide
    relevant examples).

NURBS curve editing operations:

-   Attach (two splines)
-   Detach (end point)
-   Connect (splice new curve)
-   Trim (cut curve)
-   Knot Insert
-   Reverse (change direction)

NURBS curve to surface operations:

-   Projection (see [here](Vector_Drawings_from_NURBS.md))
-   Loft/Birail (surface created between curves)
-   Cap (surface from closed curve)
-   Extrude
-   Revolve

NURBS surface editing operations:

-   Rebuild/Simplify (remove unnecessary control points)
-   Trim (evaluate to untrimmed)
-   Bevel/Fillet (replace edge with surface+edges)

# References

-   <http://ayam.sourceforge.net/>
    -   The Ayam editor is a BSD licensed, Tcl/Tk based modeler for
        NURBS. It's primary purpose is to serve as a modeler for the
        RenderMan interface, but at least some of the functionality it
        implements is of interest to BRL-CAD. It's primary license is
        compatible with BRL-CAD's, but Ayam makes use of many third
        party components so be sure to check individual files for
        license information.

<!-- -->

-   src/librt/primitives/brep/brep.cpp
-   src/libbrep
-   src/other/openNURBS
-   src/libtclcad

# Requirements

-   Familiarity with C and C++
-   Familiarity with Tcl/Tk
-   Basic understanding of NURBS
-   (optional) openNURBS and/or Ayam experience
