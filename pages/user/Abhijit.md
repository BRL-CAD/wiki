## ESA Summer of Code Project Proposal

### Non-vacuum gravity simulator for the BRL-CAD Solid Modeling tool

------------------------------------------------------------------------

#### About Myself

-   **Name:** Abhijit Nandy
-   **Mailing List ID:** abhijit.nandy@gmail.com
-   **IRC ID:** abhi2011

I am an international student (nationality Indian) in the second year of
the Computer Engineering programme at TU Delft, The Netherlands. I have
a computer science background and was working in the software industry
for three years from 2006 to 2009. After that I decided to pursue a
course in Computer Engineering to get acquainted with hardware
development. More details are present in my CV. Currently I have
finished my courses and thesis work and so I have free time on my hand
to devote 40 hours a week to the development of BRL-CAD.

#### Brief project summary

Currently BRL-CAD provides facilities for representing geometry, but has
limited capability for simulating physics effects on that geometry. The
facilities currently present were designed with animations in mind. The
proposal is to integrate rigid body dynamics using the Bullet Physics
Engine or the Open Dynamics Engine (ODE). Bullet is provided under the
zlib license while ODE is provided under both the BSD license and the
LGPL. Both engines provide a collision detection engine and a Newtonian
physics model. The exact physics engine to be used will be researched in
the first week (see Development timeline). The chosen engine’s collision
detection mechanism will be used to check for overlap of axis aligned
bounding boxes or the bounding sphere. If an overlap is detected more
accurate collision detection will be delegated to a custom collision
handler that may use the BRL-CAD gqa and rtcheck tools for precise
detection. Other collision handlers can be added if required in case
they are absent for any of the BRL-CAD primitives. After the collision
handling is tested to work correctly with the rest of the system,
support will be added for user specified forces apart from ambient
gravity. If time permits I intend to work on integrating and improving
the system for joining objects together as well(see Detailed project
description).

#### Detailed project description

The physics will be implemented as a command in the BRL-CAD Archer GUI.
This will be of the form:

Archer&gt; runphysics N

The parameter N is the number of simulation steps to run the physics.
After the user invokes this command, the Tcl code for the command will
call a C++ function containing the logic for doing the physics
simulation. The function can be of the form:

int ged_runphysics(struct ged \*gedp, int argc, const char \*argv\[\])

The following occurs in the C++ function which will be central to the
implementation:

-   The struct ged object that is typically passed to plugins will be
    used to build up the physics world in a btDiscreteDynamicsWorld
    provided by Bullet.
-   A Bullet collision shape will be inserted into the physics world
    corresponding to each object present in the struct ged. These are
    based on convex primitives such as btBoxShape, btSphereShape,
    btCylinderShape and they can approximate the BRL-CAD objects. The
    collision shapes will be constructed from BRL-CAD geometry
    information.
-   After this the force vectors requested by the user will be read
    either from the struct ged or using other LIBGED commands. These
    will be applied on the collision shapes in the physics world.
-   The physics world will then be stepped just once and the ged object
    positions will be set to the new positions using information from
    the Bullet btDiscreteDynamicsWorld.
-   The repositioning of objects in Archer happens automatically by the
    command wrapper, once the objects are modified using LIBGED
    commands.
-   The C++ function will then exit and control will return to Tcl.

The Tcl command wrapper will call the C++ function N times to obtain the
simulation result after N steps. As the object positions will be updated
on each call to ged_runphysics(), the user will be able to see the
scene’s objects animate in Archer.

Particularly with regard to Bullet, as that is the only physics engine I
have used so far, I am aware that it provides facilities for contact
tests \[2\] and callbacks using the contactTest and contactPairTest
queries. These can be accelerated using faster broadphase algorithms
such as btDbvtBroadphase or btAxisSweep3 which affects the speed of test
for overlapping AABBs \[3\]. Therefore real time updates should be
possible. Moreover there are facilities for more fine grained control
over the collision pipeline of Bullet, utilizing a custom class derived
from btCollisionDispatcher \[3\]. Custom collision detection algorithms
can be specified using btDispatcher::registerCollisionAlgorithm \[3\].

Physics engines also typically provide constraints such as point to
point, hinge and 6 degree of freedom constraints which can be used to
join objects together and improve the rudimentary joint rigging systems
currently present.

