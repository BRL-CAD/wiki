STEP is the current standard for exchange of CAD data between different
software packages. BRL-CAD makes use of the STEPcode libraries to
support its step-g converter, but the converter is still in its infancy.

The current importer focuses on AP203 import, and needs to support a
large number of data types:

-   -   Surfaces that are stored individually without Brep
        superstructure (see, for example, the wing shapes generated by
        OpenVSP: <http://www.openvsp.org/wiki/doku.php?id=step>) Even
        though these are not proper "solids" in the BRL-CAD sense of the
        term, we can and should import them - if nothing else, we can
        create one Brep object per surface and then develop
        post-processing tools to "stitch" the surfaces into a solid.
    -   Isolated curves can be brought in as part of sketch primitives.
    -   Polygonal data
    -   Unorganized triangle mesh data
    -   Metadata (in many cases can be mapped to attributes, worst case
        perhaps store as binary objects...)
    -   etc.

Right now our importer is AP203 only - we are also interested in
AP203e2, AP214, and AP242.

# References

-   src/conv/step
    -   this is where the current step-g importers and exporters resides
-   src/other/step
    -   this is STEPcode

<!-- -->

-   Recommended Practices for AP203
    -   <http://www.steptools.com/support/stdev_docs/express/ap203/recprac203v8.pdf>
-   Usage Guide for the STEP PDM Schema V1.2
    -   <http://www.steptools.com/support/stdev_docs/express/pdm/pdmug_release4_3.pdf>

# Requirements

-   Familiarity with C++