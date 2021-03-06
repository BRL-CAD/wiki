Currently, the primary mode of geometry visualization in BRL-CAD's
interactive tools is wireframes. This is relatively primitive compared
to a modern shaded display, but has some advantages in that it is fast
and general (CSG primitives with no surface representation can still
generate wireframes).

While this approach is generally useful for CSG models, it runs into
difficulties in several cases. Currently, primitives have no awareness
of how they are being viewed, and thus generate only one wireframe for
all situations. Hence, a close-up view of a sphere in wireframe mode can
easily lead to an empty screen if the wireframe is zoomed out of view,
despite the entire view being "filled" by the sphere. Conversely, a
large BoT (bag of triangles) model may thousands upon thousands of
edges, and the current drawing routines have no knowledge of which edges
are hidden behind other geometry - this slows performance dramatically
as MGED attempts to redraw huge line sets for each move of the geometry.

This project would implement a mechanism for each primitive to provide a
"view aware" wireframe, instead of a generic one. A dense tiny BoT that
takes up 1/200th of the view would know not to draw thousands of lines,
and close-up of a sphere would know to provide some more detailed lines.
Occlusion culling isn't necessary for this project (it's a difficult
problem for implicit primitives) - the goal is to keep wireframes
informative and interactive whatever the particular view/zoom is.

The particular tasks would be:

1.  Design a callback API for librt primitives to provide on request a
    view dependent wireframe
2.  For at least most of the common primitives, outline wireframe
    strategies for generating wireframes spanning very tiny to very
    large view situations.
3.  Implement and test the API and wireframe schemes.

# References

-   src/librt/primitives/table.c
-   src/librt/primitives/\*\*
    -   all primitives are in a subdirectory, each implement an
        rt_\*_tess() and rt_\*_plot() for mesh and wireframes
        respectively.
-   include/raytrace.h
-   include/rtgeom.h

# Requirements

-   Familiarity with C
-   (optional) Familiarity with MGED drawing and librt API