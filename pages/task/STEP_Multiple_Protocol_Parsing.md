STEP is the current standard for exchange of CAD data between different
software packages. BRL-CAD makes use of the STEPcode project to
implement its step-g importer, but currently our converter ends up
hard-wired to a specific STEP application protocol (AP). There are
numerous APs that are commonly encountered (e.g., AP203 and AP214),
though, and we'd like to have one importer support multiple APs.

For this project, you'd work to make our converter read at least AP203
and AP214 simultaneously. This will almost certainly involve extensive
work directly in STEPcode to produce a parser properly encapsulated.

# References

-   src/other/step
-   src/conv/step

# Requirements

-   C++ Proficiency