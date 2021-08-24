# Project Info

|                  |                            |
|------------------|----------------------------|
| **Project Name** | Materials Database Project |
| **Student Name** | Mihai Neacșu               |
| **IRC nick**     | mihaineacsu                |

# Logs

# Week 1

-   1 - 5 Jun:
    -   Nothing, had final exams

# Week 2

Nothing

# Week 3

-   13 - 22 Jun:
    -   Nothing, worked on thesis

# Week 4

-   23 Jun
    -   Learned how to use libcurl and looked into a mockup library for
        libcurl in order to test functionality.
-   24 Jun
    -   Went over the BRL-CAD tutorial series and got a basic
        understanding on how to use it.
-   25 Jun
    -   Started reading rtweight and gqa source files to get a better
        idea on how they work.
-   26 Jun
    -   Running a few experiments made it all clearer and also took on
        an easy task (rtweight behaviour on primitives). This proved
        really insightful on how rtweight and gqa work and what are some
        of the used structs.
-   27 Jun
    -   Modify rtweight to accept file paths for the .density file.
-   28 Jun
    -   Break
-   29 Jun - 1 Jul
    -   Modify rtweight and gqa to use local and remote URIs for
        .density files

# Week 5

-   2 Jul
    -   Had to digg around to understand how to add libcurl to the build
        process.
-   3 Jul
    -   break
-   4 Jul
    -   Made the suggested changes to the last patch: added 2 interfaces
        to libbu, one for curl requests (eliminated duplication) and one
        for reading lines from a string, resembling bu_fgets.
-   5 Jul
    -   Added unit tests for gqa GET requests.
-   6 Jul
    -   break

# Week 6

-   7 Jul
    -   Refactored changes made to rtweight
-   8, 9 Jul
    -   Nothing
-   10, 11 Jul
    -   Started working on what seemed a low hanging fruit, there was an
        issue with cmake when build path contained spaces
-   12-14 Jul
    -   Break

# Week 7

-   15-18 Jul
    -   Researched how objects are stored and managed within the
        database: looked into most data structures and functions
        associated to creation, db import/export. Managed to create
        dummy object with dummy data to test things out.
    -   Started working on creating the materials object and it's
        functions that will added as a new entry in OBJ, the struct
        rt_functab vector.
    -   As for the materials file formats: started integrating libcsv.
        libxml is already bundled with BRL-CAD.

<!-- -->

-   19, 20 Jul
    -   Break

# Week 8

Objective: Continue working on creating the materials object and also
check out how shaders are stored in order to also start working on
making a shaders object.