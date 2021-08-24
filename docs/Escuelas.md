## ESA Summer of Code Project Proposal

### Non-vacuum gravity simulator for the BRL-CAD Solid Modeling tool

------------------------------------------------------------------------

#### About Myself

-   **Name:** Oana Niculaescu
-   **Mailing List ID:** oana.niculaescu@gmail.com
-   **IRC ID:** elf11

I am a student at the Polytechnic University of Bucharest, Romania, in
the second year at the Computer Science faculty. I have a good
background in programming and I had an internship with a local company
here in Bucharest on game design and iOS. I also have a little bit of
experience with CUDA and GPU programming. I am currently available for
working 40 hours a week on this project. More details about my
background are provided by my CV and I will link you my Github account,
where some of my work is presented.

#### Brief project summary

The current non-vacuum gravity simulation available in BRL-CAD has not
been developed to its fully potential and it is limited. My proposal is
about continuing the work previously Abhijit Nandy did on the project
and improve on his results. Since the Bullet Physics engine has been
previously used and for this project and there are integrated tools for
BRL-CAD, like gqa and rtcheck, that perform exact collision detection I
consider there is no further need to switch to the Open Dynamics Engine
(ODE). Basically the scene is read from a list of objects, the Bullet
creates it and then forces are applied such that the position of the
object will be updated, then the two BRL-CAD integrated tools for
collision detection will be called and the collisions will be solved.
Previously aligned axis bounding boxes have been used in collision
detection and I consider it is a good thing to have a continuation with
those.

#### Detailed project summary

Since the initial developer for this project has been intending on
implementing a command in the Archer GUI for solving this problem, I
will continue from where he left and will completely integrate the

Archer&gt; run_simulation command. The main work I am thinking to do
will get done in the src/libged folder, the C++ code will get after
integrated with the Tlc scripting language, that will call the C++ code
for implementing a command. First I would further test the Sphere to
Sphere collision and the collision pair generation logic. The
btConvexConcaveCollisionAlgorithm, from the Bullet Physics Engine,
supports collision between convex shapes and (concave) trianges meshes.
This would be a nice addition to the BRL-CAD simulation. Also, in the
same folder src/libged are functions that need to be ported to the
src/librt level, the

