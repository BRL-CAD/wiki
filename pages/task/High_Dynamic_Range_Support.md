There is no fundamental reason the BRL-CAD raytracer cannot produce High
Dynamic Range output, but it currently does not do so and BRL-CAD's
image tools do not support it.

This task would involve:

1.  Investigating the OpenEXR image file format for suitability for use
    in BRL-CAD
2.  Identify BRL-CAD libraries and tools that would need to be enhanced
    (either to support OpenEXR or some other format)
3.  Allow BRL-CAD raytracing to generate HDRI output
4.  Allow BRL-CAD image editing and display tools to work with HDRI
    output

The end product should be an enhanced raytracer and toolchain that can
produce and handle HDRI images.

# References

-   <http://en.wikipedia.org/wiki/High-dynamic-range_imaging>

<!-- -->

-   src/rt
    -   most of our raytracers reside in here
-   src/liboptical
    -   where optics are calculated during raytracing
-   src/util
    -   tons of image converters

# Requirements

-   Strong familiarity with C and C++
-   Understanding of issues related to HDR images and conversions