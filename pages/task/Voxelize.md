Voxel data sets are commonly used in computational fluid dynamic
simulations. The current technique for creating voxels from BRL-CAD
geometry is to use the proprietary cubit framework.

This task would involve using raytracing to interrogate a specified
combination/region/assembly and produce a set of arb8's in a new region
approximating the shape. Interface should be similar to the facetize
command and will need the TCL binding to connect the mged editor to the
library functionality.

# References

-   src/librt
    -   raw grid shooting could go here
-   src/libanalyze
    -   or here
-   src/libgcv
    -   or here

There are tradeoffs and considerations to each of those that can be
discussed in detail if you're interested.

# Requirements

-   Familiarity with C
-   Familiarity with Tcl/Tk