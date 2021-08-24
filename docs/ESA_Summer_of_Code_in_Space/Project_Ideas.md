If you want to work on **computer-aided design (CAD), geometry,
simulation, analysis, or graphics**, you've come to the right place!
Help us improve open source CAx.

[<http://brlcad.org/images/logo/cutout_sticker_256.png>](http://brlcad.org/w/index.php?title=Google_Summer_of_Code/Project_Ideas#BRL-CAD_Projects)

Under development for 30+ years, it's big, it's complicated, it's
powerful. BRL-CAD will consider just about any project that relates to
computer graphics or existing infrastructure.

We consider proposals for all skill levels ranging from simple to crazy
hard and everything in between. [Introduce
yourself](https://lists.sourceforge.net/lists/listinfo/brlcad-devel),
and we'll help you plan one right for you.

Remember that project descriptions are just *initial ideas*. You must
expand with [considerably more
detail](Summer_of_Code/Application_Guidelines "wikilink"). Change the
goals to fit your experience and interests. See our
**[checklist](Summer_of_Code/Checklist "wikilink")** to get started.

**Project titles link to a page with more details.**

# BRL-CAD Projects

## High Priority Topics

|                                                                                                                                                             |  Languages   | Difficulty |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------:|:----------:|
| **[Convert MGED from Tk to Qt](Convert_MGED_from_Tk_to_Qt "wikilink"):** Transition BRL-CAD's graphical applications from the Tk toolkit to the Qt toolkit. | C/C++/Tcl/Qt |   MEDIUM   |
| **[Annotations](Annotations "wikilink"):** Implement support for 2D annotations, labels that can be added to geometry.                                      |    C/C++     |   MEDIUM   |

## Rendering & Scientific Analysis

|                                                                                                                                                                                                                                                   |  Languages   | Difficulty |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------:|:----------:|
| **[Shader Enhancements](Shader_Enhancements "wikilink"):** We have a functioning custom shader system in BRL-CAD, but there are now folks that specialize and there's lot of room for improvements.                                               |      C       |    EASY    |
| **[Material and Shader Objects](Material_and_Shader_Objects "wikilink"):** This one is a biggie but easy. Implement new object entities for describing shaders and material properties, use them during ray tracing.                              |      C       |    EASY    |
| **[GUI Integration of Analysis Tools](GUI_Integration_of_Analysis_Tools "wikilink"):** There are a *lot* of visualization tools in BRL-CAD, but most aren't integrated with the GUI. Visualizing directly within the GUI would improve usability. |      C       |   MEDIUM   |
| **[Generalized abstracted spacial partitioning capability](Generalized_abstracted_spacial_partitioning_capability "wikilink"):** Need more be said? If you're familiar with BSPs, KD trees, and grid structures, then this one is for you.        |      C       |    HARD    |
| **[High Dynamic Range Support](High_Dynamic_Range_Support "wikilink"):** We don't have displays supporting this yet, but that's never stopped us before. Implement support for images with more than 8-bits per channel.                          | C and/or C++ |    EASY    |
| **[Analysis Library](Analysis_Library "wikilink"):** There are various tools in BRL-CAD for calculating weights, moments of inertia, and more. They're stand-alone applications. Turn them into a library.                                        |      C       |    HARD    |
| **[Celestial mechanics particle system](Celestial_mechanics_particle_system "wikilink"):** Simulate solar systems and galaxies.                                                                                                                   |    C/C++     |   MEDIUM   |
| **[Non-vacuum gravity simulator](Non-vacuum_gravity_simulator "wikilink"):** Simulate falling to earth.                                                                                                                                           |    C/C++     |   MEDIUM   |
| **[Polarization](Polarization "wikilink"):** We already do multispectral ray tracing, but don't simulate polarization effects. Implement ray splitting and filtering.                                                                             |      C       |    HARD    |
| **[Density functions](Density_functions "wikilink"):** Accurately represent everything from atmosphere to bone. Implement support for parametric density functions for homogenous materials.                                                      |      C       |    HARD    |
| **[Bending light](Bending_light "wikilink"):** Think gravity wells and satellite cameras.                                                                                                                                                         |      C       |   MEDIUM   |
| **[Appleseed renderer integration](Appleseed_renderer_integration "wikilink"):** Appleseed is rendering infrastructure used by the film industry to make pretty pictures. Make it shoot rays at our native geometry with our ray trace library.   |      C       |   MEDIUM   |

## Web Development

|                                                                                                                                                                                                            |           Languages            | Difficulty |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------------------------:|:----------:|
| **[Benchmark Performance Database](Benchmark_Performance_Database "wikilink"):** BRL-CAD's Benchmark has been used for two decades to compare performance across configurations. Build a database website. | Depends (likely PHP or Python) |    EASY    |
| **[Materials Database](Materials_Database "wikilink"):** Create a Materials Database web site for collecting, managing, and providing programmatic interfaces to material properties.                      | Depends (likely PHP or Python) |   MEDIUM   |

## Geometry

|                                                                                                                                                                                                                              |  Languages   | Difficulty |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------:|:----------:|
| **[NURBS Editing Support](NURBS_Editing_Support "wikilink"):** BRL-CAD doesn't currently have support for editing NURBS primitives. Fix that.                                                                                |    C/Tcl     |   MEDIUM   |
| **[Overlap tool](Overlap_tool "wikilink"):** Resolving geometric interferences (aka overlaps) is a common geometry editing activity. Design an awesome GUI for resolving conflicts.                                          |     Tcl      |    EASY    |
| **[Vector Drawings from NURBS](Vector_Drawings_from_NURBS "wikilink"):** Huge impact here if you can update one or more of our raytracers to provide vector output instead of raster. Perhaps render directly to PDF or SVG. | C and/or C++ |    EASY    |
| **[Plate Mode NURBS raytracing](Plate_Mode_NURBS_raytracing "wikilink"):** Imported NURBS geometry often does NOT enclose space (i.e., not solid), so add support for specifying an implicit thickness.                      |    C/C++     |    HARD    |
| **[STEP exporter](STEP_exporter "wikilink"):** We have an importer, we need a comprehensive exporter with support for implicit CSG, NURBS, or polygonal mesh geometry.                                                       |    C/C++     |    EASY    |
| **[STEP importer improvements](STEP_importer_improvements "wikilink"):** We have an importer, but it's preliminary. Add support for importing hierarchy information, polygonal geometry, and implicit geometry.              |    C/C++     |   MEDIUM   |
| **[STEP AP 242 Parser](STEP_AP_242_Parser "wikilink"):** We already parse a subset of AP203, but the new kid on the block is AP242. Make AP242 work with BRL-CAD's step-g importer.                                          |     C++      |    HARD    |
| **[IGES import improvements](IGES_import_improvements "wikilink"):** We have extensive support for the International Geometry Exchange Standard (IGES) with our g-iges and iges-g converters, but they need updating.        |      C       |   MEDIUM   |
| **[Geometry Conversion Library](Geometry_Conversion_Library "wikilink"):** Probably our biggest open source asset is our extensive collection of importers and exporters. Turn them all into a universal conversion library. |    C/C++     |    EASY    |
| **[Voxelize](Voxelize "wikilink") command:** Convert geometry into voxel data sets by shooting a grid of rays. The finite element analysis and volumetric rendering folks will love you.                                     |      C       |    EASY    |
| **[COLLADA Importer](COLLADA_Importer "wikilink"):** Create an importer for the COLLADA file format.                                                                                                                         |    C/C++     |   MEDIUM   |
| **[X3D Importer](X3D_Importer "wikilink"):** Create an importer for the X3D file format.                                                                                                                                     |    C/C++     |   MEDIUM   |
| **[OpenSCAD Importer](OpenSCAD_Importer "wikilink"):** Create an importer for OpenSCAD's format.                                                                                                                             |    C/C++     |    EASY    |
| **[OpenSCAD Exporter](OpenSCAD_Exporter "wikilink"):** Create an exporter for OpenSCAD's format.                                                                                                                             |    C/C++     |    EASY    |

## Performance & Quality

|                                                                                                                                                                                                                    | Languages | Difficulty |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------:|:----------:|
| **[OpenCL GPGPU Raytracing](OpenCL_GPGPU_Raytracing "wikilink"):** We have about two dozen primitives that need to have a ray-object intersection function converted from C to OpenCL.                             |   C/C++   |   MEDIUM   |
| **[Coherent Raytracing](Coherent_Raytracing "wikilink"):** Our current raytrace pipeline dispatches and processes one ray at a time. Send bundles and convert the pipeline into phases.                            |   C/C++   |   MEDIUM   |
| **[NURBS Booleans](NURBS_Booleans "wikilink"):** We have NURBS surface-surface intersections working. Now we're using them to create evaluated forms of our CSG geometry. Make it more robust and faster.          |   C/C++   |    HARD    |
| **[NURBS Optimization and Cleanup](NURBS_Optimization_and_Cleanup "wikilink"):** We have a fantastic implementation of NURBS evaluation but haven't gone back to clean up or speed it up. Make it pretty and fast. |   C/C++   |   MEDIUM   |

## Infrastructure

|                                                                                                                                                                                                                      | Languages | Difficulty |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------:|:----------:|
| **[Geometric Constraint Solver](Geometric_Constraint_Solver "wikilink"):** Our LIBPC parametric constraint library is the work-in-progress foundation of being able to validate and describe geometry relationships. |   C/C++   |    HARD    |
| **[Consolidate image processing](Consolidate_image_processing "wikilink"):** We have 100+ image processing tools that independently read and write file data. Needs much reuse love.                                 |     C     |    EASY    |
| **[Astronomical units](Astronomical_units "wikilink"):** We already go "big", but accurately modeling at a galactic scale redefines that notion...                                                                   |     C     |    EASY    |
| **[Point Clouds](Point_Clouds "wikilink"):** BRL-CAD has a basic point cloud primitive. Beef it up, make it faster, maybe integrate with the Point Cloud Library (PCL) for evaluation.                               |   C/C++   |   MEDIUM   |
| **[Annotations](Annotations "wikilink"):** Implement support for 2D annotations, labels that can be added to geometry.                                                                                               |   Perl    |    EASY    |

## <An Idea of Your Own>

Do you have an idea of your own? Maybe you need [more
ideas](http://brlcad.org/~sean/ideas.html) to inspire you? We're very
open to areas of academic research, industry applications, and ideas
that get you hooked on open source CAD development.

Requirements:

-   Passion for the task being suggested

# Mentors

Contact Sean on the brlcad-devel mailing list or via IRC to begin
discussing your SOCIS project proposal:

-   Christopher Sean Morrison
    -   brlcad on irc.freenode.net