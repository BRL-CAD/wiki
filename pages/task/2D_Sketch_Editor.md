Archer is the next iteration of BRL-CAD's MGED model editing tool. We
are currently in the process of migrating functionality from MGED to
Archer. MGED currently provides a minimal sketch editor that is used to
create and edit BRL-CAD's sketch primitive.

Archer also needs the ability to create and edit sketches. This project
would entail examination of the existing sketch editor in MGED and
ensuring a new sketch editing component in Archer enabled all the
functionality of the old editor. Just "porting" the existing sketch
editor to Archer would be no more than a first step - the editing
experience and usability should also be enhanced.

# References

An interesting direction would be to examine TkCAD, which is license
compatible:

-   <https://github.com/revarbat/TkCAD>
-   <https://github.com/revarbat/TkCAD/wiki/Screenshots>

and how its functionality might be integrated into Archer for sketch
editing (and other features in the future, modular design is a good
direction to go).

# Requirements

-   Familiarity with C (understanding of sketch primitive)
-   Familiarity with Tcl/Tk