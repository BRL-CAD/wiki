## Google Summer of Code 2012

### Current

Status: Working on fluids system, starting with drag caused from falling
object.

TODO:
Gain Commit access ASAP
Work out how density is handled during simulation and add it to the
mass/volume calculations in a more accurate fashion. WOrking out how to
best calculate the coefficient of drag for objects.

Coding Environments Status:
VS2010x64 : Success, no bullet.
Fedora 17 KDE-Spin : Success, Bullet running.

### Log

#### April 2012

BRLCAD compiled and run with Windows Visual Studio 10 x64 Debug

#### May 2012

8th : Updated Wiki pages

9th-10th : Tried to compile BRLCAD with bullet on VS2010, consistently
recieved 63/70+ errors for debug/release versions. Using linux as
development environment until I have a chance to fix issues.

11th-12th : Setup a Fedora 16 environment with BRLCAD compiled and
running simulations.

13th-16th : Testing various simulations, spent time looking through the
simulation code to learn more about how it currently works and how to
best implement new features.

24-25th : Reinstalling Windows on my SSD (From HDD), computer
unavailable for a day 26th : Everything back to normal with PC, build
times using VS2010 decreased from 3+ hours to 9 minutes (from clean)

27th-29th : Fixed issues with SA/Centroid functions for Ellipsoid
Primitive patch

29th : Patch for Surface Area for Ellipsoid Primitive accepted
29th : Downloaded Fedora 17 and began to set it up for brlcad
development

30th : Successfully built and installed brlcad on Fedora 17, as well as
ran some small test simulations without issue.
30th : Working on a function to calculate the gravitational force
between every object in the simulation, in order to be able to calculate
the acceleration between them.

31st : Continued work on aforementioned function, testing tomorrow for
patch submission.

#### June 2012

2nd : Submitted initial patch for implementation of gravity forces
between rigid bodies.

4th : Added to patch with a small update for calculating mass using the
bounding box of an object, and using that to find the volume, assuming a
density of one. Density to be integrated better soon.

5th : Working on the resolving of acceleration due to gravitational
force, mainly how to store the information since there will be n(n-1)
number of forces which will then be condensed to n number of
accelerations, where n is the number of rigid bodies.

6th-8th : Finished work on resolving the acceleration and begun working
on how to integrate this into the current simulation, in terms of
running the calculations every time and altering the linear_velocity
values of the rigid bodies.

11-15th : Continue work on gravitational functions.

16th-17th : Looking at how better to implement mass and center of mass.
Trying to learn how to utilise gqa.c and also whether it would be best
to add to the rigid_body struct with volume, mass and center of mass
(as opposed to center of BB) for use in gravity functions to avoid
repeatedly recalculating it.

18th - 22nd : Continued work on gravitational function. Working out how
to intergrate the changing angular and linear velocities into the bullet
simulation, since the brlcad system would ideally recalculate this every
step.

23rd - 26th : Finalising the gravity calculations and working on the
fluid system. Need to work out suitable intervals for these
calculations. 60 times per second would be a massive performance hit,
even with the calculations themselves being relatively simple.

27th - 29th : Finishing off the gravity, videos coming soon (with highly
exaggerated values to make it obvious, movement is negligible with small
mass objects, or large distances).

30th : Continue working on fluid. Namely how to best teach the system to
use the best coefficient of drag for a shape.

#### July 2012

1st - 2nd : Integrating into system with a similar method to gravity,
alter the acceleration for the rigid body then use that to change the
velocity every step.

3rd - 5th : Learning about how to go about creating video footage. Will
need to save a render of every step of the simulation, I think. Also
worked on testing the drag functions.

6th - 7th : Changed how mass is handled in the simulation, added new
parameter to rigid_body structure to handle this. Temp using bb_vol
assuming density is 1 to calculate mass, will be changed to something
more precise soon. Also working on making sure the drag function gets
the right area, and started to try and calculate any rotational forces
around a rigid body

8th : Tested basic drag and gravity functions with rest of simulation
and values output are correct with my calculations. Made progress with
video. Still working on how to calculate the surface area for drag
function, as well as how to get a reasonable coefficient of drag.

