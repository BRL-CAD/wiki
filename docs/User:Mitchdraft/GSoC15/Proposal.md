# Application Withdrawn

**Thank you for you consideration, however after more thought, I
realized I will not be able to commit the time required for this
project. I will leave this page here for reference, but I will not be
participating in GSoC15. I look forward to participating in the
BRL-CAD/OpenSCAD community in other ways.**

# Personal Information

-   **Name**: Mitch Kelley
-   **Email-address**: mkelley32@gatech.edu
-   **IRC username**: mitch
-   **Contact Number**: 508-838-1960
-   **Project Activity Log**:
    <https://github.com/mitchdraft/scaddergories/wiki/Project-Status-Monitor>
-   **Background Information**
    -   Candidate for Master's of Science in Mechanical Engineering at
        Georgia Tech, currently conducting thesis in improving CAD
        interfaces
    -   Bachelors of Science in Mechanical Engineering from MIT, 2011
    -   4 Years (ongoing) of mechanical engineering experience as a
        product development engineer (practicing user of Solidworks and
        other CAD tools in the engineering field)
    -   Budding software developer - the tools in a software developer's
        toolbox are extremely valuable in all aspects of life, I am
        eagerly integrating these tools into my workflow. I have
        extensive experience in Matlab/Scilab,
        Processing/OpenFrameworks, and arduino. I have a good
        understanding of programming principles and am not intimidated
        by new languages or development environments.
    -   In a graduate CAD class I prototyped a method for automatically
        positioning components in an assembly using a simulated
        annealing algorithm. To do this I created a simple voxel-based
        solid modeling environment in Matlab. You can see a demo
        [here](https://www.youtube.com/watch?v=L0L1OKj12I4). (If I were
        to do it again, I would have used OpenSCAD + improved coding
        skills and gotten a bit further!).

# Project Information: OpenSCAD Standard Library

**Title:** OpenSCAD Standard Library

**Introduction**

The OpenSCAD Standard Library requires three main things:

1.  Alignment of existing library items for ease of use while
    maintaining backward compatibility
2.  Definition of a framework for library expansion, involving:
    -   Identifying the items that should be included
    -   Cataloging these items in an easily searchable form
    -   Defining these items in the most expressive way.
3.  Production of new orthogonal content.

## Project Description

### Brief

**From OpenSCAD**

OpenSCAD comes with a number of basic built-in primitives and operators.
When creating 3D designs it would be useful to have access to a library
of commonly used parts and techniques. One way of improving the current
situation would be to define an OpenSCAD Standard Library. This would
include well-defined, orthogonal, well-tested and well-documented
components. All components would be user-space OpenSCAD code.

Some initial attempts, as well as ongoing work is being on in scad-utils
and the dev branch of MCAD.

Difficulty: Medium. The main challenge is to have good enough structure,
documentation and testing in order to have trustworthy and useful
components.

### Detailed

**As interpreted by the student**

There are many ways to approach this project. For an actionable
construct, I identify three main tasks in this project:

1.  Integrate existing libraries
2.  Include complete fastener kit
3.  Abstract the library framework

The first two identified tasks serve clear and immediate needs. These
will constitute the bulk of my work. The third task provides the
opportunity to capture insights developed along the way and recommend a
path forward. Please see the Tasks section for details.

## Why I am interested in this project and why I am the best person to do it

### I have a professional interest in this project

In my work as a product development engineer at a consulting company we
often start projects by doing an orthogonal technology review. It's
often one of the most important parts of the project, setting up a
framework for analysis. I have gone through the process many times,
mentored by industry experts. I thoroughly enjoy and have become adept
at features identification, analysis, and implementation. I would like
to apply this process to creating an OpenSCAD parts library. I have seen
the way good frameworks can enhance productivity and creativity. I know
a library like this will be useful to my colleagues and the growing
maker community.

### I have an academic interest in this project

