Currently, most raytracing for analysis purposes uses textual output to
convey its results to the user, with very little integration into
graphical environments. (The nirt and gqa tools can optionally visualize
their results in MGED as wireframe lines.)

This project would significantly enhance the integration of tools such
as nirt and gqa into graphical modeling environments (preferably Archer,
since it will eventually become the new MGED modeler). A strong proposal
will show significant research into how the tools are used and what user
interface improvements would be made (be specific - creating mockups
such as <http://bzflag.bz/~starseeker/nirt_mockup.png> and including
them with your proposal is a good way to convey user interface ideas).
The student should experiment enough to have a good feel for how long it
would take to implement their proposal.

# References

-   src/nirt/nirt.c
-   src/gtools/gqa.c
-   src/tclscripts/archer

# Requirements

-   Familiarity with BRL-CAD analytical raytrace tools (nirt, rtcheck,
    rtweight, gqa)
-   Familiarity with Tcl/Tk (and preferably Itcl/Itk)