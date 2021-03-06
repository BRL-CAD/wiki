One of the most common uses of BRL-CAD is to convert geometry from one
format to another. This is a task all CAD systems must perform, and
often one of the more difficult. BRL-CAD has a wide variety of
converters, both import and export, that are coded as stand-alone tools.

Many of the geometry conversion tools share the same or very similar
code - src/conv is the of the hot-spots for removing duplicate code in
BRL-CAD. (Duplicated code is an unnecessary maintenance burden, as a
problem in one instance must be fixed in all). This project would work
on a conversion library (LIBGCV) that provides a clean API for
converting to and from different formats.

Geometry conversion is an immense topic, so a student proposal should
concentrate on the design of the library rather than the details of each
individual format, using just a few formats as focuses for initial
development. The library design should allow formats to be added to the
library as plugins. Students submitting proposals for this topic should
discuss it beforehand with developers via IRC or email.

# References

-   src/conv
    -   dozens of importers and exporters in here, most are one .c file
        per converter
    -   the more complex converters are in subdirectories
-   src/libgcv
    -   this is a placeholder for the new awesomeness, each converter
        should be an input/output plugin to the library

# Requirements

-   Familiarity with C/C++
-   Familiarity with file parsing issues (lex/yacc a plus)
-   Basic understanding of geometry information (will be needed for
    understanding conversion issues)