# Personal Information

|                   |                    |
|-------------------|--------------------|
| **Name**          | Michał Jagielski   |
| **Email Address** | <d3rvan@gmail.com> |
| **IRC(nick)**     | drv                |
| **Time Zone**     | UTC +0100          |

## Brief Background

I'm second year student in Computer Science from University of Wroclaw.
What's about my knowledge... I know Linux and other UNIX-like systems
quite good. Mainly I write in C/C++ but I also like functional languages
(Haskell, OCaml). Lately I'm interested primarily in GPGPU and I have
some experience with it ( for example, I'm writing Rubik Cube optimal
solver on CUDA). I preferred CUDA but I had also some practice with
OpenCL.

# Project Information

## Project Title

OpenCL GPGPU Raytracing

## Brief summary of Project

BRL-CAD objects are made from about two dozens of primitives. During
work they are displayed usually as wireframes, but from time to time we
want to get better image (more reallistic, bigger etc.) Raytracing for
most of primitives is implemented only on CPU. GPU is definetely better
for this task, because of parallel nature of this problem (there is a
lot of rays shooted from camera). Shooted rays are checked to intersect
with primitives from project. There is a lot of calls functions which
check if a ray is intersecting with primitive and on witch direction it
should be reflected. If there is a lot of same function calls with a
little different input data, it's best place to use GPGPU, whitch offer
great performance increase in this type of computations.

When GPU is not accessible on computer OpenCL also will be fast, because
it can be launched on multi-core CPU.

## Project Description (Detailed)

### Primitives

Some of primitives have easy to compute intersection function, but some
of them cam be really weird - for example bended pipe. I will start
generally from easiest to implement primitives. Some of primitives is
rarely used so I postpone implementing it. In my 12-week plan I also not
mentioned 2d-derived primitives, because I can't risk that I won't
finish my task on time. If I will manage to implement all of inscribed
primitives before deadline I will start implementing also 2d-derived
primitives, but if not - I will implement it after GSoC.

### Something about files

In BRL-CAD each primitive have their own raytracing function. There
exist only one example of OpenCL raytracer in special OpenCL branch of
BRL-CAD - sph primitive raytracing is written in OpenCL. It will be my
starting point. So on first place I will write raytracer for all ell.
Because CL-related functions will be used in every primitive, I will
also use separate file with functions like device finding, kernel
loading, parameters setting etc.

I will work on branch available in
<http://svn.code.sf.net/p/brlcad/code/brlcad/branches/opencl/> there
also is sph raytrace example:
<http://svn.code.sf.net/p/brlcad/code/brlcad/branches/opencl/src/librt/primitives/sph/>
. After I complete a project every primitive should have file structure
as sph.

### Algorithm

I think that there is no too much to talk about algorithm, I will try
generally rewrite C algorithms in more efficient OpenCL algorithm.
Algorithm for every primitive is described with desired amount of
details in name_of_primitive.c almost on beginning. I think it's
unnecessary to paste it here. Only thing that should be said is that in
isolated GPU environment it may be not possible or simple not
recommended to call other functions so I will try to oust this calls.
What is more GPU kernels should be light, what may imply some next
changes. It's not necessary, but it may have great impact on performance
of raytracing.

### Computing device

As I said OpenCL can also be launched on CPU so of course I will check
if GPU device is accessible and if not, launch raytracer kernel on CPU.
This task will be realized as I mentioned in files common to all
primitives.

### Deliverables

Great speedup of scenes raytracing in BRL-CAD. For this moment it's not
too fast (despite of using all threads).

## Working Schedule

### upto May 19 (Getting started)

-   Exploring the code.
-   Completing BRL-CAD tutorial for contributors.
-   Fixing at least 1-2 bugs to get familiar with devlopment system.
-   Deeper understanding of BRL-CAD usage (for example completing user
    tutorial)
-   Preparing set of function used to kernel launching. I suppose, that
    should be new file with:
    -   CL device selecting
    -   Kernel reading and loading to memory
    -   context managment

### May 19 - August 4 (Development)

1.  week - rt_ell_shot OpenCL kernel. Of course I will have library to
    handle OpenCL calls so it should be useful in same week.
2.  week - rhc and rpc ray shooting kernels.
3.  week - start of rt_tgc_shoot kernel (and 4 other primitives, that
    are special cases of tgc: rcc, rec,tec,trc). This primitive could be
    hard to implement (for example it contains some external functions)
    so I think I should reserve more time to it. First of all I will
    implement external functions, then rest of algorithm.
4.  week - finishing rt_tgc_shoot.
5.  week - ehy and epa primitives (It should be relatively easy to
    write). In this week I will have final exams, so I must have a
    little more time.
6.  week - Raytracing of torus of two kinds: tor and eto primitive. I
    should also start arbn raytracing - it seems to be easy.
7.  week - finishing arbn and start of bot raytracing.
8.  week - Starting first of more complicated raytracing: part
    primitive. It's more complicated than earlier - for example it uses
    lists (implementation of lists on GPU is non-trivial problem).
9.  week - I will finish particle raytracing. As I said earlier,
    raytracing algorithm of part is much longer than others, but I'm
    hoping that I will end before end of week and I will start most
    complicated to raytracing primitive - pipe.
10. week - Pipe raytracing - it should be most difficult in my project,
    because pipe have really complicated structure and lot of auxiliary
    functions. I Think I will end it in this week or on first few days
    of next week.

### August 4 - August 18 (Finalising)

-   During these two weeks I will test once more raytracers and
    benchmark it on some real examples.
-   Final code submission with Google.

## Time Availability

-   During summer holidays (after about 21st June) I will be completly
    free
-   Usually I will spend 40-45 hours/week on coding. In first month it
    \*may\* be little less (but over 32 hours). I can devote up to 60
    hrs/week in special cases.
-   In 16th June - 19th June I have some final exams. Probably I will
    have little less time in this week, but I will make up for this
    time.
-   Before 16th June I have university courses, but I specially take
    only three in this semester to participate in GSoC.

## Why BRL-CAD?

As I wrote before I like GPGPU and you need somebody to speedup some
part of your program. What is more, I know how expensive can be CAD
software and I think that this initiative (BRL-CAD) is really important
- I'm definetely votary of Open Source. After I worked with mged and
archer few times I've got a certainty that it's great program and I will
help to develop it.

## Why you?

I'm good in C/C++ coding and GPU programming. Also I think that I have a
quite good understanding of GPU architecture, what may be useful in
rewriting algorithms. In addition to that I'm really hard working and
stubborn when I want to reach some target. I think this project is quite
mached to my skills and interest so BRL-CAD can be noticeable beter
thanks to mine work. Furthermore I always want to participate in any
open source community so I will stay with you after GSoC ends.

# Patch

Already I've written only one patch, about RHC volume calculating and
integrating it with mged "analyze" command. Patch is aviable here:
<http://sourceforge.net/p/brlcad/patches/266> I'm planning next patch to
be related to OpenCL branch.