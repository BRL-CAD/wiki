The in-development code for BRL-CAD can be accessed via Subversion using
the command

    svn co https://svn.code.sourceforge.net/p/brlcad/code/<module>/trunk <module>

where <module> is one of the following:

-   **brlcad** - If you don't know which you want, this is probably it.
    This branch contains the code for the full BRL-CAD suite itself,
    including tools such as mged and rt.
-   **jbrlcad** - A currently inactive experimental project consisting
    of a very partial implementation of librt in pure Java. This served
    as a study of the adaptability of librt's interface to an object
    oriented paradigm, which turned out to be very high.
-   **rt^3** - Early development of a C++ geometry engine interface and
    a new modeling GUI.
-   **rtcmp** - Code for a tool to compare the output of librt with that
    of other ray tracing libs.
-   **web** - Placeholder for version control of the website.

More information about specific branches and the code contained within
them can be had by [contacting the
developers](http://brlcad.org/d/contact) responsible, or a similarly
knowledgeable community member.

Some information may be found on other pages here. To wit:

-   [Mime-types](/wiki/doc/Mime-types.md)
-   [Undoing a commit](Undoing-a-commit.md)

[category:Getting started](category:Getting_started.md)
