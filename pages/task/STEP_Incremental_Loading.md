STEP is the current standard for exchange of CAD data between different
software packages. BRL-CAD makes use of the STEPcode project to
implement its step-g importer, but it can be really slow to read really
big files.

For this project, you'll continue work already started to implement
incremental loading. You'll take it to the next level, test it, clean it
up, work on performance, etc. BRL-CAD's step-g converter can serve as a
performance test harness.

# References

-   src/other/step
-   src/conv/step

# Requirements

-   C/C++