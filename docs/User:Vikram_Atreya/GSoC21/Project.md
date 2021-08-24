## **Implementing UNDO command**

### Community Bonding

-   Set up the blog and wiki
-   Decide on which approach to implement UNDO

### Development Plan

-   Week 1: Decide architecture and create the required files to have an
    undo cmd
    -   Add files to libged, make changes in Cmake files and decide on
        space/location to store the temporary data being generated.
        Write documentation on how the undo command is going to be
        implemented and how it will work.
-   Week 2: Start implementing the UNDO logic
    -   Check for different commands like kill, make and other basic
        commands for proper compatibility with the UNDO command.
-   Week 3: Continue the implementation
    -   Start working and testing for complicated commands like dbconcat
        which deal with overwriting, creating new objects and deleting
        multiple objects. In the partial + events method this might take
        more time as splitting commands into events is a big task.
-   Week 4: Get a basic review and start testing
    -   Take inputs from my mentor on current progress and how I could
        improve the code. Write tests for various cases and check
        robustness.
-   Week 5: Continue testing and optimizing code
-   Week 6: Work on further optimizations / Account for unforeseen
    delays
    -   I will keep this week as a buffer.
-   Week 7: Optimizations to UNDO
    -   Depending on the method chosen, work on improving the time/space
        complexity of the implementation.
-   Week 8: Document work and issues faced
-   Week 9: Prepare for final evaluations

### Design ideas

-   Facilitate 10-15 undos from the latest state
-   Initially no redo command and later states are deleted once undo is
    used
-   Works only on objects and not on other data stored
-   Plain undo with no flags does just 1 undo
-   \`\`\` -n X\`\`\` flag does multiple undos, where X is no of undos
    to be done

### Implementation ideas

-   Full checkpoint is stored before 15 commands.
-   Form an array with values as names of all non-hidden objects, search
    for backups in hidden objects (backup should have a version just
    previous to the no of undos requested). After iterating through all
    backup objects if we do not find a backup, ,which should ideally be
    found in the full checkpoint even if it was not backed up later, we
    killthat object.
-   Undo can also be considered to be a normal command and full
    checpoint can be created before undoing, so that redo will be done
    with an undo.