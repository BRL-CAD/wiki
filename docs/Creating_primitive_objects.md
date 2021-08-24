Most types of [**primitive geometric
objects**](BRL-CAD_Primitives "wikilink") can be created using any of
the following MGED command line (CLI) or graphical user interface (GUI)
commands:

[**in**](MGED_CMD_in "wikilink") : Entering a CLI **in** command allows you to interactively create an object with a specified name, type and parameters. That information can either be included in the initial command or provided in response to prompts that are displayed if any required information is omitted from the command line.
**form** : Selecting **Primitive Editor** from the GUI **Edit** menu displays a form/dialog box you can use to name, set the parameters of and then create objects of most (but not all) types. Some derivative objects do not have their own forms, in which case the primitive editor will display the base object's form.
**create** : Selecting an object type from the GUI **Create** menu displays the object-naming dialog box, then creates and displays an object of that type having default parameter values.
[**make**](MGED_CMD_make "wikilink") : Entering a CLI **make** command also creates and displays an object of a specified type having a specified name and default parameter values.

Note that the Create menu is essentially the GUI equivalent of the CLI
make command. After using either, you will generally want to
[**edit**](Changing_the_properties_of_primitive_objects "wikilink") the
resulting object's default location, shape and size.

Primitive objects can also be created by:

-   using the CLI [**cp**](MGED_CMD_cp "wikilink") command to make a
    copy of an existing object, which can then be moved and modified;
-   using the CLI [**dbconcat**](MGED_CMD_dbconcat "wikilink") or GUI
    **File--&gt;Import** command to merge in all objects defined by
    another geometry file; and
-   entering TCL [**put**](MGED_CMD_put_edit_solid "wikilink") commands
    via the command window.

See also:

-   [Determining the properties of primitive
    objects](Determining_the_properties_of_primitive_objects "wikilink")
-   [Changing the properties of primitive
    objects](Changing_the_properties_of_primitive_objects "wikilink")