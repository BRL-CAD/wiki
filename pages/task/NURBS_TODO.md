# Profile BREP/NURBS ray tracing

-   Benefit: better ray tracing runtime understanding, supports test
    case development
-   Time Estimate: 2 days
-   References:
    -   src/libbrep
    -   src/librt/primitives/brep
    -   src/librt/opennurbs_ext.\*

# Optimize BREP/NURBS prep

Perform limited tree splitting during prep, split dynamically during ray
trace, store lock-free.

-   Benefit: faster ray tracing throughput, user requested, user visible
-   Time Estimate: 1 week
-   References:
    -   src/libbrep
    -   src/librt/primitives/brep/brep.cpp:rt_brep_prep()
    -   src/librt/opennurbs_ext.\*

# Convert existing entities to NURBS

Implement hooks to describe entities in BREP/NURBS form. Partially
complete for most, but some complex entities remain unimplemented.

-   Benefit: partial requirement for interactive visualization of
    implicit CSG geometry in OpenGL
-   Time Estimate: 2 days per entity
-   References:
    -   src/librt/primitives/${PRIM}/${PRIM}_brep.cpp

# BREP/NURBS-to-NMG

Implement conversion of BREP/NURBS to NMG.

-   Benefit: requirement for polygonal export, partial requirement for
    OpenGL visualization, user visible
-   Time Estimate: 2 days
-   References:
    -   src/librt/primitives/brep/brep.cpp:rt_brep_tess()

# Old BSPLINE/NURBS review

Identify useful concepts implemented in the old BSPLINE/NURBS code that
are not present in openNURBS.

-   Benefit: code reuse, potentially very useful functionality.
-   Time Estimate: 1 day
-   References:
    -   src/librt/primitives/bspline/\*

# BSPLINE/NURBS reuse

Port any useful BSPLINE/NURBS code to openNURBS data structures and
routines.

-   Benefit: code reduction, allows the old BSPLINE/NURBS code to be
    removed after functionality is migrated.
-   Time Estimate: 2 days
-   References:
    -   src/librt/primitives/bspline/\*
    -   src/librt/primitives/brep/\*

# BREP/NURBS CSG evaluation

Implement boolean evaluation of BREP/NURBS surfaces.

-   Benefit: partial requirement for interactive visualization of
    BREP/NURBS in OpenGL.
-   Time Estimate: 2 years (for 100% robustness)
-   References:
    -   ESOLID: <http://research.cs.tamu.edu/keyser/geom/esolid/>
    -   <http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.119.4341&rep=rep1&type=pdf>
    -   <http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.117.8700&rep=rep1&type=pdf>
    -   <http://www.springerlink.com/content/x3665206243u20x8/>
    -   <http://193.170.37.128/projects/basic/cgal/workdone/nurbs-97-30.ps.gz>
    -   <http://mae.ucdavis.edu/~farouki/foils.pdf>
    -   <http://portal.acm.org/citation.cfm?id=36714>
    -   <ftp://ftp.cs.unc.edu/pub/users/manocha/PAPERS/INTERSECT/IJCGA.pdf>
    -   <http://portal.acm.org/citation.cfm?id=237751>

# Implicit CSG to BREP/NURBS CSG test scripts

Develop test scripts for comparing conversion of implicit CSG to
BREP/NURBS CSG

-   Benefit: provides validation and verification via ray tracing.
-   Time Estimate: &lt; 1 day
-   References:
    -   regress/\*.sh
    -   sh/\*.sh

# BREP/NURBS documentation

Document the new BREP/NURBS primitive (user overviewdocumentation: how
to import, use, export, limitations).

-   Benefit: provides user documentation explaining capabilities,
    limitations, and benefits; user visible
-   Time Estimate: 3 days
-   References:
    -   doc/docbook/articles

# BREP/NURBS wireframe

Improve BREP/NURBS wireframe. Investigate using knots on subcurves.

-   Benefit: faster wireframe; LOD wireframes: more detailed close-up
    wireframes, less detailed far-away wireframes (LOD); user visible
-   Time Estimate: 2 days
-   References:
    -   <http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.142.3042&rep=rep1&type=pdf>
    -   <http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.70.6138&rep=rep1&type=pdf>
    -   <http://www.springerlink.com/content/k7543860533338nu/>
    -   <http://wscg.zcu.cz/wscg2003/Papers_2003/H19.pdf>
    -   <http://cg.cs.uni-bonn.de/aigaion2root/attachments/kahlesz-2002-multiresolution.pdf>
    -   <http://www.cs.cityu.edu.hk/~rynson/papers/vrst03.pdf>
    -   <http://www.flipcode.com/archives/NURBS_Curves_Surfaces.shtml>

# BREP/NURBS source code cleanup

Consolidate Owens and Reeves approaches to ray intersection.

-   Benefit: improved code maintainability, complexity reduction
-   Time Estimate: 2 days
-   References:
    -   <http://www.cs.utah.edu/~shirley/papers/raynurbs.pdf>

# BREP/NURBS healing

Implement an rt_heal(rt_db_internal \*dbi); routine. The routine
tightens up trimming curves and edge/vertex pairings so that they align
perfectly while still preserving the topological structure.

-   Benefit: more robust evaluation for improved (more stable &
    consistent) raytracing, import, export; routine interface later
    applicable to NMG/BoT too
-   Time Estimate: 3 days
-   References:
    -   src/librt/primitives/brep