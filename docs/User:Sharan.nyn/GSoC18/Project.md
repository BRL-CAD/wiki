**Name:** Saran Narayan

**Project Mentor:** Daniel Rossberg

**IRC Nick:** SaranNarayan

**SourceForge Profile:** **<https://sourceforge.net/u/sharannyn>**

**Brief Background Information**

3rd year B.Tech student aspiring Computer Science and Engineering at
Govt. Model Engineering College, Thrikkakara, India.

Google Code-In 2012 and 2013 finalist for BRL-CAD. I did 10 tasks in
2012 and 20 tasks in 2013. Most of them were modeling, graphics
designing and a few related to finding bugs.

I am well versed with C/C++ and have experience in graphic designing, UI
designing.

# Project Information

# Project Title: Implementing Check command in C and its GUI in Tcl/Tk

# Brief Project Summary

This project aims to bring cross platform compatibility to the existing
check command that is used by the Overlap tool. Also designing a GUI in
TCL that runs the check command. The output of this check command is
then used by the existing checker GUI.

# Detailed Project Description

**Introduction**

This project is amongst the user interface project ideas under the high
priority list. The overlap tool is used very often when creating models.
Overlaps are undesirable but they are bound to happen most of the times.
This tool provides features like detecting the overlaps, listing the
overlaps, visualizing it and giving options on how to eliminate them.

**Major Issue**

One of the major issues with the current implementation is the Linux
dependency of the overlap tool.The check.sh is a Linux script that is
used to detect overlaps and save them in an overlap file which is then
used by the overlap tool to tabulate, visualize and solve them. After
going through the current implementation of the check.sh, these are the
following steps that happen:

<b>

<li>

Finding the locations of the commands

</li>

</b>

The first step that happens in the script is that it finds the locations
of the commands the tool uses which are rtcheck, gqa, mged and loop.

<b>

<li>

Getting list of top objects if not provided

</li>

</b>

Next step is getting the list of top objects in the database file
provided, this list of objects are used to run the rtcheck and gqa
command.

<b>

<li>

Running rtcheck

</li>

</b>

Now for each object in the list, the rtcheck command is run for all
possible combinations of az, el ( 0, 45, 90, 135). Which gives 16
combinations for all objects. The logs of the rtcheck command is saved.

<b>

<li>

Parsing the logs of rtcheck

</li>

</b>

The logs of rtcheck are then processed by sed, cut and awk to return
just the overlap pairs, volume. This data is stored to a pairings file.

<b>

<li>

Running gqa

</li>

</b>

For a second opinion, the overlaps are checked for the same objects
again with grid spacing set to 1mm,1mm. The logs of the gqa command is
saved.

<b>

<li>

Parsing logs of gqa

</li>

</b>

The logs of gqa are now parsed using sed and awk to return just the
overlap pairs and volume. This data is appended to the pairing file.

<b>

<li>

Sorting and removing duplicate overlaps

</li>

</b>

The next step involves sorting the overlaps and removing duplicate
overlaps to get just the unique pairings. This output is then passed to
the checker.tcl file.

</ol>

Now to implement the above described features in C, I need to remove the
use of text processing done on the outputs of rtcheck and gqa commands
and refactor these commands so that they return required outputs which
can be directly used by the main program without the need of parsing.

The rtcheck command’s code is in /src/rt/viewcheck.c, the overlap list
is a linked list that has the following node structure:

1.  A pointer to the next node in the list, it’s a must in linked list.
    So that we can iterate the list
2.  Two character variables to store the overlapping regions
3.  A size_t type to store the unsigned count of overlaps
4.  A double type variable to store the depth of the overlaps

What I have to do is refactor the rtcheck command to a libanalyse
function, then make rtcheck use this function. Exactly what happens in
gqa command, which calls the add_unique_pair( ) function stored in
/src/libanalyse/overlaps.c The add_unique_pair function has the
parameters of the form:

1.  Pointer to a type of region_pair, which gets the address of the
    local overlap list used in gqa command.
2.  Two region structures which are passed from gqa after finding the
    overlapping pairs.
3.  A double type variable to pass the depth/thickness of the overlap.
4.  A point_t type variable to pass the coordinates where the overlap
    happens.

**User Interface**

I have thought of an interface that is easy to use, there will be two
ways to define the objects list to check the overlaps:

1.  Manually typing and add to the list of the objects to check
2.  Select from tree display of all items.

For a better idea look at the prototype I have in mind :

<center>

<figure>
<img src="CheckGUI.png" title="CheckGUI.png" width="800" alt="CheckGUI.png" /><figcaption aria-hidden="true">CheckGUI.png</figcaption>
</figure>

</center>

There are five components:

1.  Tree display of all objects in DB.
2.  List of the selected objects to check.
3.  Text input field to manually add or remove items from the list of
    selected objects.