9th : Accidentally broke my fedora VM by running a simulation with 1
million steps as an experiment. Files were backed up, currently setting
up another one, trying out the KDE distribution of fedora. Issue with
building that I will fix tomorrow (fb.h, unknown types window,
XVisualInfo, and a couple of others on line 136) and then I will debug
the error. VM broke due to a full harddrive of error messages as far as
I can tell. Error was somehow related to collision, from the little I
could make out from the mass of error messages. Situation was a simple
sphere dropping onto a surface.

10th : Wasted several hours getting a new VM working, had compile
issues. Now working again, however. Came across an error in one of my
functions whilst debugging, which involved NaN results. Working on
finding the cause and will fix asap.

11th : Fixed NaN results, had a 0/0 division which I changed. Also
refined code to better handle ground plane with respect to gravity from
it (i.e ignore it). Gravity is still counted as 10 down, with the
gravitational attraction seperate. Should be in position to finally make
video tomorrow morning.

12th : Ran simulation and took raytraces at 50 step intervals. Looks
like the groundplane moves, which isn't meant to happen. Will look into
this and check it's not moving, and if it is stop it. Also changed use
of gqa slightly, and implemented a, for now, debug usage rt, which I
intend to make a user option later on, if they wish to automatically
have the simulation saved as several (hundred/thousand) images.

### Development Schedule

(Unless otherwise specified, 40+ hours of work to be assumed):

23rd April – 5th May

-   Flesh out any last details in project, have all objectives clear and
    the schedule complete.
-   Gain commit access before or during this point

<!-- -->

-   Before the official start of coding, create basic, general (and some
    specific) unit tests for functions that will be implemented, such as
    testing the variable gravity, the resolving of drag forces, the
    moments and couples calculated, and so forth.

5th May – 21st May

-   Learn as much about any relevant libraries such as Bullet, and
    BRL-CAD libraries such as librt and libged as I can, to enable me to
    be able to get straight into coding with the knowledge of what is
    already there and how to use it.
-   Start writing function outlines, header files to make it clearer as
    to what goes where and how to reuse code efficiently.
-   Iron out any current bugs in the simulation files, to ensure a fully
    working simulation environment.

21st May – 28th May

-   Coding begins. Start by working on the gravitational system as this
    will be the easiest to implement and so will take the shortest
    amount of time, and will make sure I am completely familiar with the
    code.

28th May – 4th June

-   Milestone 1: Gravitational system complete and fully bug tested.
-   Once milestone 1 is reached, begin work on the fluid system,
    starting with functions to calculate drag on surfaces

4th June – 11th June

-   Exam period starts at University, limited time available.
-   In available time, work on drag functions and start to implement
    functions to resolve the forces from the drag (In x,y and z
    directions)

11th June – 18th June

-   Exam period ends
-   Carry on implementing functions to resolve forces and start on
    functions to resolve moment forces to show rotation in the
    simulation

18th June – 25th June

-   Continue working on the fluid system and begin bug testing
-   After 22nd June assume 50+ hours working, to make up for lost time
    during University term

25th June – 2nd July

-   Milestone 2: Fluid system complete and fully bug tested.
-   Start work on the collision system

2nd July – 9th July

-   Preparing for mid-term evaluations, fixing all current code up to
    this point which will be around two thirds of the whole project
-   Continue work on the collision system

9th July - 16th July

-   Continue work on the collision system

16th July – 23rd July

-   Milestone 3: Collision system completed
-   From this point forward, start black box testing to ensure
    everything works

23rd July – 30th July

-   Milestone 4: Black box testing complete
-   Start white box testing to ensure code is of a high standard

30th July – 3rd August

-   Milestone 5: White box testing complete
-   All following time is a buffer zone. If everything complete, begin
    work on adding more functionality to the fluid system, namely the
    underwater physics

3rd August – 17th August

-   I will be in Germany during this period on holiday. I will however,
    still have a laptop as well as internet access so although this is a
    critical time with respect to final evaluations and so on, there is
    no reason for me to not be able to work
-   Time spent cleaning up code if needed, write documentation to enable
    users to easily utilise any of the functionality of the simulation
    system.

17th August – 24th August

-   Any last minute fixes are made, final evaluations sorted and project
    finished.
-   Milestone 6: Project finish, submit evaluations.