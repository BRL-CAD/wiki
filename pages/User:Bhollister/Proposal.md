# Title

Command-line Editing NMG Data-structures in BRL-CAD

# Abstract

This project will expose some of the low-level NMG routines to a
command-line interface. Users will be able to add and remove various
parts of the NMG data structure, such as regions and shells, along with
manipulation of vertices, edges, and faces. Users will see the results
displayed in either MGED or Archer.

Additional info:
<http://people.ucsc.edu/~behollis/hollisterGSoC2015Revised2.pdf>

# Benefits to BRL-CAD

BRL-CAD will gain a command-line interface for directly editing NMG
data- structures via Archer. The new features will be:

-   Ability to select subsets of an NMG via the command-line.
-   Ability to add and remove elements of an NMG while still satisfying
    validity constraints through the command-line.
-   Ability to move parts of an NMG via the command-line.
-   Visual feedback in the geometry window.

# Deliverables

The implementation will consist of C code integrated with relevant
modules (/librt/primitives/nmg/, etc.).

# Project Details

See [MGED CMD nmg](http://brlcad.org/wiki/MGED_CMD_nmg). The new command
*design* is similar to [brep](http://brlcad.org/wiki/MGED_CMD_brep).

# Project Schedule

Milestones:

-   Week 1: Add placeholder commands by following example in commit
    46507, which adds the exist command. Make sure that commands can be
    added and data is reflected internally.
-   Week 2: Identify ways of specifying to the command-line the parts of
    model to be changed. For example, how to specify a vertex to a
    command that removes a vertex and update the NMG model in the render
    window.
-   Week 3: Should be able to implement commands now. Allow two weeks to
    complete each type of command. Starting this week with NMG
    CONSTRUCTION ROUTINES.
-   Week 4: CONSTRUCTION ROUTINES - initial take is to provide CLI for
    existing internal nmg_\* api routines.
-   Week 5: CONSTRUCTION ROUTINES - initial take is to provide CLI for
    existing internal nmg_\* api routines.
-   Week 6: CONSTRUCTION / DESTRUCTION ROUTINES.
-   Week 7: CONSTRUCTION / DESTRUCTION ROUTINES.
-   Week 8: High-level design of nmg command. Implement face selection /
    face removal.
-   Week 9: design / work on nmg traversal + labelling for cli + cmface,
    mm, kill F, kill V, labelface
-   Week 10: ditto
-   Week 11: ditto
-   Week 12: ditto
-   Week 13: move V, -i option for labelvert, make V, and make F
-   Week 14: move V, -i option for labelvert, make V, and make F