N-Manifold Geometries are BRL-CADs primitive for representing generic
volumes of geometry bound by flat surfaces. They are more general than
BoTs in that they are not restricted to triangles. Neither MGED nor
Archer has any significant graphical ability to edit NMG structures
directly - they are more typically used during conversion of other CSG
primitives to facetized geometry for export.

This task would involve studying the NMG data structure and how best to
provide graphical editing capabilities for it in Archer. This should
include:

-   Ability to select subsets of an NMG via table based interface (see
    Archer's support for combination editing)
-   Ability to add and remove elements of an NMG while still satisfying
    validity constraints
-   Ability to move parts of an NMG interactively
-   Visual feedback in the geometry window on which parts are selected

NMGs are complex data structures, and a basic understanding of them will
be essential to this task - a proposal on this topic should be detailed
enough to demonstrate that understanding.

# References

-   src/librt/primitives/nmg
-   src/tclscripts/archer
-   src/tclscripts/mged
-   include/nmg.h

<!-- -->

-   <http://ftp.arl.army.mil/~mike/papers/90nmg/all.ps>

# Requirements

-   Familiarity with C
-   Understanding of NMG (see referenced paper above)