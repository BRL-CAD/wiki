BRL-CAD's shader system is custom developed for the librt raytracer.
Shaders are currently coded in C and explicitly added to the active
shader list. A question of interest is whether we can utilize work being
done for other open source raytracing shader systems to improve the
flexibility of BRL-CAD's shader system and take advantage of shaders
developed for other systems.

A proposal should outline what changes are proposed to BRL-CAD's current
shaders. Initial stages would involve either writing the shader bridge
in liboptical or designing a new approach (remember though, all existing
shader functionality in the current system must be preserved, even if it
is re-implemented in some fashion. Be careful about biting off more than
you can achieve in a summer.)

# References

This task will require a fair bit of background research in order to put
together a compelling proposal - interested students should study
BRL-CAD's shader system to determine how it works, and then look at
other open source, license compatible systems to see what they may
offer. Candidates include:

-   <http://en.wikipedia.org/wiki/Shading>
-   <http://en.wikipedia.org/wiki/Shader>
-   <http://en.wikipedia.org/wiki/Shading_language>
-   Sony's Open Shader Language (OSL):
    <http://opensource.imageworks.com/?p=osl>
-   Pixie: <http://www.renderpixie.com/>
-   Yafaray: <http://www.yafaray.org/>

OSL is of particular interest because it is developed specifically for
raytracing systems.

Code of relevance:

-   src/liboptical
-   include/optical.h

Documentation of relevance:

-   -   Do lessons 1-7 minimum

-   -   Read Appendix B

-   -   Provides a broad survey from a developer's perspective

# Requirements

-   Familiarity with C/C++

# Past Efforts

[GSoC11](../user/Kunigami/GSoc2011/Proposal.md)
