BRL-CAD has two optics libraries, LIBOPTICAL and LIBMULTISPECRAL, for
simulating energy transport such as light and other wavelengths. We'd
like to be better at simulating more advanced ray interactions such as a
light ray passing through a prism (birefringent polarizer) that gets
split into component wavelengths or light that passes through a
polarization filter removing high frequency light being reflected off a
shiny surface. In theory, our multispectral optics library can be used
for both purposes since it supports rays representing bundles of
wavelengths.

This task involves performing a review and overhaul of BRL-CAD's
existing multispectral library to make sure it support light ray
polarization. A demonstration of polarizing light along diffraction,
diffusion, or other filtering effects would get added to BRL-CAD's main
ray tracer and enabled as a new lighting mode. Support will likely need
to be added for tracking the angular wavelength property, splitting
diffracted rays, and combining rays.

# References

-   src/libmultispectral
-   src/liboptical
-   src/rt
-   <http://en.wikipedia.org/wiki/Polarizer>
-   <http://en.wikipedia.org/wiki/Photographic_filter>

# Requirements

-   Strong familiarity with C