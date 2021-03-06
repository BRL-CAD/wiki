BRL-CAD currently stores shader information (settings controlling the
visual appearance of a geometric object during raytracing) in attributes
associated with each individual geometric object. This means it is
cumbersome to set up large numbers of individual objects with the same
shader settings and then make a uniform change to all of their settings.

Similarly, information on material density (used by tools such as
rtweight) is currently stored only in text files not associated directly
with the .g database at all or within a binary object in the .g
representing the contents of the text file (for gqa).

This task would be to design and implement first class "objects" in the
.g database format to hold material information and shader information.
So just as there is a sphere type and cone type, the database will have
shader types and material types. Students interested in this topic
should study BRL-CAD's shaders and other shader systems to get an idea
of what sort of information should be represented and how to store it.
Discussion with developers about work done to date would also be a good
idea.

# References

-   include/raytrace.h
-   include/db5.h
-   src/liboptical
-   src/librt

# Requirements

-   Familiarity with C