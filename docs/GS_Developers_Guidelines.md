------------------------------------------------------------------------

## Development Procedure

This procedure is to be used for developing the identified sections of
the Geometry Service framework. It is very loosely based on the Unified
Process using UML. Since both of these development tools are extensible,
we are free to modify as we see fit. These, like all things pertaining
to this project, are not set in stone. As we learn, we will adapt.

1.  Define [Requirements](GS_Requirements_Standard "wikilink").
2.  Identify [Actors](GS_Actors_Standard "wikilink").
3.  Develop [Use Cases](GS_Use-Cases_Standard "wikilink").
4.  Repeat steps 1-3 until [Actors](GS_Actors_Standard "wikilink") and
    [Use Cases](GS_Use-Cases_Standard "wikilink") are as simplified and
    comprehensive as possible.
5.  Group Use-Cases into [Packages](GS_Packages_Standard "wikilink").
6.  Build applicable [Class
    Diagrams](GS_Class_Diagram_Standard "wikilink").
7.  Build [Sequence Diagrams](GS_Sequence_Diagram_Standard "wikilink").
8.  Refine [Class Diagrams](GS_Class_Diagram_Standard "wikilink") by
    adding methods.
9.  [Implement
    code](https://brlcad.svn.sourceforge.net/viewvc/*checkout*/brlcad/brlcad/trunk/HACKING).

-   At any given step, if a change needs to be made to a previous step,
    then step down the process flow from the change back to where you
    were working. This will ensure that a change made in step 3 will be
    accurately reflected in all subsequent steps.
-   Communication is KEY. If anyone makes a change anywhere in the
    documentation, a simple email to the dev team or log entry will
    suffice.
-   Requirements, Actor Definitions, Use Case Text Descriptions, and
    Package Lists will be maintained here on the wiki.
-   Use Case Diagrams, Graphical Package Lists, Class Diagrams, and
    Sequence Diagrams will be based on our UML editing application files
    and therefore maintain them would be difficult via a wiki. These
    will be maintained in the BRL-CAD SVN store:
    /brlcad/src/geoservice/devdocs/

Note: The best ***freeware*** version of a UML documentation application
(for Win32) that I have found thus far is
[StarUML](http://www.staruml.com/).
[Umbrello](http://uml.sourceforge.net/index.php) is a good one for
Linux/GNOME. If you know of one better, PLEASE mention it. The sooner we
settle on the applications we use for development, the less re-work we
will have to do. (I prefer ZERO rework, but that's a bit
unreasonable.)

