### GSoC 2018 Project Plan

#### Overall Goals

-   Work on Debian packaging situation for FreeCAD so improvements
    filter down to Ubuntu, Linux Mint, etc.
    -   Package FreeCAD 0.17
        -   w/ OCCT 7.2
        -   w/ Qt5 support via PySide2
        -   w/ external SMESH
        -   w/ Netgen
        -   w/ Python 3
    -   Package PySide 2 suite
        -   pyside2
        -   shiboken2
        -   pyside2-tools
    -   Package Netgen 6.2.18xx w/ OCCT 7.2
    -   Update Gmsh to use OCCT 7.2
    -   Package SMESH w/ OCCT 7.2
-   Work on packaging & distribution situation on Windows using Conda
    -   Translate packaging improvements in Debian-&gt;Conda
    -   Enable debugging & development support
-   Work on CI & CD solution using Buildbot
    -   Deliverable: Ansible playbook to deploy Buildbot workers on
        -   Debian/Ubuntu
        -   Windows 7/10
-   Come up with dependency graph using Graphviz & release documentation
    to streamline release process and ease management of dependencies

#### Phase 1

-   Primary goal: Finish PySide 2 packaging
-   Secondary goal: Begin Netgen & SMESH packaging

#### Phase 2

-   Primary goal: Finish Netgen, SMESH, and Gmsh packaging
-   Secondary goal: Begin Buildbot & Conda work on Windows

#### Phase 3

-   Primary goal: Finish Buildbot automation for Linux & Windows
-   Secondary goal: Finalize package improvements in Debian &
    Windows/Conda

### GSoC 2018 Final Report

My final work product summary is available at
<https://kkremitzki.github.io/blog/google-summer-of-code-2018-with-freecad/>.

In short, large deviation from the original plan occurred since I found
out PySide 2 packaging was being done by another person who was a
sponsored and well-accomplished Debian developer. Because of this, the
main thrust of the project instead became improving the overall FreeCAD
packaging ecosystem health, starting at the source of the Debian family
tree, Debian itself, so that improvements will make their way to
downstream distributions like Ubuntu and Linux Mint.

In this goal, the project was a huge success!