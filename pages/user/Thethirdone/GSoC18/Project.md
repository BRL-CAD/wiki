## **Slic3r Face based rotation**

==**Abstract**=

The primary goal of this project would be to implement a solution to
issue \#3047. This issue is basically about implementing a way for users
to select a face and choose it to be the face that connects to the
plate.

`   Specifically, after implementing this feature, I expect that a user would be able to click a face (which should be highlighted to make clicking the right face easy) on an object and then click menu button to rotate that face to bottom of the model. If there is a part of the object below the plate after the rotation, it should either error or push the model up until it is no longer intersecting the plate (I’m not sure which is more intuitive).`

Potential Extensions:

`   In the process of writing up the plan for this, I found that I don’t think it will take me very much time. I expect a working prototype will take me a week, even if that is a dramatic underestimate, that would still leave a significant of time to be working on other issues in Slic3r. `

If different parts of the GUI can be ported to C++ independently, it
could make sense to port 3DScene as an extension to this proposal. By
the time I finish working on adding face-based part rotation, I should
be quite familiar with it so porting would be more efficient than moving
onto another area of Slic3r. Another possible extension is to work on
adding manual support pillars which would solve \#3062. I would
certainly be familiar enough with 3DScene to be able to do that side of
it, but I haven’t look at the code for support generation at all yet.

## **Implementation Plans**

`   Given a normal to rotate to the -z direction, the actual rotation is fairly simple. A rotation about the z axis so that the normal lies in the xz plane followed by a rotation about the y axis to rotate it to -z is quite straightforward. Therefore, most of the work of implementing this feature will be in determining the normal to use from user input.`

`   In order to select a face, it is important to be able to find the triangle that the users mouse is over. This is currently already done, but with entire objects instead of individual triangles. Objects are currently determined from mouse position by changing the color of the object based the looking up the color at the position of the mouse. It should be possible to extend the method to a per triangle basis without much trouble. However, it will require an extra rendering pass. The highlighting of a single face (can be multiple triangles) will likely require keeping a buffer of colors for every triangle in the object. `

`   When selecting a face, ideally the entire (flatly) connected face would be highlighted. This requires detecting which triangles make up a face. I don’t know of any algorithms which detect flat connected faces off the top of my head, but I am sure they exist. It is fairly easy though to detect triangles which lie of the same plane though. If for some reason highlighting just the connected face is impractical, highlighting all triangles on the same plane should be sufficient.`
`   `

So in a concise form the plan for each of the subtasks:

-   Selecting the face
    -   Assign a color to every triangle in the mesh
    -   Render and test the color at the mouse location
-   Highlighting the face
    -   Detecting which triangles are on the same face
    -   Adding a Color buffer for rendering
-   Rotating the object
    -   Get normal
    -   Rotate normal along z to xz plane
    -   Rotate normal along y to -z

I don’t have any concrete implementation ideas for any potential
extensions to the proposal yet.

## **Timeline**

-   May 14 - May 28
    -   Work on a first concept of rotating a base to the plate
-   May 29 - June 4
    -   Get feedback of it and fix any bugs and ensure that it is
        sensibly listed with other rotation options.
-   June 5 - 11:
    -   Look over more code and decide which extension is should be
        taken on.
-   June 12 - August 6
    -   Work on the selected extension
-   August 7 - August 21
    -   Do any final work needed to finish up the extension

## **Background**

I’m a student University of California Merced planning to graduate next
December. I am taking a course in Computer Graphics so when looking
through organizations I was drawn to BRL-CAD. I used Slic3r a few times
when I had access to a 3d printer during high school. With a quick look
through the code for Slic3r, it seems reasonably approachable. My only
reservation was the amount of Perl, I have never worked with any large
(more than 500 lines) Perl project, but given that I don’t have to
change the overall structure, I am comfortable working on it.