int apply_material (struct ged \*gedp,

`          char* comb,`
`          char* material,`
`          unsigned char r,`
`          unsigned char g,`
`          unsigned char b); `

int apply_color (struct ged \*gedp,

`          char* comb,`
`          char* material,`
`          unsigned char r,`
`          unsigned char g,`
`          unsigned char b);`

that pass the color combination and apply it to a material, showing the
current state of the object inside the physics engine. In the same
folder there are some more functions that are not properly written and
that need some additional work, like the function that gets the exact
overlap volume between the 2 aligned axis bounding boxes and some more
work on ray tracing.

Arbitrary collision detection and simulation will be the next milestone,
in this section I think it would be proper to add some more physics
specific attributes to the objects besides velocity that it is already
there. I am thinking about gravity, friction force, some bouncing ball
effect, like having a ball dropping on a hard surface and bouncing back
in the air until it gets in a stable position. Here I will also add
ground planes, materials which will be taking account of the surface of
the ground. Currently only the bounding box is present in the
implementation, but objects will get properties like elasticity and
other custom forces. Integrating the Bullet btCylinderShape and
completing the implementation of detecting collisions for arbitrary
objects would be the next logical milestone.

After the primary physical forces are implemented, I will work on an
improved gravitational system, where the gravity would depend mostly on
the corps masses, bigger mass bigger gravity. For example if we have
large objects dropping on the surface of a plane (e.g. Earth), there we
will have to take into account the Earth gravity but also the pulling
force that satellites (larger objects that gravitate around the Earth,
like the Moon). I am thinking about implementing this as a command, in
the archer GUI, after drawing the object the user can use a command
similar to

set_objectMasses(Object \*obj, type_t Value).

The function will be called and the pulling force, the gravity will be
calculated considering the object masses.

#### Proposed Schedule

So far I have managed to compile and install BRL-CAD on a 64-bit Ubuntu
11.04 version. I am momentarily focusing on the “simulate” command in
the archer, looking over the code Abhijit Nandy wrote for it. I have
been going through the documentation/resources available on the
brlcad.org/wiki. I already have the Sourceforge and brlcad.org accounts.
Now the proposed schedule, for the first month of the program, that I
have come up with it is as follows :

-   *Week 1st - 6th August - Week 6th – 13th August*

<!-- -->

-   -   getting familiar with BRL-CAD simulation, going through the
        tutorials on this sites : <http://brlcad.org/wiki/Main_Page> ,
        <http://content.gpwiki.org/index.php/BRL-CAD:Tutorials>
    -   getting familiar with the Bullet, going through the Bullet's
        tutorials and from the Bullet user manual going through the
        fallowing chapters : Quickstart, Library Overview, Bullet
        Collision Detection, Collision Filtering, Rigid Body Dynamics,
        Constraints.
    -   getting familiar with Tlc scripting language
    -   start testing the sphere2sphere collision

<!-- -->

-   *Week 13th – 20th August – Week 20th – 27th August*

<!-- -->

-   -   continuing testing the spehere2sphere collision with convex
        shapes
    -   adding the functionality of the
        btConvexConcaveCollisionAlgorithm, from the Bullet Physics
        Engine, to BRL-CAD, implementing concave-convex collision

<!-- -->

-   *Week 27th August – 3rd September*

<!-- -->

-   -   testing the new concave-convex collision with as many objects as
        possible

After this is done, further discussion with the mentoring organization
will set the course of action that I must take.

#### Log

Here I will log the changes to the project as I will make them.

1st August

Starting reading on the BRL-CAD documentation and going through the
tutorials from this page 2nd August

Going to the tutorials from Tutorials from the following sections:
*Geometry Modeling Kernel,*Geometry Conversion, ''Procedural Geometry.

3rd August

Continuing going through the tutorials from Tutorials.

4th August

Starting looking through the Bullet library, and going through the
"Hello, World!" tutorial.

5th August

From the Bullet user manual going through the fallowing chapters :
Quickstart, Library Overview, Bullet Collision Detection, Collision
Filtering, Rigid Body Dynamics, Constraints.

6th August

Continue doing some minor Bullet tutorials, learning about Collision
callbacks and Triggers in Bullet.

7th August

Starting getting myself familiar with Tcl scripting language, going over
tutorial.

8th August

Continue the Tcl tutorials.

9th August

Starting looking in the BRL-CAD source file, the source files for the
simulate command.

10th August

Problems understanding some of the simulate command functionalities.

11th August

Starting testing on the simulate command with some basic shapes like
spheres.

12th August

Some problems appeared with the simulate command, not understanding
exactly the use of it.

21st August

Looked into the simulation system and did some of the simulation
presented in the BRL-CAD documentation, also looked into the submitted
file by AI_Da_Best.

22nd August

Looked into the nirt command and Interactive raytracing- Nirt command.
The problem with the simulate command still persist.

23rd-24th August

Starting working on the improving on the simulate command, adding new
parameters (new forces to be taken into consideration). 25th-26th August

Understanding the way compiling and running a BRL-CAD tool works. First
patch with learning purpose submitted, patch \# 3562134.

27th August

Looking through the rest of the if_\*.c files from /src/libfb and
modifying all the double-buffer by default options to single buffer.
Submitting patch \#3562423. Starting looking through the source code for
porting the 'joint' command from /src/mged to /src/libged.

28th-29th August

Working on the joint command, trying to get it ported by following some
of the other get_\*() commands, so far did this \[link_extern\], but
getting some errors \[link_extern\].

30th August

This is what the /libged/joint.c command looks like so far:

-   \- header file : \[link_extern\]
-   \- joint.c : \[link_extern\]

I am having some problems with the debugging of the command, the mged
tool exiting altogether when I try to run "joint help" from the
/libged/joint.c file. Somehow an "_exit_group" syscall gets called.

31st August - 1st September

At Sean's suggestion I deleted the whole libged/joint.c file and started
with a blank ged_joint() function that only printed a message, this was
done in order to grasp the way the function calls actually works. Here
are the files :
\* header file : \[link_extern\]

-   joint.c file : \[link_extern\]

The libged/joint.c file has been modified so that the ged_joint()
function will print the same output as the f_joint() function from
/mged/animedit.c file. When the joint command doesn't receive enough
arguments, we are assuming the user needs help with it so a table with
all the joint command's arguments it's printed.
Source file joint.c : \[link_extern\]

3rd-4th September

The libged/joint command is almost done, the files can be found here :

-   header : \[link_extern\]
-   joint.c file : \[link_extern\]
-   columns.c file in libged library (needed for printing):
    \[link_extern\]

5th September

The help and debug options for the new joint command are tested and have
the same behaviour as the ones from the old joint command
(mged/animedit.c). Here are the source files so far:

-   joint.h : \[link_extern\]
-   joint.c : \[link_extern\]
-   and of course the columns.c file \[link_extern\]

6th September

Submitted patch \#3565411 for the new joint command from src/libged.

7th September

Compiled and run the simulate command, from the libged library.

9th-10th September

Mged simulate command tutorial :
<http://brlcad.org/wiki/Mged_simulation>

11th-12th September

Mged simulate command tutorial is done. Scripts for generating the png
images are working.Added explanation about how to create a movie out of
the generated png files. <http://brlcad.org/wiki/Mged_simulation>

13th September

Solved a problem with the way the simulation movie was looking, it was
way too dark, setting up a default source light did it. Added some
\*mpgs with the simulation and some gifs of the 2 scenes, one with the
viewset the other one without it :

-   \[link_extern\] - with the viewset
-   \[link_extern\] - without the viewset
-   the gifs can be seen on the wiki page :
    <http://brlcad.org/wiki/Mged_simulation>

14th - 16th September

Finished the Mged Simulation tutorial.
There was a problem with the "rt" command, the outputted image was way
too darker, at Sean's suggestion used the -W option to invert the front
and back colors, and the images look properly now.
Modified the second script, now the edges of the geometry are also
traced, the view is better and images are rendered using a frame buffer.

19th - 22st September

Started working on improving the simulate command, founded additional
problems, not sure yet where they are coming from :

-   the simulation for meter units takes way too many steps
-   the cube falls through the plane and then comes back to the top(to
    the original position) and starts falling back to the ground, e.g
    for the same simulation as the one in Mged_Simulation on the wiki
    page, with the units set to meters I ran it for 5500 steps first
    time, the cube was pretty close to the ground, then I wanted to see
    how closer can I get it, and I ran it for another 800 steps and the
    cube ended being in this position \[link_extern\]
-   simulating for 300 steps doesn't really give any real movement to
    the cube, this is wrong it should take less steps for the cube to
    have a real change in its position \[link_extern\]
-   the velocities are not correctly passed from the bullet, where they
    are being calculated back to the cube, where they should be updated
    after every step
-   the mass is calculated wrong, it is way too big for a cube, and it
    gets updated every step, mass should be a constant, for the moment
    it has been hard-codded to 1kg, that should change
-   The cube dimensions are not passed correctly to the bullet and back,
    after hard-codding those as well there is still a problem, the
    simulation looks like this \[link_extern\] with an output for the
    velocities, cube dimensions like this one \[link_extern\]
-   There is also a problem with a variable 'size' shadowing another
    variable from bullet, so basically I can't add or remove any
    bu_vls_printf, bu_log lines to the existing code in
    /src/libged/simulate/simphysics.c

23rd September

Tried to solve the m/mm problem the simulation had. The simulation acts
correctly only for the mm units, if we set the units to m before
creating the geometry, then when the geometry dimensions are being
transferred between mged and bullet, bullet gets the \#meters \* 1000
units. I am thinking that mged saves internally the units in mm, even
though we are working in meters, so we(Abhi, last year participant on
this project and I) came up with scaling the units when they are
transferred to bullet with 0.001, but then the mm geometry should be big
enough so that the bullet tolerance of 0.04m won't affect the physics. I
tested it and for geometry greater than 1000mm it works properly for m
and mm.

24th - 25th September

Checking if the bullet logic works as it is supposed to:

-   in the simphysics.cpp source file is a "run_simulation()" function,
    we replace everything that is inside that function with the code
    from the "Hello World!", here is what the simphysics.cpp looked like
    while trying to see if the bullet logic worked properly
    \[link_extern\]
-   bullet is working as it is supposed to, since the world created in
    the run_simulation() function with the sphere falling to the ground
    acted the way it was described in the bullet tutorial.

26th - 27th September

After talking with Sean, decided that the geometry should be scaled,
like if it is too small (less than bullet tolerance) then it can be
scaled up, for the moment it will be let as it is, but we have to keep
up in mind that the geometry should be larger than 1m all the time, so
that bullet can perform it's collision detection properly. Solved the
problem with the units transferred from BRL-CAD to bullet : - BRL-CAD
keeps all it's units inside as mm and transforms them on the fly in the
working unit, so if we are working in meter - units, then when we are
transferring from BRL-CAD to bullet we get the number of units amplified
by 1000. Added a fix for that.

This is what the Mged simulation cube is looking like after 300 steps,
the cube is not penetrating the surface anymore, collision detection
taking place \[link_extern\]

28th September

Started looking through the ray-tracing code, looked into registering
custom algorithms for collision with bullet, there are 4 rays shoot for
ever bounding box, the actual custom collision algorithm it is working
for box-box collision detection, that should be extended to spheres and
arbitrary shapes.

30th September

Starting from scratch on the ray-tracing collision algorithm, at Abhi's
suggestion, I am trying to experiment with a standalone bullet demo
registering a new collision detection custom algorithm.

4th - 7th October

-   checked if the bullet logic was working for a couple of geometrical
    forms, cube-cube, sphere-cube and cube-sphere, rotated cube-sphere,
    rotated cube - cube, without any callbacks - eliminate the
    broadphase and nearphase calls
-   test the broadphase collision logic and the nearphase collision
    logic outside the simulate command in a standalone program, both of
    them worked properly, tested them for the same geometry as above
-   test first the broadphase callbacks in the simulate command - it
    worked
-   add the nearphase callback - stopped working

12th - 14th October

-   started digging in the nearphase callback function, that one calls
    the generate_manifolds() function which uses the raytracing code in
    the simrt.c file
-   generate_manifolds() function shoots rays through the overlapping
    regions of the 2 colliding objects. The ray shooting logic was not
    alright, commented out most of it, and started working on a simpler
    way to shoot the rays for the manifolds. For the moment there is
    only one single ray that gets shot to the Z direction, at the middle
    of the penetrating object.

16th October

-   the idea is to investigate the region of overlap using a bunch of
    rays that covers it to the best extent possible and then get the
    biggest span in each dimension. In our case we should get 4 pairs of
    points, each in each pair, 1 point belongs to the cube the other to
    the gp. The point might be in the world space, and then they will
    match, or in the object space and then they will not match. For the
    moment we can't be sure. To investigate that region of overlap we
    need another standalone bullet test, to see what bullet generates
    for a gp and a cube. We need to print out the values that bullet
    generates using its own algorithms and match that to the best extent
    possible. We need to report back 3 things 1. Point pairs

2\. Normals 3. Penetration distance

17th October

-   created the standalone bullet simulation, the simulation respects
    the same dimensions as the Mged simulation realized awhile back in
    BRL-CAD, generated contact points and now I have to compare them to
    what BRL-CAD returns at this stage and replicate what bullet returns
    in BRL-CAD
-   the bullet simulation has the Y axis up, that's the vertical axis
    bullet considers
-   the simulation can be downloaded from
    <https://github.com/elf11/brlcad/tree/master/BasicDemo>

18th October

-   finalized the standalone bullet demo, the files can be found here
    <https://github.com/elf11/brlcad/tree/master/BasicDemo>, now there
    are printed the penetration points, the depth and the normals
-   started replicating bullets behaviour in brl-cad, for the moment
    more z rays are being shoot.
    <https://github.com/elf11/brlcad/blob/master/simrt.patch>

I HAD to remove all the external links from this page otherwise it
wouldn't have got updated.

20th October

-   a grid of ray is being shoot by the simulate command all over the XY
    plan, at the moment there are 6x6 rays being shot, tried with 10x10
    rays but the simulation was taking way too much time a picture of
    what the grid looks like can be seen here
    <https://github.com/elf11/brlcad/blob/master/grid-ray-6x6.png>
-   the code for the grid is here
    <https://github.com/elf11/brlcad/blob/master/simulate.patch>
-   made a comparison with what bullet returns
    <https://docs.google.com/spreadsheet/ccc?key=0AsmiuNTm7UBZdG92bV9veW1GYk8xRS1zOWpMX0ltNmc#gid=0>

21st October

-   tried to replicate the bullet standalone behaviour in brlcad, for
    that starting with getting the correct normals, started hardcoding
    them in the processCollision function from the simulationalgo.cpp
    file; last time the normals we got were (0,0,-1) we need (0, 0, 1)
    since the normals are from the ground plane to the cube and we want
    to replicate the standalone; it didn't work cause after hardcoding
    them we get only the first contact point, after that first contact
    point we don't get any more contacts between the 2 bodies which is
    obv wrong since the cube still falls through the gp
-   when the first contact is being processed then no more contacts are
    being added, but the cube is obv falling downwards since the depth
    grows
-   then tried to change the normals from the raytracing part, simrt.c
    file, the traverse_zray_lists() where we set up the sim_manifold
    strucure; it didn't work for the same reasons as before
-   the problem is that bullet keeps an array of manifolds and points
    for those manifolds, the m_manifoldPtr a pointer to this array
    (processCollision() function in the mged files and in the standalone
    bullet simulation) it gets cleared and updated every step;
-   last year student implemented its own structures for manifolds,
    never using the ones provided by bullet the sim_manifold struct in
    simulate.h; the difference is that in our processCollision function
    we work on 2 different structures, the bullet structure and our
    structure but bullet never gets the info from our structure past the
    first contact

TO DO : change all the sim_manifold struct uses with the native bullet
manifold structure or find a way for our particular structure to be
compatible with bullet's structure

TO DO : find a way to pick 4 points out of the 36 generated that cover
the maximum area of the object

#### Expected result

The expected result is to allow the user to apply different forces to
arbitrary objects and be able to simulate as accurate as possible the
real world physics. The forces will be applied using an Archer GUI
command and the user will be able to visualize the transformations the
object is suffering in real time. Adding these facilities to the BRL-CAD
program it will give the user the possibility to simulate a real world
physics through the software.