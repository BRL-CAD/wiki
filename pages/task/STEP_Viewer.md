STEP is the current standard for exchange of CAD data between different
software packages. BRL-CAD makes use of the NIST STEP Class Libraries
code to support its step-g converter. That gets STEP geometry data
(AP203 or AP214) into a format that we can visualize as either
wireframes or rendered via ray-tracing (2D raster or 3d point clouds).
Eventually, we will have polygonal representations available as well,
but check on the status of that before assuming meshes are available..

Depending on the approach being proposed, there are lots of ways to get
at visualizing STEP geometry via a stand-alone viewer application. You
could build an interface on top of our ADRT real-time raytracing or on
top of our libdm display manager library for wireframes and mesh
visualization. You could build an interface on top of our libfb 2D
framebuffer library (near real-time ray-tracing). You could build an
application in Qt that talks directly to our librt geometry library to
visualize wireframes and meshes. You could probably build a web
interface (but this approach is probably much more work).

The goal of this project is a 3D geometry viewer application. That
application can and should be built on top of BRL-CAD resources where
available in modular form so that a self-contained viewer distribution
could be made available to users.

# References

-   src/conv/step
-   src/adrt
-   src/libdm
-   src/libfb
-   src/librt

# Requirements

-   Strong familiarity with C or C++