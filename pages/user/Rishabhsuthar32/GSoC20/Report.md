# Project Report

## Project Plan

BRL-CAD has one of the oldest and fastest parallel ray tracing
implementations around but it doesn't currently leverage the GPU very
much. With implicit geometry and constructive solid geometry (CSG)
Boolean operations, it also has a very different approach to ray tracing
that has its own set of academic challenges.

The project here was to introduce a GPGPU pipeline into BRL-CAD using
OpenCL for existing primitives and parallelize them for faster
computation compared to the non-GPGPU implementation.

Some of the primitives that were planned to be converted in this 2020
season of Google Summer of Code are polyhedron with an arbitrary number
(ARBN), FASTGEN4 CLINE, hyperboloids of one sheet (HYP), etc.

## Patches Submitted

Following patches include modifications for better functioning and
resolution of bugs encountered while rendering via OpenCL in MGED
terminal.

-   OpenCL_CMAKE: <https://sourceforge.net/p/brlcad/patches/549/>
-   OpenCL rendering bug:
    <https://sourceforge.net/p/brlcad/patches/551/>

Following are the patches submitted for OpenCL versions of some of the
primitives.

-   CLINE: <https://sourceforge.net/p/brlcad/patches/541/>
-   ARBN: <https://sourceforge.net/p/brlcad/patches/543/>
-   PIPE: <https://sourceforge.net/p/brlcad/patches/545/>
-   VOL: <https://sourceforge.net/p/brlcad/patches/547/>
-   METABALL: <https://sourceforge.net/p/brlcad/patches/548/>
-   HYP: <https://sourceforge.net/p/brlcad/patches/553/>

## Performance

We shall take the example of HYP primitive here for comparing the
performance of C and OpenCL versions of rendering.
![](img/Hyp2_c.png)![](img/Hyp2_cl.png)
**First Test**: Both the C and OpenCL renderings should look same

On the left is the C rendering of the HYP primitive and on the right is
its counterpart rendered after enabling OpenCL. Well, on first look,
they do look same. First test passed!

**Second Test**: The performance of the OpenCL version should be much
better than the C version

So, let's compare the time displayed in their rendering logs now. While
the time taken by the C version to render was 0.31 seconds, the time
taken by the OpenCL version to render was 0.02 seconds. That is more
than **15x improvement** in the performance! Hurray!

![](img/Hyp_pixdiff.png)

**Third Test**: Checking the difference between images at a pixel level

Using the pixdiff and pix-png command of BRL-CAD, a pixdiff image shown
on the right was created. The image shows where the colour values differ
by more than 1 value in one or more of the RGB channels. Most of the
pixels are offset in intensity by just a little bit, which implies some
calculation is just slightly off. However, the hits and misses appears
to be correct.

**Fourth Test**: To confirm the hits are identical

On comparing the nirt shotline in both the renderings, the hits were
found to be identical, which implies the mismatch in intensity found in
above test is a normal issue.

## To Do List

-   **Memory Allocation** : One of the major challenges I faced was
    finding the OpenCL counterpart of bu_malloc which works fine while
    passing the variables from .c to .cl file. While I tried with malloc
    as is used normally in C programs, it apparently didn't work. The
    renderings were simply not occurring in the OpenCL version. Hence,
    the HYP and SUPERELL primitives, which didn't use the bu_malloc
    command, rendered easily while others didn't. The patches submitted
    above have no compilation or computation error. If the memory
    allocation thing works, they'd render just as fine.

<!-- -->

-   **Using Printf statement**: Another issue where I got stuck was
    being unable to use printf statement in OpenCL files. The strategy
    to debug opencl kernels using printf is to enable printf command by
    passing enumerations stated below in an array of context properties
    to the function, clCreateContext, which creates opencl context as
    follows:

<!-- -->

    CL_PRINTF_CALLBACK_ARM    0x40B0
    CL_PRINTF_BUFFERSIZE_ARM  0x40B1
    cl_context_properties context_properties[] =
    {
     CL_PRINTF_CALLBACK_ARM, (cl_context_properties)printf_callback,
     CL_PRINTF_BUFFERSIZE_ARM, (cl_context_properties)0x100000,
     CL_CONTEXT_PLATFORM, (cl_context_properties)platform,
     0
    };

This enables the device side printf built in function for OpenCL C
versions prior to 1.2. It also extends the cl_context_properties
enumeration to allow a user defined printf callback and/or printf buffer
size. OpenCL kernel code then has access to:

` #pragma OPENCL EXTENSION cl_arm_printf : enable`

This pragma must be enabled for a kernel to have access to the printf
built in function in OpenCL C versions prior to 1.2.

For the purpose of debugging in mged I used bu_log instead of printf by
passing following array of context properties

    cl_context_properties context_properties[] =
    {
     CL_PRINTF_CALLBACK_ARM, (cl_context_properties)bu_log,
     CL_PRINTF_BUFFERSIZE_ARM, (cl_context_properties)0x100000,
     CL_CONTEXT_PLATFORM, (cl_context_properties)platform,
     0
    };

But unfortunately this doesn't work and reports error that context
cannot be created. This needs further investigation. The print statement
would also be useful for debugging the memory allocation issue, as to
where and why it is failing.

## References

-   **Project Plan**: [Project](Project.md)
-   **Development Logs**: [Log](Log.md)
