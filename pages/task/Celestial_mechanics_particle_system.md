BRL-CAD can be used to model items at a celestial scale, but there is no
system available in BRL-CAD for simulating body dynamics. For example,
you could accurately model the solar system, to scale, but you cannot
simulate their orbits automatically (e.g., for an animation).

This task involves integrating or implementing a system that can be used
for simulating basic celestial mechanics. One possible approach is to
implement a particle system where mass properties can be assigned to
objects and let the simulation drive position, velocity, and
acceleration changes over time. The simulation itself could be
integrated into BRL-CAD's Archer modeling environment as a plugin that
dynamically changes geometry (updating positions over time).

A third-party particle or dynamics system can be used for this project
in leu of implementing one, but selection of such a system will need to
be discussed beforehand to ensure compatibility and maintainability.
Something like [the Open Dynamics Engine (ODE)](http://www.ode.org/) or
[the Bullet Physics Library](http://bulletphysics.org/) can be used, but
a proper particle or celestial mechanics system such as
[libnova](http://libnova.sourceforge.net/) or
[changa](http://www-hpcc.astro.washington.edu/tools/changa.html) (which
is unfortunately license incompatible) will probably be more appropriate
given the physics involved. MIT/BSD license is ideal.

# References

-   src/archer
-   src/librt
-   src/librt/primitives/pnts
-   src/librt/primitives/ell
-   [1](http://en.wikipedia.org/wiki/Point_particle)
-

# Requirements

-   Strong familiarity with C and/or C++