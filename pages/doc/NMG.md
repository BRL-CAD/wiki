[category:tutorials](category:tutorials.md)

![](img/Nmg-wiki-tutorial-screenshot.png)

BRL-CAD contains a powerful Non-Manifold Geometry (NMG) mesh primitive.
NMG objects are usually created through geometry importers, or through
commands like "facetize" that create NMG from other geometry. However,
using the low-level database commands "get" and "put", it is possible to
manually create and edit NMG objects.

BRL-CAD's internal representation is similar to the Radial Edge data
structure described in <http://www.scorec.rpi.edu/REPORTS/1986-1.pdf>.
However, the textual representations that can be created and viewed with
"get" and "put" are somewhat simpler; this representation deals with
vertices, faces, and loops. Loops, in effect, are closed curves that
form boundaries for faces, and a face can have multiple loops. For
example, a face with a hole in it might have two loops, with one
defining each boundary: one for the outer "edge" and one for the inner.

To obtain a sample of the way that nmgs are created, these commands
create a ramp structure with another primitive and then convert it with
the "facetize" command:


mged&gt; make ramp_arb arb6

`mged> facetize -n ramp_nmg ramp_arb`
`mged> get ramp_nmg`
`nmg V { { 1.500499999999999944932938 -0.5003749999999999031885523 1.500375000000000014210855 } { 1.500499999999999944932938 1.500624999999999875655021 1.500375000000000014210855 } { -0.500499999999999944932938 0.5001250000000000417443857 1.500375000000000014210855 } { 1.500499999999999944932938 -0.5003749999999999031885523 -0.5006249999999998756550212 } { -0.500499999999999944932938 0.5001250000000000417443857 -0.5006249999999998756550212 } { 1.500499999999999944932938 1.500624999999999875655021 -0.5006249999999998756550212 } } F { { 3 5 1 0 } } F { { 3 0 2 4 } } F { { 5 4 2 1 } } F { { 3 4 5 } } F { { 0 1 2 } }`

or, formatted, more nicely,

`nmg`
`V {`
`  { 1.500499999999999944932938 -0.5003749999999999031885523 1.500375000000000014210855 }`
`  { 1.500499999999999944932938 1.500624999999999875655021 1.500375000000000014210855 }`
`  { -0.500499999999999944932938 0.5001250000000000417443857 1.500375000000000014210855 }`
`  { 1.500499999999999944932938 -0.5003749999999999031885523 -0.5006249999999998756550212 }`
`  { -0.500499999999999944932938 0.5001250000000000417443857 -0.5006249999999998756550212 }`
`  { 1.500499999999999944932938 1.500624999999999875655021 -0.5006249999999998756550212 }`
`}`
`F { { 3 5 1 0 } }`
`F { { 3 0 2 4 } }`
`F { { 5 4 2 1 } }`
`F { { 3 4 5 } }`
`F { { 0 1 2 } }`

The "nmg" at the beginning is the type of what follows; the actual
information is just a list of vertices and a number of face statements.
Each face is represented by a list that contains any number of loops;
each loop is a list of vertices. The vertices are referred to by their
index into the V list.

To create a new nmg structure, use "put" instead of "get"; the first
argument to "put" should be the name of the new object. For example, to
create a similar ramp structure named "ramp_nmg2" but with different
coordinates, you'd do this (it appears that the vertices must be
specified in clockwise viewed from the outside order within each loop;
otherwise, mged crashes):

`mged> put ramp_nmg2 nmg V { { 0 0 0 } { 1 0 0 } { 0 1 0 } { 1 1 0 } { 0 1 1 } { 1 1 1} } F { { 0 2 3 1 } } F { { 3 2 4 5 } } F { { 0 1 5 4 } } F { { 0 4 2 } } F { { 1 3 5 } }`

As a slightly more complex example, consider making a box. The box
should have a vertex V for each of its corners, so the V-list should
look like
`{ { 0 0 0 } { 0 1 0 } { 1 1 0 } { 1 0 0 } { 1 0 1 } { 0 0 1 } { 0 1 1 } { 1 1 1 } }`.
It should have six faces, one for each face of the cube, but these faces
are simple ones with only one loop, since none of the faces have holes.
The bottom face is composed of `{ { 0 1 2 3 } }`, the top one of
`{ { 4 5 6 7 } }`, and the sides are given by `{ { 0 1 6 7 } }`,
`{ { 1 2 5 6 } }`, `{ { 2 3 4 5 } }`, and `{ { 3 0 7 4 } }`; this means
that the final command to create it is:

`mged> put box_nmg nmg V { { 0 0 0 } { 0 1 0 } { 1 1 0 } { 1 0 0 } { 1 0 1 } { 0 0 1 } { 0 1 1 } { 1 1 1 } } F { { 0 1 2 3 } } F { { 4 5 6 7 } } F { { 0 1 6 5 } } F { { 1 2 7 6 } } F { { 2 3 4 7 } } F { { 0 5 4 3 } }`

This yields the following object: (an MGED wireframe, from the az35,el25
view setting):
![](img/Nmg-wiki-tutorial-box-mged-screenshot.png)

Another more complex example is to create a box with a hole through it.
Much of the command is the same as the one above for creating a plain
box; the first thing to do is to add the necessary vertices to the `V`
list. For the lower face, `{ 0.25 0.25 0 }`, `{ 0.75 0.25 0 }`,
`{ 0.75 0.75 0 }`, and `{ 0.25 0.75 0 }` are the necessary vertices; for
the upper face, these are `{ 0.25 0.25 1 }`, `{ 0.25 0.75 1 }`,
`{ 0.75 0.75 1 }`, `{ 0.75 0.25 1 }`. Changing the first two face
statements from above to
`F { { 0 1 2 3 } { 8 9 10 11 } } F { { 4 5 6 7 } { 12 13 14 15 } }`
makes the faces have the necessary cutouts. Four faces must be added to
form the sides of the hole through the box; these are
`F { { 8 12 13 11 } }`, `F { { 11 13 14 10 } }`, `F { { 10 14 15 9 } }`,
and `F { { 12 8 9 15 } }`. The final command with all of this is:

`mged> put box_with_hole_nmg nmg V { { 0 0 0 } { 0 1 0 } { 1 1 0 } { 1 0 0 } { 1 0 1 } { 0 0 1 } { 0 1 1 } { 1 1 1 } { 0.25 0.25 0 } { 0.75 0.25 0 } { 0.75 0.75 0 } { 0.25 0.75 0 } { 0.25 0.25 1 } { 0.25 0.75 1 } { 0.75 0.75 1 } { 0.75 0.25 1 } } F { { 0 1 2 3 } { 8 9 10 11 } } F { { 4 5 6 7 } { 12 13 14 15 } } F { { 0 1 6 5 } } F { { 1 2 7 6 } } F { { 2 3 4 7 } } F { { 0 5 4 3 } } F { { 8 12 13 11 } } F { { 11 13 14 10 } } F { { 10 14 15 9 } } F { { 9 15 12 8 } }`

This produces the following wireframe when drawn in MGED using the
az35,el25 view setting:
![](img/Nmg-wiki-tutorial-box-with-hole-mged-screenshot.png)
