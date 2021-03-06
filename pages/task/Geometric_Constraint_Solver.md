Previous GSoC projects have made progress towards a
parametrics/constraint library. Please check [libpc Developer
Doc](../doc/Libpg_:_A_parametrics/constraint_library.md) as well as the
[libpc
source](http://brlcad.svn.sourceforge.net/viewvc/brlcad/brlcad/trunk/src/libpc/).
For this year's project, we're suggesting a specific direction as
outlined below.

BRL-CAD does not presently provide the means to specify values that are
undetermined or otherwise dependent calculations. That is to say that
there is no support for constraints and parametrics such that a modeler
can define a sphere such that the sphere's radius necessarily maintains
tangency with a given planar surface. This task would focus on
implementing basic support for this feature in the BRL-CAD geometry
format. Parametric representation of Geometry (and constraints) provides
a good foundation for various aspects of Design computation, Geometry
Generative Algorithms, and A more logically connected model not to
mention significant reduction in Modeling time (since the process of
modeling during an actual design cycle is inherently iterative).

Since the initial work on libpc began, the open source gecode constraint
solver has released version 4.0 with support for floating point data
types. The work to be done is to put gecode's constraint solver
"underneath" the libpc API in place of the existing solver and
demonstrate successful soltions to primitive constraint equation
systems. (Discuss these with the BRL-CAD developers.)

# References

-   <http://www.gecode.org/>
-   <http://www.gecode.org/doc-latest/reference/classCartesianHeart.html>
-   <http://www.nist.gov/manuscript-publication-search.cfm?pub_id=822720>
-   src/libpc
-   include/pc.h
-   src/librt/primitives/table.c
    -   contains primitive callback definitions
-   src/librt/primitives/\*\*
    -   each primitive needs to implement a routine that returns
        available parameters, rt_\*_param().

Requirements:

-   Familiarity with C/C++
-   General understanding of constraint solving
