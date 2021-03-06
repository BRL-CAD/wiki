BRL-CAD has a number of image processing tools used (among other things)
to post-process raytrace images. The rtwizard application is an example
of an interface that ties together multiple image processing tools
(under the hood) providing a useful compositing interface for users.
Another common task is simple image conversion.

Originally, all image conversion functionality in BRL-CAD was handled by
individual tools. Currently, an effort is underway to migrate image
manipulation logic into library code (LIBICV) and have existing tools
call the new library.

This task would complete work already begun on bu_image and the image
conversion library (LIBICV), and convert all existing image conversion
tools to use the new API. Correctness and robustness testing should be
part of the process (what happens when converting very large images, for
example?)

The short version is to beef up bu_image and make all the image tools
go through libicv.

# References

-   src/libicv
-   src/libbu/image.c
-   include/bu.h
-   src/util
    -   there are 100+ image conversion utilities in here

# Requirements

-   Familiarity with C