# Working Schedule

## upto June 17 (Analysis and Design Period)

-   Exploring the code.
-   Make a short rough bio about each tool - *the way they work*.
-   Find the Image Processing functionalities used in them. Look at
    duplication in the functionalities.


(5-10 tools/day depending on varied length.

-   Preparation of rough ideas of each functionalities and the way they
    will be implemented with additional improvements in usability.
-   Discuss with mentor and other developers about the final plan for
    the design of the library. This includes :
    -   the possible formats to be supported (In addition to the already
        started in include/icv.h)
    -   Addition of Different functionalities and there usability
        improvements.
    -   Discussion about common groups identified for different
        functionalities.
-   Learning usage from BRLCAD libraries like common.h libbu libbio

At the end of this period : **A finalized plan to proceed for the
development of the library**.

## June 17 - Sep 2 (Development Phase)

### June 17 - July 1 \[\~2 Week\]

-   Implementation of various Structures of the new library
-   Deciding about the functions to be included in different files based
    on categories.
-   Deciding the input parameters and return type of each function.
-   Identify error handling in each Function.
-   Witting Documentation of all the structures included. PDF+Wiki
-   Creating Patches all together.

### July 1 - Aug 12 \[\~6 Week\]

-   Implementation of image processing functionalities focusing on
    categories identified during project analysis period.
-   Enough Time is allotted to this to follow up the implementation as
    decided during analysis step.
-   Implementation of 3-4 functions a week which includes unit-level
    testing and code coverage.
-   Documentation of the functions including input output
    arguments/methods etc.

To implement the image processing functionalities common groups have
been identified details of which are given at
<http://brlcad.org/wiki/user/Level_zero/GSOC13/ImplemnetationDetails-1>
.Further these groups have varied implementation load, Thus to balance
the load for a particular following weekly plan has been chalked in.

#### Sub Division

-   WEEK-1
    -   Crop or Rect (GROUP\#1)
    -   Differences and other arithmetic operations (GROUP\#2)
-   WEEK-2
    -   Filters, (GROUP\#3)
-   WEEK-3
    -   Histograms and Equalizations (GROUP\#4)
    -   Stats (GROUP\#6)
-   WEEK-4
    -   Scale or Shrink (GROUP\#5)
    -   Interpolate/Decimate (GROUP\#8)
-   WEEK-5
    -   Thresh (GROUP\#7)
    -   Background and Border (GROUP\#9)
-   WEEK-6
    -   Reserved Week

### Aug 12 - Sept 2 \[\~3 Week\]

=

-   Implimentation of Import/Export Modules.
-   Testing these Modules.
-   Documentation of these modules

## Sep 2 - Sep 27 (Final Wrap UP and Cleaning)

### Sep 2 - Sep 9 \[\~1 Week\]

-   Code Cleaning
-   System Level testing for the library.
-   Giving final structure to the documentation.

### Sep9 - Sep16 \[\~1 Week\]

-   Creating Demos For each functionality and Final cleaning

### Sep 16 - Sep 27 \[\~1 Week\]

-   Performance Analysis using gprof for different data.
-   Final code submission with Google.
