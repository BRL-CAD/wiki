# Community Bonding Period

1.  Played around with code and build GUI.
2.  Found where is auto-arrange is being called and how it's called so
    that I could get a grasp of how it should be replaced.
    [Supermill](https://github.com/supermerill) helped by giving me
    another use of auto-arrange.
3.  Looked for a faster way to build the project rather than waiting for
    15 minutes when changing anything, LoH helped me with a faster way
    to build it.
4.  Investigated SVGNest JS code to get a feel of how the code is
    structured.
5.  Started investigating in the SVGNest desktop application as
    [gege2b](https://github.com/gege2b) has pointed out there is an
    implementation in C for SVGNest. After investigating I found the
    implementation isn't fully in C only one function of it is C and the
    rest is the previous JS code.
6.  Today I'll start reading one of the papers.
7.  I've started reading ["Complete and robust no-fit polygon generation
    for the irregular stock cutting
    problem"](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.440.379&rep=rep1&type=pdf)
    paper and it was very helpful. I went through the rabbit hole as the
    paper references other papers so I dived head first into reading
    them. I got a better understanding of the No-Fit Polygon and what
    role does it play in the whole auto-arrange algorithm, why it's
    useful and why it's better than it's predecessors.
8.  Tomorrow I'll take a look at SVGNest and compare how they implement
    the NFP with what the paper suggests. Today I'm studying for my
    final exams in my University tomorrow.
9.  Finished Reading the required papers and took notes to start
    summarizing them.

# Coding Period

## May 27-June 15

### Required

Final Exams period.

-   Delivering summary on the related papers. (O)
-   Investigating SVGNest JS library (structure, utilities).

### Activity Log For This Period

From 27/5 to 2/6 is my final exams week so my productivity won't be much
and I'm making up for this time in the weekends and by working extra
hours after 2/6. Deliverables won't be affected as I'm following the
timeline for each period.

1.  Investigated SVGNest C and JS code to find out what has changed
    between these two projects and if I can make use of the C
    implementation.
2.  Took notes on the related papers and started summarizing them.
3.  Designing bounding object function to get a 2d boundaries for the
    objects to work with.
4.  Finished my final exams and working full time.
5.  Faced some issues with wxWidgets library and trying to fix them.
6.  Continued working on designing an efficient bounding object function
    to get 2D outer contours of 3D objects to work on them. I've looked
    for similar function in the current 2D preview functionality in the
    application but the method I want isn't there so I'll continue
    coding it.
7.  Tried concave hull and found papers on generating a bounding concave
    object to generate a 2D equivalent for the objects but I found that
    there are some cases that concave hull will fail in so we'll need
    convex hull.
8.  Created a class "BoundingHull" to hold the bounding shape to
    transform 3D into 2D and still maintain the boundaries of the object
    so that no two objects would intercept with each other.
9.  Eid Elfetr Holiday so I'm working between family visits.
10. Completed [calculating bounding
    hull](https://github.com/3bhady/Slic3r/commit/ce678e817fb82642c68da1bd545a3bbddcee8325)
    for each model with each copy of it after applying transformations
    on it.
11. Going through SVGNest code to find important functions to start
    writing tests for them.
12. Debugging SVGNest JS code and commenting on it while comparing the
    code to the papers.
13. Added comments and played with functions in SVGNest JS library and
    compared it to the read papers. Summary of the papers would make
    more sense being written into the code to help later in porting each
    function which relates to how each function contributes to the whole
    algorithm.
14. Forked the SVGNest repo and commenting on it
    [here](https://github.com/3bhady/svgnest)

## June 15-June 20

### Required

-   Extract useful functions from SVGnest JS.
-   Write skeleton for unit tests for extracted functions.(T)

### Activity Log For This Period

-   NFP (No Fit Polygon) is the core of the polygon packing algorithm
    but it makes more sense to start with implementing it now and port
    helper functions along the way to understand the functions being
    ported more as Their use appears instead of porting helper functions
    by themselves.

1.  Creating the basics of the NFP function.
2.  Continuing porting NFP function and useful functions which are
    required for it to run.
3.  Calculated the touching edges for polygons to help creating the NFP.
4.  Generated the translation vectors for orbiting shape to slide
    alongside the stationary shape.

## June 20 -June 28

### Required

-   Write unit test for the geometry functions to be used.(T)
-   Implement the geometry utility functions.(C)

### Activity Log For This Period

-   All the following functions are utility functions used in the NFP
    function which is the core of the packing algorithm this was
    supposed to be implemented next month but it makes sense to start
    with it and porting each helper function along the way.

1.  Started rejecting the translation vectors which will cause
    intersection.
2.  Wrote a skeleton code for a function to calculate the maximum
    distance a polygon can slide in a given direction without
    intersecting with another polygon.
3.  Created a function that takes two edges and finds the maximum
    distance one edge can travel in a given direction without
    intersection.
4.  Found each possible arrangement for the edges to be in without
    intersecting with each other.
5.  Created a function to calculate the maximum distance a vertex can
    travel in a given direction.
6.  Finished calculating the maximum sliding distance for each
    translation vector.
7.  Day off studying for a job interview wish me luck.

## June 28-July 4

### Required

-   Writing unit test skeleton for placement algorithm.(T)

### Activity Log For This Period

1.  Fixing the flow in the NFP function as it wasn't working correctly.
2.  Development laptop got stuck in a login loop after installing CUDA
    so I spent the whole day trying to fix it.
3.  Continued modifying and fixing the NFP function.
4.  Debugging and fixing issues with the placement algorithm. ( the NFP
    had very large values )

## July 4- July 21

### Required

-   Implementing unit testing for placement algorithm.(T)
-   Implementing placement algorithm.(C)
-   Parallelizing the placement algorithm.(C)

### Activity Log For This Period

-   Taking two days off to finish my graduation project. (I've already
    started working on this period's work 2 weeks ago).
-   Debugging and tracing the placement algorithm.
-   Fixing issues with the Point and Pointf in the placement algorithm
    as what everything should be.
-   Fixed issues with trimming the vectors as it wasn't working
    correctly.
-   Designed test case for the placement algorithm.
-   Continued working on the placement algorithm and fixed issues with
    sliding as it wasn't moving correctly.
-   Solved couple of issues as it was producing some garbage values.
-   Looked for a way to visualize it's output to understand the results
    better.
-   Fixed multiple issues where the variables names were wrong like
    replacing next_A_index with prev_A_index which were causing
    wrong results.
-   Fixed issue with the starting point.
-   Fixed issues with polygon slide distance.
-   Fixed issues with segment distance.
-   Created NFP for convex shapes.
-   Working on moving the objects to a point on the NFP.
-   Finished moving objects and now they are packed close to each other.
-   Found an interesting method which takes a simpler and much faster
    approach to the NFP problem but needs at least one of the shapes to
    be convex which fits perfectly to our problem as we're starting with
    a convex hull for each shape.

## July 21-July 26

### Required

-   Design skeleton code for unit testing optimization algorithm.(T)

### Activity Log For This Period

-   Continued working on the placement algorithm as I took a new simpler
    approach and read multiple papers with simpler and faster approaches
    than the orbiting polygon with sliding edges presented in the
    SVGNest library.

1.  ["JONAS LINDMARK Thesis at
    CSC"](http://www.diva-portal.org/smash/get/diva2:699750/FULLTEXT01.pdf)
2.  "A comprehensive and robust procedure for obtaining the nofit
    polygon using Minkowski sums" Which I thank [JULIA A
    BENNELL](https://www.researchgate.net/profile/Julia_Bennell) for
    providing me with the full text when I requested it.
3.  Fixed the IFP with orbital approach.

## July 26-Aug 9

### Required

-   Implementing unit testing for optimization algorithm. (T)
-   Implementing optimization algorithm.(C)
-   Determining threshold for when to stop optimizing.
-   Adding needed buttons in GUI for allowing user to specify threshold
    for stopping optimization. (C)

### Activity Log For This Period

N/A

## Aug 9-Aug 19

### Required

-   Testing the whole auto-arranging module against SVGnest library and
    fixing bugs if the outputs are not identical. (T)
-   Testing the output through the perl GUI. (T)

### Activity Log For This Period

N/A

------------------------------------------------------------------------

Deliverables are marked in the timeline as follows:

-   Code is marked as (C).
-   Tests are marked as (T).
-   Others are marked as (O).

Code and comments on existing code can be found on my forks
[Slic3r](https://github.com/3bhady/Slic3r)
[SVGNest](https://github.com/3bhady/SVGnest).