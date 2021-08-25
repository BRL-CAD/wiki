## Project

### Non-vacuum gravity simulator

The current simulation available in BRL-CAD has not been developed in
depth, and is quite limited in its implementation. It can currently only
simulate very basic situations in vacuums. For this project I aim to
vastly improve this area by adding additional features such as variable
fluid for the object to fall through, a variable ground surface which
would allow simulating reactions from it through use of the coefficient
of restitution and other such formulae. Another feature would be to
allow for variable gravity, since gravity is weaker at greater distances
from the Earth, and indeed other large masses. After some thought and
looking at the available physics engines I have opted to go with the
Bullet engine. The reasons for this include its superior capability to
constantly check for collisions, combined with its relatively fast
simulations compared to, say, ODE and it is already integrated to some
extent into BRL-CAD. All my work would follow on from what has been done
by Abhijit, who created the current simulation systems during his
ESA-Summer of Code project. During improving this project I would make
sure to keep in mind compatibility between both MGED and Archer, to make
sure it is ready for the future of BRL-CAD.


So there are 3 clear features I want to implement into the simulation
system, fluid dynamics, ‘rebound’ mechanics and improved gravitational
system.

#### Fluid Dynamics

This is an area with hugely far reaching possibilities, with CFD
potential in the long run, and open source libraries such as OpenFVM
being available, however to begin with I intend to keep this relatively
simple. To start with, this would consist of having a user-defined
fluid, or more specifically if desired, the density of the fluid. From
this the software would be able to calculate an estimate of the drag
coefficient and thus drag which will result in a more correct
representation in the simulation if a user wished to see the position of
an object at certain time intervals. I would also want to add the
functionality for a variable fluid as this would allow the density to
increase say if an aircraft was simulated to drop from 30,000 feet. This
would involve the creation of several functions that would include
calculating the surface area of the object facing perpendicular to the
firm plane, a function to either calculate or retrieve (if it is a
standard shape) the value of its coefficient of drag, which would then
be passed to a larger set of functions and it would more or less
directly counter gravity. This does open up another potential path of
functions, for moments. Now, whilst calculating the drag on the surface
of the object is a good start, there is much more potential that would
allow for the calculation of the rotation of the object as it falls
through space, by resolving the forces caused by drag. This would of
course mean that the centre of gravity of the object will need to be
found, and that is relatively easy to do, but will depend on how complex
the shape is and may require some estimation. An issue with objects
rotating is that they will create variable drag, and whilst the software
will be able to calculate the drag at every point in the simulation,
there will be a loss in accuracy since the fluid will be assumed to be
moving at a user pre-defined velocity, and this won’t be affected by the
motion of the object as it realistically should be.

#### Collision Physics

There is already some implementation of this within the simulation,
however it is in a very early stage and I feel has much more potential
than it currently uses. As I briefly mentioned I would like to allow for
variable materials. Expanding further upon this, and taking into account
the makeup of the Earths’ surface, I would very much like to implement
some water physics. By that I mean for the software to be able to
simulate the effect of dropping an object from high atmosphere into
water, and allowing for forces such as upthrust as this would allow for
simulating say, satellites dropping from orbit. The collision physics
would need a lot of testing to ensure it could hope with very high
velocity impacts (e.g. a comet, just in case).

#### Improved Gravitational System

The simulation currently can certainly handle gravity, however only at a
basic level of things falling to the ground. As far as I can tell, it is
very lightly implemented, just passing a value of -10 for gravity to the
bullet class, this would be replaced by a separate function that would
take into account the gradual increase of the acceleration due to
gravity since at 500km away from Earth gravity is a fair amount smaller,
and simulating that distance would make a noticeable difference between
a standard value of 9.81 and the true values. I would want to improve
this to take into account other user specified masses. For example, if
something were to drop from orbit, there would be a sizable
gravitational force upon it from the Earths’ moon. Furthermore, if we
are simulating several large objects, to increase accuracy it would be
ideal for the simulation to take into account the gravitational pull
each object will have on the others, however minor it is. This function
would need to be called repeatedly, to calculate the gravity for each
step of the simulation to allow for it to constantly change. There will
be some overhead will this of course, however the calculate is very
simple. It would vary however, depending on the Gravitational Constant,
which is different for different masses. This would be user input with
presets (Planets in the Solar System, and some others) available.

### Deliverables

A system that can calculate the drag resulting from a falling object, as
well as calculate rotation due to that drag.
A system that can consistently cope with any collisions with a surface
that takes into account the force exerted upon the object by the surface
and also allows for said surface to be water, in which the fluid system
will take over again.
A system that can calculate gravity at any distance from the surface,
which will also take note of the gravitational effect from other large
masses.
A method, either command line or GUI, that will allow the user to
specify as many options as is possible to allow for a simulation that is
suited to the users’ needs.

### Extra

BRL-CAD interests me because I have some background in CAD and modelling
work and I expect to be doing a lot more of it as the years progress on
my course and potentially in a working environment in the future. The
simulation project caught my eye specifically, as whilst I am interested
in several of the ideas, simulations are an area I like to use and would
be very interested in improving.

Whilst my knowledge of C/C++ are not as strong as I would like, I am
confident that I can learn a lot from this project and build my skills
up before the coding begins properly to a more than adequate level. I
believe that I have all the mathematical ability that I will need to
complete this project, including knowing how and where to use which
formula's. Naturally, this would help reinforce what I have been taught
which will be useful during exams and the coming years.

I would undoubtedly continue to work on BRL-CAD after this project is
complete, most likely on the simulation software as I still have several
ideas for improving that, ranging from full computational fluid dynamics
modelling to a fully featured fracture system.