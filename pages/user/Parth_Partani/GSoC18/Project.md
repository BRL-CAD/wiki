## **LibreCAD 3 OpenGL rendering**

### **Abstract**

Librecad ( 2D cad application) can be used for drawing all types for
basic shapes on a specified grid area with a very good precision in the
position and can be used to draw 2D figures using lines, circles ,
rectangles, arc’s, etc. Also there are other tools of layers, snap,
measure of two points and a command line interface to figure out all the
shapes using commands.

### **Brief Summary**

Currently rendering of the complete librecad is done using cairo engine.
It’s backend does involves some part of opengl but I would like to
change the rendering engine and create a complete implementation of
OpenGl for the rendering. It would reduce some dependencies of cairo,
GTK, etc and another advantages of using OpenGl is it has lower CPU
overhead for draw calls which will make the working of Librecad faster.

Right now rendering is done completely using cairo, so my goals will be
writing code for the rendering engine in OpenGl ( c/c++ ).

Under the time period of GSoC I would be working on changing the
rendering engine which mainly involves the Working Area which contains
painter and this will include everything that needs to draw on screen.
Also this task will involve with the changes in the part of Command Line
Interface tool that creates the image of the result depending on the
command entered and for the testing of the engine task will include some
unit tests.

### **Detailed Project Description**

-   Creating the drawing area with the background and adding grid using
    horizontal and vertical lines that renders when the program begins
    and display of the image until any changes are made.

<!-- -->

-   Implementation of scroll bar (both horizontal and vertical) and set
    the camera coordinates to fix initial fixed coordinates as the grid
    is very large to fit in a single screen.

<!-- -->

-   Adding the feature of zoom in and zoom out to the working area. On
    zoom, the engine scales the grid and everything on the drawing area
    with a particular factor and output the scaled image keeping the
    center according to mouse pointer where zoom is done.

<!-- -->

-   Creating the mouse pointer with the shape as in the earlier code and
    display of current coordinates of the mouse pointer. On movement of
    mouse, continuous rendering occurs and renders the image with
    pointer at new position and also the display of the coordinates of
    that position.

<!-- -->

-   Working of draw tools such as lines, circles, arcs, etc. On select
    of any of the tool for UI command line interface displays the
    arguments for the tool. The shape gets created over the grid which
    displays and highlights the vertices with small squares and
    highlights the shape when mouse pointer passes through the shape.

<!-- -->

-   Creating of the select feature. On selecting any point on the
    working area and dragging the mouse pointer a rectangle gets created
    of different color and the engine keeps on displaying the rectangle
    of different area as the mouse moves. If any object happens to lie
    completely inside the selected area. The particular object gets
    highlighted along with its reference points. After the release of
    the mouse, the image of the rectangle dissolves.

<!-- -->

-   Currently cairo consists of subdirectory cmake which check for the
    dependencies i.e. cairo, pango, GDK, etc. For the new engine it will
    check for all dependencies of OpenGl. Also adding part for compiling
    using opengl in CMakeFiles.txt and further it would give a choice of
    compiling Librecad using any of the engine according to user.

<!-- -->

-   Working on unit tests for the testing of rendering by OpenGl. There
    will be changes in unit tests for rendering and comparing ( with
    some tolerance ) examples from the resources. Along with this there
    will be some changes in CMakeFiles.txt because these tests need to
    be compiled with OpenGl.

### Timeline

Tentative timeline of the project over the summer of 2018.

-   Community Bonding Period :
    -   I will try to complete the research of the previous
        implementation of the proposed task and also do with the
        documentation and description of opengl required in my task) and
        try to get familiar with the working before this period and move
        on to creation of basic classes in the code.
    -   I will look at the other implementations of my proposed task and
        learn about their implementation and get started with it.

<!-- -->

-   Week 1 (May 14 - May 20) :
    -   Build a layout for the painter i.e. basic grid and setting
        camera coordinates at some initial fixed position.
    -   Also adding scrollbar for horizontal and vertical scrolling up
        to some extent.

<!-- -->

-   Week 2 (May 21 - May 27) :
    -   Creating a mouse pointer of particular shape and making it's
        movement in sync with the movement of the mouse.
    -   Dynamic saving and printing of the current coordinates of the
        mouse.
    -   Working of the scrollbars and printing of the grid according to
        the scroll amount.

<!-- -->

-   Week 3 (May 28 - June 3) :
    -   Working of the zoom feature and testing of the proper scaling
        according to the zoom.
    -   Getting started with the drawing of the cad tools.

<!-- -->

-   Week 4 (June 4 - June 10) :
    -   Test my activity and refine it.
    -   Take more reviews for my work from the mentors.
    -   Make required changes on the basis of reviews.

<!-- -->

-   Week 5 (June 11 - June 17) :
    -   Completing the working of all the basic draw tools.

<!-- -->

-   Week 6 (June 18 - June 24) :
    -   Working on the other tools i.e. the dimension tools and also the
        working of the modify tools.

<!-- -->

-   Week 7 (June 25 - July 1) :
    -   Continued working on the implementation of cad tools.
    -   Testing of the working of draw shapes using command line
        interface.

<!-- -->

-   Week 8 (July 2 - July 8) :
    -   Working of the select feature by click and drag on the area and
        working on rendering rectangle and related objects.
    -   Dissolving of the rectangle for selection area on release and
        highlight of the shape select.

<!-- -->

-   Week 9 (July 9 - July 15) :
    -   Continuing the unfinished work of the rectangle and highlight of
        objects due to it.
    -   Working of the building of unit tests for the rendering and the
        comparing the rendered image with the image in the resources.

<!-- -->

-   Week 10 (July 16 - July 22) :
    -   Checking tests for different tolerance values and check on the
        proper working of the tests.

<!-- -->

-   Week 11 (July 23 - July 29) :
    -   Working on the choice feature of the CMakeFiles.txt to compile
        the render according to the user input.

<!-- -->

-   Week 12 (July 30 - Aug 5) :
    -   Testing the working on both engines and working of choice
        feature and \*\*resolving bugs.

Get the changes reviewed from mentors and make the changes accordingly.

### Why Me

I am a second year undergraduate engineering student from International
Institute of Information Technology, Hyderabad (IIIT-H), pursuing B.Tech
in Electronics and Communication Engineering. I have been contributing
to open source projects from the last few months. I love developing
games and I have created a few games on Qt and OpenGl.