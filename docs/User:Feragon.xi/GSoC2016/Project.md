## LibreCAD 3 Scriptable User Interface Creation

### Brief project summary

LibreCAD 3 have a new code base. Currently the only way to create
objects is writing a Lua script, and there is no means to manipulate
entities after their creation.

This project aims at making the program usable for an end-user, who
should be able to create and edit documents without writing Lua code.

### Detailed project description

LibreCAD 3 is currently divided into 3 parts:

-   The user interface
-   The kernel
-   The CAD Viewer

This project involves working with the LC user interface by creating a
framework and a GUI, and the LC kernel to add the selection of entities.

#### Kernel

Actually items selection is only available in the drawer¹, not in the
kernel. The kernel will need a modification to add the possibility to
select one or more elements and operate on them.

A new method will be added to the entities to get their definition
points, that will be displayed when hovering them. The user can modify
the document by moving these points.

##### References

-   <https://github.com/LibreCAD/LibreCAD_3/blob/master/lcviewernoqt/drawitems/lcvdrawitem.cpp>

#### Framework

The framework should allow to create and modify entities stored in the
kernel.

The constraint is to be independent of drawing engine and input method,
so others CAD programs could use the LCv3 engine and it can facilitate
the port to other platforms (mobile, tablet, ...), so it should not
depend on Qt or other GUI library. It must be extendable to evolve with
the code. The framework should be able to deal with all the methods used
to create and modify entities, for example a circle can be created by
giving two points or a point and the radius.

It will be called by the UI for each user action and will be composed of
an element for each entity available in the kernel.

The framework will be scriptable so we can modify the interface without
recompiling. Lua will be used for this part, the actual kernel bindings¹
should be sufficient for this part.

##### Reference

-   <https://github.com/LibreCAD/LibreCAD_3/blob/master/lcadluascript/cad/lualibrecadbridge.cpp>

#### GUI

The GUI should contain all the elements to create and manipulate
entities. The framework will be called when an operation is selected and
should allow the user to enter data manually in the console, or
automatically in the canvas by selecting points or entities.

It will be composed of Lua scripts for the same reason as the framework.
The current Lua interpreter contains Qt bindings¹ but it’s only the data
types.

New bindings will be created to manipulate Qt elements with Lua.

An API will be created to allow the framework to request data from the
user. The main window will contain the buttons for each actions and a
command prompt to enter Lua code, so instead of writing all the Lua
script, the user can select the elements on the window and just enter
one function.

##### Reference

-   <https://github.com/SteveKChiu/lua-intf/blob/d6f17a8a474814d337e1dd867238e1d5ba1b7e5c/LuaIntf/QtLuaIntf.h>

### Deliverable

This project will add the following features to LibreCAD 3:

-   Scriptable User Interface
-   Operations on entities exposed to the user
    -   Creation
    -   Rotation
    -   Move
    -   Copy
    -   Remove
-   GUI elements to do the operations
-   Unit tests

### Why LibreCAD ?

I used some CAD programs before and LibreCAD is the only one compatible
with Linux which allows me to do what I need. And I think LibreCAD 3 has
advantages over some proprietary CAD software, it is faster to start.

### Why me ?

I have a good experience with C++, Qt and Lua as required for this
project. As I already worked with CAD softwares, I understand the users
expectations from LibreCAD.

### Time availability

I can work at least 40 hours a week and more if needed.

I have a finals week during the week of the 23 May, I'll do some work on
the selection part during the community bonding period to not having too
much delay on the schedule.

### Development schedule

-   Community Bonding Period:
    -   Get to know about the community and the code
    -   Adapt proposal with feedback and new ideas
    -   Remove unused files of actual User Interface
    -   Improve the Lua UI code sent for evaluation
    -   Begin working on the selection instead of the week of 23 May
-   23 May - 28 May:
    -   Finals week
-   29 May – 31 May:
    -   Add selection of entities in the kernel
-   1 June – 14 June:
    -   Add GUI elements
    -   Add the API to use them
-   15 June – 26 June:
    -   Implement creation for each entities
-   27 June – 6 July:
    -   Implement rotation for each entities
-   7 July – 17 July:
    -   Implement move for each entities
-   18 July – 27 July:
    -   Implement copy for each entities
-   28 July – 3 August:
    -   Implement remove for each entities
-   4 August – 14 August:
    -   Creating unit tests
-   15 August – 23 August:
    -   Code cleanup
    -   Fixing bugs
    -   Preparing final submission