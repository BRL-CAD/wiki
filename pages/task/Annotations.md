BRL-CAD currently has only very basic labels that are attached to CSG
primitive parameters in 3D wireframe views. We need much more than that
- modern systems typically show a variety of leader line and text
graphics that illustrate information associated with 3D geometry. There
are two aspects to this task - one is to create an "annotation
primitive" in BRL-CAD that can hold this information, and the other is
to display that information in the 3D view. The second depends on the
first - "hacking in" a 3D text and leader-line display won't get us what
we need.

# References

-   TODO starting at line 1400
-   <http://en.wikipedia.org/wiki/Geometric_dimensioning_and_tolerancing>
-   include/rt/primitives/annot.h
-   src/libdm/\* (display managers)
-   src/librt/primitives/annot/annot.c
-   include/rt/geom.h

Requirements:

-   Familiarity with C/C++
-   (For graphical components) familiarity with OpenGL + Text