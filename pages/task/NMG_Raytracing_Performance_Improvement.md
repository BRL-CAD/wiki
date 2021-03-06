BRL-CAD uses two primary primitive types to represent mesh data -
N-Manifold Geometry (nmg) and Bags of Triangles (BoTs). In principle,
all planar nmg surfaces can gracefully downgrade to a BoT representation
without introducing geometric changes to surfaces (indeed, this should
be VERY straightforward, but a few bugs remain in BRL-CAD's
implementation of that process.)

Recent work on raytracing of BoT models has yielded significant
speed-ups for complex models, and BoT raytracing has always been faster
than direct raytracing of nmg data. There are implementation issues with
nmg raytracing, but an interesting alternative to directly raytracing
nmg primitives would be to raytrace their BoT conversion. The actual
raytracing code does not require the topological sophistication of the
nmg representation (that's used elsewhere) so results should be
identical to within floating point noise. This would allow one common
raytracing code for nmg and bot primitives, simplifying the code and
making improvements more general.

This task would involve extensive testing of nmg-&gt;bot conversion
logic, setting up methods to allow the raytracer to work on a BoT
representation of the nmg (need to consider approaches - can the
raytracer call the nmg-&gt;bot routine on a per surface basis on the
fly, does it need to pre-generate the whole bot, etc). It may very well
be that the project would find fixing direct nmg raytracing is the best
option for performance improvement, in which case the task would be to
make those fixes.

# References

-   src/librt/primitives/nmg
-   rt
    -   our main raytracer, renders pictures
-   db
    -   lots of sample geometry
-   mged 'facetize' command
    -   useful for turning any geometry into NMG representation

# Requirements

-   Familiarity with C
-   Good debugging/troubleshooting skills