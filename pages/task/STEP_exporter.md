STEP is the current standard for exchange of CAD data between different
software packages. BRL-CAD makes use of the STEPcode libraries to
support import and export of STEP files, but STEP is a very large
standard and there is a lot of additional work to be done.

For this project, there's a lot of directions that can be taken:

-   We usually export Brep geometry since that is what AP203 supports,
    but newer STEP standards (AP214, AP242) also support a number of
    geometric primitives. We also don't currently support exporting mesh
    geometry (triangle or polygon based) and that's something we need to
    support, even if STEP isn't really a traditional container for
    triangle meshes.

<!-- -->

-   We don't do much about trying to preserve our attribute metadata
    currently - explore what options are available for doing so.

<!-- -->

-   Undoubtedly many more possibilities.

The relevant standards are: AP203, AP203e2, AP214, and the
in-development AP242. A number of useful resources are listed below.

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