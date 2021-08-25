## Personal Information

Name: Djimeli Konrad Niba

E-mail address: djkonro35@gmail.com

IRC-nick: konrado

### Project priority : 1

## Project Title: X3D Importer

## Abstract

`   Geometry conversion is a very important aspect for every CAD software as it is the basis for CAD data exchange between various CAD softwares. BRL-CAD has dozens of importer and exporters but this does not include support for X3D file import. This project seeks to implement an X3D importer for BRL-CAD and would rely on using the FreeWRL's X3D parsing  library for this task. FreeWRL is an open source compliant VRML/X3D browser for Microsoft Windows, Linux and Mac OS X which is multi-threaded, written in C, and uses OpenGL for rendering.`

## Detailed description

### Introduction

`   Implementing an X3D importer would require parsing an X3D file (with .x3d extension), which uses the xml file format  for representation. The nodes encountered within the file are stored in a scene graph. Various geometry entities are retrieved from the scene graph, processed(transformed) and converted to BRL-CAD type entities and stored in a BRL-CAD database file (with a  .g extension). Achieving this would require implementing a wrapper class for both FreeWRL and BRL-CAD like that of the step importer,  in order to facilitate interaction between BRL-CAD and FreeWRL.`

### Implementing X3D wrapper class

`   This wrapper class would be used to invoke the FreeWRL routine for parsing X3D file and also retrieving  nodes from the scene graph and their properties. `

-   This class would contain as class data members input and output
    filename and also a pointer of type struct X3D_Group to the root
    node of the scene graph.

<!-- -->

-   We would begin by developing a load function were we would set up
    the main file / world to be parsed then we call the file parsing
    routine after threads initialization.

<!-- -->

-   The file parser would return a pointer to the root node which would
    be stored in this class root node pointer and used to traverse the
    scene graph.

<!-- -->

-   The class would also contain a doColor(...) and doTransform(...)
    function used to add colour and transform variables to the
    Geometry3D components. This is because FreeWRL splits every shape
    into polygons and carries out transformation on their vertices just
    before it passes it to OpenGL. But we do not want this since BRL-CAD
    already has support for various primitives which would require us to
    use their respective functions and not split them. These function
    would traverse the scene graph assigning transform values to
    children nodes from parents and also colour values from Material
    node to its shape children nodes. This would ease passing primitive
    nodes to BRL-CAD.

<!-- -->

-   Terminating threads. This would actually entail writing some unit
    test to ensure that all threads are successfully terminated after
    the scene graph is generated and also ensure that all nodes are
    obtained from the file being parsed before the threads terminate.

### Implementing BRL-CAD wrapper class

`   This class would handle the conversion of geometry node to various BRL-CAD representation. We would have to deal with X3D Geometry3D Component, Shape Component, Grouping Component and Rendering Component.`

-   Rendering Component. This consist of Coordinate, IndexedLineSet,
    IndexedFaceSet, IndexedTriangleFanSet, IndexedTriangleSet and
    IndexedTriangleStripSet nodes. These are all polygonal
    representation nodes, so we would have to obtain their coordIndex ,
    points , generate vertices , carry out parent transformation then
    call mk_bot(...) to process the vertices and store in a BRL-CAD
    database file.

<!-- -->

-   Geometry3D Component. This consist of Box, Sphere, Cylinder and Cone
    nodes.

`   Box node would require getBox(...)  function which would compute x, y and z coordinates from box size array. This coordinates are further used to compute box edge points which are passed to mk_arb8(...) to make box primitive and store in a BRL-CAD database file.`
`    Sphere node would require getSphere(...)  function which would use radius of sphere to compute point A, B, C and center points of an ellipsoid and pass to mk_ell(...) to make sphere primitive and store in a BRL-CAD database file.`
`    Cylinder node would require getCylinder (…) function which uses height and radius values for Cylinder to compute points to be passed to mk_tgc(...) to make cylinder primitive and store in a BRL-CAD database file.`
`   Cone primitive is very similar to cylinder except for the fact that the bottom radius of a cone is different from that of the top.`
`   `

