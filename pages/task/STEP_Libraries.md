STEP is the current standard for exchange of CAD data between different
software packages. BRL-CAD makes use of the NIST STEP Class Libraries
code to support its step-g converter, but this source code was written
before many current C++ standard practices and libraries were finalized.
As a consequence, it needs both cleanup and performance enhancements.

For this project, a student should examine the existing STEPcode repo at
<https://github.com/stepcode/stepcode> and create a list of tasks that
need to be done in order to modernize the C++, improve library
performance, improve code maintainability, and better document the STEP
libraries. BRL-CAD's step-g converter will serve as a test for the
functionality of the library.

Specific items to remember:

-   The libraries should compile with strict compiler flags, as used in
    recent BRL-CAD compilations.
-   Large files need to be handled quickly, so performance is
    important - this could be as simple as modernizing string handling,
    but if there are more fundamental issues they will need to be
    addressed as well.
-   BRL-CAD makes use of the doxygen system for source code
    documentation, so organizing source code documentation in the step
    libraries to work well with doxygen should be part of the review and
    updating process.

Improving this library is a good project for students looking for a
geometry related project with potential impact beyond BRL-CAD - other
open source geometry projects are also likely to be interested in STEP
conversion.

# References

-   src/other/step
-   src/conv/step

# Requirements

-   Familiarity with C++
    -   will need to be able to both understand older C++ and how to
        utilize "modern" STL containers