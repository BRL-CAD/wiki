BRL-CAD provides facilities for representing geometry, but limited
capability for simulating effects on that geometry, such as gravity.
There are basic forward-kinematic animation facilities and rudimentary
joint rigging systems that can be used to simulate connectivity, but
they were predominantly designed for animations.

This task minimally involves integrating or implementing a simple rigid
body dynamics system that can be used for simulating gravity and basic
newtonian physics. We want to be able to "turn on" the system and have a
simulation take over. For example, you might model a scene with an
ambient gravity force, model a firm ground plane, model a box up in the
air, then turn on the simulation and watch the box fall to the ground
plane onto a flat face. The system will need to be driven from a single
time parameter so that frames can be rendered for animation and other
visualization purposes.

A third-party physics system (such as [the Open Dynamics Engine
(ODE)](http://www.ode.org/) or [the Bullet Physics
Library](http://bulletphysics.org/)) can and should be used for this
project in leu of implementing one, but selection of such a system will
need to be discussed beforehand to ensure compatibility and
maintainability. MIT/BSD license is ideal.

# References

-   src/archer
-   src/librt

# Requirements

-   Strong familiarity with C/C++

# Past Efforts

-   [GSoC12](../Google_Summer_of_Code/2012.md)
