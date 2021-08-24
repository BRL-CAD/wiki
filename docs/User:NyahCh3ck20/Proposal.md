# Personal Information

NAME : Check Nyah Watad Wallah

EMAIL: check.nyah@gmail.com

IRC: Ch3ck

#### Background Information

I am a freshman Computer Engineering Student at the University of Buea,
South West Region,Cameroon. After wining the 1st prize for Programming
among the freshman year students at my university. I have founded a
programmers club to help develop the coding skills among members of my
university community

## Programming Background

Languages: C(Very Good), Java(learning/Intermediate),
C++(learning/basic)

C:

Wrote over a thousand lines of c code to increase performance of a
sorted online dictionary used by French speaking students in our
University using a redblack tree.

Implemented a fibonnacci heap to demonstrate how it can increase
performance of the Dijkstra's algorithm used in solving the
single-source shortest path problem used in graph search.

​Java: Currently working on a Medical app to be integrated into the
university website to determine the body mass Index of students in
relation to the Health Awareness Initiative of the University.

# Project Information

MATRIX PULL ROUTINE FOR PERFORMING THE OPPOSITE OF THE MATRIX

`              PUSH ON GEOMETRY.`

### Brief Project summary

The pull routine takes a specific node on a CSG tree, walking down to
the primitive shapes restoring the geometric transformations(scaling,
translation or rotations) at each stage down the CSG tree traversal
based on reversing all the geometric transformations that occured on the
primitive shapes located at the leaf. Pull routine also stores the local
coordinate systems ate each point during the traversal from the
primitives up to the given initial node. All transformation matrices
visited along the tree will be set to their original tranformation
matrices. This command will fail if no changes occured to the primitive
shapes at the leaves of the csg tree.

# Detailed Project Description

### Introduction

The Pull/unpush command/routine is a high priority project for BRL-CAD.
The pull command seeks to restore the original state of the csg tree
from any particular node after the push command has been executed.
However, the Push command is used to walk the geometry tree from a
specified head node to the leaf nodes(primitive level), collecting the
matrix transformations such as (translations, rotations or scales)
applied to new assemblies using matrix edits(oed command). The push then
applies the matrix transformation parameters to the primitives,
eliminationg the need for storing the various matrix transformations
thereby setting them to identity matrices. This process however looses
any local coorrdinate system used in constructing the geometric objects.
The pull routine seeks to restore the original tree state by reversing
any tranformation operations performed on the primitive shapes from a
designated top node on the csg tree. Here, I would like to show my
detailed proposal in solving this summer's project. My code patch will
have a sample routine that takes as argument a designated node(such as a
primitive) and performs the Inverse of any rotation, Inverse of any
translation and the inverse of a scale.) and performs the matrix inverse
the primitive matrix.

#### The Working of the Pull Routine

Syntax

`   pull `<objects>

arguments

`   `<objects>
`   valid brlcad objects currently in database.`

The Pull routine takes as arguments a valid object, moves down the tree
and performs an inverse rotation which is stored in a list, inverse
scale and inverse translation which is stored on the list and transforms
the primitive object by the Inverse transformations and recursively
inserts the original matrix transformations on the tree as it moves up
from the primitive

Matrix Transformations BRL-CAD uses three main transformations on
objects stored in a 4x4 matrix defined by 'mat_t' data type Assuming
the 4x4 matrix is represented as shown below

`   [0 ][ 1][ 2][ 3]`
`   [4 ][ 5][ 6][ 7]`
`   [ 8][9 ][10][11]`
`   [12][13][14][15]`

The rotation operation is represented by the 3x3 matrix

`   [0 ][ 1][2 ]`
`   [3 ][ 4][ 5]`
`   [6 ][ 7][ 8]`

The scale transformation is represented by the diagonal matrix

`   [0][4][ 8]   or  [0] 0  0  0 `
`                 0 [4] 0  0`
`                 0  0 [8] 0`
`                 0  0  0  1`

The translation transformation is represented by

`          1 0 0 [3]`
`          0 1 0 [7]`
`          0 0 1 [11]`
`          0 0 0  1    `

However, the various geometric transformations will be separated into
different column matrices by the det_matrix() routine explained below.

The Inverse of the various transformations will be computed by the
routine

/\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
void InverseTransform(mat_t transf); shown in the code patch

`     **********        or  ***************`
`   a preprocessor directive`
`#define InverseTransform(transf)   //so as to increase speed of execution.`
` **************************************************************************/`

The Mathematics of the Inverse Transformation

Inverse Rotation: In Euclidean geometry, a rotation is an example of an
isometry, a transformation that moves points without changing the
distances between them. Rotations are distinguished from other
isometries by two additional properties: they leave (at least) one point
fixed, and they leave "handedness" unchanged. Since BLR-CAD represents a
rotation by the 3x3 matrix, an Inverse of a rotation would be the
transpose of the 3x3 matrix so if RotA(3x3 rotation), Inverse(RotA) =
Transpose(RotA).