**Note**: The implementation will not rely on any polygonal mesh data as
BRL-CAD does not store a mesh for its primitives. Instead physics
objects for Bullet’s dynamics world will be created from other geometry
information e.g. radius and tire width can be used to make a bounding
cylinder for a tire.

#### Log

-   Nov 9th

1.  Sphere-Sphere case works :
    <http://imageshack.us/photo/my-images/406/forceb.png/>
2.  Wasnt unitizing the vector used to indicate the direction in which
    the ray should be shot using rt.
3.  Trying to improve convex-convex collisions now.

....but first videoz!

1.  Slow spheres: <http://www.youtube.com/watch?v=nrOtSd07rCY>
2.  Fast spheres : <http://www.youtube.com/watch?v=7cZesIJapF4>
3.  Seems like the summing normals in the overlapping region may need to
    be applied as the reaction force is not in the correct direction in
    both cases.
4.  Its dependent on the normal I give to Bullet with the contact pairs
5.  There are a number of ways to solve the case of objects striking
    each other while moving fast and interpenetrating too much(leading
    to very high reaction forces)
    1.  Measure the smallest air Gap between objects while shooting rays
        and when its smaller than a tolerance value, start generating
        'contact' pairs.
    2.  Reduce Bullet timestep, so objects are moved in smaller
        increments in each step.
    3.  Increase boundary of object by a tolerance factor, so that
        contact pairs are produced before objects actually
        interpenetrate. This may be non-trivial for arbitrary objects
    4.  Another way could be to step back the simulation by one step if
        there is too much penetration, this would be possible as the
        state of each object is stored after every iteration.

-   Nov 5th

1.  The box-box case appears to be stable with forces being applied to
    push them apart when they strike each other.
2.  It works purely on :

-   -   normals(direction of the linear velocity of the body),
    -   contact pairs generated on the surface of body B(i.e. whichever
        body is considered as B in a colliding pair, by Bullet), these
        are got by shooting a circular bunch of rays in the direction of
        the velocity and recording the points on body B's surface where
        the rays exit the body.
    -   depth of penetration of body B into body A, got simply as the
        distance between the entry point in body A and the exit point in
        body B

Note that all 'bodies' are actually BRL-CAD combinations comprised of
one or more solids.

1.  Currently I have tested a simple case as shown in this picture :
    <http://imageshack.us/photo/my-images/708/forceb.png/>
2.  Testing a more complex case with box-sphere now, where raytracing
    will be much more important to get the right contact points along
    the surface of the bodies.

-   Oct 29th

1.  Trying with the contact points again as calculating forces manually
    and relying on Bullet is not an optimal approach. When using contact
    pairs, Bullet calculates the appropriate force for us, so its best
    to use it.
2.  The contact pair approach works for the simple sphere-sphere
    collision case. Testing the box-box case now.

-   Oct 20th

1.  Adapting the collision logic to use forces instead of contact pairs.
    Simply \#adding contact points between objects does not seem to
    cause Bullet to apply reaction forces between bodies
2.  So now forces are applied through the center of the contact region
    and normal to the surface of either body, which should be enough to
    push them apart.
3.  Friction forces need to be applied parallel to the surface too,
    which needs to inserted ,otherwise we won't have balls rolling on
    planes.

-   Oct 16th

1.  Added contact processing callbacks to investigate the issue with
    forces not being applied after contact pairs between 2 objects are
    added to the physics world.
2.  Got rid of multiple linked lists which were put in to support
    varying lists of manifolds, but which turned out to be more of
    trouble than its worth

-   Oct 12th

1.  Finishing the logic for creating manifolds using rays shot in the
    direction of the positive X axis.

-   Oct 7th

1.  Grinding out memory leaks using valgrind !
2.  Lesson : when in doubt always free memory and cause a double free
    crash, better to be sure!
3.  Raytracer is properly recording overlap areas and hit regions now.

-   Oct 6th

1.  Hmm things getting even more interesting, it seems that there can be
    extremely thin overlap regions between objects which are resting on
    top of each other, down to 0.000001 m, so a plane with all the
    manifold points can be generated for such a case, as a cuboidal
    regions would be too small for the solvers to analyze
    accurately(need to verify this).
