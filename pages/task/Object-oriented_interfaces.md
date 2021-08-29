The [Geometry Service Project](../misc/Geometry_Service_Project_Main.md)
aims to restructure the geometry management services within BRL-CAD and
provide a new user interface. As part of these efforts [BRL-CAD's core
C++ interface](../doc/BRL-CAD's_core_C++_interface.md) should become a
self-contained object-oriented interface to BRL-CAD's geometry kernel,
hence the Geometry Engine. With that, the C++ interface would be a
canonical API for external applications, interfaces to other programming
languages, etc.. That's why it is included in the brlcad.dll (and its
SDK): Easy distribution of BRL-CAD functionality to MS Windows programs.

The C++ interface already provides access to the 3 database types
read-only, write-on-change and in-memory. The last one provides the
usual "load -&gt; change -&gt; save" behavior for applications.
Additionally objects for most of the simple primitives and combinations
are included too.

Possible tasks are

-   Implement the C++ core classes for the remaining primitives
-   ...

# References

-   [Geometry Service Project Main](../misc/Geometry_Service_Project_Main.md)
-   [BRL-CAD's core C++ interface](../doc/BRL-CAD's_core_C++_interface.md)
-   /rt^3/trunk/src/coreInterface
-   /rt^3/trunk/include/brlcad

# Requirements

-   Familiarity with C/C++
