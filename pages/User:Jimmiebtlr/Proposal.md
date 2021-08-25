Jimmie Butler
jimmiebtlr@gmail.com
jimmiebtlr

<h1>

About Me

</h1>
<h2>

Physics Experience

</h2>

When I first started at Colorado School of Mines I planned on majoring
in physics, I was a teachers assistant for physics 1 at this time.
Throughout my time until I decided I in fact wanted to major Computer
Science, I took the following pertinant classes, Classical Mechanics,
and Advanced lab.

<h3>

Classical Mechanics

</h3>

This class covered nearly everything this project would entail (from a
physics perspective). This included relativistic motion, lagrangian
dynamics, some error calculation, and basic programming.

<h3>

Advanced Lab

</h3>

This class had a very heavy emphasis on error calculation.

<h3>

Thermal Physics

</h3>

This class covered everything to do with thermodynamics from the
microscopic to the macroscopic.

<h2>

Programming Experience

</h2>

Now that I have switched to Computer Science I have taken or am
currently taking the following courses Software Engineering, Computer
Organization, Operating Systems, Scientific Computing, Algorithms, Data
Structures.

<h3>

Software Engineering

</h3>

This class is primarily focused on team development, using subversion,
with an agile background.

<h3>

Computer Organization

</h3>

This class focused on computers at the hardware level, giving a basic
view of how machine numbers and optimization work.

<h3>

Operating Systems

</h3>

This course focuses on memory handleing, as well as rounding off the
subjects covered in Computer Organization.

<h3>

Scientific Computing

</h3>

Scientific computing is completly based around the concept of reducing
or elemenating error due to machine numbers in scientific calculations.

<h3>

Algorithms

</h3>

Algorithms is a course which teaches how to implement and analize your
own home rolled algorithms and how to analyze fellow programmers
algorithms.

<h3>

Data Structures

</h3>

Which data structure is most effecient for which use case, and how would
I implement my own? Problem solved.

<h1>

Brief project summary (&lt;500 words)

</h1>

Non-vacuum gravity simulator
Simulate falling to a planet from a known starting point, knowing
atmospheric composition and planets mass, as well as geometric shape and
density function of the falling object.

<h1>

Detailed project description (&gt;500 words)

</h1>

The starting point will be to implement an iterative loop which takes
into account all forces until the object reaches at or below ground
level, at which it will interpolate to find end conditions.

Air resistance would have to be calculated not only linearly but also
rotationally, A target accuracy, or otherwise sane defaults should be
taken into account.

<h2>

Basic Features

</h2>

Calculate the gravitational strength at a set point in time, move the
object in the direction of its velocity.

<h2>

Air Resistance

</h2>

Air resistance would need to take into account torque on the object as
well as the usual linear drag, i.e. an arrow would tend to fall tip down
to the planet, yet a baseball could rotate violently. This section could
also be used to determine interactions on material changes i.e. hitting
water while falling. This would likely be implemented as a separate
program.

<h2>

High speed objects

</h2>

Take into account an object falling on the order of magnitude of c.

<h2>

Thermal Conversion

</h2>

How much energy is expended to thermal energy, make estimates of end
temperature? This would likely be similar to the air resistance section
and implemented as a separate program.

<h2>

Constraints

</h2>

Use Lagrangian mechanics to determine motion of a falling object in
relation to itself. This could become a large portion of the project and
would likely be its own program, taking in forces constraints, and the
object.

<h2>

Bending Light

</h2>

Should be able to be implemented through the implementation of the High
speed objects section.

<h2>

Optimization

</h2>

This project would take into account what the starting parameters are in
order to determine what algorithm to use i.e. falling 10 feet on earth
with a moderate allowance of error could be done assuming constant
atmospheric density and gravity. Whereas an object falling from several
miles up would need to take into account the atmospheric density and
changing gravitational strength.

<h2>

Error

</h2>

Any potential outputs would need their own error calculations, but
perhaps more importantly is to keep track of error from machine number
use. Using a double is clearly preferable in nearly all cases, but even
that can have large amounts of error if ignored.

<h2>

Using Bullet Physics engine

</h2>

Bullet is intended primarily for realtime physics simulation, and as
such may be applicable in cases where high amounts of error are
acceptable (from a scientific perspective), or in the case of quick
previews/realtime rendering.

<h2>

Using Open Dynamics Library

</h2>

Another Game engine with the same constraints against the accuracy of
the simulation.

<h2>

Interesting Features

</h2>

After implementing calculations for the high speed objects section, the
correct configuration should yield an answer to gravitational lensing.

<h2>

Implementation

</h2>

A new anim file, which would call the physics engine for a path that the
objects should take, and which at that point would render it for the
user to see.

<h1>

Links to any code or algorithms you intend to use

</h1>

For Air Resistance
<http://en.wikipedia.org/wiki/Drag_(physics)>
For fast objects
<http://en.wikipedia.org/wiki/Special_relativity>
For motion of complex objects.
<http://en.wikipedia.org/wiki/Lagrangian_mechanics>

<h1>

Deliverables

</h1>

Constant gravity constant atmospheric density simulation simplistic air
resistance
Varying gravity constant atmospheric density simulation simplistic air
resistance
Varying gravity varying atmospheric density simulation simplistic air
resistance
Varying gravity varying atmospheric density simulation complex air
resistance (take rotation into account)

<h1>

Development schedule

</h1>

May 15 - May 30
-Get a better feel for BRL-CAD and interfacing with it, as well as
implementing a dragless falling object in three dimensions.

June 1 - June 15
-Take into account air resistance and rotation.

June 15 - June 30
-Work on an error management system, and optimizations.

July 1 - July 15
-Take into account Non-Newtonian speeds.

July 15 - July 30
- Basic Thermal Calculations, extensive Refactor.

August 1 - August 15
-Non-Newtonian entrance speeds, basic fluid dynamics integration
(falling through water or striking it)

<h1>

Time availability

</h1>

-4 week Field session ( Should be able to work \~40 hour weeks )
-Rest of summer free.

I am applying to GSOC with BRL-CAD because it pertains to several area's
I'm interested in, namely physics and 3D graphics. More importantly
however is that it is a needed open source alternative which will
further both the education of future generations, and also a valueable
asset to the Engineering world.

I would like to work with BRL-CAD for GSOC because I feel I can bring my
knowledge of physics and programming to aid the developement.

<h1>

Anything Else

</h1>

I use nearly exclusivly open source software and would like to become a
permenant member of the open source community.