2.  Added code to actually shoot the rays now and record the overlap
    regions in a circularly linked lists, needs some debugging however.

-   Oct 5th

1.  Began writing a manifold generator based on raytracing. The rays
    will be shot only where broadphase collision detection finds AABBs
    overlaps
2.  This will allow higher accuracy with rays being shot in a 3D grid of
    higher granularity without sacrificing performance.

-   Oct 4th

1.  Added code to display manifold normals correctly.
2.  Figured out how to generate the normals based on the direction in
    which objects overlap. This will be required when generating the
    contact manifolds using raytracing.

-   Oct 3rd

1.  Contacts manifold are getting drawn and will help in reproducing
    them through raytracing.
2.  Corrected some code to position objects correctly and stopped
    creating bounding boxes every iteration as it has been causing
    issues.

-   Sept 30th

1.  Added code to display bounding boxes, recalculating the BB every
    iteration is causing boxes that have moved to stay bent in their new
    position as each ounding box is inserted as a new cube in the next
    iteration. This problem should disappear when contact points are
    calculated correctly.

-   Sept 25th

1.  Finished reorganizing the code to integrate raytracing. Ran into
    some issues with the positioning of objects after each physics
    steps, so had to revert to some older working copies.
2.  Basically at the beginning of each step I rebuild the world and
    after the simulation, I save the world transform and
    velocities(linear and angular) for initializing the next step.
3.  Each step has the bounding box for all objects in the scene
    calculated again as was originally planned.

-   Sept 16th

1.  On the other hand it seems better to add a new collision detection
    algorithm for box-box collisions.
2.  Bullet allows custom algos for each combination of colliding shapes.
    However we are interested only in the box-box case since all
    arbitrary shapes are represented by the btBoxShape collision
    primitive in Bullet. However manipulation of the contact points
    according to rt output should still allow correct behaviour of
    arbitrary shapes.
3.  Inserted some framework code for a basic rt based collision
    algorithm.
4.  The contact manifolds will be generated by rt, the algorithm will
    then insert them into the bullet collision pipeline.
5.  Hopefully forward dynamics will take off correctly after that.

-   Sept 15th

1.  Add callback for broadphase and narrowphase collision detection.
2.  May be possible to add contact points detected during raytracing
    overlaps.
3.  Wrote some tcl code to generate scenes automatically and raytrace
    them.

-   Sept 7th - Sept 14th

1.  Chugging along, now added code to retrieve bounding boxes from
    Bullet
2.  Now object activation states inside Bullet (idle or sleeping) are
    displayed through different colors on the boxes
3.  Wrote some initial code to shoot rays and add points to the bullet
    points cache.

-   Sept 4th - Sept 6th

1.  Not much coding done, was mostly going through the collision
    detection code in Bullet
2.  Almost done adding bounding box and object state colors for easier
    debugging in mged.
3.  Apparently a solution to arbitrary shapes is to remove all contact
    manifolds generated by Bullet and apply a force ourselves. Need to
    test the idea.

-   Sep 3rd

1.  Corrected object positioning code in mged

-   Sep 2nd

1.  Updated the code for the simulate command. Now objects fall "out of
    the sky"
2.  Finally reached the first milestone :
    <http://www.youtube.com/watch?v=SByoQQStH2s>

-   Aug 29th - Sep 1st

1.  Added regions and groups to the bounding box function
2.  Added code to pass regions from a model to bullet for the sim

-   Aug 22nd - Aug 28th

1.  Finished the bounding box function
2.  Modified CMake logic to compile the simulate command as a separate
    library
3.  Working on passing multiple objects from a Mged model to the
    simulation so scenarios like n balls on a billiard table can be
    simulated.

-   Aug 21st

1.  Compiled Bullet with libged and loaded its dynamic libs with mged.
2.  Ran a sphere dropping on a plane scenario and it gave the correct
    results
3.  Now updating it to translate the position of a sph in mged to the
    final position of the sphere, before passing the bounding box etc.

-   Aug 13th - Aug 20th

1.  Submitted a fix for Mged. The issue was that a body may be in edit
    mode when it killed. Then accepting any tranformations done on it
    can result in a Segmentation fault due to the NULL illump pointer.
    titles.c was changed.
