# Project Report

-   **Student Name:** Vikram Atreyapurapu
-   **GSoC Project:** Implementing UNDO

The project started with deciding which kind of undo to be implemented.
Various implementations were thought about including a complete re-run
approach, partial checkpoint, full checkpoint, etc as discussed in
detail in my
[Proposal](https://docs.google.com/document/d/1cZLgqVvxOiy7PgkUzEzeyXXhmLx1sEgRB1xw3hDFUlA/edit?usp=sharing).
Using a version control system like libgit2 was also explored, but was
found to be sub-optimal since it was occupying a lot of extra space and
was also not very time efficient.

It was decided that the undo would be implemented using a partial
checkpoint-like approach, where a change in an object at any step would
be the only thing stored at that step instead of storing a full
checkpoint of the .g file at that point. After each step, we would need
to store the last action and some details like which action and object.
this information is stored as a string-value-pair in the _GLOBAL
object. Initially, this data was stored in 2 separate variables one for
the last action and one for the object being acted upon.

Since storing different information divided over many variables is
unsuitable, a data structure was made to hold all the information. This
proved to be tough and making a linked list of these data structures
wasn't easy. So a method was chosen to have all the information in 1
string and store that in _GLOBAL. Every time a command is performed
relevant information is concatenated to the action_string stored in
_GLOBAL. For eg, make sph1.s sph would add "1 sph1.s". When undo is
called the last action will be reversed and the last command info is
popped from the string. For complex commands, we create a separate
attribute object that might have multiple make or kill operations, which
as a combination represents a complex command/action.

The notation used was
1 obj_name == obj1_name was made
2 obj_name == obj1_name was killed
0 attr_obj == reverse all sub-actions within attr_obj which is an
attribute object containing lot of sub-actions <be>

Every command can be broken down into a series of makes and kills and
can be represented in the string. The way make is undone is by deleting
the object with the name stored.For kill, a backup of it is hidden and
stored with a suffix attached, when UNDO is called, the backup is
renamed by removing the suffix and unhidden.

Using the above mentioned technique undo was implemented for many
commands, but not a complex commands don't have undo functionality yet.
There are also a few TODO tasks before the PR is merged

-   Handle flags properly in the wrapper code
-   Enable the -n flag for UNDO
-   Randomize names of attribute objects that are created

Overall my GSoC experience was very good from the start to the end. I
ended up learning a lot of things from C functionality to how a
developer works and the importance of consistency. I would like to thank
Google, BRL-CAD, and my mentor Sean Morrison for the opportunity and
constant support.

Link to my PRs:
[Dummy UNDO command](https://sourceforge.net/p/brlcad/patches/570/)
[UNDO for make, kill and simple
commands](https://sourceforge.net/p/brlcad/patches/571/)
[UNDO using action
strings](https://sourceforge.net/p/brlcad/patches/572/)
- Vikram