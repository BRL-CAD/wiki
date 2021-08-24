<h1>

<b>GPU Boolean Evaluation for CSG Ray-Tracing</b>

</h1>

In BRL-CAD, some work has been done in order to optimize the ray-tracing
process, with ray-intersection calculations implemented in OpenCL for
several primitives, taking advantage of GPGPUs parallel mechanisms to
render scenes in a faster way. I propose to continue the optimization of
the ray-tracing in BRL-CAD, by implementing the CSG Boolean evaluation
on the GPU using OpenCL.

<h4>

<b>Description</b>

</h4>

The CSG Boolean evaluation method in BRL-CAD uses a Boolean weaver
algorithm to create ray partitions from intersection segments, that will
be later evaluated against the CSG tree that represents the CSG object.
I intend to rewrite a similar algorithm in the GPU, by implementing the
main functions used for Boolean evaluation in the file
'src/librt/bool.c', like 'bool_weave', 'bool_eval', 'rt_boolfinal'
and other functions used by these, in OpenCL.

Currently, the CPU code uses dynamic data structures to store the line
segments and the partitions that are used in the Boolean evaluation, and
has some 'goto' statements that are not supported by OpenCL. I will
start by implementing this algorithm with a linked-list data structure
to store the ray partitions on the GPU, using two fixed size buffers to
represent the data structure.

After having a working implementation of the algorithm in OpenCL, I will
add a CSG coherence method to further optimize the algorithm, by taking
advantage of the fact that adjacent rays may intersect the same
primitives in the same order as previous rays, and the Boolean
classification for those rays can be avoided in those situations.

<h4>

<b>Useful Links</b>

</h4>

-   [Project Proposal](https://goo.gl/jNb9H4)
-   ["Depth-order point classification techniques for CSG display
    algorithms", Jansen, Frederik
    W](http://dl.acm.org/citation.cfm?id=99904)
-   ["Concurrent Manipulation of Dynamic Data Structures in OpenCL.",
    Mulder, Henk](https://goo.gl/PdNvOQ)
-   [OpenCL API 1.2 Reference
    Card](https://www.khronos.org/files/opencl-1-2-quick-reference-card.pdf)

<h4>

<b>Deliverables</b>

</h4>

-   Patch to weave intersection segments into partitions in OCL
    (rt_boolweave()).
-   Patch to evaluate partitions over the CSG tree (bool_eval() and
    rt_boolfinal()).
-   Patch to reuse Boolean classification of previous rays by taking
    advantage of CSG coherence.

<h4>

<b>Development Schedule</b>

</h4>

-   <b>Week 1-2:</b> create OCL kernel to perform weaving of segments
    and create data structure to store the ray partitions.
-   <b>Week 3-4:</b> process and weave the segments into partitions in
    the OCL kernel and analyze the partitions created from a simple CSG
    scene / submit patch.
-   <b>Week 5-6:</b> restructure bool_eval() and implement the function
    in OCL.

</li>
<li>

<b>Week 7-8:</b> implement the rt_boolfinal() kernel function and other
needed functions to perform Boolean evaluation in OCL and test with
different CSG scenes/ submit patch.

</li>
<li>

<b>Week 9-10:</b> implement statistics for a CSG coherence method by
creating a list to store order and result of Boolean evaluation of
previous rays.

</li>
<li>

<b>Week 11:</b> compare the intersection order of new rays against the
stored order of previous rays. If the order is the same, read the
Boolean evaluation from the list. Otherwise, calculate the Boolean
classification for the new ray and update the list.

</li>
<li>

<b>Week 12:</b> compare the time efficiency between the CPU-based and
GPU-based Boolean evaluation algorithms / submit patch.

</li>
</ul>
<h4>

<b>Availability</b>

</h4>

During the GSOC period, I am able to dedicate 40-45 hours per week to
the project, as it coincide with the summer break period of my
university. I will not have others ongoing projects and neither planned
vacations for that period, so I intend to fully commit to BRL-CAD from
day 1 to the last day.

<h4>

<b>Why BRL-CAD? Why me?</b>

</h4>

I am looking forward to contribute to the BRL-CAD project because I
always enjoyed 3D modeling and I am familiar with the source code and
documentation of BRL-CAD. Currently working on a master's thesis on
Boolean evaluation for CSG ray-tracing, I believe that I could apply the
knowledge acquired on the BRL-CAD project and speed up the rendering of
CSG scenes.

<h4>

<b>Personal Information</b>

</h4>

<b>Name:</b> Marco da Silva Domingues

<b>Email:</b> marcodomingues20@gmail.com

<b>IRC:</b> mdtwenty

<b>Brief background:</b> I am in the last year of a Computer Science
master degree at Instituto Superior Técnico, University of Lisbon,
Portugal, focused in computer graphics and video games development.