BoTs (bags of triangles) are BRL-CADs basic triangle primitive,
generally used to represent other triangle based formats that are
imported into BRL-CAD. MGED has very limited abilities when it comes to
editing BoTs, and Archer has virtually none.

This task would be to design and implement in Archer user interfaces,
tools (if needed), and routines to allow for intuitive, effective
editing of BoT primitives. Some operations to support:

-   Tabular lists of all vertex, edge, and face components of a BoT,
    with ability to select subsets (see Archer's Combination Editor for
    an example of using tktable for this kind of editing)
-   Graphical selection of subsets of a BoT (building on existing
    functionality that can perform some of this work - discuss with
    developers in IRC before submitting a proposal)
-   Graphical in-window feedback on what bot components are selected.
-   Merge, delete, and insert operations (these will take some thought)
-   Apply translation to subsets of a BoT and update the graphical
    display while doing so.

Other ideas based on other mesh editing tools are certainly welcome, but
the goal is to allow basic operations in a straightforward, organized
fashion. User interface mockups are a good idea for this proposal.

# References

-   src/librt/primitives/bot
-   src/tclscripts/mged
-   src/tclscripts/archer
-   src/libtclcad

# Requirements

-   Familiarity with Tcl/Tk
-   Basic understanding of BoT data structures and editing operations