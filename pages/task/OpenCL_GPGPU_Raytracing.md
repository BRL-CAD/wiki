Contact "brlcad" on irc.freenode.net

BRL-CAD has one of the oldest and fastest parallel ray tracing
implementations around but we don't currently leverage the GPU. With
implicit geometry and constructive solid geometry (CSG) Boolean
operations, we also have a very different approach to ray tracing that
has its own set of academic challenges.

Your project is to help us introduce a GPGPU pipeline into BRL-CAD using
OpenCL. You're welcome to use a library that encapsulates OpenCL. We
have a dozen primitives in BRL-CAD that need to be converted to OpenCL.
Your objective is to implement at least two more while evaluating how
your conversion compares to the non-GPGPU implementation.

One primitive which is done is an arbitrary polyhedron, so you have an
example to follow. These primitives still need to be converted: FASTGEN4
CLINE.

Difficulty: Easy

Languages: C and OpenCL (or other GPGPU API)