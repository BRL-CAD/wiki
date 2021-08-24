# GPGPU Support for Boolean Evaluation

**Name:** Param Hanji

**Email:** param.catchchaos@gmail.com, param.hanji.2015@ieee.org

**IRC Handle:** catchchaos

## Background

I’m a second year undergraduate student at the National Institute of
Technology, Karnataka, pursuing a degree from The Department of
Information Technology. I recently started getting myself involved in
the wonderful world of open source and am looking to use this
opportunity to really immerse myself in it. An AI enthusiast at heart,
I’ve been teaching myself GPU programming in my freetime.

## Project Information

### Description

BRL-CAD has an excellent parallel Ray Tracing implementation, but use of
the GPU to achieve it was introduced by Jon Engbert and then, recently
developed by Vasco Alexandre da Silva Costa during GSOC 15. The purpose
of this project is to build on this and introduce GPU parallelism for
Constructive Solid Geometry (CSG) boolean operations. Existing GPU
implementations are in OpenCL and I will continue to use the same due to
its similarity to C (extension of C99), platform independence and
extensive documentation.

Currently, OpenCL support exists only for a handful of primitives. My
project will start by accelerating a few more (such as eto, hrt, part
etc.) to get used to the existing codebase and give me time to learn
more about ray tracing and CSG. Also the code has a few bugs as it is
relatively new. Constantly looking for and fixing these bugs will also
improve OpenCL support.

The next part of the project involves looking at the code responsible
for boolean evaluation (largely in librt/bool.c) and identifying the
functions that can and should be parallelized, including but not limited
to rt_bool_eval, rt_boolweave, rt_boolfinal and others. Currently,
they cannot be ported to OpenCL directly because of the presence of
structure pointers, linked lists, goto statements and dynamic allocation
of memory, features which are simply absent in OpenCL.

The boolean weave function used by BRL-CAD accepts lists of segments and
partitions as input. These are internally stored as doubly linked lists.
However, only arrays can be passed to OpenCL kernel functions. Several
operations including traversing the lists, inserting at the front and
back, deleting elements, etc. need to be altered if these lists are to
be replaced with arrays. Also, several structures need to be redefined
inside the OpenCL file so that they can be received and instantiated.
Parallelizing weave can start with bool_weave0(), which is a special
case of boolweave(), with similar inputs and similar operations, without
the extensive branching that is present in the latter. Several macros
used in both the functions like GET_PT_INIT, BU_LIST_FIRST,
BU_LIST_DEQUEUE, INSERT_PT need to be either rewritten or eliminated.

Function boolfinal() uses gotos in its body. The first step will be to
restructure the code to get rid of the goto statements. Very much like
weave, this function too extensively uses linked lists. Again, the task
is to represent all the relevant information in the form of arrays to be
used by OpenCL. Boolfinal() is called by other functions in shoot.c and
bundle.c. Once .cl file is generated, it needs to be linked, compiled
and, run from these files, if and when OpenCL is detected on a
particular system (much like it is done with the primitives currently).

Before doing that, miscellaneous functions like bool_eval(),
partition_eligible(), bool_equal_overlap_tables() etc. That are used
by boolfinal() need to be re-written in OpenCL. Some of these require a
little more effort than others. For example, bool_eval() has a number
of goto statements, while rt_bool_growstack() performs dynamic memory
allocation. The report linked below\[1\] maybe could be of help for the
memory allocation. Otherwise, other options need to be explored.

### Useful Links

-   Roy Spliet, “A comprehensive study of Dynamic Memory Management in
    OpenCL kernels”, Master thesis report, Delft University of
    Technology, June 5th, 2013
-   <http://www.scratchapixel.com/lessons/3d-basic-rendering/get-started>

### Deliverables

-   Patch containing .cl files for accelerating some primitives(eto,
    hrt)
-   Patch introducing OpenCL support to rt_boolweave()
-   Patch to extend OpenCl support for rt_boolfinal() by including
    rt_boolfinal() as well
-   Patch to complete bool.c OpenCL implementation by including other
    miscellaneous functions

### Brief Timeline

