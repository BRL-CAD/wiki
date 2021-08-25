Mario Meissner SOCIS 2017 Logs

**10-8**

Moving task over to rtexample. Including Voronoi tesselation. 0 and 1
points working, including user input (no hardcoded points).

**11-8**

Continued working on n-point Voronoi. Todays code doesn't compile yet.

**12-8 & 13-8**

Break.

**14-8**

Continue working on n-point Voronoi.

**15-8**

Finished initial Voronoi point implementation.

Will now continue working on implementing vectors.

**16-8**

Break.

**17-8**

Working on read_density_points to support vector input.

**18-8**

Finished read_density_points vector update and will now give support
to transitions (vectors) with arbitrary 'rate' inside segment_density
calculations.

Moved old logs to a separate page
(http://brlcad.org/wiki/user/Mariomeissner/logs/old) to keep this one
clean.

**30-8**

Left the code in a more stable shape. Fixed some bugs, projections are
now skipping.

**5-9**

Finally set myself up in Germany. New objective: test out code and fix
any more bugs. Took my time to set up dev environment, but couldnt work
because of compilation issues.

**6-9**

Testing and fixing code. Found major flaw in projection skipping.

**7-9**

Worked on a new model to properly skip projections.

**8-9**

Implemented the new projection skipping model and re-ran the tests.
Everything seems to work correctly for now.

**9&10-9**

Break

**11-9**

Cleaning code and moving over to rtweight. Once I moved I will run
rtweight tests to see if mass is correctly computed for simple shapes.

**12-9**

Found some more mistakes in the code.

**13-9**

Preparing the move to rtweight.

**14-9**

Moving code to rtweight. It's harder than expected and things don't work
yet. I tried cleaning out most of the code that was used to read
densities from the file, and rely only on my own function call (so that
I can avoid the stupid segmentation fault I can't get rid of).

**15-9**

Break.

**16-9**

Mass returns as NaN so something is wrong somewhere. Debugging.

**17-9**

Had several compilation problems. I can now compile on VS again. Density
file loads. Mass now returns 0.

**18-9**

Break.

**19-9**

Investigating cause of negative densities that end up causing the final
mass to be 0.

**20-9 & 21-9**

Because of course registration and orientation events, busy. Break.

**21-9**

Fixing code in rtweight.

**22-9**

Fixed several issues, mass now computes, but wrongly.

Trying to learn to use the VS debugger.

Starting to get a feel on why things don't work. I'm finding and
polishing several issues. I also noticed that I am not correctly
handling two edge cases for segment density:

-First point should be a skip (for now I had assumed first point would
never be one, without really thinking about it).

-First bunch of points or last bunch of points' projections lay outside
the segment. They should receive special consideration.

**23-9**

From today I will try to approach the final step of my code in a
slightly different way, in order to correctly handle projections outside
the segment, but who's boundaries actually lay inside. I will use
intersections to compute a list of boundaries, and then just loop
through them once to calculate avg density. I will not use the
projection point in this stage (I will still use it to predict a skip).

I know I should write complete code, but this overhaul will take some
time. I will try to release in-progress working stages if I can. I
really think this new version cleans up the mess quite a lot, simplifies
the concepts, makes it all more readable, and most importantly, will
support more situations than before, removing several flaws.

The whole projection concept wasn't that good of an idea to begin with,
I shouldn't have stuck to it for so long. It's only useful for
predicting skips.

**24-9 to 1-10** Holiday (trip).

**02-10**

Refactoring stage 1.

**03-10**

Desiging new algorithm for stage one.

**04-10**

Designed and published new algorithm and published it.

**05-10**

Starting with implementation.

**06-10**

Broke down implementation steps. Got rid of intersection function,
replaced by a new, more complete function that tells us if a point's
region will be crossed or not, directly. Computes the intersection,
checks if it lays inside the segment and checks distances to evaluate if
the boundary is crossed by the segment or not, returns a boundary_t
struct.

**07-10**

Implementing new algorithm step 1.

**08-10**

Break

**09-10**

Finished and submitted new algorithm, tested for 0, 1 and 2 points.

**10-10**

Hunting for bugs and removing old/unused variables and code blocks.

**11-10 && 12-10**

University.

**13-10**

Testing more cases and making sure no more bugs are present.

**14-10**

Moving code over to rtweight (again).

**15-10**

Finished moving code over, and testing the implementation. Basic cases
seem to work. Submitted code.

Mario Meisner.
