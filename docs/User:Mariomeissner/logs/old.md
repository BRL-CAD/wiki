OLD LOGS

**20-6**

Build successfull on Arch Linux (Antergos) x64 Working my way through
the Introduction_to_MGED.pdf

**21-6**

Successfully calculated mass of a copper sphere using rtweight.

**11-7**

Diving into the source code of rtweight. I will need some help
understanding the overall structure of the repository and some details
about rtweight.

**12-7**

Proposed an initial model of representation. I would use a
three-variable function that returns the density of the material at a
certain point in space. Integrating this function over the boundaries of
the object yields it's mass. Example can be found here:
<https://drive.google.com/file/d/0Bz6hfFobLeoyZC1vQ1JwSU05NDg/view?usp=drivesdk>

**14-7**

Started working on the example raytrace application. I am setting
highest priority to understanding the basic behaviour of this little
program, as I know it is the foundation I will need in order to continue
with the project.

I will try to modify it in some ways and see if I break it.

From today onwards, I will be working from 15:00 to 22:00 most days, and
from 10:00 to 13:00 as well a few days a week. After evaluating how much
can be done with this schedule, adjustments will be made accodingly.

**15-7**

Drafted an example of how to obtain a function that returns the density
a ray sees at it crosses the object.

**16-7**

Reading through, understanding and compiling the example applications.

**17-7**

Modeling the sword and continuing yesterdays work.

Starting with the candle example to get practice.

**18-7**

Making new, blade that actually fits the specifications; remaining time
digging through the viewweight.c code.

**19-7**

Designing proper density model that allows for good implementation.

**20-7**

Studying source code.

**25-7**

Setting up eclipse development build and studying source code.

Facing problem where Eclipse does not properly recognize tons of symbols
in the code, including basic types like "FILE". One candidate solution
is to browse to the C/C++ pre-processor settings and adding and
configuring the CDT GCC built-in compiler. Details here:
<https://stackoverflow.com/questions/21065616/multiple-could-not-be-resolved-problems-using-eclipse-with-mingw>

However performing the steps on there crashes the indexer while it's
updating.

I'm using Arch, Eclipse Oxygen and the latest available GNU compiler
suite. I built the project for eclipse using CMake following the guide
over at wiki/compiling.

Thinking about how the user should input the density data and how we
should handle it inside, I found this to be relevant:
<https://en.wikipedia.org/wiki/Curve_fitting>

We could let the user set any number of points throughout the material
with specific densities, and then we can apply a simple curve fitting
algorithm to create a continuous density function. This function could
be stored in some struct or array and then be used to return the density
value at any given point with precision. These requested points could be
used for interpolation by the calling code.

**26-7**

New goal: modify the example application to shoot a ray to the object
and calculate it's density assuming it's a 0 to 1 change.

Working on goal.

Results: [screenshot](https://puu.sh/wTDzC/5c3a15af9a.png)

**27-7**

New goal: snippet code to read density points from command line into
data structure.

**28-7**

Debugging yesterdays work.

Managed to make it work to a point where I think the goal has been
reached. Further expansions of this goal may be made once more is known
about the density specification.

**29-7**

New goal: write simple function that returns the density value for a
material at any point in space, for simple specifications (a few
density_points at max).

Working on goal.

Todays work: [1](https://transfer.sh/PvVCy/rtexample.c)

**30-7**

Continuing with yesterdays work. Decided to make a new structure to
store vectors and their factors. We can go through the list of provided
points for a material specification and compute the vectors we care
about, push them to a list.

**31-7**

Received feedback on yesterdays work. Apparently I tried to do breadth
first, which resulted in too ambiguous code that obviously wasnt working
yet either. Today I tried to revert that and made a simpler situation
work. Figuring out how to properly use vmath macros and bu_lists, as
well as debugging my mistakes, took away most of my time today but I
feel it was an enlightening process. Emailed results.

**1-8**

Day off

**2-8**

Partial day off. Ｗoring on blade.

**3-8**

Finished blade curve.

Working on density(), will try to make the vector list work.

Facing a little design problem. If we have a vector_list, we need to be
able to keep track of who's vector each projection is. We cannot store
it inside the vector bc we will want to reuse it on other calls. One
solution could be creating struct contribution and store both the value
and a pointer to the vector it came from. After all we only need the
factor. Calculing everything necessary (projection and contribution)
within the loop and then throwing away the information has also been
considered. It could work if we do average but would not work if we want
to perform some other more complex operation on them.

**4-8**

Continuing yesterdays goal.

Separating code into my own files, and restoring rtexample to the
original.

Figuring out how to set up new projects within the solution in
VisualStudio.

**5-8**

Carrying my work over to viewweight.c . New goal is to make case 0 and 1
points work while using my code. Will also model a box that will serve
as initial dummy example object. Calculate results by hand and compare
with code output.

**6-8**

Some more tests on current code. Started working on the new 4 point
example.

**7-8**

Finishing off new example. Separating vector creation from
query_density code, so that initial vector list is only created once.
Performance of rtweight right now is not so good, this should help.

New example works: [code](https://transfer.sh/R8o7z/viewweight.c),
[result](https://puu.sh/x3MZm/d32523b6f4.png), [expected result on
paper](https://drive.google.com/file/d/0Bz6hfFobLeoyRmI5elVlRkN2X00/view?usp=drivesdk).

**8-8**

Incorporating readDensityPoints() into the current code (writing data
into the .density file) so that the whole thing is 'complete'. Instead
of hardcoded data I will load it from the file.

**9-8**

Continuing yesterdays task.