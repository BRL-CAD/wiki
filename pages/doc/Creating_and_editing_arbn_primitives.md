An **arbn** primitive is an arbitrary complex polyhedron bounded by N
three-dimensional planes.

Such solids are constructed by specifying N sets of plane coefficients
and distances, which collectively define the space \~outside\~ of the
solid. The coefficients define a vector whose normal is a plane parallel
to the face of the solid. The surface of the solid is at the specified
distance along this vector.

The distances may be negative and are used when a face lies on the
opposite side of the origin as the tip of its vector. An example is if
the left side of a box lies on the positive X axis. In this case,
because the left side is being defined, the vector points left
(coefficients -1 0 0), but since the point is on the positive X axis its
distance is opposite its vector and therefore negative.

Handled by: make in create
Arguments
Number of planes

xyz direction vector and distance for each plane

<!-- -->

Example
in arbn.s arbn 8 1 0 1 1 -1 0 0 1 0 1 0 1 0 -1 0 1 0 0 1 1 0 0 -1 1 0.5
0.5 0.5 1 -0.5 -0.5 -0.5 1

<!-- -->

Example with negative distance
in arbn2.s arbn 6 1 0 0 100 -1 0 0 -10 0 1 0 200 0 -1 0 -10 0 0 -1 0 0 0
1 1.5

...is equivalent to...

in rpp.s rpp 10 100 10 200 0 1.5