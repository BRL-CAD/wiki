BRL-CAD has a very simple LIBPKG network "package" library used for
transmitting data across the network. It's a rudimentary client-server
based protocol intended to integrate with applications that have
low-level direct socket management. The library is used by BRL-CAD's
geometry editors, framebuffer processing tools, and more. The library,
however, assumes minimal embedded use and uses globals for data access.

This task involves performing a variety of extensions and enhancements
to LIBPKG to make it easier to use and to ensure it's working optimally.
The first task would be to implement a minimal testing framework to make
sure any changes made do not break functionality. Included in those
tests should be performance metrics from tests to characterize how the
library performs with different packet sizes being passed (small to
increasingly larger packets). With testing in place, tasks remaining
would be to investigate and fix any performance bottlenecks and to
eliminate the assumption of globals in the API by adding user callbacks.

# References

-   src/libpkg
-   include/pkg.h
-   src/gtools/gtransfer.c

# Requirements

-   Familiarity with C
-   Strong familiarity with networking
-   Basic familiarity with unit and integration testing