-   **Community Bonding Period:** Learn up about general ray tracing
    concepts and CSG. Get a working knowledge of the various custom
    BRL-CAD structures (seg, partition, soltab, rt_i, region to name a
    few) relevant to boolean evaluation. Also enhance current knowledge
    of OpenCL with the intention of applying it to this project - like
    dynamic allocation, representation of structure pointers etc.
    Lastly, thoroughly read HACKING plain text file in the root folder
    of BRL-CAD.

<!-- -->

-   **Week 1:** Accelerate 1 among eto, hrt, part (or some other
    primitive) to learn codebase. Also, read up about how to represent
    relevant data as arrays for bool.c functions.

<!-- -->

-   **Week 2:** Complete acceleration of 1 or 2 more primitives. Submit
    patches incorporating the inclusion.

<!-- -->

-   **Week 3:** Start work on boolweave(). A good starting point is
    bool_weave0() as it is a simpler function, yet quite similar. In
    the meanwhile, profile the code to decide which functions need to be
    parallelized.

<!-- -->

-   **Week 4:** Finish up generating OpenCL code for weave and submit a
    patch.

<!-- -->

-   **Week 5:** Restructure bool_eval() to get rid of the goto
    statements and decide how to perform dynamic memory allocation for
    rt_bool_growstack().

<!-- -->

-   **Week 6:** Complete OpenCL implementations of the 2 functions.
    Also, profile the code to check for any other functions which need
    special attention.

<!-- -->

-   **Week 7:** Buffer week to finish any pending tasks. Test the code
    to make sure it works as required.

<!-- -->

-   **Week 8:** Start work on boolfinal() by eliminating goto statements
    and redefining macros.

<!-- -->

-   **Week 9:** Based on the earlier learning (for boolweave()),
    restructure the data to be processed as arrays instead of doubly
    linked lists.

<!-- -->

-   **Week 10:** Finish up accelerating boolfinal() and test it to
    ensure the new code works well with the rest of BRL-CAD code.

<!-- -->

-   **Weeks 11 & 12:** Compare the OpenCL code against the serial
    version. Check and measure the performance increase obtained. See
    how it matches up with the theoretical estimate. Perform code clean
    up as well.

### Availability

My exams will get over in April. Hence, I might be a little inactive
during the beginning of the community bonding period. I'm free and
willing to put in 45-50 hour shifts (or more if needed) during the
summer. I have vacations from the end of April to late July, which fits
in nicely with GSOC timeline. Even after that, my first month of college
is bound to be less stressful and I'll have plenty of time to work on
this project. I'm extremely flexible with timings and am willing to
adjust to my mentor's schedule if required. The only period of
inactivity would be a week long vacation sometime in late April.

### Why BRL-CAD?

I first came across BRL-CAD when I was looking for GPGPU projects using
OpenCL. I then started interacting with the community which I found
really interactive and welcoming. My lack of computer graphics concepts
was overlooked and I was directed to relevant resources whenever I
required any. I submitted my first ever patch with BRL-CAD! The
documentation for BRL-CAD is also extensive and helpful. I'm looking
forward to continue my open source experience with BRL-CAD and have
listed it as my one and only choice of organization for GSOC '16. I've
learned a lot in such a short period and am looking forward to continue
doing so.

### Why Me?

I learned that a 20-25% performance improvement can be achieved using
OpenCL for Boolean evaluation, which is significant. I've spent the last
couple of weeks making a patch, getting familiar with the code and will
continue to do so. My patch to accelerate epa was recently accepted. I'm
also working on two other projects for my course in OpenCL on prime
number generation and FFT.

The project on prime number generation is still being formulated. The
basic idea is to implement the Sieve of Eratosthenes algorithm in a
parallel manner. With a small set of predefined primes (less than 100),
we hope to recursively call the function and assign the task of
“crossing-off” multiples of a single prime to a single GPU. This will be
written in OpenCL, using the PyOpenCL API within the next couple of
weeks. The parallel implementation of Cooley-Tukey algorithm for FFT is
almost complete and due for submission in a week.

I believe that I will be well equipped to tackle this project right in
time for the start of the GSoC coding period. I've been constantly in
touch with members of the community and will continue to do so. I'd love
to use this opportunity to really start development with the core
BRL-CAD team.