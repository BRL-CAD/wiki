Tessellation - the process of converting implicit primitives into NMG
and triangle representations - is fundamental to most of BRL-CAD's
converters and techniques for interactive shaded displays.

BRL-CAD's tessellation logic operates using boolean tree structures and
primitive tessellations - for a given geometric tree, primitives (leaf
nodes in the tree) are tessellated, and the results of those
tessellations are merged to form the combination above them. Then those
results are in turn merged to form higher level tessellations, until
either the top of the tree is reached or a stopping point (like a region
designation on a combination) is reached.

Unfortunately, current methods of merging meshes do not take into
account geometric proximity - which parts of various meshes need to be
considered for merging and which parts can be safely ignored for a given
merge. This tends to result in a great deal of unnecessary work, slowing
conversions.

Proposals for this task should outline partitioning strategies as well
as testing methods - before-and-after timing for tessellation
performance and quality testing of resulting geometry are key benchmarks
to track.

# References

-   src/libgcv
-   src/librt/primitives/\*\*
    -   each primitive is in a subdirectory with an rt_\*_tess()
        function defined that performs tessellation
    -   the rt_\*_prep() routine calculates the bounding box, ideal
        candidate to be broken out into a separate callback which could
        be useful during space partitioning
-   src/conv
    -   just about every converter performs boolean evaluation on
        tessellated geometry

Requirements:

-   Familiarity with C