Space Partitioning - the breaking out of a generic volume of space into
structured sub-volumes - is fundamental to a wide range of geometric
algorithms. There are multiple methods of partitioning a volume, and
while BRL-CAD makes use of partitioning approaches in a number of places
with its codebase the partitioning logic is integrated into each
individual task and not generalized.

This task would be to design and implement a generalized, abstract
method that would allow existing and new code to utilize a
pre-implemented partitioning scheme. Say, for example, a ray
intersection method wanted to make use of KD-Tree space partitioning -
with a successful implementation of a space partitioning API the problem
is reduced to implementing calls to test whether nodes satisfy criteria
and what action to take in various cases, instead of the details of
storing and walking the KDTree data structure itself. Ideally it would
be simple for code to swap in and out various space partitioning schemes
to compare performance.

Students proposing ideas for this task should discuss it on the email
list or IRC to make sure they understand what the requirements for such
an API are.

# References

-   src/librt
-   src/librt/bool.c
-   src/librt/shoot.c
-   src/librt/prep.c

# Requirements

-   Familiarity with C/C++
-   General understanding of space partitioning schemes