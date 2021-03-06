The majority of geometric primitives implemented in BRL-CAD are implicit
primitives - that is, they are descriptions of volumes and not surfaces
enclosing volumes. (A concrete example would be storing a sphere as a
center and a radius, rather than a collection of triangles that describe
the surface of the sphere). This representation is extremely compact and
good for guaranteeing solidity, but has distinct disadvantages when it
comes to interactive shaded displays and conversion to other formats.

There has been a lot of work done in BRL-CAD to support representing
implicit primitives as NURBS boundary representations. This increases
the range of options available for conversion, and sets up possibilities
for other features (like 3D shaded displays). We currently have basic
implementations for most of our primitives as NURBS, but only located at
the mathematical origin and not fully robust (for example, the pipe
primitive only works with certain parameter settings, and should work
for all pipes).

This GSoC task would be to take the current CSG implicit primitive to
BREP conversion routines, complete any missing features (like the
ability to represent shapes at locations other than the origin) and make
the results robust (valid CSG primitives would generate valid BREPs).
The test will be take our example CSG models, convert the CSG primitives
to BREPs while preserving the same tree structure, and test to confirm
that the raytrace does not change. If it does not, that means the
conversion logic has faithfully represented the original data as NURBS
data.

# References

-   src/librt/primitives/\*\* (each primitive is in a separate subdir,
    see rt_\*_brep() functions)

# Requirements

-   Familiarity with C/C++
-   (optional) Solid mathematical background (in case NURBS related
    issues appear)