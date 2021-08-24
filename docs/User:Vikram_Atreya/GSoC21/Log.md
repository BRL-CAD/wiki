# Development Logs

## Community Bonding Period

-   Forked github repo and compiled working version of BRL-CAD
-   Made the pages for project plan and dev logs
-   Ideated various ways to implement undo and set constraints

## Weekly update - Coding Period

-   Week - 1
    -   Day 1-2
        -   Working version of undo command implemented in mged which
            prints name of database when command is given.
        -   Understood how commands use wrapper functions and function
            of cmd_ged_plain_wrapper()
        -   Set flags -n and -h aimed to execute multiple undos and show
            usage respectively
        -   Understood how hidden objects work, have to explore
            temporary file alternative to save backup objects
        -   Stuck, trying to iterate over all objects in database but
            not finding the right function
        -   Finally found way to iterate over all objects from
            move_all.c
        -   Converted undo.c to undo.cpp so that code can be more
            functional
    -   Day 3-4
        -   Had a discussion with my mentor how to proceed further on
            the undo
        -   Data accesible over all processes stored in _GLOBAL as
            name, value pairs
        -   Name of the last added object and last killed object stored
            in _GLOBAL
        -   Wrappers of make and kill modified to add the labels
        -   Introduced 3 variables in undo.cpp to keep track of
            latest_change and then take necessary action to undo
    -   Day 5-6
        -   Enabled undo for in command; Now working to enable undo for
            killall
        -   Did tutorials to understand how combinations and regions
            work
        -   Went in the wrong direction intially; Took a day to
            understand how combinations are stored
-   Week - 2
    -   Day 1-2
        -   Encountered many bugs while implementing undo for killall
        -   Ubuntu had some problems; mouse and keyboard stopped working
            and stopped work for sometime
        -   Tired refactoring code of backup storage for make; Chose to
            make a gmd_cmd for it but did not happen, also felt it was
            not the best option
        -   Succesfully implemented undo for kill by modifying code in
            libged/killrefs; Might have to write a new wrapper for this
        -   Created new wrapper for g (group) command and implemeted
            undo for it; Some refinement left here
    -   Day 3-4
        -   Refined code of g cmd undo and updated PR
        -   Attempt at reefactoring code to libged/undo.cpp failed; Not
            right place to put the code
        -   Refactored make's undo code into mged/utility1.c and
            replaced code in make, in and g
        -   Solved major bug that made children objects disappear when
            any object was killed
        -   logic: renamed all leaves by adding sufffix, thereby poiting
            to imaginary objects and not hiding the references it had
            previously
    -   Day 5-6
        -   Implemented undo for mv and mvall
        -   Also restructured code in undo.cpp to accommodate more cmds
            easily
        -   Made a spreadsheet with status of implementation for all
            commands

<!-- -->

-   Week - 3
    -   Day 1-2
        -   Solved a long pending bug
    -   Day 3-4
        -   Took a break
    -   Day 5-6
        -   Started work on storing objects as data in binary objects
        -   Understood code of mk_binunif, make and libged/bo.c

<!-- -->

-   Week - 4
    -   Day 1-2
        -   Done writing basic test to store and recover objects from a
            binary object
        -   Stored internal data in binary object, storing external data
            is better since it contains type information as well
        -   Switched code from storing internal to external of object
    -   Day 3-4
        -   Ideated and tried different ways in which we could store the
            recovery data
        -   Wrote code implementing a new struct in ged/defines.h
        -   Mimicked history implementation for the struct
    -   Day 5-6
        -   Implemented undo using the struct but realized it would not
            work
        -   Thought of using char\*\* arrays to store the commands
        -   Have to discuss with mentor on a better approach