Inverse Scale: Scaling transformations stretch or shrink a given
coordinate system and as a result change lengths and angles. So, scaling
is not an Euclidean transformation. The meaning of scaling is making the
new scale of a coordinate direction p times larger. In other words, the
x coordinate is "enlarged" p times. This requirement satisfies x' = p x
and therefore x = x'/p. Scaling can be applied to all axes, each with a
different scaling factor. For example, if the x-, y- and z-axis are
scaled with scaling factors p, q and r, respectively, the inverse
transformation matrix is:

`   Inv(SclA) = 1/p  0   0`
`                0   1/q 0`
`                0   0   1/r`

Inverse Translation: A translation is an affine transformation with no
fixed points. Matrix multiplications always have the origin as a fixed
point. Nevertheless, there is a common workaround using homogeneous
coordinates to represent a translation of a vector space with matrix
multiplication: Write the 3-dimensional vector w = (wx, wy, wz) using 4
homogeneous coordinates as w = (wx, wy, wz, 1). so the Inverse of a
translation simply reverses the direction of the vector or matrix if
TrnA = (a, b ,c , d) Inverse(TrnA) = (-a, -b, -c, -d)

## The Inverse of the Transformation

The key point mathematically is the reversibility of the
transformations.

For 3D, the typical transformation is

`[ new_x ]     [ Xx Xy Xz Tx ]  [ x ]`
`[ new_y ]  =  [ Yx Yy Yz Ty ]  [ y ]`
`[ new_z ]     [ Zx Zy Zz Tz ]  [ z ]`
`[   1   ]     [  0  0  0  1 ]  [ 1 ]`

which is usually written as

`v = M p `

where v is the transformed vector, p the original vector, and M the
transformation matrix (that includes rotation, scaling, and moving).

Because the matrix is formed as a 4-by-4 matrix as above,
transformations can be combined via matrix multiplication (new matrix on
the left side):

`Mcombined = Mlater Mearlier`

.

Because each transformation is reversible, there is also an inverse
matrix

``   M` M = I.  ``

Thus, starting at a leaf in the object tree, the current transformation
matrix on the left is multiplied with the new transformation matrix, to
obtain the one that applies to the current object). The transformations
are cumulative from the root to the leaf.

Reversing the matrix M is very simple (Xx' means transformed Xx
component of the matrix, and so on):

`D   = Determinant(M) = Zz Xx Yy - Zz Yx Xy - Zx Xz Yy - Zy Xx Yz + Zy Yx Xz+   Zx Xy Yz`

`Xx' = (Yy Zz - Zy Yz) / D`
`Xy' = (Zy Xz - Xy Zz) / D`
`Xz' = (Xy Yz - Yy Xz) / D`
`Tx' = ( -Xy Yz Tz + Xy Zz Ty + Xz Tz Yy - Xz Zy Ty - Tx Yy Zz + Tx Zy Yz) / D`
`Yx' = (-Yx Zz + Zx Yz) / D`
`Yy' = (Zz Xx - Zx Xz) / D`
`Yz' = (-Yz Xx + Yx Xz) / D`
`Ty' = (Xx Yz Tz - Xx Zz Ty + Ty Zx Xz - Yz Zx Tx - Yx Xz Tz + Yx Tx Zz) / D`
`Zx' = (Yx Zy - Zx Yy) / D`
`Zy' = (-Zy Xx + Zx Xy) / D`
`Zz' = (Yy Xx - Yx Xy) / D`
`Tz' = (-Tz Xx Yy + Tz Yx Xy + Zx Tx Yy + Zy Xx Ty - Zy Yx Tx - Zx Xy Ty) / D`

So When the cummulative matrix is stored for each object,and its inverse
any matrix transformation can be applied in the object coordinates. This
is simply done by multiplying the transformation with the object
coordinates for any object; which then gives the transformation in the
root coordinate system. When this is then applied to the left with each
of the transformation matrices, the original transformation matrix is
obtained in local object coordinates / transformations.

### Overall Structure Pull routine

The pull routine works down a tree from the node pushing the directory
pointers to a linked list and when it reaches the leaf, it copies the
transformation matrix performs an inverse transformation on the leaf
restoring it back to its initial form and moves back up the tree
restoring the original tranformation matrices using the directory
pointers which also stores the local coordinates.

However,brlcad already has the functionality for performing matrix
operations on objects as in(src/libged/push.c, xpush.c). I will use the
InverseTransf() as a subroutine in the pull operation and simply use the
MAT_COPY directive to copy the various 4x4 original matrix
transformations to the corresponding node up the tree from the leaf.
after the various matrix transformations have been copied from the
matrix stored at the leaf node.

So, here is a summary of the pull command

