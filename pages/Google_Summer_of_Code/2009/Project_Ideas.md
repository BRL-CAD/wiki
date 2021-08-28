**`!!!!!!!!!!!!!!`**
**`!!!`` ``NOTICE`` ``!!!`**
**`!!!!!!!!!!!!!!`**

**`This`` ``page`` ``is`` ``provided`` ``as`` ``a`` ``historic`` ``reference`` ``only.`**

The list of possible projects below should serve as a good starting
point for new developers that would like to get involved in working on
BRL-CAD. The ideas below range from the very hard and math intense to
the very easy, feel free to scale the scope of the project up or down as
needed. The suggested project ideas below are merely starting points. In
addition to those below, you may also want to consider some of **[these
ideas](http://brlcad.org/~sean/ideas.html)**.

A detailed articulate (i.e. excellent) proposal that has been discussed
with us beforehand will generally trump any listed priority. Please do
contact us (IRC or brlcad-devel mailing list) if you have any questions,
corrections, comments, or ideas of your own that you'd like to suggest.

Be sure to read up on our [application
process](../../Google_Summer_of_Code.md) for getting started with your
proposal submission if you have not done so already.

# Project Ideas

## <AN IDEA OF YOUR OWN>

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

Difficulty: variable

## OpenGL GUI Framework

This was a GSoC 2008 project. Talk to the developers before proposing
this task to obtain project status.

BRL-CAD includes a graphical solid modeler named MGED as well as an
experimental refactoring named Archer, both written in Tcl/Tk. While
MGED is extensively powerful in its modeling capabilities and is in
production use, new users and developers usually expect something rather
different. They expect and want an interface that doesn't require
extensive training and expert knowledge before they can use it. A
redesign of the modeling interface is under way and this project idea
focuses on one piece of that effort, the front-end display.

This project is necessarily a **continuation and extension** of the
graphical application framework started in GSoC 2008 (not something
completely new). Rather than reimplementing existing functionality, the
framework needs to be an extendible plug-in-based client-server system
that will utilize existing binaries and editing functionality available
in BRL-CAD. More to the point, this task entails creating solidifying
the GUI interactions and command framework. *This is a high-priority
topic.*

See <http://brlcad.org/design/gui/ioe_proto_final.mov> for some
background on an *interaction* prototype that was developed in relation
to the new GUI.

Requirements:

-   Strong knowledge of C++
-   Strong knowledge of object oriented design

Difficulty: high

## Object-oriented geometry engine API

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

Difficulty: high

## MGED User Interface Improvements

Most users discovering BRL-CAD for the first time are usually introduced
to MGED first. MGED, however, has always been considered an "expert
interface" that requires substantial investment of time and effort to
learn and use effectively. There are many enhancements to the interface
that would improve usability and discoverability.

The idea behind this task would be propose improvements to MGED's
existing Tcl/Tk user interface implementation. Proposals could include
usability improvements, improving discoverability of features,
refactoring the existing implementation, and more. The approach can be
minimal, drastic, or incremental, but should be appropriately scoped and
include detail. *This is a high-priority topic.*

Requirements:

-   Strong knowledge of Tcl/Tk
-   Usability and interface design experience
-   (optional) Familiarity with C

Difficulty: low

## CSG evaluation of Boundary Representations

One of the current primary BRL-CAD development efforts is the complete
integration of hybrid model support. BRL-CAD leverages the Rhino
openNURBS library to provide fundamental BREP support but there is still
much work to be done to evaluate BREPs.

These guys implemented something very similar although their
implementation was not robust:
<http://www.cs.unc.edu/~geom/CSG/boole.html> These guys followed that
work and implemented a robust solution, but killed performance:
<http://www.cs.unc.edu/~geom/ESOLID/> You will need to be very careful
about tolerances and tolerance tracking without resorting to
fixed-precision arithmetic.

This task basically involves implementing BREP-on-BREP CSG evaluation
routines (resulting in a new evaluated BREP object). If you get done
fast enough, you could also work on implementing the routines that
generate a BREP for all of our implicit primitives which would bring us
one step closer towards providing complete dual-representation support.
*This is a high-priority topic.*

Requirements:

-   Familiarity with C/C++
-   Strong math skills
-   Familiarity with CSG operations
-   Familiarity with BREP/n-Manifold spline surface geometry
-   (optional) Strong familiarity with implicit geometric
    representations

Difficulty: high

## CSG ray-trace optimizations

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

Difficulty: high

## Constraints and Parametrics

This was a GSoC 2008 project. For more information about
libpc(parametrics and constraints library) please check [libpc Developer
Doc](../../doc/Libpg_:_A_parametrics/constraint_library.md) as well as the
[libpc
source](http://brlcad.svn.sourceforge.net/viewvc/brlcad/brlcad/trunk/src/libpc/).
The work is effectively long-term considering the amount of work
required. Talk to the developers before proposing this task to obtain
project status.

BRL-CAD does not presently provide the means to specify values that are
undetermined or otherwise dependent calculations. That is to say that
there is no support for constraints and parametrics such that a modeler
can define a sphere such that the sphere's radius necessarily maintains
tangency with a given planar surface. This task would focus on
implementing basic support for this feature in the BRL-CAD geometry
format. Parametric representation of Geometry (and constraints) provides
a good foundation for various aspects of Design computation, Geometry
Generative Algorithms, and A more logically connected model not to
mention significant reduction in Modeling time (since the process of
modeling during an actual design cycle is inherently iterative).

Primary work would be in terms of constructing Constraint Solvers.
Geometrical constraints in our context can be broadly classified into

-   Implicit : Constraints implicit in the definition of a primitive :
    Tangency or perpendicularity of Vectors, Equality of scalars etc.
-   Explicit : Constraints explicitly expressed between two or more
    primitives.

One of the intricate parts of the work is the actual integration of
libpc with librt. Associated work going on with libpc involves the
creation of a Math Virtual Machine for parsing and evaluating (math)
expressions which would be used for stating the constraints, along with
the grammar. As of now [Boost](http://www.boost.org/) libraries are
being used for various functionalities.

Requirements:

-   Strong familiarity with C
-   Strong familiarity with C++ (check pcMath\* source code)
-   Ability to implement within an existing framework

Difficulty: high

## Merge MGED and Archer

BRL-CAD contains two GUI modeling interfaces called MGED and Archer.
MGED is BRL-CAD's comprehensive solid modeling editor that has been
around for more than two decades. It's predominantly written in a mix of
C and Tcl/Tk. Archer is a new interface that has been developed as a
much cleaner re-implementation of MGED. Archer is predominantly Incr
Tcl/Tk while calling the same C library as MGED. We would like to merge
those two efforts into one, retaining the extensive feature set of MGED
while leveraging Archer's much more modular plugin-based design and more
appealing GUI.

This project would involve adding major functionality missing from
Archer that MGED provides and putting the finishing touches on Archer.
There will need to be some minor bridge work to clean up the shared
LIBGED interface that both codes utilize. There will need to be a lot of
production quality release testing to make sure features aren't broken
or lost during the merge.

Requirements:

-   Strong familiarity with Tcl/Tk or the ability to get up to speed
    with it very quickly
-   Good familiarity with C
-   Ability to read and comprehend other developer's code

Difficulty: medium

## Aqua MGED on Mac OS X

BRL-CAD primary editor, MGED, is a hybrid application with the main
logic predominantly written in C and the GUI written in Tcl/Tk. Given
MGED's heritage, though, and for porting ease, it still requires X11 on
Mac OS X. Ever since [AquaTk](http://tcltkaqua.sourceforge.net/) was
unveiled several years ago, we've wanted to leverage it to run MGED
natively on Mac OS X without a major porting/coding effort. Alas, much
testing of AquaTk indicated that it was not quite ready for prime time
(this was several years ago).

<http://tcltkaqua.sourceforge.net/>

This project entails getting the latest AquaTk release build working
with MGED, then with our bundled Tcl/Tk distribution, and working to
make it so that everything "just works". MGED without an X11 dependency.
This may or may not require fixing minor issues in Tk, this will likely
require subtle tweaks to MGED's Tcl/Tk code to make things look
reasonable. Either way, your task would be to figure it all out, have a
plan, and make it work.

Requirements:

-   Basic familiarity with Tcl/Tk
-   Familiarity with Autotools-based build systems and resolving
    compilation/linkage issues
-   Good diagnostic/porting abilities

Difficulty: low

## Bug Fix Buffet

BRL-CAD is a massive code base with more than a million lines of code.
When you have that many lines, bugs are pretty much guaranteed. That
said, code quality is of paramount importance for the long-term
longevity of a code.

<https://sourceforge.net/tracker2/?group_id=105292&atid=640802>
<http://brlcad.svn.sourceforge.net/viewvc/brlcad/brlcad/trunk/BUGS>

This project is obviously pretty easy to explain. Propose a set of bugs
that you would like to work on fixing. They can be hard or easy, many or
few. Given the general nature of this task, be sure to be as specific as
possible in your proposal.

Requirements:

-   Methodical approach, deductive reasoning, and strong problem solving
    skills
-   Able to read and debug large amounts of other people's code
-   (optional) Familiarity with a debugger (if you don't know how to use
    a debugger, you will by the time you finish this)

Difficulty: variable

## IGES importer/exporter enhancements

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

Difficulty: low

## Universal geometry converter API

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

Difficulty: low

## STEP converter

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

Difficulty: medium

## New geometry converter

Though we have more than 30 geometry importers and exporters, there are
plenty that we don't have support for and existing converters that could
use improvements. Some examples of converters we would like to see
implemented include (in rough priority/interest order):

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

Difficulty: low

## Implicit to Explicit boundary representation support

Throughout BRL-CAD's numerous supported primitive geometry types (see
<http://brlcad.org/gallery/s/diagrams/primitives.png.html> for
examples), they are implemented using an implicit geometric
representation. This means, for example, that for a sphere with a given
radius, we store and manipulate it *as a sphere with a given radius* and
not as collection of triangles/polygons, not as some sort of spline
surface, not as a voxelized data set, etc.

Look in src/librt/primitives for the code to all of the primitives. The
\*_brep.cpp files in ell, nmg, sph, and tor include the work performed
to date.

This project requires implementing a routine for many/most/all of our
primitives that generates a NURBS/BREP spline surface representation of
that primitive shape. There are a few primitives that are already
complete due to previous developments, but there are still many
primitives that have yet to have the routine implemented.

Requirements:

-   Familiarity with C/C++
-   Solid mathematical foundations are required

Difficulty: medium

## New primitive

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

Difficulty: high

## Annotations

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

Dificulty: medium

## Web-based solid geometry model repository

This task focuses on creating a web interface to a geometry repository
where the community can store and exchange geometric models in any of
the supported BRL-CAD formats. The website could be written such that it
integrates with an existing content management system (e.g. Drupal
extension), wiki (e.g. Mediawiki extension), or could be custom with the
appropriate design plan. The site would need to provide a relatively
easy means for users to upload models and have those models be indexed,
categorized, searched, converted, and downloaded through the website
interface.

This tends to be a very popular submission. Make sure you relate your
idea specifically to BRL-CAD, our tools and services, and how you are
not ignoring what we already do. It needs to be a well-integrated
service if you're going to propose it.

Requirements:

-   Strong web development skills
-   (optional)Familiarity with Drupal or Mediawiki customization and/or
    module development
-   Must integrate well with BRL-CAD's format, tools, and services

Difficulty: low

## Global illumination renderer

This was a GSoC 2008 project. Talk to the developers before proposing
this task to obtain project status.

Our LIBRT library provides advanced solid modeling ray-trace facilities.
This idea is to use the LIBRT library and implement a global
illumination renderer such as a bidirectional path tracer (e.g.
metropolis light transport) or radiosity renderer.

Requirements:

-   Strong familiarity with C
-   Familiarity with global illumination rendering
-   Solid math background
-   Ability to learn and utilize existing C API

Difficulty: low

## Geometry database (i.e. ".g" file format) enhancements

Our ".g" file format is a binary geometry file format that provides a
robust, efficient, and flexible object storage framework. There are,
however, many features that would be really useful to have in the
database layer that are not presently implemented.

See <http://brlcad.org/OLD/newdb/newdb.html> to get started on some the
low-level details about our .g file format. See the source code for the
definitive status.

The idea behind this task would be to propose a set of enhancements,
whether they be backwards-compatible with our current "v5" geometry file
format or whether it be the development of a new "v6" file format. The
sorts of enhancements needed include time-stamping of geometry database
objects, support for constraints and parametric equations as intrinsic
object properties, objects with versioning and construction histories,
intrinsic support for surrogation, dynamic geometry, automatic space
compression, deleted object recovery, performance enhancements, and
more. There's plenty of room for new features and improvements, so be
specific in your scope and goals.

Requirements:

-   Familiarity with C
-   Ability to learn and extend an existing API

Difficulty: high

## Fixed-precision compile-time interface

BRL-CAD uses floating point computation pervasively with extensive
efforts taken to account for various floating point types and floating
point instability. For the purposes of regression testing and the
validation and verification of routines, it is highly desirable to have
the ability to guarantee calculations to a given precision.

Basically, this task entails implementing a GMP C++ interface as our
fastf_t type as a compile-time option. The task will require
refactoring a cleaning up a lot of the code throughout BRL-CAD so that
fastf_t's are pervasive to a given ray trace evaluation. It will also
require developing C++ operators to override behavior for \[\], +, -,
\*, and various others. BRL-CAD already includes a regression testing
suite that can be used to

See the "benchmark" tool in a BRL-CAD install to get started as well as
include/\*.h and src/libbn and src/librt for libraries you'll have to
work with. The main 'rt' raytrace binary is in src/rt/.

Requirements:

-   Familiarity with C/C++

Difficulty: low

## g_qa GUI

The g_qa tool provides a handful of ways to analyze a geometry file.
Providing an intuitive GUI with check boxes to select modes as well as
parsing the results for easier interpretation would be handy. See
<http://sourceforge.net/tracker/?func=detail&aid=2717388&group_id=105292&atid=640805>
for more details.

Requirements:

-   Basic familiarity with Tcl/Tk

Difficulty: low

## BRL-CAD Benchmark database website

The *BRL-CAD Benchmark* tests the performance of a system by iteratively
evaluating a system's overall computational performance capacity by
using a highly CPU-intensive application metric. The Benchmark renders a
series of scenes into 512x512 images and compares the results against a
reference baseline. The local machine's performance is compared to the
base system (called VGR) and a numeric "VGR" multiplier of performance
is computed. This number is a cumulative metric from which one may
qualitatively and directly compare cpu performance, cache performance,
differing versions of BRL-CAD, and different compilers.

This task entails wrapping up a web interface around the BRL-CAD
Benchmark suite so that results may be received from users, stored in a
database, and be summarized through a searchable web interface. The
project would be specific to the summary metric computed by the BRL-CAD
benchmark and various system and compilation characteristics for a given
result. Users should be able to visit the site, submit their results,
and see a comparison of their performance to other systems already in
the database.

Requirements:

-   Strong web development skills
-   (optional)Familiarity with Drupal or Mediawiki customization and/or
    module development
-   Must integrate well with the BRL-CAD Benchmark

Difficulty: low

# Mentors

BRL-CAD operates via *group mentoring* meaning that you may call upon
multiple individuals for assistance. Our mentors available to assist
are:

-   Sean Morrison (brlcad)
-   Erik Greenwald (\`\`Erik)
-   Daniel Rossberg
-   Brad Harder (yukonbob)
-   Cliff Yapp (starseeker)
-   David Loman (d-lo)
-   Keith Bowman (indianlarry)

[category: Summer of Code](category:_Summer_of_Code.md)
