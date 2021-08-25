**`!!!!!!!!!!!!!!`**
**`!!!`` ``NOTICE`` ``!!!`**
**`!!!!!!!!!!!!!!`**

**`This`` ``page`` ``is`` ``provided`` ``as`` ``a`` ``historic`` ``reference`` ``only.`**

The list of possible projects below should serve as a good starting
point for new developers that would like to get involved in working on
BRL-CAD. The ideas below range from the very hard and math intense to
the very easy, feel free to scale the scope of the project up or down as
needed. The suggested project ideas below are merely starting points. In
addition to those below, you may also want to consider some of [these
ideas](http://brlcad.org/~sean/ideas.html).

A detailed articulate (i.e. excellent) proposal that has been discussed
with us beforehand will generally trump the priorities. Please do
[contact us](http://brlcad.org/d/contact) if you have any questions,
corrections, comments, or ideas of your own that you'd like to suggest.

Be sure to read up on our [application
process](Google_Summer_of_Code.md) for getting started with your
proposal submission if you have not done so already.

# <AN IDEA OF YOUR OWN>

Do you have an idea of your own? Let us know and maybe we'll like it
too. We're very open to new ideas, areas of academic research, industry
applications, and any other ways that may help get you hooked on BRL-CAD
development. Just remember that BRL-CAD is a solid modeling CAD suite so
keep that in mind when scoping your project. The idea needs to fit in
with our project goals, it needs to be specific, and it needs to be
detailed.

Requirements:

-   Passion for the task being suggested
-   Buy-in from one of the existing developers

# OpenGL GUI Framework

BRL-CAD includes a graphical solid modeler named MGED as well as an
experimental refactoring named Archer, both written in Tcl/Tk. While
MGED is extensively powerful in its modeling capabilities and is in
production use, new users and developers usually expect something rather
different. They expect and want an interface that doesn't require
extensive training and expert knowledge before they can use it. A
redesign of the modeling interface is under way and this project idea
focuses on one piece of that effort, the front-end display.

The goal of this project would be to implement the graphical application
framework that communicating with a geometry service back-end. Rather
than reimplementing existing functionality, the framework would be an
extendible plug-in-based client-server system that would utilize
existing binaries and editing functionality available in BRL-CAD. More
to the point, this task entails creating that (basic) client-server
communications API using an OpenGL client front-end that leverages an
existing scene graph and display management interface (e.g. OGRE). *This
is a high-priority topic.*

Requirements:

-   Strong knowledge of C++
-   Strong knowledge of object oriented design

# Object-oriented geometry engine API

BRL-CAD includes four libraries that provide the basis for our core
geometry engine: libbu, libbn, librt, and libwdb. These libraries
provide a C API to various geometry processing and ray-tracing
capabilities. The focus of this idea is to provide an object-oriented
API in either C++ or Java (or both, SWIG?) for those capabilities. The
library should be designed such that it provides features similar to
those found in other commercial geometry engines such as the ACIS or
Granite engines, but designed with BRL-CAD's existing capabilities in
mind. The API design should leverage as much of our C libraries as
possible for the implementation approach. See our 'jbrlcad' module for
an example (initial) structuring. *This is a high-priority topic.*

Requirements:

-   Strong familiarity with C
-   Strong familiarity with C++ or Java (or both)
-   Strong familiarity with object oriented API design
-   (optional) Familiarity with SWIG

# MGED User Interface Improvements

Most users discovering BRL-CAD for the first time are usually introduced
to MGED first. MGED, however, has always been considered an "expert
interface" that requires substantial investment of time and effort to
learn and use effectively. There are many enhancements to the interface
that would improve usability and discoverability.

The idea behind this task would be propose improvements to MGED's
existing Tcl/Tk user interface implementation. Proposals could include
usability improvements, platform-specific release integration (e.g., get
AquaTk working), improving discoverability of features, refactoring the
existing implementation, and more. The approach can be minimal, drastic,
or incremental, but should be appropriately scoped and include detail.
*This is a high-priority topic.*

Requirements:

-   Strong knowledge of Tcl/Tk
-   Usability and interface design experience
-   (optional) Familiarity with C

# CSG evaluation of Boundary Representations

One of the current primary BRL-CAD development efforts is the complete
integration of hybrid model support. BRL-CAD leverages the Rhino
openNURBS library to provide fundamental BREP support but there is still
much work to be done to evaluate BREPs. This task basically involves
implementing BREP-on-BREP CSG evaluation routines (resulting in a new
evaluated BREP object). If you get done fast enough, you could also work
on implementing the routines that generate a BREP for all of our
implicit primitives which would bring us one step closer towards
providing complete dual-representation support. *This is a high-priority
topic.*

Requirements:

-   Familiarity with C/C++
-   Strong math skills
-   Familiarity with CSG operations
-   Familiarity with BREP/n-Manifold spline surface geometry
-   (optional) Strong familiarity with implicit geometric
    representations

# STEP parser integration

Several BRL-CAD developers are working on implementing a full STEP
converter. This task is a big effort given the complexity of the STEP
standard (ISO 10303). This task focuses on helping with that effort by
working on one of the fundamental components to the STEP converter,
getting an EXPRESS parser working. This would most likely entail
updating and integrating the NIST STEP AP 21 parser or developing/using
a similar EXPRESS parser. The NIST sources as well as copies of the STEP
standard can be provided. If that is ends up being too easy, the next
step is jumping in on AP 203 and AP 214 hooks. *This is a high-priority
topic.*

Requirements:

-   Familiarity with C and/or C++
-   Ability to integrate with and update an existing code library
-   Familiarity with writing a robust parser
-   Ability to tolerate bloated ISO standards

# CSG ray-trace optimizations

BRL-CAD has one of the best high-performance CSG boolean evaluation
engines anywhere, but we're always looking for ways to improve
performance and accuracy. This task could consist of refactoring the
LIBRT ray-trace library to fix a bug related to negative object segment
detection (high-priority). This task could consist of implementing a
high-performance generic CSG tree processing library providing
transformations, tree contraction, null object detection, various
traversals, cycle detection, etc and hooking that into LIBRT. Yet
another approach could be to apply the same real-time ray-trace
optimizations of exploiting cache coherency, branch minimization, data
vectorization, accelerated spacial partitioning, and other optimization
techniques. *This is a high-priority topic.*

Requirements:

-   Strong familiarity with C
-   Strong familiarity with CSG

# IGES importer/exporter enhancements

IGES is one of the most prevalent CAD geometry file formats used to
exchange geometry data between CAD systems. BRL-CAD inludes extensive
support for IGES, but only up to version 5.0 whereas the current/final
version of IGES was 5.3 and there are non-final versions beyond that.
This task would make the changes necessary to the existing IGES importer
and exporter to fully support the latest IGES standard, possibly
modifying the converter to simultaneously support multiple formats.

Requirements:

-   Familiarity with C
-   Strong ability to review and improve existing code

# Universal geometry converter API

With more than 30 geometry importers and exporters, including several
that are of paramount importance to CAD communities such as IGES and
DXF, BRL-CAD contains a multitude of converters that can be chained
together to go to and from various formats. This task would involve
refactoring the existing converters into a clean "universal" geometry
converter and API that could read and write from any of the supported
formats as run-time plugins. If you have more time, you can always start
work on a new converter too.

Requirements:

-   Familiarity with C or C++
-   Ability to understand and refactor existing code

# New geometry converter

Though we have more than 30 geometry importers and exporters, there are
plenty that we don't have support for and existing converters that could
use improvements. Some examples of converters we would like to see
implemented include (in rough priority/interest order):

-   STEP (.step)
-   Collada (.dae)
-   X3D \[importer\] (.x3d)
-   Alias Wavefront \[importer\] (.obj)
-   Rhino (.3dm)
-   AutoCAD drawings (.dwg)
-   G-Code (.nc)
-   Solidworks (.sat, .sldprt, .sldasm)
-   Parasolid/UGS (.x_b, .x_t)
-   POV-RAY (.pov)
-   Blender (.blend)
-   Universal 3D (.u3d)
-   Polygon \[exporter\] (.ply)
-   Sketchup (.skp, .skb)
-   VRML \[importer\] (.vrml)
-   3D Studio Max (.3ds)

Requirements:

-   Familiarity with C or C++

# New primitive

BRL-CAD provides more than 30 different primitives but there are a few
we don't have that would be highly desirable to have implemented. The
goal of this task is to fully implement support for one of them:

-   Sweep
-   Revolution
-   Birail/Skin
-   Annotation
-   Blend/Fillet/Chamfer
-   Dynamic Scripted
-   Compound Procedural

Requirements:

-   Familiarity with C
-   Solid mathematical basis for the primitive being suggested

# Annotations

This task is pretty simple on the surface: implement annotations. This
effectively amounts to implementing a new primitive in BRL-CAD that can
be associated with other objects for providing annotation information.
Annotations would allow the modeler to leave notes and draw simple
diagrams around geometry during the modeling process where the
annotations are either fixed with respect to the view or align with the
object(s) they refer to (if any). There are design considerations as to
whether you can ray-trace an annotation as well as how to most
effectively display them. It would be awesome if users could
interactively edit their annotations through the GUI.

Requirements:

-   Strong familiarity with C
-   Ability to implement within an existing framework

# Constraints and Parametrics

BRL-CAD does not presently provide the means to specify values that are
undetermined or otherwise dependent calculations. That is to say that
there is no support for constraints and parametrics such that a modeler
can define a sphere such that the sphere's radius necessarily maintains
tangency with a given planar surface. This task would focus on
implementing basic support for this feature in the BRL-CAD geometry
format.

Requirements:

-   Strong familiarity with C
-   Ability to implement within an existing framework

# Web-based solid geometry model repository

This task focuses on creating a web interface to a geometry repository
where the community can store and exchange geometric models in any of
the supported BRL-CAD formats. The website could be written such that it
integrates with an existing content management system (e.g. Drupal
extension), wiki (e.g. Mediawiki extension), or could be custom with the
appropriate design plan. The site would need to provide a relatively
easy means for users to upload models and have those models be indexed,
categorized, searched, converted, and downloaded through the website
interface.

Requirements:

-   Strong web development skills
-   (optional)Familiarity with Drupal or Mediawiki customization and/or
    module development

# Global illumination renderer

Our LIBRT library provides advanced solid modeling ray-trace facilities.
This idea is to use the LIBRT library and implement a global
illumination renderer such as a bidirectional path tracer (e.g.
metropolis light transport) or radiosity renderer.

Requirements:

-   Strong familiarity with C
-   Familiarity with global illumination rendering
-   Solid math background
-   Ability to learn and utilize existing C API

# Geometry database (i.e. ".g" file format) enhancements

Our ".g" file format is a binary geometry file format that provides a
robust, efficient, and flexible object storage framework. There are,
however, many features that would be really useful to have in the
database layer that are not presently implemented. The idea behind this
task would be to propose a set of enhancements, whether they be
backwards-compatible with our current "v5" geometry file format or
whether it be the development of a new "v6" file format. The sorts of
enhancements needed include time-stamping of geometry database objects,
support for constraints and parametric equations as intrinsic object
properties, objects with versioning and construction histories,
intrinsic support for surrogation, dynamic geometry, automatic space
compression, deleted object recovery, performance enhancements, and
more. There's plenty of room for new features and improvements, so be
specific in your scope and goals.

Requirements:

-   Familiarity with C
-   Ability to learn and extend an existing API

[Category: Summer of Code](Category:_Summer_of_Code.md)
