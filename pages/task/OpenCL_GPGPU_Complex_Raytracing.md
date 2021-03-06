Contact "brlcad" on irc.freenode.net

BRL-CAD has one of the oldest and fastest parallel ray tracing
implementations around but we don't currently leverage the GPU. With
implicit geometry and constructive solid geometry (CSG) Boolean
operations, we also have a very different approach to ray tracing that
has its own set of academic challenges.

Your project is to help us introduce a GPGPU pipeline into BRL-CAD using
OpenCL. You're welcome to use a library that encapsulates OpenCL. We
have a dozen primitives in BRL-CAD that need to be converted to OpenCL.
One of them which is done is an arbitrary polyhedron, so you have an
example to follow. Your objective is to implement at least two more
while evaluating how your conversion compares to the non-GPGPU
implementation.

These complex primitives still need to be converted: pipe, displacement
map, metaball, and 3-D volume (also similar to displacement map).

The bot (Bag Of Triangles) primitive i.e. triangle mesh also needs plate
mode support. i.e. triangles with thickness. In addition the current
ray-triangle intersection algorithm needs to be replaced with an
algorithm which is watertight. This might either be the algorithm in the
ANSI C backend or perhaps the one below.

-   <http://jcgt.org/published/0002/01/05/> - Watertight Ray/Triangle
    Intersection.

Difficulty: Medium

Languages: C and OpenCL (or other GPGPU API)