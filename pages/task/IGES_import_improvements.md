One of BRL-CADs most complex and complete converters is the iges-g
converter, which converts Initial Graphics Exchange Specification files
into BRL-CAD geometry databases.

There are two more or less distinct challenges for iges-g improvement,
which may go hand-in-hand. Since the original code was written, BRL-CAD
has changed the underlying storage format for its NURBS primitive. The
iges code needs to be updated to write out the new openNURBS format.

The other challenge is that as exporters have changed in CAD systems
over the years, new wrinkles have appeared that our IGES converter does
not seem to handle. Once iges-g is generating the new NURBS files, it
needs to be tested against current IGES exports from CAD programs and
updated to handle any items it doesn't currently deal with.

The first focus is getting the NURBS import code updated, but it may
well be that other fixes to the IGES code will be needed before the
converter can import a reasonably modern test model - this will be
something for a student to determine when putting together a proposal.

# References

-   src/conv/iges
    -   src/conv/iges/n_\* is a 'new' IGES importer started for
        importing NURBS, but never finished
    -   the old importer only imports polygonal IGES
    -   the two should be merged and support for NURBS import added
-   src/other/openNURBS
    -   we use this library for representing NURBS
-   src/proc-db/\*.cpp
    -   examples of using openNURBS to construct geometry

# Requirements

-   Familiarity with C
-   Sufficient understanding of NURBS geometry to understand import
    issues
-   (optional) Familiarity with the IGES standard