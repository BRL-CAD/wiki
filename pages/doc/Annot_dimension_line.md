[category:tutorials](category:tutorials.md)

![](../img/DL.png)

A dimension line annotation is suggested and not final yet, it is
currently created through the "in" command. This capability is
constructed using the same existing annotation primitive. it allows
users to draw a dimension line between two points in the wireframe view.
The lines that construct the dimension line is aimed to be in the model
space, and the dimension line text will be always in the plane of the
screen irrespective of the rotations and zooming . "get" and "l"(ell)
commands give an overview about the structure. The input format can also
be found below.

    mged> in
    Enter the name of solid: DL
    Enter solid type: annotDL
    Enter the first point: 20
    Enter Y: 20
    Enter the second point: 30
    Enter Y: 30
    Enter the text size: 3
    Enter the relative vertical position(1->bottom, 2->middle, 3->top): 3
    Enter the relative horizontal position(1->right, 2->center, 3->left): 1
    DL

you can notice the get command in the picture.

What we currently have is a foundation for future work. the rotation
angle of the text is calculated based on the coordinates of the first
and the second points.
