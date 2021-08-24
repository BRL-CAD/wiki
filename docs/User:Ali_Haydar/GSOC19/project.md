## **Annotations: Implement more annotation support: labels, notes, and dimensions**

The project is divided into three concepts:

-   extending the MGED and Archer commands to inculde the new annotation
    types:
-   calculating each type templet dimensions if nedded like the fields
    in the annotation box
-   drawing the new types in the wire frame view

### **extending the MGED and Archer commands to inculde the new Annotations types**

-   New types of annotaions :
    -   dimention line
    -   multible lables in multible fields box
    -   label in a box
    -   single or multible line note in a box

<!-- -->

-   the extending in mged will be like:



    mged> in
    Enter name of solid: annot_1
    Enter solid type: annot
    Enter annotation type : dimension_line
    "sudo "
    Enter starting point of the dimention line
    Enter end point of the dimention line
    Enter dimension ( or the dimention can be calculated (this choice can be taken if the user wants to override the actual dimention )


-   all the annotions types should be entered in the same annotaion
    primative so this will require modifications on the current
    primative
-   We can consider the same approach of manual annotions as an example
    in the multible field annotion the usuer will provide the number of
    fields and the lables or we can consider half manual abrouch a
    spcific characteer like (@) when encounterd the program considers it
    the end of the field and the label existed in it and the end of this
    label vlist( this will help with the calculation of the the field (
    cell ) dimentions so the user enters all the lables in the same
    line.( this can be discused withe the socity)

Example : Enter the text label: sudo1@sudo2 this annotation will be
constructed from two vlist and calculte the dimentions accordingly.

-   The leader lines will be constructed in correspondance with each
    type.
-   rendering each primative type in wire frame.

### **calculating each type dimentions if nedded like the fields in the annotation box**

-   in the case of the single line note in a box once the annotation
    became a vlist the containing box dimentions will be calculated
    doing simple mathematical operation on the vlist points coordinates

wedth=\[(max X+const)-(min X+ const)\] the same for the hight, since the
box will be drawn with respect to the refrance point of the annotation
just like the lable.

-   in the case of multible cells annotation if we considerd the half
    manual approch each label will be a separat vlist and the cell
    dimentions can be calcuated as above.

## **drawing the new types in the wire frame view**

-   all the new types of annotaions will be converted to a vlist either
    inside the lable vlist or separate one and can be drawn in the same
    way as the lable .
-   For the rendering part, we will try to have annotation on a rendered
    image.

### **attatch the annotation to apoint from a solid**

in this case the annotated opjects name hase to be selected and pass the
point to be calculated as annotated point like the center of a circl and
we have to make some call back function to recalculate the point at each
change if the solid moves the annotaion will move with it .

### **Milestones**

-   Fixing the wrong depiction with OpenGl in windows.
-   Extending the MGED and Archer commands to inculde the new
    Annotations types.
-   Calculating the needed dimentions for the new annotaions and
    implimenting the necessary leader lines.
-   Drawing the new types in wire frame view.
-   Documentation Support

### **fixing the wrong depiction with OpenGl in windows**

currently the annotation representation is correct in Xwindow display
manager where the annotation doesn't undergo rotations or zoon when the
primative does but this is not the case in OpenGl this has to be fixed
by identifing the cause of this problem which I expect will be because
of the display matrix we have to assure that the annotations isn't
defined in the primitive coordinate system.

### **Extending the MGED and Archer commands to inculde the new Annotations types.**

in this case we are going to make a genrial input method for all types
of line segments line_seg carc_seg nurb_seg bezier_seg.

### **Calculating the needed dimentions for the new annotaions and implimenting the necessary leader lines.**

in the case of the box around the lable the calculation must be done
after the lable Vlist is constructed and put the box points coordinates
in the same Vlist or a separet one

### **Drawing the new types in wire frame view.**

the represintation of the annotaions in the wire frame will be the same
in the current annotation primative just adding the nessesary Vlists and
functions nessesary to draw them.

### **Documentation Support**

we are going to make a wiki pages to demonstrate the use of the
modifications we created to make it easy to the user to use the
annotaion primatve.

## **Time Table**

### **Timeline**

IN the bonding period I am trying to understand the code perfectly and
make use of some experemnts and sociaty openions The time table of the
coding period is not clear because the time needed for each task isn't
known exactly

**Deliverables** :

Community bonding period

\[ May 5 - May 20 \]:Review the pipeline Take inputs from the community
Gain insight into the on screen rendering of the primitive

Coding period ( I aim to start coding from May 27 onwards)

-   \[May 27 - June 7\]:understanding the pipe line and trying to fix
    the wrong depiction in OpenGl

<!-- -->

-   \[June 7 - June 20\]: writing functions to calculate and draw the
    box around the labels and modifing the mged commands

<!-- -->

-   \[June 20 - June 26\]:Tests for the written functions

<!-- -->

-   three days for university exams not known exactly because of the
    nature of the master degree combined with other branches in civil
    engineering.

<!-- -->

-   \[July 1 - July 20\]:Implement support for all the line segments
    suggested by the socity

<!-- -->

-   \[July 20 - July 24\]:Write the tests and solve any issue if arises

<!-- -->

-   \[July 28 - Aug 5\]:Support for rendering the annotations

<!-- -->

-   \[Aug 5 - Aug 15\]:ray trace simple annotation and adding the fiture
    to all types

<!-- -->

-   \[Aug 15 - Aug 20\]:Write tests and clear any issue if arises

<!-- -->

-   \[Aug 20 - Aug 25\]:Documentation support.

### **Personal Details**

-   **Name** : Ali Haydar

<!-- -->

-   **Country** : Province of Brescia (GMT+2)

<!-- -->

-   **Contact Details**
    -   Email : lgoogl696@gmail.com
    -   University Email : a.haydar@studenti.unibs.it
    -   IRC Nick : lois_googl

<!-- -->

-   **Education**
    -   Bachelor degree in civil engineering Al-Baath univeristy Syria
    -   Master in civil and environmental engineering Brescia university
        Italy

<!-- -->

-   **Github**:AliHaider93