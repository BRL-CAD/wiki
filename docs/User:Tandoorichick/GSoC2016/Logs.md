Blog with week-wise work including all ideation and explanation at:
<http://tandoorichick.github.io/>

## Development Logs

23/5/16, 24/5/16 - Confusion regarding the indexed and unindexed format
of BRL-CAD and OpenSCAD -&gt; researched other ways to implement the
portable module. Confusion regarding the use of DCEL as well.

25/5/16 - Outlined the PolygonalMesh abstract class. Listed out the
functions that will be required for the conversion from PolygonalMesh to
the DCEL.

26/5/16 - Outlined the doubly-connected edge list class. Declared
virtual functions (that will obtain information from the intermediate
mesh to convert to the DCEL) in the PolygonalMesh abstract class. Others
will be added later on when the need arises.

27/5/16 - Set up the BrlcadMesh class and defined functions. Implemented
few geometry utility functions - orientation checking. Went through
source to find function function: rt_bot_same_orientation() to check
if an edge and a triangle are oriented the same way.

28/5/16 - Vertex record functions definition

29/5/16 - Face record functions definition

30/5/15 - Edge record functions definition

31/5/16 - Setting up OpenSCAD and going through the code. Little bit
confusion regarding the Vector3D variable.

1/6/16 - Implemented some geometry util functions - checking if two
triangles are oriented the same way, calculating determinant. Face
record functions

2/6/16 - Vertex record functions and some of edge record functions

3/6/16 - Edge record functions

4/6/16 - Classes' design changes. Functions common to both native
structures were implemented in the PolygonalMesh class itself.

5/6/16 - UI commands support - added a dummy command "heal" and tested
with a sample message

6/6/16 - Changes in the conversion module code according to Daniel's
suggestions

7/6/16 - Defined the queue element for the zipper gaps algorithm, set up
the files and started with outline.

8/6/16 - Wrote functions for initializing priority queue and listed out
other utility functions that might be needed

9/6/16 - Function to zipper gaps

10/6/16 - Implemented utility functions - finding orthogonal projection,
calculating feature pair, etc.

11/6/16 - Out of station

12/6/16 - Out of station

13/6/16 - Set up the module inside the libanalyze folder in the BRL-CAD
source. Functions to update the DCEL structure - like splitting a face,
inserting a vertex on an edge

14/6/16 - Created a separate header Geometry.h to keep all geometry
related functions like finding if a point can be orthogonally projected
to a line, find such a projection, distance between two points, distance
between a point and a line, etc. Continued writing functions to update
the DCEL structure and inserted calls to them.

15/6/16 - Wrote utility functions for accessing and updating the
rt_bot_internal structure.

16/6/16 - Had set the unbounded face id to be the number of faces
initially, changed that after facing problems while adding and deleting
faces. Updated all relevant functions. Came up with an approach for
finding the closest edge that does not cross any existing
vertex/edge/face. Solved other errors. Built code successfully.

17/6/16 - Had to write TCL command binding again (because i had checked
out revision without saving the work). Analysed the closest edge
function logic.

18/6/16 - Personal commitments

19/6/16 - Moved header files around to include directory, but undid.
Build errors due to missing headers when i included a header file in the
existing code. Asked for help on the IRC.

20/6/16 - Wrote analyse_heal_bot to link to the TCL command. Function
to find free edge chains that are not loops was also written. Including
C++ headers in the MeshConversion.h file gives errors while including
MeshConversion.h in src/libwdb/bot.c for analyse_heal_bot(). Yet to
figure out. Went through earlier code to correct any apparent mistakes.

21/6/16 - Modified code for finding closest edge. And modified code to
conform to BRL-CAD coding standards. Uploaded modified patch on
SourceForge. Started work with stitching gaps since compilation was
unsuccessful. Got solution, made changes. Yet to compile successfully.

22/6/16 - Error while linking C++ code to C. Started with stitching in
the meanwhile. Compiled module later on. Started debugging.

23/6/16 - Tested code. Conversion module gets DCEL to shape. Testing of
zippering gaps going on.

24/6/16 - Changed logic for closest edge function, to handle feature
edge and feature vertex properly. Works for most cases. Rest yet to be
fixed.

