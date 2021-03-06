In recent years, tools like graphviz have made automatic graphical
layout of graph structures in images both practical and useful.
Traditionally, geometric hierarchies in BRL-CAD databases have been
visualized either as lists or trees, and those methods continue to be
the primary geometry browsing methods.

This task would follow up on work from 2012 using automatic graph layout
libraries to produce a graph based visualization of the structure of .g
databases:

[user/Cprecup/GSoC2012_progress](../user/Cprecup/GSoC2012_progress.md)

The task is not simply to generate images of graphical geometry
hierarchies - that is relatively straightforward and can be done with
scripts - but to design graphical, interactive widgets that utilize
graph algorithms to interactively display geometry structure in useful,
intuitive and interactive ways (tying changes in wireframe 3D renderings
to selection or de-selection of nodes in a graph display of .g geometry,
for example). Some progress was made in 2012, but there is a lot more
that can be done.

Our current interfaces use the Tk toolkit, but Qt would also make an
interesting toolkit for this sort of work.

Proposals should include specific ideas (mockups and example layouts are
a good way to convey graphical ideas).

# References

-   src/tclscripts
-   src/tclscripts/mged
-   src/tclscripts/archer
-   src/libtclcad

Potentially useful libraries must be under a compatible (BSD, MIT,
LGPL2) license - (work so far has been done using the Adaptagrams
library):

-   Adaptagrams: <http://adaptagrams.sourceforge.net/>

# Requirements

-   Familiarity with Tcl/Tk and/or Qt
-   Familiarity with C/C++
-   Comfortable understanding of graphs (will be working with graph
    libraries)

# Past Efforts

-   [GSoC12](../user/Cprecup/GSoC2012_progress.md)
