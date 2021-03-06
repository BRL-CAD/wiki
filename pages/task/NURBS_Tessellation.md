Non-Uniform Rational B-Spline surfaces are not suitable for direct
visualization on modern GPU systems, and also cannot be represented in a
number of widely used geometry storage formats (stl, dxf...). Thus, for
both visualization and conversion BRL-CAD needs to implement the ability
to tessellate NURBS volumes into explicit NMG representations.

There are various "quick and dirty" approaches to tessellating NURBS,
but BRL-CAD's routines also should satisfy solidity constraints - e.g.
if NURBS surfaces form a solid Boundary Representation (BREP) the
results of the tessellation should also form a valid NMG solid. This
involves successfully "merging" individual tessellations from surfaces
to form solid meshes.

The first step will be to successfully tessellate and display individual
surfaces, followed by merging the individual surface tessellations into
solid meshes.

# References

-   <http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.142.3042>
    -   It's a good paper to start with to understand some of the issues
        involved.

<!-- -->

-   src/librt/primitives/brep (new nurbs implementation)
-   src/librt/primitives/bspline/nurb_tess.c (this is our old
    implementation)
-   src/librt/primitives/nmg/nmg_tri.c (triangulation of polygons while
    preserving topology)

# Requirements

-   Familiarity with C/C++