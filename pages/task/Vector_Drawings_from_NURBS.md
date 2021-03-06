BRL-CAD can render hidden line drawings using rtedge, but the images it
generates are raster images (consisting of pixels) rather than vector
drawings (based on lines and curves). This is often suboptimal - line
drawings are often edited and rescaled using vector based editing
programs, and rtedge output must be manually traced in order to be used
in those environments.

Without explicit surface representations we cannot (currently) calculate
vector forms of significant lines () directly from models using CSG
without using raytracing. BRL-CAD can import and raytrace NURBS based
models, and focusing on those as a starting point is a valid direction
(the completion of the NURBS Boolean project would offer a path for CSG
models via NURBS significant lines.) However, a possible alternative
approach to directly deal with CSG models is to take the grid results of
the rtedge raytrace and use the knowledge inherent in the ray about what
object it's returning the pixel from to group pixels into groups based
on objects. From there, the set of xy points in image space could be
fitted with spline curves to produce vector representations.

# References

-   <http://www.cs.princeton.edu/gfx/proj/sg08lines/>

<!-- -->

-   <http://people.csail.mit.edu/sparis/publi/2009/siggraph/Eisemann_09_A_Visibility_Algorithm.pdf>
    -   For the ambitious, it might even be possible to go beyond lines
        and bound areas - this paper illustrates possibilities with
        layered 2D output from 3D models.

<!-- -->

-   rtedge
-   src/rt/viewedge.c
-   src/rt/view.c
-   rt

Requirements:

-   Familiarity with C/C++
-   Solid mathematical background (algorithms for fitting curves to
    points)