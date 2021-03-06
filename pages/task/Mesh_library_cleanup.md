BRL-CAD has an extensive n-manifold (NMG) polygonal mesh library called
LIBNMG. N-manifold is mostly a fancy way of saying it provides an
arbitrary boundary representation structure. This library is used for a
wide range of tasks but is commonly interacted with during geometry
export to polygonal formats (e.g., g-stl). The library goes to extensive
lengths to ensure that geometry is "correct" at every step along the
way, that solidity is preserved, that topology is preserved, and more.
All of that work means that the library can be slow and over time has
become even more "unrobust" to real geometry. There are lots of O(n^2)
and O(n^3) algorithms with dynamic memory allocations that make
performance suboptimal. The source code is the documentation. It's one
of the best at what it does, but far from good enough.

This project entails basic source code cleanup, validation, and
verification. The first step is documentation cleanup pulling all of the
source code comments into the nmg.h public header (or sub-header
thereof) to become familiarized with the API. Then begin testing the
lowest-level functions to make sure they do exactly what they are
supposed to do by creating API unit tests. Test-driven development is a
must here.

# References

-   <http://en.wikipedia.org/wiki/Topological_manifold>
-   <http://cubit.sandia.gov/help-version8.1/Chapter_1/Features/Non-Manifold_Topology.html>
-   <http://ftp.arl.army.mil/mike/papers/90nmg/>
-   src/librt/primitives/nmg
-   include/nmg.h
-   include/raytrace.h

For the problem of boolean operations on NMG structures, recent papers
should be studied. Some examples:

-   Fast, Exact, Linear Booleans:
    <http://www.gilbertbernstein.com/resources/booleans2009.pdf>
-   Exact and Efficient Booleans for Polyhedra:
    <http://liris.cnrs.fr/Documents/Liris-4883.pdf>
-   Fast and robust Booleans on polyhedra:
    <http://www.sciencedirect.com/science/article/pii/S0010448512002412>
-   Exact, robust, and efficient regularized Booleans on general 3D
    meshes:
    <http://www.sciencedirect.com/science/article/pii/S0898122115003028>
-   Fast, Exact and Robust Set Operations on Polyhedrons Using Localized
    Constructive Solid Geometry Trees:
    <http://wwwen.zte.com.cn/endata/magazine/ztecommunications/2015/3/articles/201510/P020151021364587175341.pdf>

# Requirements

-   Ability to read and refactor complex C
-   Ability to write API unit tests