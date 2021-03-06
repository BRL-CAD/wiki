Archer is the next iteration of BRL-CAD's MGED model editing tool. We
are currently in the process of migrating functionality from MGED to
Archer, and there are many command-line commands that are currently not
supported in Archer but should be. Proposals for this task should
identify those commands, how to migrate them, how to test them, and any
features needed but not implemented in Archer to support running them.
The work over the course of the summer would be to perform the
migrations, verify the results, and fix issues as needed along the way.

A good proposal for this topic would include details on what commands
would be migrated and how (not per command, some general techniques are
in place), identify specifics needed to achieve full functionality in
Archer, and factor in time required for testing - if it don't work it
ain't migrated! Should also be looking to consolidate functionality
where it is duplicated and clean up, rather than blindly copying - if
there is a cleaner solution than the current setup for a particular task
the preferred way forward is to implement the "right" way and support
older commands as specific invocations of newer commands - for example,
dbfind should be a call to the more powerful search command, and the
graphical pattern tool in MGED needs to have its functionality merged
into the command line tool clone. A student looking to submit a proposal
for this task should do their homework and know what they're dealing
with.

# References

-   src/mged
-   src/libged
-   src/libtclcad
-   src/tclscripts/mged
-   src/tclscripts/archer
-   src/librt

# Requirements

-   Familiarity with C
-   Familiarity with Tcl/Tk
-   Knowledge of command handling in MGED, Archer, libged and possibly
    librt - scope of libraries and where functionality should live.
-   Background knowledge of BRL-CAD will make a major difference!

# Past Efforts

-   [GSoC11,GSoC12](../user/Bhinesley.md)
