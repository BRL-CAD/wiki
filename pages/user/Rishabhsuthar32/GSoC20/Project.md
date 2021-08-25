## **OpenCL GPGPU Raytracing**

### Development Plan

-   Week 1 (June 01 - June 05):

Developing the OpenCL patch for ARBN primitive. BRL-CAD uses such
primitives to represent polyhedra having any number of sides, edges and
vertices. Given ARB8 primitive which has already been converted, it will
give an insight as to how to proceed with this.

-   Week 2 (June 08 - June 12):

Developing the OpenCL patch for PIPE primitive which is responsible for
hollow and solid pipes and wires.

-   Week 3 (June 15 - June 19): Displacement Map primitive

<!-- -->

-   Week 4 (June 22 - June 26): Code Review and Testing

<!-- -->

-   Week 5 (June 29 - July 3): Phase 1 evaluations

<!-- -->

-   Week 6 (July 6 - July 10): Converting 3-D volume primitive to OpenCL
    version. The vol solid is defined by a 3-dimensional array of
    unsigned char values. The solid requires a file of these values, the
    extent of the file (in bytes) in each dimension, the size of each
    cell, and high and low thresholds.

<!-- -->

-   Week 7 (July 13 - July 17): Extruded bitmap primitive. The EBM solid
    requires the dimensions of the bitmap file (height and width in
    bytes), an extrusion length, and a transformation matrix to position
    the EBM. Each byte in the bitmap file is treated as the base of a
    cell that is extruded by the specified extrusion length.

<!-- -->

-   Week 8 (July 20 - July 24): Code Review and Testing

<!-- -->

-   Week 9 (July 27 - July 31): Phase 2 evaluations

<!-- -->

-   Week 10 (August 3 - August 7): Metaball primitive

<!-- -->

-   Week 11 (August 10 - August 14): Code Review and Testing

<!-- -->

-   Week 12 (August 17 - August 21): Code Review and Testing

<!-- -->

-   Week 13 (August 24 - August 28): Final evaluation and code
    submission