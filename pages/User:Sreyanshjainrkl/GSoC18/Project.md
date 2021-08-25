## **OpenCL GPGPU Raytracing**

### **Abstract**

BRL-CAD objects are made from about two dozen primitives, ray-tracing of
which can be quickly realised in a GPU owing to its parallel
architecture. There are lot of function calls to see if the shooted ray
is intersecting with the primitive and to check on which direction it
should be reflected. These calls on different data can be effectively
launched on GPU/multi-core CPU if ported into OpenCL to achieve higher
speedups.

### **Methodology**

The project has two parts divided as follows:

-   Accelerating primitives by porting the ray-primitive intersection
    (shot) code from C to OpenCL and provide the glue code which packs
    and unpacks that primitive from the C side to the OpenCL side.
-   Developing BREP support involves serializing the ‘ON_BREP \*’ of
    the primitives and passing it to the GPU and then porting the
    generic ray-BREP intersection code.

### Timeline

Tentative timeline of the project over the summer of 2018.

-   Upto May 14:
    -   Week -2 (30th April - 6th May): Developing HYP shot routine in
        OCL
    -   Week -1 (7th May - 13th May): Accelerating ARBN primitives via
        OCL

<!-- -->

-   May 14 - June 15:
    -   Week 1 (14th May - 20th May): Developing DSP shot routine in OCL
    -   Week 2 (21st May - 27th May): Accelerating PIPE primitives via
        OCL
    -   Week 3 (28th May - 3rd June): Developing METABALL shot routine
        in OCL
    -   Week 4 (4th June - 10th June): Buffer week for finishing pending
        tasks, validating whether it matches the C version, working on
        scope of performance improvement in the OCL codes developed
    -   Week 5 (11th June - 15th June): Phase I evaluation report
        submission

<!-- -->

-   June 16 - July 13:
    -   Week 6 (16th June - 24th June): Code perusal and formulating
        strategies regarding the BREP support
    -   Week 7 (25th June - 1st July): Improve the performance of
        existing OCL codes
    -   Week 8 (2nd July - 8th July): Developing code for BREP support
        in OCL
    -   Week 9 (9th July - 13th July): Phase 2 evaluation report
        submission

<!-- -->

-   July 13 - August 14:
    -   Week 10 (14th July - 22nd July): Porting the generic ray-BREP
        intersection code
    -   Week 11 (23rd July - 29th July): Wrapping up code development
        for BREP support
    -   Week 12 (30th July - 5th Aug): Buffer week to complete pending
        tasks, testing the raytracers for their performance and
        benchmarking it on some real examples
    -   Week 13 (6th Aug - 14th Aug): Final evaluation report submission

### Deliverables

Every shot routines developed in OpenCL also involves verifying and
validating if the OpenCL version matches the C version of it in my
timeline. Once it does, a final patch for that primitive incorporating
the inclusion shall be submitted to integrate the code into the mainline
tree as per the proposed schedule. This shall be executed by
implementing changes in the primitives bit by bit during the bonding
period to get my work authenticated and approved to earn direct commit
rights during the coding period.