In my research as a master's candidate under Professor Rosen at Georgia
Tech I am working to improve CAD funcationality and useability. My
specific thesis topic is establishing a framework for and evaluating the
utility of Human-Computer Interface (HCI) devices for CAD and other
technical, creative work. This work involves developing a CAD
environment to represent common practice user interactions and test new
interactions and features enabled by the integration of software and
existing and new interface devices. Professor Rosen is an authority on
the topic of modern CAD systems. He has been a great mentor, identifying
the state of the art and avenues towards the improvement of CAD systems,
focusing the work towards areas of maximum benefit. In this project I
have the opportunity to integrate insights of experts, community
members, and an analytical framework into a fully functional open source
platform.

### I have a personal interest in this project

My personal objective is to help people identify and achieve their
goals. I believe that Computer Aided Design (including 3D geometry
modeling and many other computer-facilitated organization and evaluation
systems) is the best tool for expressing the imagination. I
enthusiastically believe that it is true that "if you can dream it you
can do it." And since dreaming is difficult and important I want to do
whatever I can to help people realize their personal simple and
fantastic dreams.

## Tasks

### Integrate Existing Libraries

Hyperair has done a good job streamlining the existing MCAD library. The
[contents of the updated MCAD
library](contents_of_the_updated_MCAD_library "wikilink") feature 25
directories. There are many parts in these libraries, and many more on
[Thingiverse](http://www.thingiverse.com). It is difficult for the
average user to find and deploy parts from this library. I will make an
interactive catalog that will make it easy for users to scan through the
available parts and manipulate their parameters in real time.

I have made a prototype of this tool using OpenSCAD's live render
preview feature. You can see the tool in action
[here](https://www.youtube.com/watch?v=CiY9SCviUyg).

I will be able to move quickly in this task because Hyperair has done a
good job collecting the various parts in the existing library and I have
already identified the key features of the catalog tool and proven the
concept. By the time I finish this task (\~1 month) I will have an
intimate knowledge of the current library. I will have gained insights
into how to wrap it into a more holistic framework and identified areas
for improvement.

-   Deliverables:
    -   *Develop an interactive tool for rapidly navigating and
        selecting customized parts from the parts library*
    -   *Add support for all parts in the current MCAD library*

<!-- -->

-   Languages used:
    -   Processing - to make the library interface which will output a
        text file for rendering by OpenSCAD.
    -   OpenSCAD - for modifying existing MCAD code

<!-- -->

-   Reference technologies:
    -   PHP Composer
    -   Git hub
    -   Ubuntu package manager
    -   Solidworks parts libraries
    -   Thingiverse

<!-- -->

-   Expected time:
    -   1 Month

### Include complete fastener kit

Fasteners are a key part to most mechanical designs. Mechanical
engineers spend a considerable amount of time selecting and integrating
fasteners into designs. This can significantly impede the prototyping
process. Fortunately, fasteners are well standardized and cataloged, so
OpenSCAD is a perfect platform for automated fastener selection and
integration.

While it can be interesting and, at times necessary, to generate
complete models of thread geometry (ex: for 3D printing a model of a
screw), in most cases, mechanical designers only care about the
fastener's mechanical properties and volume occupancy. Complex thread
representation can slow render rates. Many professional CAD tools like
Solidworks offer "cosmetic threads" which replace thread meshes with
textures mapped to simple geometry. A few cylinders are capable of
capturing the key dimensions of most fasteners.

Fastening hardware is well standardized. Most hardware vendors have a
common core of fastener offerings. Many vendors offer CAD models of
these parts too. It is helpful for the mechanical designer to find a
part in an online catalog and download the CAD model to test for
interference. Often these vendors only provide the complicated full
geometry representations. Many instances of these parts can make model
manipulations sluggish. Furthermore, the CAD designer often has to
specify the fastener mounting location, clearance holes, and mating
hardware. It can take an adept designer several minutes to define the
parameters for simple fastener application.

I would like to develop a tool for calling a fastener by the desired
parameters (strength, material spec, screw driver type, etc.). The tool
would filter the the fastener list and prompt the user to select an item
or provide more filters. This would be similar to the parts filtering
interface on [McMaster](http://www.mcmaster.com).

Additionally, I would like to develop a function for specifying a
fastener assembly (nut, bolt, washers) by position and fastener name.
The function would make the necessary clearance holes in the existing
assembly and add the fastener assembly geometry to the model.

-   Deliverables:
    -   *Create a simple hardware selection tool (build into the
        interactive library tool)*
    -   *Create .scad representations for all nuts, bolts, and washers
        in a leading hardware supplier's catalog*

<!-- -->

-   Languages used:
    -   Processing - to make the fastener selection tool and integrate
        with the library tool.
    -   OpenSCAD - for generating hardware templates and
    -   SQLite(?) - for storing hardware catalog (could use .scad
        instead, will discuss with mentors)
    -   Data mining (TBD) - for collecting hardware parameters
    -   TBD - for converting available, verbose, CAD files to .scad
        hardware representations

<!-- -->

-   Reference technologies:
    -   Machinist's Handbook
    -   Fastener standards
    -   Strength of materials
    -   McMaster-Carr web catalog
    -   SDP-SI web catalog
    -   Data mining
    -   Least squares and other fitting algorithms (for extracting .scad
        representations from IGES and other verbose solid models)
    -   Interference detection algorithms

<!-- -->

-   Expected time:
    -   6 weeks

### Abstract the library framework

There is a good amount of design work to be done to generate an
effective standard library. A good way to approach this type of project
is with iterative prototypes. I view the current MCAD library as a
strong initial prototype. I hope to improve MCAD with my contribution
but I would be naive to believe that the best library can be produced in
a three month project and I would be negligent to discard lessons
learned. I intend to sketch-out/mock-up a larger framework for the
standard library based on my experience developing the features of Tasks
1 and 2.

I will conduct a more thorough evaluation, but at first pass, some
components which I think are important to have well represented in the
standard library include:

-   Stock material in standard dimensions (thickness, profile)
-   Standard electronics components (non-board mounted)
-   Fixtures
-   Chassis

Some features which would be very useful in the standard parts library
include:

-   Tolerance representation
-   Annotation
-   Part-specific insertion calls (some parts need to be on the surface
    on an assembly, some can be left inside)
-   Personal inventory
-   Personal library creation or filtering
-   Domain-specific filters
-   Vendor-specific parts names and prices

<!-- -->

-   Deliverables:
    -   *Integrate and abstract lessons learned to a larger library
        framework draft.*
    -   *Identify at least 10 categories of parts which should be
        included in future versions of the standard library*
    -   *Implement at least 5 additional part categories*
    -   *Identify and justify at least 5 desirable features of a future
        library.*
    -   *Prototype two future library features.*

<!-- -->

-   Languages used:
    -   Processing - for extending the Task 1 & 2 library interface.
    -   OpenSCAD - for generating seed models for the abstracted library
        framework.

<!-- -->

-   Reference technologies:
    -   Qt language interface features (the tool used for OpenSCAD's
        interface, prototypes should be designed with awareness of Qt's
        capabilities)

<!-- -->

-   Expected time:
    -   2 weeks

## Schedule/Milestones

-   Weeks 1-4
    -   Study MCAD library, extract all functions and parameters
    -   Develop interactive parts selection and customization tool
-   Weeks 5-10
    -   Develop fastener selection tool
    -   Develop fastener assembly insertion functions
    -   Establish database/calling functions for all common hardware
-   Weeks 11-12
    -   Seed library with additional parts
    -   Create future library feature prototypes
    -   Document additional opportunities for library expansion

# Availability

-   I work a full time job but will still be able to commit 40-45 hours
    per week to this project. This project is important to me. In one
    sense, my work as a mechanical engineer is the ultimate user study.
-   I can be reached online or by phone 5-9 AM or 5-11 PM EST.
-   I will spend one week during July at the beach. During this time
    I'll reflect on the bigger problems (haha). I can route any lost
    time to the weekends.