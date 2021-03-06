Often when modeling, it is necessary to represent solids with very large
surface areas but very small thicknesses, such as sheet metal. It is
often impractical to represent these thin solids exactly as bounded
volumes, so an alternative approach is to model a surface and "tag" it
with an implicit thickness. That is, when a ray intersects the surface,
an "out" hit point is assigned some small distance from the initial hit
point along the ray. BRL-CAD currently implements this modeling
technique for the BoT primitive, and BoTs that utilize it are referred
to as "plate mode".

This task would be to implement plate mode raytracing for NURBS
surfaces. Thin materials (such as those used for airplane skins) are a
common modeling scenario for NURBS models.

A student proposal on this topic would need demonstrate research into
the various issues that arise when plate-mode raytracing is used and how
to address them.

# References

-   src/librt/primitives/brep/brep.cpp
    -   our new nurbs primitive
-   src/libbrep
    -   where most of the current brep algorithms live
-   src/librt/primitives/bot
    -   our "bag o' triangles" primitive implements plate mode meshes,
        perfect example to follow

# Requirements

-   Familiarity with C/C++