There are currently several slightly different functions to recursively
walk the CSG tree. This task would be to implement a new tree walking
function capable of replacing them all and altering software that uses
the old walkers to use the single new unified one.

Time would be spent carefully designing a new interface that has the
appropriate hooks and callbacks so it could replace all of the existing
routines. Then time would be spent updating and testing all of the
various walkers as they're replaced with your new traversal routine.

This one is prime for test-driven development. Show what the interface
will look like for a variety of cases, then implement to that interface.

# References

-   src/librt
-   include/raytrace.h (grep for tree or walk or recurse)

# Requirements

-   Familiarity with C