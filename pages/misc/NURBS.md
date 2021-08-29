Implementing complete support for Non-Uniform Rational Basis Spline
(NURBS) boundary representation geometry is a major area of active
development. With NURBS, it becomes possible to import and modify
geometry from other CAD and solid modeling systems without resorting to
lossy format conversions, such as to polygonal mesh (BoT) geometry.

NURBS features are considered complete or are demonstrated (but not yet
considered adequate) include:

-   import via 3DM and STEP file formats
-   robust ray tracing of valid and solid entities
-   non-solid tessellation for interactive visualization
-   losslessly converting implicit entities unevaluated
-   documented Boolean evaluation debugging process
-   solid tessellation for polygonal export (demonstrated)
-   export via 3DM and STEP file formats (demonstrated)

Implementing import and robust solid ray tracing support for NURBS
geometry took more than 5 years of active effort and remains a priority
area of development. It supports a long-term goal of fully hybrid
representation geometry where 3D data may be transparently converted
between representation formats as needed.

BRL-CAD's implementation heavily leverages and extends the [OpenNURBS
Toolkit](http://wiki.mcneel.com/developer/opennurbs/home) from Rhino3D
for import and in-memory representation support. Beginning with release
7.26.0, NURBS are considered viable for production users of BRL-CAD
needing import, ray tracing support, and editing via implicit CSG
operations.

BRL-CAD does not yet offer complete support for NURBS. There are many
features pertinent when referring to implementing NURBS that are
important to some users and not others. The details regarding what NURBS
functionality is started but considered incomplete include:

1.  [explicit NURBS Boolean evaluation](../task/NURBS_Booleans.md)
2.  [interactive surface editing](../task/NURBS_Editing_Support.md)
3.  [export to polygonal mesh](../task/NURBS_Tessellation.md)
4.  [export to vector drawings](../task/Vector_Drawings_from_NURBS.md)
5.  [ray tracing performance (optimization)](../task/NURBS_Optimization_and_Cleanup.md)
6.  [converting explicit entities (e.g., BoT, NMG, EBM, Vol)](../task/Implicit_to_NURBS_conversion.md)
7.  [support for (non-solid) surface NURBS](../task/Plate_Mode_NURBS_raytracing.md)

See [here](../task/NURBS_TODO.md) for more TODO topics. Help wanted.
