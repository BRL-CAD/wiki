# Automatic Polygonal Mesh Healing

## Existing features

Removal of isolated and duplicate vertices in rt_bot_condense() and
rt_bot_vertex_fuse() functions in src/librt/primitives/bot/bot.c
Removal of dangling edges and and decimation of edges by removing the
faces that contain that edge, the edges that those faces contain and
changing references of one vertex of the edge to the other all functions
in decimate.c in src/librt/primitives/bot Fusing of equivalent faces in
rt_bot_face_fuse in src/librt/primitives/bot/bot.c

## Changes that could be incorporated in the existing code

The current code uses bin sorting to check for duplicate vertices. While
it is true that it works in O(n) time on an average, the worst case
complexity is O(n²). This might happen when all the vertices have the
same x-coordinate. To optimise this, an AVL tree can be used to store
the vertices and check if any vertex that is yet to be checked is
equivalent to (is within the merge tolerance of) any existing point.
This method works in O( n\*logn) on an average.

In the existing bot_edge structure, the faces containing it can be
added as well. This functionality will be used when we check for
singular vertices and while removing redundant elements while checking
for overlaps in the mesh. Without this topological information of face
adjacencies, if we need to check for adjacent faces, O(n) time will be
required. But with it being set, it will be reduced to O(1).

## Detailed Description of the Project:

**Features to be added (inclusive of tasks to be done if time
permits):**

### Removal of gaps and T-joints

Two approaches will be used - Zippering and Stitching. Both methods will
be implemented and which method to use will be decided based on a
tolerance for small and large gaps (user inputs). Stitching is used when
the gaps are slightly larger - when they are small enough to be gaps but
not large enough to be holes.

It is easy to detect boundaries of polygonal chains; they can done
through the presence of free edges (there is support for this in the
existing bot_edge structure). When there is any vertex/edge close to it
within the merge tolerance (and not inside it) - zippering or stitching
can be performed based on the tolerance.

**Subdivisions:**

**1. Zippering:**

We identify the the boundary chains of the mesh. For all the boundary
vertices, we find the nearest boundary edge that is non-incident to the
vertex. If an orthogonal projection of the said vertex on the found edge
is possible, the edge is stored as the paired feature. Else, the nearest
vertex of the edge is stored. For each of the feature pairs, the
distance between them is computed and stored as an error measure. Then,
all the feature pairs are sorted according to that error measure and
stored in a priority queue. We pop the the feature pair with the least
error measure. If the feature is a vertex, vertex contraction is
performed. Vertex contraction: If the BoT has mode surf, plate or
plate_nocos, we just find the midpoint of the line connecting the
vertices and place both the points there. If the mode is volume, we find
the midpoint of the line formed by the intersection of the two
tangential planes at both the boundaries. This is the vertex that the
initial two vertices are moved to. Else if the feature is an edge, edge
contraction is performed. This is the case of T-joints. The boundary
vertex is projected on to the said feature pair (the edge). The triangle
which contains the edge is split at that vertex. And then vertex
contraction of the boundary vertex and the projected vertex is done.
This method works for all the BoT modes.

Note: It will be taken care not to introduce any singular elements at
this stage

**Pseudo code:**

**ZIPPER_GAPS (PQUEUE):**

`Vertex V ←POP_MINIMUM (PQUEUE)`
`Feature F ← NEAREST_FEATURE (V)`
`if f is a vertex then`
`     VERTEX_CONTRACTION (V, F)`
`else`
`   VERTEX_EDGE_CONTRACTION (V, F)`
`EdgeSet E ← MODIFIED_EDGES`
`for all e ∊ E do`
`   for all v ∊ {CORRESPONDING_FEATURES (e)} do`
`       MAINTAIN_CORRESPONDENCES (v)`
`       REINSERT (v)`
`   end for`
`end for`

Where, **ZIPPER_GAPS (PQUEUE)**zippers the pair with the least error
distance

**POP_MINIMUM (PQUEUE)**pops the element with minimum error distance
from the priority queue PQUEUE.

**NEAREST_FEATURE (V)**gives the nearest feature pair of the vertex V.

**VERTEX_CONTRACTION (V, F)** and VERTEX_EDGE_CONTRACTION (V, F)
perform contraction of the the vertex V with its feature pair F.

