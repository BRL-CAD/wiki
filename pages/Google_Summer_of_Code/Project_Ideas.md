If you want to work on **computer-aided design (CAD), geometry, or
graphics**, you've come to the right place! Help us improve open source
CAD.

Well prepared proposals from capable students have an *outstanding*
chance of getting selected. We consider proposals for all skill levels
ranging from simple to crazy hard and everything in between. [Introduce
yourself](https://lists.sourceforge.net/lists/listinfo/brlcad-devel),
and we'll help you plan one right for you.

Remember that project descriptions are just *initial ideas*. You must
expand with [considerably more
detail](../Summer_of_Code/Application_Guidelines.md). Change the
goals to fit your experience and interests. See our
**[checklist](../Summer_of_Code/Checklist.md)** to get started.

This year, BRL-CAD is coordinating with five other communities that will
get 1-2 students each to help bridge our work and encourage
collaboration. Projects that help exchange data or share code are
desired!

|                                                                                                                                                         |                                                                                                                                                                          |                                                                                                                                  |
|---------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------|
| [![](http://www.openscad.org/assets/img/logo.png)](#openscad-projects)              | [![](https://raw.githubusercontent.com/alexrj/Slic3r/master/var/Slic3r_128px.png)](#slic3r-projects) | [![](https://librecad.org/img/logo.png)](#librecad-projects) |
| **OpenSCAD**: rich syntax, programmable geometry. Lots of possibilities to make it interoperate with BRL-CAD and LibreCAD.                              | **Slic3r**: toolpath/G-code generator for 3D printers.                                                                                                                   | **LibreCAD**: specializes in 2D CAD modeling, drafting, drawings. Help build a bridge to BRL-CAD or add STEP support.            |
| [![](http://brlcad.org/images/logo/BRL-CAD_gear3d_logo_164.png)](#brl-cad-projects) | [![](http://www.freecadweb.org/images/logo.png)](#freecad-projects)                                  |                                                                                                                                  |
| **BRL-CAD**: 3D solid modeling, geometry processing, and robust high-performance ray tracing. Help us make a better CAD system.                         | **FreeCAD**: parametric 3D modelling with strong Python interface and general engineering functionality like FEM and CAM                                                 |                                                                                                                                  |

**Project titles link to a page with more details.**

# BRL-CAD Projects

## High Priority Topics

This year, we are most interested in topics that will immediately
benefit BRL-CAD users. Please align your proposal with one of the
following three focus areas. Talk with us at
<http://brlcad.zulipchat.com>

|                         |                                                                                                                                                                                                                            |
|:-----------------------:|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     **Performance**     | Faster geometry. In order, ideas like**[Coherent Raytracing](../task/Coherent_Raytracing.md)**, anything involving OpenCL, parallelizing serial code, and eliminating LIBBU pointer aliasing.                              |
|   **User Interface**    | Build on Google Code-In progress (OpenSCAD-style GUI), [Convert MGED from Tk to Qt](../task/Convert_MGED_from_Tk_to_Qt.md), revamp our [Overlap tool](../task/Overlap_tool.md) GUI, etc. Qt and ray tracing are fair game. |
| **Core Infrastructure** | Integrate appleseed rendering, extend and deploy Online Geometry Viewer (OGV), expand our geometry conversion (GCV) library.                                                                                               |

## Web Development

|                                                                                                                                                                                                                                  |              Languages               | Difficulty |                                                                                              Contacts                                                                                              |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------------------------------:|:----------:|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| **[Synchronize Wiki with Docbook](../task/Synchronize_Wiki_with_Docbook.md):** We use Docbook for most of our user documentation but find editing a wiki page much easier to use. Set up a system so the two are always in sync. |    Depends (likely PHP or Python)    |   MEDIUM   |                                                                   [Yapp](#mentors)                                                                   |
| **[Online Geometry Viewer Back-end](../task/Online_Geometry_Viewer_Back-end.md):** Continuation of existing work, improve our interface for viewing geometry online. Focus on the back-end infrastructure.                       | C++, Javascript, Meteor.js, Three.js |   Medium   | [Morrison](#mentors),[Pooh](#mentors), [Panda](#mentors) |
| **[Mediawiki 3D Geometry Extension](../task/Mediawiki_3D_Geometry_Extension.md):** Write an extension for Mediawiki that will visualize our .g files. Maybe leverage LLVM C-&gt;Javascript translation.                          |    Depends (likely PHP or Python)    |    HARD    |                                                                 [Morrison](#mentors)                                                                 |

## Geometry

|                                                                                                                                                                                                                              |  Languages   | Difficulty |                                        Contacts                                         |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------:|:----------:|:---------------------------------------------------------------------------------------:|
| **[Plate Mode NURBS raytracing](../task/Plate_Mode_NURBS_raytracing.md):** Imported NURBS geometry often does NOT enclose space (i.e., not solid), so add support for specifying an implicit thickness.                      |    C/C++     |    HARD    |           [Morrison](#mentors)            |
| **[Overlap tool](../task/Overlap_tool.md):** Resolving geometric interferences (aka overlaps) is a common geometry editing activity. Design an awesome GUI for resolving conflicts.                                          |     Tcl      |    EASY    |   [Yapp, Morrison, Greenwald](#mentors)   |
| **[NURBS Editing Support](../task/NURBS_Editing_Support.md):** BRL-CAD doesn't currently have good support for editing NURBS primitives. Fix that.                                                                           |    C/Tcl     |   MEDIUM   |             [Yapp](#mentors)              |
| **[Vector Drawings from NURBS](../task/Vector_Drawings_from_NURBS.md):** Huge impact here if you can update one or more of our raytracers to provide vector output instead of raster. Perhaps render directly to PDF or SVG. | C and/or C++ |    EASY    |           [Rossberg](#mentors)            |
| **[NMG Editing](../task/NMG_Editing.md):** Our structured polygonal mesh geometry (N-Manifold Geometry = NMG) is a common export format, but our NMG edit support is non-existent. We need something.                        |      C       |    HARD    |      [Morrison, Rossberg](#mentors)       |
| **[Geometry Conversion Library](../task/Geometry_Conversion_Library.md):** Probably our biggest open source asset is our extensive collection of importers and exporters. Turn them all into a universal conversion library. |    C/C++     |    EASY    | [Greenwald, Morrison, Rossberg](#mentors) |
| **[STEP importer improvements](../task/STEP_importer_improvements.md):** We have an importer, but it's preliminary. Add support for importing hierarchy information, polygonal geometry, and implicit geometry.              |    C/C++     |   MEDIUM   |             [Yapp](#mentors)              |
| **[STEP exporter](../task/STEP_exporter.md):** We have an importer, we need a comprehensive exporter with support for implicit CSG, NURBS, or polygonal mesh geometry.                                                       |    C/C++     |    EASY    |        [Yapp, Morrison](#mentors)         |
| **[Convert BoT to Pipe](../task/Convert_BoT_to_Pipe.md):** Command line interface to convert facetted fluid/electrical line geometry into BRL-CAD native pipe solids.                                                        |  C/C++/Tcl   |   MEDIUM   |           [Morrison](#mentors)            |
| **[OpenSCAD Importer] (../task/OpenSCAD_Importer.md):** Create an importer for OpenSCAD's format.                                                                                                                             |    C/C++     |    EASY    |           [Morrison](#mentors)            |
| **[OpenSCAD Exporter] (../task/OpenSCAD_Exporter.md):** Create an exporter for OpenSCAD's format.                                                                                                                             |    C/C++     |    EASY    |           [Morrison](#mentors)            |
| **[Python Geometry](../task/Python_Geometry.md):** Wrap BRL-CAD's primitives in Python (or Lua), make it easier to script geometry creation.                                                                                 |  Python/Lua  |    Easy    |           [Morrison](#mentors)            |

## Performance & Quality

|                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Languages | Difficulty |                                      Contacts                                       |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------:|:----------:|:-----------------------------------------------------------------------------------:|
| **[Coherent Raytracing](../task/Coherent_Raytracing.md):** Our current raytrace pipeline dispatches and processes one ray at a time. Send bundles and convert the pipeline into phases.                                                                                                                                                                                                                                                          |   C/C++   |   MEDIUM   |    [Morrison, Rossberg](#mentors)     |
| **[OpenCL GPGPU Raytracing](../task/OpenCL_GPGPU_Raytracing.md):** We have about a dozen simple primitives that need to have a ray-object intersection function converted from C to OpenCL.                                                                                                                                                                                                                                                      | C/OpenCL  |    EASY    |         [Morrison](#mentors)          |
| **[OpenCL GPGPU Complex Raytracing](../task/OpenCL_GPGPU_Complex_Raytracing.md):** We have about half a dozen complex primitives that need to have a ray-object intersection function converted from C to OpenCL.                                                                                                                                                                                                                                | C/OpenCL  |   MEDIUM   |         [Morrison](#mentors)          |
| **[OpenCL GPGPU Spatial Partitioning Raytracing](../task/OpenCL_GPGPU_Spatial_Partitioning_Raytracing.md):** We use a Bounding Volume Hierarchy (BVH) to reduce the amount of intersections we need to compute to render an image. We need to replace this with a Kd-tree in order to be able to early terminate a render in models with high depth complexity. This should speed up render speed significantly for those models (e.g. Goliath). | C/OpenCL  |    HARD    |         [Morrison](#mentors)          |
| **[OpenCL GPGPU Brep Raytracing](../task/OpenCL_GPGPU_Brep_Raytracing.md):** We need to support Brep NURBS raytracing over the GPU. There is example CPU only code. Execution on the GPU should significantly enhance rendering performance of these primitives.                                                                                                                                                                                 | C/OpenCL  |    HARD    |         [Morrison](#mentors)          |
| **[NURBS Booleans](../task/NURBS_Booleans.md):** We have NURBS surface-surface intersections working. Now we're using them to create evaluated forms of our CSG geometry. Make it more robust and faster.                                                                                                                                                                                                                                        |   C/C++   |    HARD    |      [Yapp, Rossberg](#mentors)       |
| **[NURBS Optimization and Cleanup](../task/NURBS_Optimization_and_Cleanup.md):** We have a fantastic implementation of NURBS evaluation but haven't gone back to clean up or speed it up. Make it pretty and fast.                                                                                                                                                                                                                               |   C/C++   |   MEDIUM   |      [Yapp, Morrison](#mentors)       |
| **[Space Partitioning for Tessellation](../task/Space_Partitioning_for_Tessellation.md):** Technically an optimization task, make our geometry converters run an order of magnitude faster by using spatial partitioning during tessellation.                                                                                                                                                                                                    |     C     |    HARD    | [Greenwald, Yapp, Morrison](#mentors) |
| **[Faster Overlap Detection](../task/Faster_Overlap_Detection.md):** BRL-CAD has a 'gqa' tool that detects overlaps. Implement a replacement using a better approach.                                                                                                                                                                                                                                                                            |     C     |   MEDIUM   |    [Greenwald, Morrison](#mentors)    |

## Infrastructure

|                                                                                                                                                                                                                                               | Languages | Difficulty |                                      Contacts                                       |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------:|:----------:|:-----------------------------------------------------------------------------------:|
| **[New Cross-Platform 3D Display Manager](../task/New_Cross-Platform_3D_Display_Manager.md):** BRL-CAD uses ***display managers*** for visualizing 3D geometry in a window. We want one that uses a cross-platform toolkit such as Qt + OGRE. |   C/C++   |   MEDIUM   |         [Morrison](#mentors)          |
| **[New Cross-Platform 2D Framebuffer](../task/New_Cross-Platform_2D_Framebuffer.md):** BRL-CAD uses ***framebuffers*** to display 2D imagery. The merits of having a single interface for most platforms is self-evident.                     |   C/C++   |    EASY    |      [Morrison, Yapp](#mentors)       |
| **[General Tree Walker](../task/General_Tree_Walker.md):** We have a half dozen or more functions that will traverse a geometry hierarchy in different ways. There only needs to be one.                                                      |     C     |    EASY    | [Greenwald, Yapp, Morrison](#mentors) |
| **[GED Transactions](../task/GED_Transactions.md):** Migrating functionality from our MGED geometry editor into our LIBGED library provided excellent code reuse, but now we need transactions so that actions can be undone.                 |     C     |    EASY    |      [Morrison, Daga](#mentors)       |
| **[Add exec option to search](../task/Add_exec_option_to_search.md):** Our LIBGED library provides a *search* command very similar to the UNIX *find* command for scanning through geometry. Implement the -exec option.                      |     C     |    EASY    |        [Yapp, Daga](#mentors)         |
| **[Astronomical units](../task/Astronomical_units.md):** We already go "big", but accurately modeling at a galactic scale redefines that notion...                                                                                            |     C     |    EASY    | [Morrison, Greenwald, Daga](#mentors) |
| **[Object-oriented C++ Geometry API](../task/Object-oriented_interfaces.md):** Extend our C++ library which provides a simple interface to BRL-CAD's core functionality. Kickstart start a new geometry kernel.                               |    C++    |   MEDIUM   |      [Rossberg, Kamga](#mentors)      |
| **[Point Clouds] (../task/Point_Clouds.md):** BRL-CAD has a basic point cloud primitive. Beef it up, make it faster, maybe integrate with the Point Cloud Library (PCL) for evaluation.                                                        |   C/C++   |   MEDIUM   |      [Browder, Kamga](#mentors)       |
| **[Annotations](../task/Annotations.md):** Implement support for 2D annotations, labels that can be added to geometry.                                                                                                                        |   Perl    |    EASY    |          [Browder](#mentors)          |

## Rendering & Scientific Analysis

|                                                                                                                                                                                                                                                 |  Languages   | Difficulty |                                   Contacts                                    |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------:|:----------:|:-----------------------------------------------------------------------------:|
| **[Appleseed renderer integration](../task/Appleseed.md):** Appleseed is rendering infrastructure used by the film industry to make pretty pictures. Make it shoot rays at our native geometry with our ray trace library. |      C       |   MEDIUM   |      [Morrison](#mentors)       |
| **[Material and Shader Objects](../task/Material_and_Shader_Objects.md):** This one is a biggie but easy. Implement new object entities for describing shaders and material properties, use them during ray tracing.                            |      C       |    EASY    |      [Morrison](#mentors)       |
| **[Generalized abstracted spacial partitioning capability](../task/Generalized_abstracted_spacial_partitioning_capability.md):** Need more be said? If you're familiar with BSPs, KD trees, and grid structures, then this one is for you.      |      C       |    HARD    | [Greenwald, Morrison](#mentors) |
| **[High Dynamic Range Support](../task/High_Dynamic_Range_Support.md):** We don't have displays supporting this yet, but that's never stopped us before. Implement support for images with more than 8-bits per channel.                        | C and/or C++ |    EASY    |   [Greenwald, Yapp](#mentors)   |
| **[Analysis Library](../task/Analysis_Library.md):** There are various tools in BRL-CAD for calculating weights, moments of inertia, and more. They're stand-alone applications. Turn them into a library.                                      |      C       |    HARD    |   [Yapp, Morrison](#mentors)    |
| **[Celestial mechanics particle system](../task/Celestial_mechanics_particle_system.md):** Simulate solar systems and galaxies.                                                                                                                 |    C/C++     |   MEDIUM   |      [Greenwald](#mentors)      |
| **[Density functions](../task/Density_functions.md):** Accurately represent everything from atmosphere to bone. Implement support for parametric density functions for homogenous materials.                                                    |      C       |    HARD    | [Rossberg, Morrison](#mentors)  |
| **[Bending light](../task/Bending_light.md):** Think gravity wells and satellite cameras.                                                                                                                                                       |      C       |   MEDIUM   |      [Morrison](#mentors)       |

Open Channel For Goods Using Optics +robotics concept: We can Create A
Tunnel Like way Where we can transport goods like We Transport data
through seas Using Optics. Only Need Is To make it automated with
perfect coding for destination. We can Do this with the help of
Software+Mechanical Engineers. Where coding and assembly plays important
role.. Coding can Be Done In General By C/c++ language which is Simpler

# OpenSCAD Projects

[OpenSCAD](http://openscad.org) is a parametric solid 3D modeling tool
which uses a Domain Specific Language to specify designs as plain text.
It is specifically designed with 3D printing in mind.

|                                                                                                                                                                                                                                                                                             | Languages/Tools | Difficulty  |                                 Contacts                                 |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------:|:-----------:|:------------------------------------------------------------------------:|
| **[Improve DXF Import and Export](https://github.com/openscad/openscad/wiki/Project%3A-Improve-DXF-import-and-export):** Look into using an external library for DXF import (and export?).                                                                                                  |       C++       |   MEDIUM    | [Marius/Torsten](#mentors) |
| **[OpenSCAD Standard Library](https://github.com/openscad/openscad/wiki/Ideas-for-Development-Tasks#openscad-standard-library):** Create a standard user-space OpenSCAD library.                                                                                                            |    OpenSCAD     |   MEDIUM    | [Marius/Torsten](#mentors) |
| **[OpenGL framework](https://github.com/openscad/openscad/wiki/Project%3A-Improve-OpenGL-rendering):** Rewrite the OpenGL rendering code to use a rendering framework. Focus on compatibility with OpenGL ES2 and rendering performance.                                                    |   C++ OpenGL    |   MEDIUM    | [Marius/Torsten](#mentors) |
| **[Improve Text Editor](https://github.com/openscad/openscad/wiki/Project%3A-Improve-Text-Editor):** Add more IDE style features to the text editor integrated in OpenSCAD.                                                                                                                 |       C++       |   MEDIUM    | [Marius/Torsten](#mentors) |
| **[Persistent Caching](https://github.com/openscad/openscad/wiki/Ideas-for-Development-Tasks#persistant-caching):** Implement a disk-based version of the internal memory caches                                                                                                            |       C++       |   MEDIUM    | [Marius/Torsten](#mentors) |
| **[Multi-threaded Geometry Evaluation](https://github.com/openscad/openscad/wiki/Project%3A-Multi-threaded-geometry-rendering):** Implement multi-threaded evaluation of geometry.                                                                                                          |       C++       |   MEDIUM    | [Marius/Torsten](#mentors) |
| **[Survey of CSG algorithms](https://github.com/openscad/openscad/wiki/Project%3A-Survey-of-CSG-algorithms):** Review existing research, evaluate and prototype algorithms.                                                                                                                 |       C++       | MEDIUM-HARD | [Marius/Torsten](#mentors) |
| **[Add support for exporting models in STEP format](https://github.com/openscad/openscad/wiki/Project%3A-Add-support-for-exporting-models-in-STEP-format):** Enable better integration with other CAD tools by adding STEP export.                                                          |       C++       |    HARD     | [Marius/Torsten](#mentors) |
| **[Issue Handling](https://github.com/openscad/openscad/wiki/Ideas-for-Development-Tasks#issue-handling):** Day-to day issue and community management, fix incoming and existing issues. Good place to get started.                                                                         |       C++       |    EASY     | [Marius/Torsten](#mentors) |
| **[Test Framework Improvements](https://github.com/openscad/openscad/wiki/Ideas-for-Development-Tasks#test-framework-improvements):** Improve tests and test framework. Good place to get started.                                                                                          |   Python, C++   | EASY-MEDIUM | [Marius/Torsten](#mentors) |
| **[SVG Import](https://github.com/openscad/openscad/wiki/Ideas-for-Development-Tasks#svg-import):** Improve/finalize SVG import.                                                                                                                                                            |    C++, SVG     |   MEDIUM    | [Marius/Torsten](#mentors) |
| **[Larger tasks for particularly experienced people](https://github.com/openscad/openscad/wiki/Ideas-for-Development-Tasks#larger-tasks-for-particularly-experienced-people):** Various harder tasks which are not fully specified and requires significant effort to design and implement. |       C++       |    HARD     | [Marius/Torsten](#mentors) |

The OpenSCAD team is also open to new ideas. Please [get in
touch](http://www.openscad.org/community.html) to discuss your ideas and
convince a mentor to back it.

# LibreCAD Projects

LibreCAD is a free Open Source CAD application for Windows, Apple and
Linux. Support and documentation is free from our large, dedicated
community of users, contributors and developers. Please refer to
[LibreCAD GSoC 2018
ideas](http://wiki.librecad.org/index.php/GSoC_2018#LibreCAD_Project_Ideas)
for more detailed description.

|                                                                                                                                                                                                                                                                              | Languages | Difficulty  |                                                              Contacts                                                              |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------:|:-----------:|:----------------------------------------------------------------------------------------------------------------------------------:|
|                                                                                                                                                                                                                                                                              |           |             |                                                                                                                                    |
| **[LibreCAD 3 UI](http://wiki.librecad.org/index.php/GSoC_2018#LibreCAD_Project_Ideas):** Add missing features, e.g. snapping, to the very basic GUI.                                                                                                                        | C++,Math  |   MEDIUM    | [Armin](#mentors), [Florian](#mentors) |
|                                                                                                                                                                                                                                                                              |           |             |                                                                                                                                    |
| **[LibreCAD 3 DXF Entities](http://wiki.librecad.org/index.php/GSoC_2018#LibreCAD_Project_Ideas)** Implement missing DXF entities, e.g. blocks, use LibreCAD 2 for reference.                                                                                                | C++,Math  |   MEDIUM    | [Armin](#mentors), [Florian](#mentors) |
|                                                                                                                                                                                                                                                                              |           |             |                                                                                                                                    |
| **[LibreCAD 3 OpenGL rendering](http://wiki.librecad.org/index.php/GSoC_2018#LibreCAD_Project_Ideas):** Replace our current rendering engine *Cairo* with pure OpenGL rendering.                                                                                             |    C++    | MEDIUM/HIGH | [Armin](#mentors), [Florian](#mentors) |
|                                                                                                                                                                                                                                                                              |           |             |                                                                                                                                    |
| **[LibreCAD 3 Plugin Interface](http://wiki.librecad.org/index.php/GSoC_2018#LibreCAD_Project_Ideas)** Right now we have some LUA based scripting support for LibreCAD 3. But we want to be much more extensible, e.g. with a XML/JSON interface.                            |    C++    | MEDIUM/HIGH | [Armin](#mentors), [Florian](#mentors) |
|                                                                                                                                                                                                                                                                              |           |             |                                                                                                                                    |
| **[LibreCAD 3 trimming support](http://wiki.librecad.org/index.php/GSoC_2018#LibreCAD_Project_Ideas)** LibreCAD 3 trim operation doesn't support all entities and is entirely written in Lua. We need a better system which would support all entities and divide operation. | C++,Math  |   MEDIUM    | [Armin](#mentors), [Florian](#mentors) |
|                                                                                                                                                                                                                                                                              |           |             |                                                                                                                                    |

# STEPcode Projects

|                                                                                                                                                                                                                                                                                                         |              Languages               | Difficulty |                                Contacts                                 |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------------------------------:|:----------:|:-----------------------------------------------------------------------:|
| **[STEP Coverage Test](../task/STEP_Coverage_Test.md):** Write a program that links against STEPcode and generates a STEP output instantiating every entity for a given schema. Goal is a comprehensive program and data file for testing STEP import/export.                                           | ANY (C/C++, Python, Java, Perl, ...) |    EASY    | [Mark, Charlie](#mentors) |
| **[STEP Incremental Loading](../task/STEP_Incremental_Loading.md):** Basically take a work-in-progress to the next level. Modify the STEP parser to only read what it needs when it needs it, test, clean up, profile, and optimize.                                                                    |                 C++                  |    EASY    | [Mark, Charlie](#mentors) |
| **[STEP Minimal Examples](../task/STEP_Minimal_Examples.md):** Create minimal examples for various schemas - such as AP214 or AP242 - in the style of [ap203min](http://github.com/stepcode/stepcode/blob/master/example/ap203min/ap203min.cpp)                                                         |                 C++                  |   MEDIUM   | [Mark, Charlie](#mentors) |
| **[STEP Multiple Protocol Parsing](../task/STEP_Multiple_Protocol_Parsing.md):** Currently creates a parser that works with a specific application protocol (e.g., AP203, AP214). Make it work with multiple simultaneously.                                                                            |                 C++                  |   MEDIUM   | [Mark, Charlie](#mentors) |
| **[STEP Source Code Documentation](../task/STEP_Source_Code_Documentation.md):** We already use doxygen, but could do much better. Improve code documentation and utilize additional doxygen features such as topic pages. Add a 'make doxygen' target to invoke doxygen.                               |                C/C++                 |    EASY    | [Mark, Charlie](#mentors) |
| **[STEP EXPRESS Documentation](../task/STEP_EXPRESS_Documentation.md):** Write 'exp2html', similar to exp2py or exp2cxx (python and C++ generators) but outputs graphs and hyperlinked documentation with JavaScript search. Output will include EXPRESS comments (this requires modifying the parser). |          C/C++, JavaScript           |   MEDIUM   | [Mark, Charlie](#mentors) |
| **[STEP Viewer](../task/STEP_Viewer.md):** STEP is a common CAD file format supported by just about every major CAD system. Given we have an importer and an interface for displaying geometry, a stand-alone STEP file viewer has some great potential.                                                |                C/C++                 |   MEDIUM   | [Mark, Charlie](#mentors) |
| **[STEP Code Refactoring](../task/STEP_Code_Refactoring.md):** Split large files and functions, add unit tests, move contents of LISTdo loops into separate functions.                                                                                                                                  |                C/C++                 |    EASY    | [Mark, Charlie](#mentors) |
| **[STEP Thread Safety and Performance](../task/STEP_Thread_Safety_and_Performance.md):** Modify the libraries to improve thread safety, increase performance using hotspot analysis                                                                                                                     |                C/C++                 |   MEDIUM   | [Mark, Charlie](#mentors) |

# Slic3r Projects

[Slic3r](http://slic3r.org) is CAM desktop application for
toolpath/G-code generation for 3D printers.

|                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |    Languages    | Difficulty  |                                  Contacts                                   |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------:|:-----------:|:---------------------------------------------------------------------------:|
| **Port the GUI to C++:** The GUI is currently coded in Perl using wxWidgets and our goal is to have it ported to C++. The wxWidgets API is almost identical between Perl and C++, so it's an easy task. There are a couple things where we use the dynamic features of Perl which are trickier and interesting to port.                                                                                                                                                                                                |  C++/wxWidgets  |    Easy     | [Alessandro/Joseph](#mentors) |
| **Port the SVGNest library to C++:** The SVGNest library provides an algorithm for polygon nesting. It's written in JavaScript and a C++ port of it would improve Slic3r's auto-arrange feature. [\#3237](https://github.com/alexrj/Slic3r/issues/3237)                                                                                                                                                                                                                                                                |       C++       |    Easy     | [Alessandro/Joseph](#mentors) |
| **Fix bugs of the Boost.Voronoi library:** The good but unmaintained Boost.Voronoi library has a couple minor issues affecting Slic3r's results. Interesting task for learning the Voronoi algorithm and how to troubleshoot a computational geometry issue. [\#2948](https://github.com/alexrj/Slic3r/issues/2948)                                                                                                                                                                                                    |       C++       |   Medium    | [Alessandro/Joseph](#mentors) |
| **Wireframe printing:** Implement the wireframe printing algorithm. [\#2274](https://github.com/alexrj/Slic3r/issues/2274)                                                                                                                                                                                                                                                                                                                                                                                             |       C++       |   Medium    | [Alessandro/Joseph](#mentors) |
| **Automatic part rotation:** Automatically rotate a part to make some face of the part the bottom. [\#3047](https://github.com/alexrj/Slic3r/issues/3047)                                                                                                                                                                                                                                                                                                                                                              |       C++       |   Medium    | [Alessandro/Joseph](#mentors) |
| **Manual support creation:** Allow users to place and move support pillars by clicking in the 3D GUI. [\#3062](https://github.com/alexrj/Slic3r/issues/3062)                                                                                                                                                                                                                                                                                                                                                           | C++/Perl/OpenGL | Medium/Hard | [Alessandro/Joseph](#mentors) |
| **Refactor the TriangleMesh class and support non-solid walls:** Replace the internal mesh representation (currently based on admesh) using an existing 3D mesh library or implementing a half-edge structure; only use admesh for fixing models. Keep non-solid walls and slice them as single paths. Bonus: import SVG paths and position them freely using the GUI for printing as single extrusions. [\#3560](https://github.com/alexrj/Slic3r/issues/3560) [\#3523](https://github.com/alexrj/Slic3r/issues/3523) |       C++       | Medium/Hard | [Alessandro/Joseph](#mentors) |
| **Non-planar printing:** Implement techniques for non-planar printing. [\#3442](https://github.com/alexrj/Slic3r/issues/3442)                                                                                                                                                                                                                                                                                                                                                                                          |       C++       |   Medium    | [Alessandro/Joseph](#mentors) |
| **Support surface colors and mixing extruders:** Read surface colors from AMF or OBJ and keep them throughout the slicing process in order to generate G-code for mixing extruders. [\#3546](https://github.com/alexrj/Slic3r/issues/3546)                                                                                                                                                                                                                                                                             |    C++/Perl     |    Hard     | [Alessandro/Joseph](#mentors) |
| **Clean the libslic3r API and write bindings for it:** Expose the internal algorithms of Slic3r as a library and write bindings for Python, Perl etc.                                                                                                                                                                                                                                                                                                                                                                  |     C++/any     |    Easy     | [Alessandro/Joseph](#mentors) |
| **Write a Slic3r plugin for Grasshopper:** Expose Slic3r functionality as many separate components that can be plugged in larger GH definitions (for example: slice a NURBS model in GH and feed the slices to the toolpath generation process in order to skip mesh generation, or provide flow calculation for people driving 5-axis robots with custom motion). This requires a fair amount of design work.                                                                                                         |       C++       | Medium/Hard | [Alessandro/Joseph](#mentors) |

# FreeCAD Projects

|                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | Language                | Difficulty  | Contact                                                                                                                                                    |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **[Advanced FreeCAD test system](http://www.freecadweb.org/wiki/Advanced_FreeCAD_test_system)**: Create a framework for result file based comparisons and workbench specific comparators. Also creation of test cases should be simplified by a GUI or wizard.                                                                                                                                                                                                                                                                                                                                                                                                                               | Python/C++              | Medium      | [Ickby](http://forum.freecadweb.org/memberlist.php?mode=viewprofile&u=686)                                                                                 |
| **[Topological Naming Project](http://www.freecadweb.org/wiki/Topological_Naming_Project)**: Implementation of subshape identifiers based on creation history and update of topology class to work with those identifiers.                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | C++                     | Hard        | [Ickby](http://forum.freecadweb.org/memberlist.php?mode=viewprofile&u=686)                                                                                 |
| **[Direct modeling tools](http://www.freecadweb.org/wiki/Direct_modeling_tools)**: Create a new layer of tools and objects, that work on top of existing Part-based 3D objects, that allow a user to graphically modify their geometry.                                                                                                                                                                                                                                                                                                                                                                                                                                                      | Python/C++              | Medium      | [Yorik](http://forum.freecadweb.org/memberlist.php?mode=viewprofile&u=68)                                                                                  |
| **[FEM Post Processing based on VTK](http://www.freecadweb.org/wiki/FEM_Post_Processing_based_on_VTK)**: Base the existing FEM VTK post processing on the updated SMESH data structure and design a python interface for it. Also improve integration into the workbench.                                                                                                                                                                                                                                                                                                                                                                                                                    | C++                     | Medium      | [Ickby](http://forum.freecadweb.org/memberlist.php?mode=viewprofile&u=686)                                                                                 |
| **[IPython notebook integration](http://www.freecadweb.org/wiki/IPython_notebook_integration)**: Create a way to export the open inventor scenegraph as a JavaScript file and add functions for seamless interaction with the IPython display system                                                                                                                                                                                                                                                                                                                                                                                                                                         | C++, JavaScript, Python | Easy        | [Ickby](http://forum.freecadweb.org/memberlist.php?mode=viewprofile&u=686)                                                                                 |
| **[Integrate Cycles renderer](https://www.freecadweb.org/wiki/Integrate_Cycles_renderer)**: Add Blender's new Cycles renderer as a new render engine to the Raytracing Workbench                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | C++                     | Medium      | [Yorik](http://forum.freecadweb.org/memberlist.php?mode=viewprofile&u=68)                                                                                  |
| Stepwise integration of ElmerFem into FreeCAD should be done in three phases: Phase 1 - **[New solver object for handling ElmerFEM execution in FEM-workbench](https://www.freecadweb.org/wiki/New_solver_object_for_handling_ElmerFEM_execution_in_FEM-workbench)**. Phase 2 - **[Mapping of main ElmerSolver setting for mechanical simulations](https://www.freecadweb.org/wiki/Mapping_of_main_ElmerSolver_setting_for_mechanical_simulations)**. Phase 3 - **[Give graphical access to a wide range of available ElmerSolver setting from within FreeCAD](https://www.freecadweb.org/wiki/Give_graphical_access_to_a_wide_range_of_available_ElmerSolver_setting_from_within_FreeCAD)** | Python/C++              | Medium-Hard | [Bernd](https://forum.freecadweb.org/memberlist.php?mode=viewprofile&u=2069), [HoWil](https://forum.freecadweb.org/memberlist.php?mode=viewprofile&u=6222) |
| **[PartDesign Updates](https://www.freecadweb.org/wiki/PartDesign_Updates)**: Finish PartDesign port to new Body object, simplify the workflows and extend tools while making them more robust.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | C++, Python             | Medium      | [Ickby](http://forum.freecadweb.org/memberlist.php?mode=viewprofile&u=686)                                                                                 |
| **[GSoC FEM Solver Z88](https://www.freecadweb.org/wiki/GSoC_FEM_Solver_Z88)**: Extend the capabilities of FEM solver Z88OS in FreeCAD FEM workbench.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | Python                  | Easy-Medium | [Bernd](http://forum.freecadweb.org/memberlist.php?mode=viewprofile&u=686)                                                                                 |
| **[GSoC FEM Unit Tests](https://www.freecadweb.org/wiki/GSoC_FEM_Unit_Tests)**: Extend the unit tests of FreeCAD FEM workbench.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | Python                  | Easy-Medium | [Bernd](http://forum.freecadweb.org/memberlist.php?mode=viewprofile&u=686)                                                                                 |
| **[GSoC Path/Robot Integration](https://www.freecadweb.org/wiki/GSoC_Path/Robot_Integration)**: Path is the CNC/CAM workbench. It currently lacks any simulation capability. Robot workbench is a tool for simulating industrial robots. Extend Path and Robot workbenches to support simulation of CNC operations in the Robot workbench.                                                                                                                                                                                                                                                                                                                                                   | C++, Python             | Easy-Medium | [Yorik](http://forum.freecadweb.org/memberlist.php?mode=viewprofile&u=68), [sliptonic](https://forum.freecadweb.org/memberlist.php?mode=viewprofile&u=708) |

# Mentors

BRL-CAD operates under group mentorship. That means you can contact
anyone, not just the person assigned to you, for assistance. The mailing
list and IRC channel are the preferred communication methods.

-   Christopher Sean Morrison
    -   brlcad on irc.freenode.net
    -   Org admin, BRL-CAD open source project lead

<!-- -->

-   Erik Greenwald
    -   \`\`Erik on irc.freenode.net
    -   Org admin, BRL-CAD core dev
    -   mainly FDM/FFF, geometry conversion, CAE/prototyping

<!-- -->

-   Cliff Yapp
    -   starseeker on irc.freenode.net
    -   BRL-CAD Mentor, core dev

<!-- -->

-   Daniel Rossberg
    -   d\_rossberg on irc.freenode.net
    -   BRL-CAD Mentor, core dev, math expert

<!-- -->

-   H.S. Rai
    -   hsrai on irc.freenode.net
    -   BRL-CAD Mentor, math expert

<!-- -->

-   Tom Browder
    -   BRL-CAD Mentor, analysis expert

<!-- -->

-   Bryan Bishop
    -   BRL-CAD Mentor, python guru

<!-- -->

-   Isaac Kamga
    -   Izakey on irc.freenode.net
    -   BRL-CAD Mentor, C/C++ Programmer

<!-- -->

-   Mohit Daga
    -   zero\_level irc.freenode.net
    -   BRL-CAD Mentor, Computer Science Engineer

<!-- -->

-   Inderpreet Singh (Pooh)
    -   Pooh on <https://brlcad.zulipchat.com>
    -   OGV mentor

<!-- -->

-   Gauravjeet Singh (Panda)
    -   Panda on <https://brlcad.zulipchat.com>
    -   OGV mentor

<!-- -->

-   Mark Pictor
    -   mpictor on irc.freenode.net
    -   STEPcode Mentor

<!-- -->

-   Charlie Stirk
    -   cstirk
    -   STEPcode Mentor

<!-- -->

-   Marius Kintel
    -   kintel on irc.freenode.net
    -   OpenSCAD Mentor

<!-- -->

-   Torsten Paul
    -   teepee on irc.freenode.net
    -   OpenSCAD Mentor

<!-- -->

-   Armin Stebich
    -   LordOfBikes on irc.freenode.net
    -   LibreCAD Mentor

<!-- -->

-   Florian Roméo
    -   Feragon on irc.freenode.net
    -   LibreCAD Mentor

<!-- -->

-   Alessandro Ranellucci
    -   Sound on irc.freenode.net
    -   Slic3r Mentor

<!-- -->

-   Joseph Lenox
    -   LoH on irc.freenode.net
    -   Slic3r Mentor

<!-- -->

-   Shubham Rathore (:gabbar1947)
    -   gabbar1947 on irc.freenode.net
    -   BRL-CAD Mentor
