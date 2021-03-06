Contact "brlcad" on irc.freenode.net

BRL-CAD has one of the oldest and fastest parallel ray tracing
implementations around but we don't currently leverage the GPU. With
implicit geometry and constructive solid geometry (CSG) Boolean
operations, we also have a very different approach to ray tracing that
has its own set of academic challenges.

Currently we use a [Bounding Volume
Hierarchy](wikipedia:Bounding_volume_hierarchy.md) (BVH), an
object partitioning scheme, to reduce the amount of intersections that
we need to compute on the OpenCL librt. The advantage of the BVH is that
it does not compute duplicate intersections, which is typically an issue
with spatial partitioning schemes. This allows us to use less per thread
memory since we do not require the use of mailboxing . But an issue with
the BVH is that it requires computing all the primitive intersections
along the ray path. This is an issue in scenes with high depth
complexity like Goliath or architectural scenes.

This task requires you to write an ANSI C prototype of a new spatial
partitioning acceleration structure for BRL-CAD and to port this
prototype to OpenCL. The complex construction stage can remain in ANSI C
on the CPU. Then the resulting acceleration structure is copied to the
GPU, in this way only the traversal, i.e. intersection stage, needs to
be ported to OpenCL.

The ANSI C librt uses a BSP tree (really a
[Kd-tree](wikipedia:k-d_tree.md)) so that can be used an initial
example. You can also use the PBRT Kd-tree source code as an initial
example. Since we do not want to have duplicate intersections (we have
complex primitives which can take a long time to intersect, also
duplicates would needlessly complicate CSG processing), you would need
to use some kind of Kd-tree hybrid in order to prevent the need for
mailboxing. The issue with mailboxing is that it uses one bit per
primitive in the model per thread. Imagine you have a model with a
million primitives. This would reduce the amount of threads you can have
in-flight (i.e. which can run simultaneously) because of the reduced
cache memory available on a platform like a GPU.

A suitable Kd-tree hybrid which does not compute duplicate intersections
would be either the [Bounding Interval
Hierarchy](wikipedia:Bounding_interval_hierarchy.md) (BIH), or a
Kd-tree which stores the larger primitives in the inner nodes, instead
of only storing primitives at the leaf nodes (like the Kd-tree described
by Choi, et al). Alternatively as a first step, you can simply discard
any primitive intersections which are located outside the current
traversed Kd-tree cell, this will eliminate the need for mailboxing, but
will still require the computation of duplicate intersections, and
perhaps complicate the CSG algorithm.

-   <https://github.com/mmp/pbrt-v3/tree/master/src/accelerators> - PBRT
    source code.
-   <http://grmanet.sogang.ac.kr/ihm/webpapers/1310PG2013.pdf> - Choi's
    Kd-tree presentation.
-   <https://www.highperformancegraphics.net/previous/www_2011/media/Papers/HPG2011_Papers_Wu.pdf> -
    SAH KD-tree construction on GPU.

Difficulty: Hard

Languages: C and OpenCL (or other GPGPU API)
