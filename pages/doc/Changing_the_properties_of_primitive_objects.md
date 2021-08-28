MGED provides several different ways to modify and reposition [BRL-CAD
Primitives](BRL-CAD_Primitives.md) by changing the values of
their associated parameters:

-   the [primitive object editor](#Primitive_Editor.md) dialog
    box
-   the [interactive editing](#Interactive_editing.md) commands
-   the get and put [TCL commands](#TCL_Commands.md)

See also: [Determining the properties of primitive
objects](Determining_the_properties_of_primitive_objects.md)

;

# Primitive Editor

Most of the parameters associated with many primitive objects can be
edited using the **Primitive Editor** dialog box:

1.  Invoke the GUI **Edit--&gt;Primitive Editor** command to display
    that dialog.
2.  Type the object's name into the **Name:** field and then click the
    **Reset** button to display its associated form and the current
    values of its editable parameters.
3.  Interactively change and reposition the object by changing
    appropriate parameter values. Your changes are immediately written
    to the database and the object is redrawn in the Display Window each
    time you click the **Apply** or **OK** button (OK also closes the
    dialog box). Unapplied changes can be undone by clicking the
    **Reset** button.
4.  Repeat the above steps to edit additional objects, or click the
    **OK** or **Dismiss** button to close the dialog.

Note that forms have not been defined for all object types. Those that
lack such forms cannot be edited using this method.

# Interactive editing

Any *currently displayed* primitive object can be selected for
modification or relocation using either the GUI **Edit--&gt;Primitive
Selection...** or the CLI [**sed**] (MGED_CMD_sed.md) command.

Objects that aren't currently displayed will not be listed in the
Primitive Selection Menu dialog, and the sed command will display an
error message if you try to edit such an object. In either case, using
the CLI **draw** or **B** command to display such an object would then
allow you to select it for editing.

When such an object is selected for editing, the **Edit** menu will
display a set of commands specific to the corresponding primitive type.
Invoking any such command will allow you to change the corresponding
parameter(s) by entering CLI **p** commands or activating the Graphics
Window and using associated **shift grip** mouse actions. Similarly, the
CLI will enable various edit-mode commands that can be used to modify or
relocate the selected primitive. As you use either approach to make such
changes, you can:

-   record the changes you have made so far by invoking the GUI
    **Edit--&gt;Apply** or entering the CLI **apply** command;
-   undo any unrecorded changes by invoking the GUI **Edit--&gt;Reset**
    or entering the CLI **reset** command;
-   record the changes you have made and return to viewing mode by
    invoking the GUI **Edit--&gt;Accept** or entering the CLI **accept**
    command; or
-   discard any unrecorded changes and return to the viewing mode by
    invoking the GUI **Edit--&gt;Reject** or entering the CLI **reject**
    command. You can also reject unrecorded changes by pressing the
    escape key while the Graphics Window is active.

# TCL Commands

Although it is a cumbersome approach that is best reserved for scripted
editing, primitive objects can also be edited by entering TCL **get**
and **put** commands via the CLI:

1.  Enter a "get object_name" command to display the current database
    entry for that object.
2.  Enter a "kill object_name" command to delete that database entry
    and erase the object from the Graphics Window.
3.  Enter a "put object_name properties" command to recreate that
    object with modified parameter values.
4.  Enter a "draw object_name" command to redisplay the object and
    verify your changes.