2.  Committed changes for the simulate command in Mged.
3.  Modified top level CMakelists.txt to link to Bullet libs.
4.  Had an issue accessing the Bullet headers, but that was due to a
    non-standard install location of Bullet. Now trying to link to
    Bullet libs.
5.  Tried using db_functree() to load missing primitives into the
    in-mem database instance, but the tree representing the primitives
    are not available, so trying to find a way to convert the
    rt_db_internal to union tree.
6.  More code reading.

-   Aug 12th

1.  Mostly read the extra articles in the BRL-CAD documentation
2.  Tried to extend the bounding box code to use rt_comb_internal
    instead of rt_gettree()

-   Aug 11th:

1.  Submitted patch 3390331 for BB of primitives.

-   Aug 10th:

1.  Finished the code for the bounding box. It works now for basics
    shapes.Should be extended to work for regions and groups.

-   Aug 9th:

1.  Mostly reading libwdb and librt code and finishing the function
2.  Read some of the tutorial articles on BRL-CAD

-   Aug 8th:

1.  Mostly reading code and documentation.
2.  Started working on function for librt which calculates the bounding
    RPP when a shapes, region or group is passed in the database
    internal format struct rt_db_internal.

-   Aug 7th:

1.  Figured out how to transform objects to their new orientations and
    positions now in Mged !. The plan is to now move geometry in a model
    using the output transformation matrices of a physics sim. However
    mged draws the object only when the command is finished, so the
    command needs to be repeatedly called for multiple steps, to see the
    object animate.
2.  Changed the runphysics command to "simulate" to imply more general
    usage based on brlcad's suggestion.
3.  Working on a wrapper for the C++ based Bullet physics engine code to
    be called from the simulate.c file.
4.  Started maintaining daily logs

-   Aug 5th - Aug 6th:

1.  Inserted a runphysics command in Mged.
2.  Working on moving objects using matrix transforms inside Mged
3.  Reading principles of effective modeling and going through code in
    librt.
4.  Downloaded and compiled Bullet to make sure its installed and
    working.

-   Aug 3rd - Aug 4th:

1.  Finished most of the tutorials and articles for BRL-CAD
2.  Worked through the Interactive Ray Tracing using NIRT guide to get
    familiar with ray tracing.
3.  Converted the bounding box program to use librt functions only.

-   Aug 1st - Aug 2nd:

1.  Compiled BRL-CAD on OpenSUSE 11.4 using debugging options
2.  Went through code in libged especially get_obj_bounds.c
3.  Finished a stand alone program based on the very high level libged
    for getting the bounding box of arbitrarily shaped geometry.

#### Updated Development Time line(Nov 9th)

-   The plan currently is to test the collision pair generation logic
    with as many convex shapes as possible

<!-- -->

-   Then move on to concave-convex collisions
-   Finally introduce multiple manifolds for concave-concave collisions
-   Targeting end of November.

#### Expected Result and eventual benefits for BRL-CAD

The expected result is to allow the user to model an object such as a
sphere or a box and apply forces on them. The forces can be gravity, but
will also allow the user to specify other additional forces to be
applied during the simulation. The user can then “turn on” the physics
using a simple command. The command allows the user to specify the
number of physics steps as well. After the simulation begins the user
will be able to see the object move in the GUI as the physics is
updated. As time permits accurate material properties can be allowed to
be specified and will be used to affect object collisions during the
simulation. The system will allow frames to be captured during the
simulation for video playback later on. Adding accurate physics to
BRL-CAD will expand the scope of its usage allowing users to simulate
and test concepts within the software. It provides an exciting addition
to a powerful piece of software.

#### References

1.  Bullet Physics:
    <http://bulletphysics.org/mediawiki-1.5.8/index.php/Bullet_User_Manual_and_API_documentation>
2.  Bullet custom collision callbacks and triggers :
    <http://bulletphysics.org/mediawiki-1.5.8/index.php/Collision_Callbacks_and_Triggers>
3.  Bullet User Manual:
    <http://code.google.com/p/bullet/source/browse/trunk/Bullet_User_Manual.pdf>
4.  Open Dynamics Engine: <http://www.ode.org/>