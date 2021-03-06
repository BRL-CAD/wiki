# Overview

A solid of revolution can be described by its axis of revolution (point
& vector), an angle (-2\*pi, 2\*pi), and a 2D sketch coplanar with the
axis of revolution. The start and end surfaces will be planes, and a
positive angle is counterclockwise rotation. There are several options
for how to specify the start and end planes. Starseeker suggests using:

-   a vector 'r' such that <axis> x <r> = direction of revolution
-   an angle

In order to analytically solve for the ray/shape intersection points,
the sketch must be limited to splines of at most second order.

# Internal Representation

struct rt_revolve_internal:

-   point_t V3D;
-   vect_t axis3D;
-   point2d_t V2D;
-   vect2d_t axis2D
-   vect_t r;
-   fastf_t angle;
-   char \*sketch_name;
-   struct rt_sketch_internal \*sk;

*Questions:* Should the sketch be restricted to revolve about its
y-axis, or should I allow for an arbitrary point & axis defined in the
sketch plane (\*2D)? If yes, the sketch would undergo a
rotation/translation - is rotation/translation of a sketch already
possible? If it is possible, then restricting to the y-axis will not
limit the user.

# General Algorithms

## rt_rev_shot() - ray intersection

1.  If (angle != 2\*pi) check against the start and end surfaces.
    1.  Find the parameter values for the intersection of the ray with
        the start/end surfaces. These two plane intersections will give
        the bounds on the parameter for intersections. In some cases,
        there will only be an upper or lower bound.
    2.  Check if the plane intersection point(s) are inside the 2D
        sketch.
2.  For the revolved portion:
    1.  Flatten out the intersection to 2D (ignore theta): ray becomes
        hyperbola in the r-z plane (parameterized- use same variable for
        length along ray as length along hyperbola to keep mapping from
        3D to 2D)
    2.  Check the hyperbola's path against the 2D revolve outline. Find
        the parameter values at the intersection points.
    3.  Check the parameter value against the bounds determined in 1.1.

## rt_rev_norm() - surface normals @ hitpoint

1.  If the hitpoint is on the precomputed 2D revolve outline, the normal
    vector will lie in the r-z plane, and it will also be normal to the
    2D revolve outline.
2.  Otherwise, the hitpoint is on the plane at the start or end of the
    revolve, and the normal vectors for each plane can be stored to
    speed calculations.

## rt_rev_curve() - surface curvature @ hitpoint

1.  On the revolved portion (similar to toroid calculation):
    1.  Get the curvature in the r-z plane from the precomputed 2D
        revolve bounds.
    2.  Calculate the curvature in the z-theta plane from r.
2.  On the planes at the limits of the revolve, the curvature will be 0.

## rt_rev_plot() & rt_rev_tess()

plot() and tess() can be done using the same basic algorithm that the
toroids use, with some modifications:

1.  Use the precomputed revolve boundary instead of the ellipse/circle
    for the 2D shape to be revolved.
2.  Add +/- limits to the angle of the revolve.
3.  Add the planes at start and end of revolve (if angle != 2\*pi).

# Additional Features

## General Primitive or Combination

Add support for using a 3D primitive or combination as the basis of the
revolve.

## End Caps

This would keep the first half of the primitive or group being revolved
at the start plane, and add a copy of the primitive/group to the end. If
this was applied to a cone over 90 degrees, where the cross-section used
for the revolve was a circle, the result would be a frustum attached to
right angle pipe curve, with a cone at the tip.

## Complex End Conditions

This would create a partial revolve (angle &lt; 2\*pi) with a 3D shape
where the maximum outline does not fall in a r-z plane. A 2D example of
this is revolving an ellipse with focii at (4,1) and (6, -1) about the z
axis. For this case, the minimum radius and maximum radius do not occur
along the same plane. If the end cap method (above) was used, there
would be an abrubt transition from the ellipse to the revolved body.

This feature can best be implemented by using a sweep along a circular
path, because the sweep primitive will need to handle this end condition
for sweeping any other general 3D primitive. This approach minimizes
code duplication, and keeps the revolve primitive focused specifically
on revolving.