**MODIFIED_EDGES ()**returns the set of all edges that are modified
after the contraction routines.

**CORRESPONDING_FEATURES (e)** returns the set of all vertices whose
feature pair the edge e (from the modified set) is.

**MAINTAIN_CORRESPONDENCES (v)** updates the feature pair of the vertex
v after the modification of the edges.

**REINSERT (v)** reinserts the vertex v into PQUEUE.

**2. Stitching:**

We have two input polygonal chains that are within the tolerance (for
gap stitching). We start with one of any chain and merge them as if they
were sorted lists. In each step we have pointers to the current vertex
on each of the chains (vertices - u and v) and we advance the pointer on
one of the chains according to some advancing rules, say to vertex w.
Now we make a triangle uvw, unoriented (if the rest of the mesh is
unoriented) or with orientation that is same as the rest of the mesh (CW
or CCW). When we reach the last vertex on one chain we advance the
pointer only on the other chain. We terminate when we have reached the
last vertices on both the chains.

**The advancing rule:**Whichever triangle has the least perimeter, the
pointer is advanced on the chain whose edge is present in the
above-mentioned triangle. Formulating this:

This advancing rule has been seen to give the best results.

**Pseudo code:**

**STITCH_GAPS (MESH_A, MESH_B):**

`//MESH_A and MESH_B denote the boundaries of the two meshes to be stitches (essentially a sequence a vertices)`
`u ← STARTING_VERTEX (MESH_A)`
`v ← STARTING_VERTEX (MESH_B)`
`while both meshes haven’t reached their terminal vertices`
`   u′ ← NEXT_VERTEX (MESH_A, u)`
`   v′ ← NEXT_VERTEX (MESH_B, v)`
`   if PERIMETER ( u, u’, v) < PERIMETER ( u, v, v’ ) then`
`       MAKE_TRIANGLE ( u, u’, v)`
`       ADVANCE_POINTER ( MESH_A, u)`
`   else `
`       MAKE_TRIANGLE ( u, v, v’ )`
`       ADVANCE_POINTER ( MESH_B, v)`
`while MESH_A has vertices left`
`   MAKE_TRIANGLE ( u, u’, v)`
`   ADVANCE_POINTER ( MESH_A, u)`
`while MESH_B has vertices left`
`   MAKE_TRIANGLE ( u, v, v’ )`
`   ADVANCE_POINTER ( MESH_B, v)`

Where, **STARTING_VERTEX (MESH)** returns the starting vertex in the
sequence of vertices in MESH.

**NEXT_VERTEX (MESH, a)** returns the vertex after a in the sequence.
MESH

**PERIMETER ( a, b, c)** returns the perimeter of the triangle formed by
the three vertices a, b, and c.

**MAKE_TRIANGLE (a, b, c)** adds the triangle formed by the three
vertices to the list of faces.

**ADVANCE_POINTER (MESH, a)** updates the current vertex pointer from a
to the next vertex in MESH.

### Removal of overlaps:

Clipping one mesh against another and removing small triangles formed if
any. Overlaps are detected by checking if there are any vertices/edges
close to a boundary vertex within the merge tolerance (and inside the
boundary).

**Steps involved:**

**1. Removal of redundant surfaces of the mesh:**

General idea is to eat away at both the mesh boundaries until the two
meshes just meet. We repeat the process of redundancy removal until both
the meshes in consideration (say, mesh A and mesh B) are unchanged.
Redundancy checking done through the nearest_on_mesh(P, d, M) routine,
which returns the nearest point on mesh M to the point P within a
distance of d, or nothing if no such point exists. This function will be
written.

**2. Clipping one mesh against another:**

The next step is clipping mesh A against the boundary of mesh B. We
introduce new vertices on the boundary of mesh B where edges of the
boundary triangles of mesh A intersect it. The set of new vertices added
and the existing boundary vertices of mesh B form the final vertices of
the mesh boundary between the meshes A and B. The boundary triangles of
mesh B are split at the new vertices. Degenerate triangles might be
introduced (which will be solved later). The region of the boundary
triangles of mesh A inside the boundary of mesh B is discarded (clipped
away) and the region outside this boundary is retained. The portion of
mesh A that is retained can be triangulated using the stitching routine,
that has already been discussed. Any degeneracies introduced will be
handled later.

