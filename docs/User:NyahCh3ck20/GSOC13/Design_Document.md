### Implementation of Pull routine Design Document

## Introduction:

The Pull command/routine restores the original state of a CSG tree by
reversing all the geometric transformations from the leaf(primitive)
nodes applied during the Push operation on the CSG tree. The pull
routine reverses the matrix operation on the primitives and recursively
restores all matrix transformations on the parent nodes up the CSG tree
during an inorder tree walk, from the leaf to the designated head of the
tree.

## Intended Implementation Approach:

The pull routine works down a tree from a specific node(head) pushing
the directory pointers to a linked list till when it reaches the
leaves(primitives); It then copies the geometric transformation on the
primitive and restores the primitives to its initial state and moves
back up the tree restoring the original matrix transformations on the
parent nodes by performing an Inverse of the current matrix
transformation stored on the linked list; hence it restores the local
coordinates of the parent nodes.

On a CSG tree, the transformation matrices are always a 4x4 matrix

Code:

`   [ Xx Xy Xz Tx ]`

M = \[ Yx Yy Yz Ty \]

`   [ Zx Zy Zz Tz ]`
`   [  0  0  0  1 ]`

The unit X vector in new coordinates \[ 1 0 0 \] matches \[ Xx Xy Xz \]
in old coordinates. The unit Y vector in new coordinates \[ 0 1 0 \]
matches \[ Yx Yy Yz \] in old coordinates. The unit Z vector in new
coordinates \[ 0 0 1 \] matches \[ Zx Zy Zz \] in old coordinates. The
origin \[ 0 0 0 \] in new coordinates is moved to \[ Tx Ty Tz \] in old
coordinates.

With the matrix transformation matrix M defined as above, inverse matrix
R = M-1(Inverse of M) defines the rotation back to the original
coordinate system. R is simple to calculate: Code: d = Det(M) = Zz Xx Yy
- Zz Yx Xy - Zx Xz Yy - Zy Xx Yz + Zy Yx Xz + Zx Xy Yz

So I'll require a routine(Inverse_transf() and det_trans() routines)

`   [ (Zz Yy - Zy Yz)/d  (Zy Xz - Zz Xy)/d  (Xy Yz - Xz Yy)/d   (Xy Ty Zz - Xy Yz Tz + Xz Tz Yy - Xz Zy Ty - Tx Zz Yy + Tx Zy Yz)/d ]`

R = \[ (Zx Yz - Zz Yx)/d (Zz Xx - Zx Xz)/d (Yx Xz - Yz Xx)/d (Xx Yz Tz -
Xx Ty Zz + Ty Zx Xz - Yz Zx Tx - Yx Xz Tz + Yx Tx Zz)/d \]

`   [ (Zy Yx - Zx Yy)/d  (Zx Xy - Zy Xx)/d  (Yy Xx - Xx Xy)/d   (Tz Yx Xy - Tz Xx Yy + Zx Tx Yy + Zy Xx Ty - Zy Yx Tx - Zx Xy Ty)/d ]`
`   [        0                  0                  0                             1                                 ]`

R(Inverse_transf()) algorithm will be used in determining the inverse
of the transformation taking into consideration othogonal
matrices(transpose of matrix is the same as the inverse of the matrix.)

In a case where d=0, the matrix is degenerate (also called singular),
and does not describe a true transformation. Such a matrix flattens the
space into a flat plane or a single point. In practice, d is always near
one.

In a case of more than one transformation matrices, the matrices are
multiplied in the order below:M = MN MN-1 ... M2 M1

Assuming the transformation matrix Mself transforms parent coordinates
to current object coordinates, and Mchild transforms current object
coordinates to child object coordinates. To transform current object
coordinates to world coordinates we use

M = Mself Mparent ... Mancestor and to transform child object
coordinates to world coordinates you use M = Mchild Mself Mparent ...
Mancestor

To transform world coordinates to current object coordinates, you use R
= Mancestor-1 ... Mparent-1 Mself-1 = (Mself Mparent ... Mancestor)-1

Considering the small tree below: Code:

