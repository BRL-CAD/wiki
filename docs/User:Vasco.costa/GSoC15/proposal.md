Hello. I am interested in ray-tracing, and GPGPU. I plan to work on
[OpenCL (OCL) acceleration of the BRL-CAD librt rendering
pipeline](User:Vasco.costa/GSoC15/logs.md).

# Project Information

## Links to code or algorithms

-   Lagae, Ares, and Philip Dutré. Compact, "Fast and Robust Grids for
    Ray Tracing." Computer Graphics Forum. Vol. 27. No. 4. Blackwell
    Publishing Ltd, 2008.
-   [3D Object Intersection - Real-Time Rendering
    Resources](http://www.realtimerendering.com/intersections.html).
-   [OpenCL API 1.2 Reference
    Card](https://www.khronos.org/files/opencl-1-2-quick-reference-card.pdf).

## Deliverables

-   M1 - patch with ell and arb8 shot routines in OCL.
-   M2 - patch to refactor dispatcher, shoot, optical renderer to
    process many rays in parallel in C when rendering an image or block.
-   M3 - patch with grid spatial partitioning in OCL.
-   M4 - patch to add GPU side database storage of OCL implemented
    primitives.
-   M5 - patch to port compute intensive or critical parts of the
    dispatcher, boolean evaluation, optical renderer to OCL.
-   M6 - patch with tor and tgc shot routines in OCL.
-   M7 - patch with bot shot routine in OCL.

## Development Schedule

-   1 week - ellipsoid (ell), arb8 (arbitrary polyhedron) shot routines
    in OCL
-   1 week - to refactor dispatcher, shoot, optical renderer to process
    many rays in parallel in C when rendering an image or block
-   3 weeks - grid spatial partitioning in OCL
-   2 weeks - to code for GPU side database storage of OCL implemented
    primitives
-   3 weeks - to port the compute intensive or critical parts of the
    dispatcher, boolean evaluator, optical renderer to OCL
-   1 week - torus (tor), truncated general cone (tgc) shot routines in
    OCL
-   2 weeks - bot (bag o' triangles) shot routine in OCL

Code should be implemented in C and OpenCL. The boolean weaving should
be implemented in the 3 week segment where the boolean evaluator will be
reimplemented in OCL. bot implementation is near the end because it
might be possible to reuse some of the spatial partitioning code in it.

# Why BRL-CAD? Why me?

I chose BRL-CAD because I think it is an important project. We currently
are experiencing a large boom in desktop manufacturing tools such as
lowcost CNC machines and 3D printers. BRL-CAD is one of the few
open-source projects operating in this space. In addition BRL-CAD relies
extensively on computer graphics ray tracing algorithms to perform this
task and I have considerable experience to bring to bear on these
problems. Last but not least I have experience with open source
development, administration, and culture.

# Personal Information

Name: Vasco Alexandre da Silva Costa
Webpage: <http://web.ist.utl.pt/vasco.costa>
IRC username: vasc

## Brief background info

I am a PhD student at Instituto Superior Técnico, University of Lisbon,
Portugal. The background is computer graphics. In particular in the area
of real-time ray tracing on GPGPUs. At one time I was a project
maintainer of Freeciv (an open source real-time strategy game). Before
the maintainer post I was a developer. I coded a graphic game client,
improved the TCP/IP networking, and the game rule inference engine
processing.
