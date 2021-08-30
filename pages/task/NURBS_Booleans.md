Non-Uniform Rational B-Splines are the dominant geometric representation
format in Computer Aided Design. BRL-CAD's support for these primitives
is relatively recent, and while we can raytrace them we are still
developing the ability to perform operations such as subtraction and
intersection between two solid NURBS Boundary Representations (Breps).
This ability is fundamental to a wide variety of editing operations and
essential to the process of converting implicit-primitive based boolean
geometry trees to evaluated NURBS models.

This task would build on work done in previous GSoC projects to make
existing functionality robust and fast.

# References

-   src/libbrep
-   src/librt/primitives/brep
-   src/other/openNURBS
-   include/raytrace.h
-   include/rtgeom.h

<!-- -->

-   [user/Phoenix/GSoc2013/Reports](../user/Phoenix/GSoc2013/Reports.md)

# Requirements

-   Familiarity with C++
-   Solid mathematical foundations
