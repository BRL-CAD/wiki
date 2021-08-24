Hello. I am interested in ray-tracing, and GPGPU. I work on the [OpenCL
acceleration of the BRL-CAD librt rendering
pipeline](User:Vasco.costa/GSoC15/logs "wikilink"):

-   [GSoC 2015
    Abstract](https://www.google-melange.com/gsoc/project/details/google/gsoc2015/vasc/5657382461898752)
-   [GSoC 2015 Project
    Proposal](User:vasco.costa/GSoC15/proposal "wikilink")
-   [GSoC 2015 Development
    Logs](User:vasco.costa/GSoC15/logs "wikilink")

# OCL librt TODO

-   Split `struct hit` in common.cl into two structs. One for `shot()`
    results and another for `norm()` results. This will reduce the
    amount of memory used to store temporary results between stages.
-   Execute prefix sums and reductions in `clt_frame()` on the device to
    eliminate round-trips.
-   Refactor code so single-hit and multi-hit don't require recompiling
    all the sources twice.
-   Cache the compiled binaries so things aren't recompiled on every
    launch.
-   Quadrics Primitives: HYP, SUPERELL.
-   Grids Primitives: **DSP**, <s>EBM</s>, VOL.
-   Composite Primitives: **PIPE**, **NMG**, METABALL, EXTRUDE, REVOLVE.
-   Instancing Primitive: SUBMODEL.
-   Make Phong shader results look 100% similar to ANSI C librt.
-   Support lights in the shader.
-   Don't intersect primitives twice. This requires a dynamic memory
    allocator.
-   Smarter kernel scheduling for reduce thread divergence. For example
    coallesce all the quadric intersections.
-   Spatial partitioning (perhaps a hybrid Kd-tree) in order to have
    early exit on scenes with high depth complexity.
-   UV routines for all OCL implemented primitives.
-   BREP support.
-   BOT plate mode.
-   FASTGEN support (both CLINE primitive and bool.cl code).

Deprecated primitives:

-   ARS is converted to BOT.
-   HF is converted to DSP.

# OCL librt Development Status

-   Refactored dispatcher, shoot, optical renderer to process many rays
    in parallel when rendering an image or block.
-   HLBVH object partitioning builder in C. traversal in OCL.
-   GPU side database storage of OCL implemented primitives.
-   Ported compute intensive or critical parts of the dispatcher,
    boolean evaluation, optical renderer to OCL.
-   OCL dispatcher that performs the shot routines for a whole frame.
-   OCL rasterizer that does the pixel pushing for a whole frame.
-   OCL lighting modes: Phong, Diffuse, Surface Normals.
-   OCL lighting modes: Multi-hit transparent (Single Stage Render
    Pipeline only).
-   ARB8, EBM, EHY, ELL, EPA, ETO, PART, REC, RHC, RPC, SPH, TGC, TOR
    shot routines in OCL.
-   Surface normal routines for all OCL implemented primitives.
-   CPU HLBVH BOT shot construction with OCL traversal and interpolated
    per pixel normals.