25/6/16 - Figured out way to separate the boundary of a mesh from the
defects (using orientation). Till initization of the priority queue
works fine (finding free edge chain, finding closest edge for those,
calculating error and inserting into the priority queue. Memory
corruption error with the zipperGaps() function. I'm trying to resolve
it.

26/6/16 - Resolved one memory corruption error. Another popped up with
the priority queue. Finding ways to resolve that.

27/6/16 - Resolving memory corruption errors

28/6/16 - Made changes in the zipperGaps() function. Tested them. Errors
in logic still exist in some of them. Looking into it.

29/6/16 - Errors with the functions modifying the DCEL. Rectifying them.

30/6/16 - Still modifying the DCEL access functions. Wasn't well for a
part of the day.

1/7/16 - Errors with function addEdge rectified. Setting references
while deleting edge modified.

2/7/16 - Rectified errors with delete functions. Edge contraction and
vertex contraction processes working fine.

3/7/16 - Corrected minor errors.

4/7/16 - Next and previous edge references set right after the
contractions. Sorted out memory issues, changed function prototypes
accordingly. Parameters with double pointers changed to reflect that
they are 3D arrays. Undefined behavior w.r.t even memory issues seen.
Trying to resolve. Started coding stitching algorithm.

5/7/16 - Memory corruption issue wrt push operation with priority queue.
Looked for solutions. Couldn't find any fix. Coding the stitching
algorithm. Made changes from yesterday - that both chains move in
opposite directions by virtue of being a part of the same loop.

6/7/16 - Coded the rest of the stitching algorithm. Included a part in
the zippering gaps algorithm to accommodate for gaps that are square in
shape (in which case none of the vertices on the chain would have any
valid feature - hence it needs to be treated separately). Changed some
function parameters to const as Daniel had suggested.

7/7/16 - Tried fixing the memory corruption error with the priority
queue, but couldn't. Check the stitching algorithm code. Went through
the overlaps fixing algorithm for coding.

8/7/16 - Held up with some other work. Thought about changes to the
existing zipper module code, and the stitching algo.

9/7/16 - Zippering gaps modified to include boundary edges. bool vector
is used to avoid multiple checks to the same chain of edges. Stitching
gaps algo modified slightly. Zippering - vertex contraction has not been
done right. Debugging.

10/7/16 - Weekend

11/7/16 - Issues with vertex contraction resolved. Facelist starting
edge references are out of place. Degenerate cases wrt orientation of
triangles causing those issues. Changes to stitching gaps module
outline.

12/7/16 - deleteEdge() function changed to cope with the degeneracy wrt
orientation. Works fine. Checking the functions that might be causing
the memory issues. Added changes to stitching algorithm.

13/7/16 - Memory issues resolved. Found cases where triangles might
cross over each other due to the transformations. Thus, need to check if
the orientation of the triangle changes. Changes made in the
rt_bot_internal struct pointer not being reflected with draw. Need to
figure out.

14/7/16 - Changes could be seen. But with distorted triangles. Changes
for orientation check was added. Works. Few more cases of erroneous
detection of feature edges, looking into them.

15/7/16 - Zippering gaps module works fine. Need to test with other
meshes where the tolerance and the size of the triangles is not so
comparable.

16/7/16 - Cleared out dead code. Wrote includes properly. Added a bit of
stitching code.

17/7/16 - Weekend

18/7/16 - Had to test a few times with a mesh that needs no healing.
Made changes for the case when the defect is a square (the normal case
does not work, special case was written for a square) - works fine.
Created two disconnected hemispheres on Blender to test, and exported
the geometry as an .obj file. Testing it.

19/7/16, 20/7/16 - Was not well. Couldn't spend much time. Fixing two
hemispheres works okay, but needs more testing.

21/7/16 - Came up with results.

22/7/16 - 25/7/16 - Fell ill again

26/7/16 - Made changes according to Daniel's suggestions.

27/7/16 - 11/8/16 - Had fallen ill and couldn't get to work.

12/8/16 - Outlining skewed lines support for 3-D lines (while
calculating feature).

13/8/16, 14/8/16 - Debugging the instance of the heal command being
called on a mesh on which the heal command had already been called.

15/8/16 - Debugging the coplanar condition addition while finding the
closest edge.

16/8/16 - Debugging errors in making the DCEL, with a torus.

17/8/16 - Testing with meshes to figure out the point of breaking. Wrote
blogs for weeks missed.

18/8/16 - Started with taking tolerance as user input. Errors popped up.
Could not identify what was causing them even after falling back to old
code.

19/8/16 - Build error resolved. Added feature to take in zipper
tolerance as user input. Debugged with Daniel's suggestions. Error seems
to be with setting the incident face reference - because of the
orientation checking. With the spheres the origin was within the whole
sphere, so orientation was consistent. With the torus, the origin is not
inside the object, so inconsistencies with orientation don't allow some
edges to get the right incident face. Hence, the next and previous
references get messed up too. Yet to think of a fix.

20/8/16 - Dealing with the mesh not being completely healed because some
vertices don't get valid feature pairs, even while having them. Added a
special case for when the hole is triangular to reduce compute time.

21/8/16 - Had missed a condition in checkAndSetTwins() routine. Debugged
and found it. This prevented the case where, when a mesh is healed with
the heal command, and the heal command is called again on the mesh, the
algorithm hung. This was because of the presence of singular vertices
which was in turn because the mesh was not completely healed. This was
rectified.