The BRL-CAD Benchmark Suite is a system performance analysis benchmark
that tests the performance of a given system's CPU, memory, cache
coherency, kernel context switching, and compiler optimization
capabilities. The benchmark provides a linearly comparable metric of
overall system performance that may be used to quantitatively evaluate
the relative performance of a given system, particular compilers,
compilation options, and hardware architecture designs. This performance
test is based on a real-world CPU intensive application of ray-tracing,
providing a reliable metric of actual system performance that may be
compared across more than two decades of computing.

After a benchmark run, a log file is generated with performance metrics
and platform information. A database will need to be designed for
indexing all of the information in the log file. A parser will need to
be developed for reading the information from the log file during import
as well.

The website should offer multiple mechanisms for adding new performance
run data into the database. The website should provide multiple
graphical and non-graphical visualizations of aggregate performance data
(i.e., graphs, charts, tables, etc).

# References

-   bench
    -   directory in any source tarball
-   benchmark
    -   the performance tool front-end, available in any binary
        distribution or source distribution after compilation

Muie Cornoiu!!!

# Requirements

-   Ability to run shell scripts
-   Ability to navigate a UNIX/Linux command-prompt
-   Familiarity with web development technologies

# Past Efforts

-   [GSoC14](../user/Ankeshanand/GSoC14/logs.md)
-   [GSoC12](../user/Stattrav/GSoC2012_log.md)