4.  Check top objects button.
5.  Check and Clear buttons.

For tree display, I will look into the code for the browse geometry
tool, located in /src/tclscripts/geometree/

Adding the list would be fairly simple, I would look into the
checker.tcl which uses a list to display overlap pairs.

For the manual inputs, I need to check if it exists already in the list
of objects before removing or adding items and show an error if an
already added item is being added or an item is deleted which doesn’t
exist in the list.

The check top objects button calls the check.c command without any
arguments so it automatically run the tool on top objects.

The clear button would be useful to discard the list of selected objects
and start over.

The check button executes the newly written check.c command with
selected objects as arguments.

# Deliverables

-   First Deliverable:
    -   Libanalyze function.
    -   Refactored rtcheck command.
    -   Basic implementation of check command.

<!-- -->

-   Second Deliverable:
    -   Complete implementation of the check command
    -   Basic GUI for the check command.

<!-- -->

-   Final Deliverable:
    -   Finished GUI for the check command.

# Timeline

-   Week 1:
    -   Implement a libanalyze function - analyze_overlaps() to do the
        work rtcheck does.
    -   Start implementation of the check command - call this libanalyze
        function like the current shell script does for rtcheck, get the
        results as overlapList.

<!-- -->

-   Week 2:
    -   Continue work on rtcheck if it was incomplete in the previous
        week.
    -   Add capabilities of gqa to this libanalyze function.
    -   Call the libanalyze function for the newly added gqa features
        and get the results as the overlapList in check command

<!-- -->

-   Week 3:
    -   Continue work on gqa if it was incomplete in the previous week.
    -   Refactor the existing rtcheck to use the new libanalyze
        function.

<!-- -->

-   Week 4:
    -   Testing, debugging and cleanup.
    -   Getting the check command ready for the first deliverable.
    -   Start adding functions to do the processing of the overlapList.

<!-- -->

-   Week 5:
    -   1st evaluation report submission.
    -   Add the remaining work done by the shell script to the check
        command, like sorting, removing duplicates and writing output to
        a pairing files to be used by the overlap GUI.

<!-- -->

-   Week 6:
    -   Calling the overlap checker tool from the check command.
    -   Start working on the GUI part of the check command.

<!-- -->

-   Week 7:
    -   Finish a basic GUI to call the check command before the 2nd
        evaluation.

<!-- -->

-   Week 8:
    -   Testing, debugging, documentation and cleanup to prepare for the
        second deliverable.

<!-- -->

-   Week 9:
    -   2nd evaluation report submission.
    -   Start adding more advanced features to the check commands GUI
        like tree list view.

<!-- -->

-   Week 10 & 11:
    -   Complete the GUI part with the proposed features fully
        implemented.
    -   If time allows add ability to use \* wild card for bulk
        add/remove objects to the list.

<!-- -->

-   Week 12:
    -   Final testing and bug fixing.
    -   Documentation and code cleanups before final submission.

<!-- -->

-   Week 13:
    -   Prepare final report on the project.

# Time Availability

I will be devoting at least 40 hours/week for this project and more if
needed. During my vacations that is from May 17,2018 to August 1,2018, I
have no other obligations planned that overlaps with the coding period.
I will be having my end semester exams from April 26,2018 to May
17,2018. I will manage by allocating time judiciously.

# Additional Information

I have submitted the following patches during application period and
application review period:

Fixed a bug with the existing overlap tool:

`   `[`https://sourceforge.net/p/brlcad/patches/476/`](https://sourceforge.net/p/brlcad/patches/476/)

A task assigned by Sean, a simple command that prints hello message

`   `[`https://sourceforge.net/p/brlcad/patches/478/`](https://sourceforge.net/p/brlcad/patches/478/)

A TODO task under libged, in src/libged/tables.c where a temporary file
is getting used, is created by bu_temp_file( ).

`   `[`https://sourceforge.net/p/brlcad/patches/479/`](https://sourceforge.net/p/brlcad/patches/479/)

A TODO task, added support to rt tools and gtools for specifying az/el
in radians or degrees with an explicit 'rad' suffix and an implicit
'deg' suffix.

`   `[`https://sourceforge.net/p/brlcad/patches/481/`](https://sourceforge.net/p/brlcad/patches/481/)
`   `[`https://sourceforge.net/p/brlcad/patches/482/`](https://sourceforge.net/p/brlcad/patches/482/)

# Why BRL-CAD?

CAD softwares and making models in 3D were always my interests. BRL-CAD
gave me the taste for open source development in my experience with
Google Code-In. The mentors are really friendly and helpful. The
projects under BRL-CAD are interesting and practical.

# Why Me?

I am really excited to work with BRL CAD on this project. I am always
looking forward to opportunities to learn new things. I am persistent
and hardworking.