`   *. pull_obj -create a structure to hold the original matrix and corresponding local coordinate systems while calling            inverse_tranf().`
`   *. det_trans()create a routine to copy the different matrix transformations performed on the primitive; which will then be          given to InverseTransf() as an argument.`
`   *. create a loop to move down the tree to the leaf and then recursively move up restoring the original matrix           transformations.`
`   *. pull leaf() routine : which runs in parallel restoring the original primitive state and copies the matrix transformation`
`       which then calls the det_transf() routine to seperate the different matrix tranformations.`
`   *. mat_restore() routine: which restores the original matrix transformation and coordinate system at each node.`

### The det_trans() routine

`   This takes the primitives transformation matrix and separates the various types of matrix transformations from it before `
`   passing the results to calling function. This routine returns an array of three 4x4 matrices having the scale, rotation and         translation transformations.It returns 1 upon success and 0 otherwise. `

### The inverse_transf() routine

:

`   This routine takes any of matrix transformations determined by the det_trans() routine and determines the inverse of the `
`   transformation which will then applies to the primitive to restore its original state. It stores the results on the         pull_obj structure will will then be applied to the primitive object to restore its original state.`

### The mat_restore() routine

`   This routine takes the directory arguments and corresponding transformation matrices from pull_obj structure and restores       the original matrix tranformation of nodes in a particular tree.`

### The pull_leaf() routine

`   This routine applies an inverse transformation a primitive object restoring the original state or dimensions of the         primitive object. returns truthfully if the object has been restored to its original state.`

### Tests and Verification

I believe test driven development would be key in finding and fixing
problems with the pull routine and then with more tests to ensure the
code functions correctly and its bulletproof to all forms of object
inputs. This will be enhanced with the creation of a special regression
test for the pull command to avoid modification of unwanted
nodes/objects.Also, this command will be included among the MGED
commands and a well written manual will be made so support the usage of
the command.

### Links

\[1\] CodePatch(Sample linked list that holds the matrices and inverses
and corresponding directories together with the sample implementation of
the Inverse of a transformation function) Link:
<https://sourceforge.net/p/brlcad/patches/169/>

\[2\] Geometric Transformations and Inverses:
<https://www.cs.mtu.edu/~shene/COURSES/cs3621/>.../geometry/geo-tran

<http://www.cg.info.hiroshima-cu.ac.jp/~miyazaki/knowledge/teche53>

# Deliverables

Implementation of the inverse_tranf(), mat_restore(), det_transf()
routines and other pull subroutines.

Implementation of the complete pull routine with further
testing.:(pull_leaf())

Integration of the Pull routine into MGED command interface together
with Documentation containing(summary together with usage capabilities)

# Development schedule

### July 1st (\~ 3 weeks)

Study of BRLCAD Manuals and other Documentation on the Push Command

Discuss with other developers concerning implementation details.

Study the (src/libged , /include ) libraries and the implementation of
push/xpush commands.

Discuss more coding specifications and implementations details with
mentor/other developers

### July 21 - July 28 (1 week)

Implementation of the det_trans() and InverseTransf() routines with
determination of original matrix transformations.

Tests on sample primitive matrices

### July 29 - Aug 17(3 weeks)

Implementation of do_restore() routine(1 week) which traverses nodes
restoring the original matrix and tests

Implementation of pull routine(pull_leaf() and others)(2 weeks)

Testing and functionality verification of function.

Mid-term evaluation in July 29 - Aug. 2

### Aug. 18 - Aug. 31 (2 weeks)

Finalization of complete pull routine

Tests Tests of the final pull routine on primitives

### Sept 01 - Sept 14( 2 weeks)

Integration of Pull into MGED command interface.

Testing of functionality of command and debuggging

### Sept 15 - Sept 21(1 week)

Tests Fix bugs and improve performance of routine

Documentation and code clean up

### Sept 23 - Sept 27(1 week)

Final Evaluation Submission of Final code to Google.

# Time availability

I would be able to offer over 40 hours on the project. However, Our
Second Semester ends late june or early july and our next semester
begins in early October. However, if the semester extends to early july
it will be for completion of exams so i would dedicate most of my
evenings and weekend in the first week of July to start work on studies
of the brlcad documentation and libraries.

# Why BRL-CAD?

From the day i read the Document "How to become a Computer Hacker" by
Eric S. Raymond, I started coding very seriously and praying for the day
i would become a true hacker by contributing code to the opensource
community. I believe working with brlcad this year will give the joy of
working on my first real opensource project. I will really cherish the
experience of having contributed code to a great organizaton like
BRLCAD.

# Why me ?

I believe having won the prize as the best computer programmer in my
freshman class at my university I would be capable of contributing
software to brlcad and the opensource commmunity. I see this brlcad
project as a challenge to gain both the respect of brlcad geeks and
other great programmers which would give me additional confidence in
climbing the ladder of hackerdom. I pray that you give me this great
opportunity to greatly impact humanity and the world using software.