# STEP Viewer Project Development Log

## Week 01/05/2015 to 08/05/2015

-   I am getting familiar with the source code of libdm and librt.
-   Design and Developing Qt GUI for STEP Viewer program

## Week 09/05/2015 to 16/05/2015

As Sean mentioned in brlcad-devel Digest, Vol 607, Issue 1

-   Look in to myriad of examples in the src/util directory
-   Started a sample project which is capable of generating libdm
    window.

## Week 16/05/2015 to 23/05/2015

-   Worked on STEP Viewer functionality
-   Downloaded the current version of the BRL-CAD code and build it
-   Studied the libdm library

## Week 23/05/2015 to 30/05/2015

-   Start coding StepViewer
-   First task (as Sean has mentioned) Try to create a libdm window
-   Creation of the libdm window of type X and OGL failed.
-   Creation of the libdm window type of null and text succeeded.
-   Found that libdm is hard to work with
-   No Proper Documentation for the libdm library

## Week 30/05/2015 to 7/06/2015

-   Refereed on OpenGL
-   Created a separate OpenGL Window
-   Trying to embed OGL view to a existing Qt window.
-   Success fully embedded the OGL view in the main window.

## Week 7/06/2015 to Week 14/06/2015

-   Development of STEPViewer GUI.
-   OpenGL view zoom in/out functionality added
-   OpenGL view rotation according to mouse movement functionality added
-   Displaying the 3D axis system in OpenGL view.
-   Current Code can be found at
    <https://bitbucket.org/milindasf/stepviewer/src>
-   Referring on how to use BRLCAD functionality to browse the triangles
    in a STEP file and visualize them in the OGL viewer.

## Week 14/06/2015 to 22/06/2015

-   Used step2g converter to convert .step file .g file.
-   Read the .g file to STEPViewer program
-   Conversion from db_i\* to rt_brep_internal\*
-   Iterated brep for edges and visualized those edges in OpenGL view.

\[1\]
<https://bitbucket.org/milindasf/stepviewer/src/f888657ba24b0a1e7cfe9b6de27b6d356089ab22/images/step1.png?at=default>

\[2\]
<https://bitbucket.org/milindasf/stepviewer/src/f888657ba24b0a1e7cfe9b6de27b6d356089ab22/images/step2.png?at=default>

## Week 22/06/2015 to 29/06/2015

-   Looked into the brlcad/src/conv/step/step-g code.
-   Found that STEPWrapper::convert is responsible for convert the .step
    file to .g file
-   Wrote a new method bool convert(BRLCADWrapper\* dot_g,ON_Brep\*
    brep) which doesn't write to .g file but from the
    AdvancedBrepShapeRepresentation::GetONBrep method we can get the
    .step file converted to the ON_Brep Structure
-   Above mentioned change complies fine. Currently I am looking how to
    get statically link library instead of .out file
-   Finalized the code in current implementation

### Current status of the project

-   Currently StepViewer reads a .step file and generates temporary .g
    file.
-   .g file is read to db_i structure then converted to the
    rt_db_internal structure -&gt; rt_brep_internal -&gt; ON_Brep
    structure
-   Once we get the ON_Brep structure of the .step file I iterate
    through all the edges of the brep and draw them in the OpenGL
    visualizer. (This looks like the wire frame of the .step file)
-   User can interact with the loaded geometry by rotation (using LEFT
    CLICK + mouse movement) , Zooming (Mouse scroll movement) and
    panning (to be implemented)

### Main Challenges

I believe I have 2 main challenges. 1). How to render a solid object in
OpenGL viewer using the data in ON_Brep structure. (According to the
charlie, he mentioned that building the solid from primitive brep shapes
(i.e vertex, edge,facet etc) is out of the scope of this project. But he
did not mention some alternative method to do that. Currently I have no
idea to what to do to solve this)

2). Build a statically linked library which can get ON_Brep structure
from .step file. By modifying the step-g conversion code. This is not a
huge challenge. I think I almost solved it.

### MID TERM EVALUATION DEMO

-   You can clone the code from the bitbucket repository.

<https://bitbucket.org/milindasf/stepviewer/src>

-   Open the project from the Qt Creator. Build the project. Run and you
    can play with the basic STEPViewer functionality that I have
    described in "Current Status of the project".
-   If you have any questions regarding running the project or any
    matter related to this project please feel free to contact me by
    e-mailing to dev-mailing lists (Both BRLCAD and STEPCODE) or
    personally e-mailing me to milindasf@gmail.com.

## Week 30/06/2015 7/7/2015

-   Changed the step-g conversion code to return the ON_Brep Structure.
    (.step to .g file conversion is stopped at the binary memory format.
    )
-   Struggling with changing the cmake files to get step-g conversion as
    a statically linked library (I am not an expert in cmake)
-   Since I have completed the step-g conversion to stop at ON_Brep
    structure and I struggled to build the step-g code as statically
    linked library (I believe this is a very trivial task) I thought I
    will complete that task later.
-   Started working on How to visualize the ON_Brep shape in OpenGL
    view.
-   Get to know that I need to browse the surface triangles in order to
    visualize the ON_Brep structure as a solid in OpenGL View.

## Week 7/07/2015 15/07/2015

-   Start referring the poly2tri_CDT method in
    librt/src/primitive/brep/brep.cpp file.
-   I am still struggling with browsing surface triangles in ON_Brep
    structure.