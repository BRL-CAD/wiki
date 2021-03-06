# Application Domain

The C++ interface is a object oriented API to BRL-CAD's core libraries
around librt. The target users are developers of applications which use
BRL-CAD libraries.

Furthermore, this interface should be a good reference to the use of
BRL-CAD's standard C interface, although a higher level interface should
also be available.

# Requirements

## The interface should be self-contained

I.e., source code using this interface should not need to include any
other BRL-CAD header file (nor TCL, openNURBS, ...).

As a consequence, the interface will hide implementation details.
Therefore the implementation can be changed without affecting an
application using this interface.

# Main Classes

## ConstDatabase

The **ConstDatabase** class provides a handle to read-only database
content.

If it is associated with a file the file will be opened read-only. I.e.
multiple instances of this class can refer to the same file.

## Database

The **Database** class is a virtual class which declares a handle to a
writable database. It is derived from **ConstDatabase** and expanded by
methods to modify the database's content.

## FileDatabase

The **FileDatabase** class provides a handle to writable file-based
database derived from **Database**.

## MemoryDatabase

The **MemoryDatabase** class provides a handle to writable in-memory
database derived from **Database**.

## Object

The **Object** class is the base class of all database objects (e.g.
primitives etc.).

# Examples

-   [A kind of a "Hallo World"
    program](CoreInterface_Hallo_World_Example.md)
-   [PrintTitle](CoreInterface_PrintTitle_Example.md)
-   [Tree walker](CoreInterface_Tree_Walker_Example.md)