`        World`
`          |`
`       Ancestor`
`          |`
`     Grandparent`
`       /       \`
`   Parent     Uncle`
`   /    \        \`
` Self  Sibling  Cousin`
` `

Starting with an identity matrix, M = I = \[ \[ 1 0 0 0 \] \[ 0 1 0 0 \]
\[ 0 0 1 0 \] \[ 0 0 0 1 \] \] If you move down, multiply the
transformation by the target transform on the left: M â† Mtarget M If
you move up, multiply the transform by the inverse of the source
transform on the left: M â† Msource-1 M

In both cases the source/target transform corresponds to the lower node
in the tree. Example:

We need to transform current coordinates to coordinates in uncle's
coordinate system. The path is Selfâ†‘Parentâ†‘Grandparentâ†“Uncle:
\[INDENT\]M = I M â† Mself-1 M M â† Mparent-1 M M â† Muncle M
\[/IDENT\] or, in other words, M = Muncle Mparent-1 Mself-1 and
describes the transformation from current coordinates to Uncle's
coordinate system.

Generally, in implementing the pull routine, i'll need the matrix
transformation of the leaf(primtive) nodes and recursively compute its
inverse while moving up the tree and restoring the various matrix
transformations. So, (Muncle Mparent-1 Mself-1)-1 = Mself Mparent
Muncle-1 which also matches the inverse path,
Uncleâ†‘Grandparentâ†“Parentâ†“Self!

However, in implementing the pull routine I would need the following:

-   . pull_obj -create a structure to hold the original matrix and
    corresponding local coordinate systems while calling
    inverse_tranf() routine.

<!-- -->

-   . inverse_tranf(): this performs the inverse of a 4x4 matrix using
    the procedure shown above.
-   .
-   . det_trans(): This determines the determinant of a 4x4 matrix as
    shown above.
-   . create a loop to move down the tree to the leaf and then
    recursively move up restoring the original matrix transformations.
-   . pull leaf() routine : which runs in parallel restoring the
    original primitive state and copies the matrix transformation which
    then calls the det_transf() routine to seperate the different
    matrix tranformations.

<!-- -->

-   . mat_restore() routine: which restores the original matrix
    transformation and coordinate system at each node, which will
    consist in calling the rt_matrix_tranform() as defined in
    (/src/librt/transform.c)

1.) The det_trans() routine:

`   This determines the determinant of a 4x4 matrix which is to be called in inverse_tranf() routine. `

2.) The inverse_transf() routine:

`   This routine takes any of matrix transformations determined by the det_trans() routine and determines the inverse of the transformation which will then be applied to all the nodes up the CSG tree from the primitive by pull leaf() in restoring the original state of the matrix transformations up the CSG tree. This routine will consider orthogonal matrices in order to increase runtime for some matrix transformations.`

3.) The mat_restore() routine:

`   This routine called by pull_leaf() uses rt_matrix_transform() routine to restore the original transformation matrix at the parent nodes up the tree.`

4.) The pull_leaf() routine:

`   This routine starts reversing all the geometric transformations the leafs then calls mat_restore(), inverse_tranf() routines to determine and restore the original matrix transformations up the CSG tree.`

Tests and Verification:

I believe test driven development would be key in finding and fixing
problems with the pull routine and then with more tests to ensure the
code functions correctly and its bulletproof to all forms of object
inputs. This will be enhanced with the creation of a special regression
tests for the pull command to avoid modification of unwanted
nodes/objects.Also, this command will be included among the MGED
commands and a well written manual will be made so support the usage of
the command.

## Milestones and Deliverables:

Implementation of the inverse_tranf(), mat_restore(), det_transf()
routines and other pull subroutines.

Implementation of the complete pull routine with further
testing.:(pull_leaf())

Integration of the Pull routine into MGED command interface together
with Documentation containing(summary together with usage capabilities)

## Original Development Schedule:

Since my semester ends by late june or early july, i will start coding
on July 1st.

`   July 1st (~ 3 weeks)`
`       Study of BRLCAD Manuals and other Documentation on the Push Command`
`       Discuss with other developers concerning implementation details.`
`       Study the (src/libged , /include ) libraries and the implementation of push/xpush       commands.`
`       Discuss more coding specifications and implementations details with mentor.`
`       `
`   July 21 - July 28 (1 week)`
`       Implementation of the det_trans() and InverseTransf() routines with`
`           determination of original matrix tranformations.`
`       Tests on sample primitive matrices`
`       `
`   July 29 - Aug 17(3 weeks)`
`   Implementation of do_restore() routine(1 week)`
`       which traverses nodes restoring the original matrix and tests`
`       Implementation of pull routine(pull_leaf() and others)(2 weeks)`
`          Testing and functionality verification of function.`
`          `
`       Mid-term evaluation in July 29 - Aug. 2 `
`       `
`   Aug. 18  - Aug. 31 (2 weeks)`
`       Finalization of complete pull routine `
`       Tests`
`           Tests of the final pull routine on primitives `
`   `
`   Sept 01 - Sept 14( 2 weeks)        `
`        Integration of Pull into MGED command interface.`
`           Testing of functionality of command `
`           and debugging`
`   `
`   Sept 15 - Sept 21(1 week)`
`       Tests`
`           Fix bugs and improve performance of routine`
`       Documentation and code clean up`
`       `
`   Sept 23 - Sept 27(1 week)`
`       Final Evaluation`
`       Submission of Final code to Google.`
`       `

## References and Resources:

Graphics Gems: Matrix identities, transformation axes, Fast matrix
multiplication, Matrix orthogonalization, www.graphicsgems.org
Wikipedia: Composing and inverting transformations, Quaternion-derived
rotation matrix, Invertible
matrix(www.wikipedia.org/transformation_matrix,
www.wikipedia.org/Rotation_matrix)