A bag of triangles of created out of the retained portion in mesh A and
it can be combined with the rest of the mesh using the rt_bot_merge
function in src/librt/primitives/bot/bot.c

**3. Removal of the small triangles introduced during clipping:**

This will be done as a part of the degeneracy removal.

Adapting this algorithm to 3 dimensions is easy. What we do is, we
thicken the mesh boundary of mesh B. A wall runs around the mesh
boundary which is roughly perpendicular to the mesh at all points. The
wall is a collection of four triangles at each edge E. To find the
intersection, see where the boundary of mesh A intersects the wall.
Project this point onto the edge E. The rest of the algorithm is same as
what is mentioned above.

### Triangulation of large holes:

Simple and ring holes (complex). A simple hole is a hole of any shape
with only one boundary loop. A ring hole contains at least two
peripheral loops.

Hole-filling algorithms should possess the following properties: 1. Able
to cover an arbitrary hole for any model (robustness) 2. Capable of
filling large holes in a reasonable amount of time (efficiency) 3.
Enable the patched surface to match the missing geometry well
(precision)

**Procedure for simple holes:**

**1. Detecting the hole boundary:**

To check if a vertex is a boundary vertex, we check the number of 1-ring
vertices and 1-ring edges. If the two numbers are not equal, then it is
a boundary vertex. When we get a seed boundary vertex, we trace along
the path of the boundary edges. If we get a loop, we’ve identified a
hole. In this manner, all holes can be identified.

**2. Using the Advancing front algorithm to create the mesh:**

The situations are divided into three cases, based on the minimum angle
(say, ɑ) between two adjacent edges of a free element (in a closed
loop):

\(i\) ɑ ≤ 75° - Make a triangle out of the two edges of the free
elements.

\(ii\) 75° &lt; ɑ ≤ 135° - Make two equilateral triangles out of the two
free elements’ edges. The two normal vectors are obtained by averaging
the common vertex and the vertex at the other end of the edge in the
said triangle. These normals are obtained by averaging the 1-ring
vertices of each vertex. The two new nodes that are formed are averaged
and merged. Whenever any new node is added, it is checked whether this
node is within the tolerance of any other existing node, and if it is,
it is merged with that node. If not, no action is performed.

\(iii\) ɑ &gt; 135° - Make two equilateral triangles corresponding to
the two free elements’ edges.

**Complex/Ring holes:**

Two approaches can be taken.

\(i\) Disregard the island patch and treat it as a simple hole, but this
approach reduces fidelity.

\(ii\) Keep the island patch and mesh only the missing parts.

\(a\) This could be done by identifying corresponding elements on the
inner and the outer loop and finding the shortest bridge between the two
but it is a specific case.

\(b\) Another approach could be to use the AFM technique to mesh until
the triangles being added just overlap with the existing island meshes.
Then we use the technique which was mentioned for overlaps, where we
clip the newly added mesh with the existing mesh.

Which method to employ will be decided based on the number of island
meshes and the presence of corresponding vertices on the inner and outer
loop, after discussions with the mentor.

### Removal of degenerate faces (will be completed if time permits):

User input: Face factor and tolerance edge length.

A triangle is labelled degenerate if it has an angle either too acute (≤
∊)- needle, or too obtuse( ≥ π - ∊) - cap. Cap and Needle:

Done by element reconstruction algorithm - nodal merging and edge
swapping (to improve the overall quality of the mesh). Edge swapping
done by changing the connectivity of the common edge between the two
connecting triangles. Any element with edge lengths lesser than that
will face removal or reconstruction. If the face factor of the element
is less than the user input, it will undergo removal by nodal merging.
If not, it undergoes edge swapping.

E is the equilateral factor a triangle. A triangle with E = 0 is an
equilateral triangle. The maximum value of E is ⅔ ², which is also the
most undesirable value. Thus, we put that value as the constant while
calculating the shape factor, f.

### Manifold connectivity (will be completed if time permits):

**Criteria for manifold surfaces:**

a\. Every edge is shared by exactly two faces (absence of singular
edges)

