LibreCAD Kernel Documentation/API Documentation for the usage with other
softwares.

LibreCAD kernel is a library to perform 2D operations. Rightnow it
supports the basic entities like circle, line, arc, ellipse ( Although
can be extended to b-splines, beizer curves ) and the code is built in
C++ and Qt. .

It now follows a document based approach and has been designed to be
very extensible.

It supports the operations of creating, deleting and trimming of
entities. Has an undo-redo stack hence you can do unlimited undos and
redos.

Things that are going to be implemented in GSoC are,

-   support for moving entities from one position to another.
-   Ability to copy entities any number of times.
-   Scaling the entities.
-   Rotating the entities with respect to some point.

<!-- -->

-   It will have support for text and dimensioning after the GSoC
    period.

Directory structure and operations,

Base directory :

cadentity.\*

It is the base class for all entities and each entity is inherited from
this class.

id.\*

These file contain the class that generates a unique ID for every new
entity so created.

metainfo.\*

These files contains the classes which are metatypes for any entity. For
example the pen color, line width, layer of entity.

Dochelpers :

These are the implementation files of the files in document folder(
containing the virtual functions).

documentimpl

contains the following functions,

-   addentity
-   removeentity
-   begin a process
-   commiting a process

documentlayerimpl

-   add entity // adds an entity to the layer
-   remove entity // removes the entity from the layer
-   find by id // Finds the entity by the unique ID specified

layermanagerimpl It manages the layers, adds/deletes layers.