-   Shape Component and Grouping Component are basically containers for
    other geometry node and their related properties. For example
    grouping component, groups related nodes together, thus transform
    node is an example of a grouping component . Shape component
    contains Material node which hold colour description for shape
    geometry child node. This colour would have to be obtained and
    assigned to appropriate geometry entity within the X3D wrapper
    class.

### Implementing x3d-g.cpp

`   This file woulds process command line arguments, call wrapper functions like load function and handle/check file input and output.`

### Further work/improvements

-   Develop X3D exporter. Given that most of the work on import would be
    handled by the FreeWRL library, any extra time left would be used to
    work the x3d exporter.

<!-- -->

-   Since FreeWRL does no yet have any implementation support for nurbs,
    I would like to add this support to the library after the Google
    summer of code period.

## Reference

1.  <http://www.web3d.org>
2.  <http://freewrl.sourceforge.net/index.html>
3.  <http://en.wikipedia.org/wiki/X3D>

## Previous Related work (patch)

1\. vrml-g converter

`   `[`http://sourceforge.net/p/brlcad/patches/320`](http://sourceforge.net/p/brlcad/patches/320)

2\. g-stl default top level objects conversion

`   `[`http://sourceforge.net/p/brlcad/patches/301/`](http://sourceforge.net/p/brlcad/patches/301/)

## Deliverables

1.  Integrating FreeWRL with BRL-CAD
2.  Implement import support for polygonal geometry entities
3.  Implement import support for primitive geometry entities

## Time-line

### 27 April – 24 May (4 weeks) Community Bonding

`   Initiating communication with mentors, better familiarization with FreeWRL source code, isolating parsing bits of source code and ensure code compiles within BRL-CAD. `

### 25 May – 11 June (2 weeks)

`   Implement load(...) function. Test and ensure node are entirely parsed and threads  are successfully terminated after scene graph is obtained.`

### 12 June – 20 June (1 week)

`    Implement doColor(...)  function to traverse scene graph and obtain geometry node colour from shape component Material node. Write unit test to evaluate function.`

### 21 June – 29 June (1 week)

`   Implement  doTransform(...) function to traverse scene graph and obtain geometry node parent transform value and apply on node. Write unit test to evaluate function.`

### 30 June – 3 July (3 days) Mid term evaluation

### 3 July – 16 July (2 weeks)

`    Add support for rendering component.`

### 17 July – 1 August (2 weeks)

`   Add support for  Geometry3D component.`

### 2 August – 9 August (1 week)

`   Implementing x3d-g.cpp. Code cleanup, documentation and test converter functionality`

### 10 August – 16 August (1 week)

`    Begin work on g-x3d exporter.`

### 17 August – 23 August (1 week) Suggested 'pencils down'

`   Conclude work on x3d importer. Code cleanup, documentation and testing.`
`   `

### 24 August – 28 August (4 days) Final Evaluation

## Time Availability

`   I have no commitment within the Google summer of code period except for my end of semester exams which would run for about two weeks around 24 June– 11 July , but I would make up for the time by putting in more hours before this period guarantying at-least 40 hours a week.`

## About Me

-   2013 – 2014: Freshman Computer Engineering [University Of Buea
    Cameroon](http://www.ubuea.cm)
-   2014 – 2015: Freshman Computer Science and Mathematics [University
    Of Buea Cameroon](http://www.ubuea.cm)

`   My change in department was because of my passion for coding and mathematics and also due to my low interest/motivation for electronics which was a large part of the engineering curriculum. This has given me the time to focus on the thing I am very passionate about and since this is the first year computer science is being offered as a major for the undergraduate level at my university, participating in the Google summer of code would be an encouragement to others who intend to enroll into this department.`
`   I am primarily a c/c++ programmer with special interest in computer graphics, computer networking, multi-threading and artificial intelligence.`

## Why Me

`   I have always had the interest of contributing to open-source and have made some contributions to BRL-CAD like development of a vrml-g converter. Working on the vrml-g converter has given me some experience on what geometry conversion is all about, thus higher chances of success in completing this project. I would also have the opportunity to gain more experience and learn lots of new things.`

## Why BRL-CAD

`   I choose BRL-CAD because since I started contributing to this community I have had the opportunity to learn so much about software and open-source development and also due to my special interest in computer graphics.`