b\. Every vertex is surrounded by a single cycle of faces and edges
(absence of singular vertices): These could be formed by duplicate
vertices reduction (to reduce the amount of space used). So it will be
taken care that, vertices condensation will take place before this step.

\(i\) Singular edges have constituent singular vertices. They are first
removed through cutting.

\(ii\) Each vertex has a list of faces that reference it. Around a
vertex, when one cycle of connected components are found, if the number
of faces in that cycle is not equal to the total number of faces that
contain the vertex (valency), then it is singular.

\(iii\) By going through the face list of singular vertices, the number
of connected components can be found. If there are n connected
components, make n - 1 copies of the vertex and assign each of the
connected components discrete labels of the vertex. This makes the mesh
devoid of singular vertices.

\(iv\) At this step we have removed all singular vertices and edges, but
we would like to stitch together some of the erstwhile singular edges to
preserve the geometry.

\(v\) Stitching of edges can take place only when the configuration
after stitching does not produce any singular elements.

\(vi\) Stitching of two edges can take place when the faces containing
the edge have the same normal. This condition is subject to change.

c\. Shells must have consistent orientations

There is support for this in the existing code. We check if each face if
oriented according what is mentioned in the rt_bot_internal structure
(if it is oriented, that is), and if not we flip the orientation.

## Links to the algorithms I intend to use:

1\. AVL Tree method for vertex merging - Generating Topological
Information from a "Bucket of Facets" - Rock and Wozny, 1992.

2\. Zippering algorithm for gap and T - joint closing - Progressive Gap
Closing for Mesh Repairing, Borodin et. al, 2002, Stitching and Filling:
Creating Conformal Faceted Geometry, Patel et. al,

3\. Stitching algorithm for gap and T - joint closing - Filling gaps in
the boundary of a Polyhedron, Barequet and Sharir.

4\. Removal of overlaps - Zippered polygon meshes from range images,
Turk and Levoy.

5\. Triangulation of holes - A robust hole-filling algorithm for
triangular mesh, Zhao et. al.

6\. Removal of degeneracies - Automatic mesh-healing technique for model
repair and finite element model generation, Chong, Senthil Kumar, Lee.

## Deliverables:

Patch containing functions for removal of gaps and T-joints. Patch
containing functions for removal of overlaps. Patch containing functions
for triangulation and correcting of holes. Patch containing functions to
identify all the defects and set the right callbacks

## Development Schedule:

**Community Bonding Period:** The exact layout of where in the codebase
to include all the functionalities will be discussed with the mentor and
decided. Certain situation have ambiguities as to which approach to
take; this will also be clarified. Other than that, suggestions for
improvements on proposed methods will also be taken from the mentors.

-   **Week 1 (May 23rd to May 29th):** Conversion process for the
    portable module

<!-- -->

-   **Week 2 (May 30th to June 5th):** Front end for the mesh healing

<!-- -->

-   **Week 3 (June 6th to June 12th):** Gaps and T-joints - Zippering

<!-- -->

-   **Week 4 (June 13th to June 19th):** Gaps and T-joints - Stitching

<!-- -->

-   **Week 5 (June 20th to June 26th):** Gaps and T-joints - Testing

<!-- -->

-   **Week 6 (June 27th to July 3rd):** Overlaps fixing

<!-- -->

-   **Week 7 (July 4th to July 10th):** Overlaps - testing

<!-- -->

-   **Week 8 (July 11th to July 17th):** Hole - filling using AFM

<!-- -->

-   **Week 9 (July 18th to July 24th):** Hole - filling testing

<!-- -->

-   **Week 10, 11 (July 25th to August 7th):** Detection of all errors
    in meshes and setting the appropriate callbacks to existing features
    and added features.

<!-- -->

-   **Week 12, 13 (August 8th to August 23rd):** Buffer period. Code
    cleanup and final testing of all functionalities. Documentation.

**If time permits:**

Manifold connectivity checking of the meshes. Degeneracy removal Make a
command ‘heal’ with parameters - small gap tolerance, large gap
tolerance, minimum edge length allowed, face factor. And provision could
also be made to skip any particular step in the mesh healing process.

These parts are less essential to mesh healing than fixing gaps, holes,
etc. are. Thus, if I end up going ahead of the schedule, these tasks
will be done. If not, they will be done after the GSoC coding period
ends.