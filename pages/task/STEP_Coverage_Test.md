STEP is the current standard for exchange of CAD data between different
software packages. BRL-CAD makes use of the STEPcode project to
implement its step-g importer, but there is a lot of work to fully
implement the STEP standard. We need test infrastructure.

For this project, you'll create a program that links against STEPcode
and generates a STEP output instantiating every entity for a given
schema (e.g., AP203, AP214, or AP242). It'd provide a good example of
exporting via SDAI and of course a great test file for import.

BRL-CAD's step-g converter will serve as a test harness for the data
file being produced by your program.

# References

-   src/other/step
-   src/conv/step

# Requirements

-   Familiarity with being able to link against a 3rd party C/C++ API