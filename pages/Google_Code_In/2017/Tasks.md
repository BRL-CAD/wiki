# Dashboard for Ideas for the Google Code In 2017

## Roles

-   Coder (C/C++)
-   Web Coder (Javascript/HTML)
-   Modeler
-   Writer

## Beginner tasks

These require absolutely no prior experience or knowledge.

-   Anyone: Download and run BRL-CAD (via VM), submit screenshot
-   Anyone: Communications checklist: chat, mailing list, survey
-   Coder: Compile BRL-CAD from source, submit screenshot
-   Web Coder: Clone BRL-CAD website or OGV, submit screenshot
-   Modeler: Model a cup, submit model
-   Writer: Blog about any task, submit link
-   Annotate a primitive: Submit screenshot

## Task chain ideas

These would take us more than 2 hours, to be broken up into multiple
tasks.

-   C: OpenCL pipelining
-   C: Boolean evaluation debugging
-   Javascript: OGV
-   ThreeJS/Verb: OGV Nurbs
-   C/C++: libbu C++11 threading
    -   implement bu_semaphore_acquire/bu_semaphore_release in C++11
    -   implement bu_parallel in C++11
-   C/C++: libbu container testing
    -   Write program comparing performance of bu_list vs c++ lists
    -   Write program comparing performance of bu_list stacks vs c++
        queues
    -   Write program comparing performance of bu_hash vs c++ map
    -   Write program comparing performance of bn_randmt vs c++ random
-   C/C++: primitive unit tests (ProcDBs)
    -   arb8/arb7/arb6/arb5/arb4, arbn, ars, datum, dsp, ebm, ehy,
        ell/sph, epa, eto, extrude, half, hrt, hyp, metaball, pipe,
        pnts, revolve, rhc, rpc, sketch, submodel, superell, tgc/rec,
        tor, vol
    -   (intentionally leaving out bot, brep, bspline, cline, grip,
        joint, nmg, part, poly)
-   Docbook/XML: primitive guide
    -   arb8/arb7/arb6/arb5/arb4, arbn, ars, datum, dsp, ebm, ehy,
        ell/sph, epa, eto, extrude, half, hrt, hyp, metaball, pipe,
        pnts, revolve, rhc, rpc, sketch, submodel, superell, tgc/rec,
        tor, vol
    -   also: bot, brep, nmg
    -   (intentionally leaving out bspline, cline, grip, joint, part,
        poly)
-   Qt/C++: New visualization GUI
-   Qt/C++: geometry viewer
    -   [BRL-CAD Viewer](https://github.com/asadpiz/brlcad-viewer):
        (Task 1) Open a simple GLFW window from the source
    -   [BRL-CAD Viewer](https://github.com/asadpiz/brlcad-viewer):
        (Task 2) Write a program that opens geometry, executes
        db_walk_tree(), and gets a bounding box.
    -   [BRL-CAD Viewer](https://github.com/asadpiz/brlcad-viewer):
        (Task 3) Print out the bounding box center point into the GUI
    -   [BRL-CAD Viewer](https://github.com/asadpiz/brlcad-viewer):
        (Task 4) Display wireframes, regions on to the window.
-   Qt/C++: openscad-style asc-to-display GUI
    -   (Task 1) Open a simple Qt window from source
    -   (Task 2) Write a program that opens .asc, displays in Qt text
        window
    -   (Task 3) Write a simple program that converts .asc to .g in
        memory
    -   (Task 4) Write a simple program that renders an in-memory .g to
        .pix
    -   (Task 5) Write a program that displays a .pix image into a Qt
        window
    -   (Task 6) Tie it all together: Qt button that converts, renders,
        and displays.
-   C/C++: appleseed integration
    -   Create and render a box in Appleseed and BRL-CAD
    -   Write a small program in BRL-CAD that renders an image
    -   Write a small program in Appleseed that renders an image
    -   Implement an Appleseed hello world plugin
    -   Integrate BRL-CAD rendering into Appleseed plugin
-   C: Boolean weaving unit tests
    -   implement a regression test for rt_boolweave()
    -   implement a regression test for rt_boolfinal()
-   C: Annotation object callbacks
-   C: point cloud object callbacks
    -   Implement the prep() and shot() functions for point clouds
    -   Implement a function that reads point data from files
    -   Integrate function reading points from files into libged
-   Merge push and xpush code
    -   Implement an xpush/push unit test
    -   Add xpush logic to push command via -x option
    -   Eliminate redundate xpush+push code
    -   Merge xpush documentation into push documentation
-   C: libged plugin refactoring
-   C/C++: stand-alone geometry viewer GUI
-   C: Centroid/Volume/Surf_area
-   HTML/CSS: website integration
-   Docs: geometry URI specification
-   Docbook/XML: datum docs

<!-- -->

-   Disconsidered...
    -   C: Layer object callbacks
    -   C: image object callbacks

## Independent task ideas

These should take one of us 2-4 hours of effort to complete.

-   Implement sphere flake non-recursively

<!-- -->

-   Model and render the number "404"
-   Model the word "BRL-CAD"
-   Model the BRL-CAD logo
-   Model a ball and jacks
-   Model an hourglass (with sand)
-   Model dice (with white numbers)
-   Model a chess pawn
-   Model a chess knight
-   Model a chess bishop
-   Model a chess rook
-   Model a chess queen
-   Model a chess king
-   Model a chess board
-   Model a coffee cup (with coffee)
-   Model a soccer ball / fútbol accurately
-   Model a basketball accurately
-   Model a baseball (with stitching)
-   Model a baseball bat (with woodgrain texture)
-   Model a golf ball accurately
-   Model a volley ball
-   Model an American football
-   Model a tennis ball
-   Model a tennis racket

<!-- -->

-   Import and render any model
-   Import and render a point cloud