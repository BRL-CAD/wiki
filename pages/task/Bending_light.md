BRL-CAD provides extensive facilities for representing geometry and a
robust high-performance ray tracing library for interrogating geometry.
BRL-CAD's LIBRT ray tracing library provides a means to shoot rays at
geometry, obtain intersection hit points, obtain object thicknesses, and
much more. BRL-CAD's LIBOPTICAL and LIBMULTISPECTRAL optics libraries
control shooting rays with the intention of representing energy
transport (e.g., light rays) with various possible outputs (such as
rendering an image).

The existing ray tracers either shoot a grid of rays orthogonal to an
image view plane or shoot rays divergent to a view plane for perspective
images. The rays travel in a straight line until they hit something
whereupon the optics library is called to calculate a color, usually for
rendering pixels of a picture.

This task involves adding support for rays that don't necessarily
traverse in a straight line. This will probably entail changes to either
LIBOPTICAL and/or LIBRT. A proposal of changes will need to be written
up and discussed beforehand. Any implementation of ray bending should be
consistent with the existing API and will need to be maintainable within
BRL-CAD's sources.

# References

-   src/librt
-   src/liboptical
-   src/rt/view\*.c
-   include/raytrace.h
-   include/optical.h

# Requirements

-   Strong familiarity with C