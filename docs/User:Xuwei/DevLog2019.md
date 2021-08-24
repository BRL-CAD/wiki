# Coummunity Bonding Period

-   Set up the Development log
-   Set up the development environment such as OS.
-   Start to look at the different potential libraries code base.
-   Discuss with mentors which external library to choose.

## May 16th

-   Start to check the checklist.
    -   Agreement sent.
    -   Dev log created.
    -   My Profile created.

## May 17th

-   Had four of my wisdom teeth extracted. The progress for the
    following week may be slow due to teeth extraction.

## May 19th

-   Looking at
    [Coin3D/Dime](https://bitbucket.org/Coin3D/dime/src/default/) code
    base, a possible library for DXF import/export.
    -   It has no external dependency.
    -   It supports all past and should support the future version of
        DXF format.
    -   It compiles on Windows, Linux, MacOS, etc.
    -   But it only loads DXF files into Dime object hierarchies and
        saves Dime object hierarchies as files conforming to DXF format.
    -   Seems only support 3D.

## May 20th

-   Looking at
    [BRL-CAD](https://sourceforge.net/p/brlcad/code/HEAD/tree/brlcad/trunk/src/conv/dxf/)
    DXF import/export code. Trying to understand how it works and see if
    it is suitable for OpenSCAD.
    -   It converts DXF format to .g and .g to DXF which is a BRL-CAD
        format.
    -   It seems that BRL-CAD does not support the entire format, only
        the part that is relative to solid-model.

## May 21st

-   Looking at [dxflib](https://qcad.org/en/90-dxflib) which is used by
    QCAD and works fine, but it only supports 2D which is not ideal
    since OpenSCAD is already supporting 2D.
    -   Maybe we can add the 3D part. But not sure how hard it is to add
        that.

## May 22nd

-   Searching for a library that supports both 3D and 2D DXF
    import/export.
    -   Libraries above are for either 2D or 3D.
    -   Found some libraries support both but they are written in python
        instead of C++.

## May 23rd

-   Continue on searching for the potential library.

## May 24th

-   Looking at and Compile
    [libdxfrw](https://github.com/LibreCAD/libdxfrw) code base which is
    used by LibreCAD.
-   Will be out of town for the next two days.

# Coding Period

## May

### May 27th

-   Looking at both libdxfrw(libdxfrw.h, dxfreader.cpp) and
    OpenSCAD(dxfdata.cc, dxfdim.cc, import.cc) relative code.
    -   Comparing the differences between these two on how they handle
        DXF data.
    -   Trying to form a connection between these two.
    -   dxfdata.cc seems a bit complicated. Need some time to digest.
    -   The way that libdxfrw reads DXF file is kind of mixing with DRW
        code.
    -   libdxfrw encounters problems when dealing with elevated arcs(no
        response yet).[1](https://sourceforge.net/p/librecad/bugs/596/)
-   Looking at dxflib code base as well.
    -   dxflib does not store any entities, only pass supported
        entities.
    -   A useful link for understanding dxflib data
        structure.[2](https://qcad.org/doc/dxflib/2.5/classref/class_d_l___dxf.html)

### May 28th

-   Move on to reading dxflib code for now
    -   Continue reading the link about the data structure of dxflib
        above.
    -   Trying to understand form the connection between dxflib and
        OpenSCAD code base.
-   Continue reading dxfdata.cc

### May 29th

-   Found another one existing integration with dxflib that I can use it
    as
    reference.[CAMotics](https://github.com/CauldronDevelopmentLLC/CAMotics/tree/master/src)
-   Continue on reading dxflib and import.cc, dxfdata.cc.
    -   Keep trying to write some code that may help understanding how
        to integrate the library.
-   Fill out the comparison [wiki
    page](https://github.com/openscad/openscad/wiki/DXF-Library-overview)

### May 30th

-   Had to go the dentist this morning, will catch up the afternoon and
    at night.
-   Keep browsing for more information for those four libraries.
-   Reading [DXF
    standard](https://images.autodesk.com/adsk/files/autocad_2012_pdf_dxf-reference_enu.pdf)
    to learn how DXF format works

### May 31th

-   Searching more information for potential libraries.
    -   Add more information that found to the comparison page.
-   Learning how to integrate the library from the
    [instruction](https://ribbonsoft.com/doc/dxflib/2.5/reference/contents.html)
    written by QCAD.

## June

### June 3rd

-   We stick with using BRL-CAD's code for now.
-   Try to implement the circle entity.
    -   Add a callback function on
        [dxf-g.c](https://github.com/leonplust/brlcadDXF/commit/1abc40cbe24793fbd9f94001b1a8d30e28602780#diff-3db848059130b96c98744620379df21a)
        to pass the data back to openSCAD.
    -   Add processentitiyecircle() to
        [dxfdata.cc](https://github.com/leonplust/openscad/blob/dxflibrary/src/dxfdata.cc)
        and some other changes to enable that function.
    -   Having some issue with ADDLINE. Will dig into that later.

### June 4th

-   Push few commits on [import_dxf
    branch](https://github.com/leonplust/openscad/tree/dxf-import).
    -   Basically create a new import_dxf() function that replace the
        old dxfdata.cc
    -   Implement a simple geometry to test out the function

### June 5th

-   Modify the code committed yesterday to output a simple circle.
-   Trying to understand layer, block.

### June 6th

-   Created a new branch
    [prototype](https://github.com/leonplust/brlcadDXF/tree/prototype)
    on brlcadDXF repo.
    -   Trying to clean up the code so that it could compile
        independently.

### June 7th

-   Switch some functions and datatype and continue on cleaning up the
    code.
-   Spend most of my day studying the exam tonight. Will make up the
    time tomorrow.

### June 8th

-   Walked through the whole file line by line and cleaned up as much as
    I can so far. There are still many details that I need to learn to
    clean up the rest.

### June 10th

-   Made changes to dxf-g.c according to the answer from brlcad.

### June 11th

-   fix bu_list with std::list and related functions, etc.

### June 12th

-   Add functions for circle eclipse from vmath.h, color.h.

### June 13th

-   Added more functions from dependencies.
-   uploaded a file that records to-do list, question, notes, etc.

### June 14th

-   few fixes on dxf-g.cc.
-   Study for the midterm tonight for the most of the day will make up
    the hours tomorrow.

### June 15th

-   Finished converting all bu_list data structure to std::list except
    in one function drawmtext().
    -   drawmtext() may be removed later.

### June 17th

-   Finished fixing all bu_vert_tree structure.
-   Started on fixing vls a bit.

### June 18th

-   Finished fixing all vls except those in the main().

### June 19th

-   Finished most of the parts of dxf-g.c.
    -   Create a new branch
        [test](https://github.com/leonplust/brlcadDXF/tree/test) for
        testing and commented out some less necessary functions to test.
    -   Upload test files from openSCAD testdata/dxf
    -   Need to fix the segmentation fault.

### June 20th

-   Fixed numbers of segmentation faults mainly caused by malloc.

### June 21st

-   Fix strncmp function error
-   Tested with circle, ellipse, failed at block section.
-   Tried to reconstruct block_list, block_head data structure.

### June 24th

-   Fix block_list data structure
-   Now dxf-g.cc can go through the whole dxf file and spit out data to
    file output
-   Done basic testing with circle, ellipse, polygons, lwpolyline. files
    from openscad testdata/dxf.
    -   Found the correct geometry.
    -   coordinates of the vertices are correct.

### June 25th

-   Randomly picking files from openscad/testdata/dxf to check geometry
    and coordinates.
-   Trying to figure out if the data structure is actually storing the
    correct data.

### June 26th

-   Trying to extract data from the data structure to test if it's
    reading correct data.
    -   For circle, extract cirlce_pts.
    -   For line, extract line_pts.
    -   For lwpolyline, extract polyline_vertice.
    -   For elllipse, center and majorAxis
    -   For point, pt.

### June 27th

-   More data extracting continue from yesterday.
-   Try to start integrating openscad and dxf-g.cc just for circle
    entities.

### June 28th

-   Run openscad together with dxf-g.cc.
-   Implemented circle entities using dxf-g.cc called a openscad
    function.
    -   Later the day discussion concluded that this is not the
        preferred way. deprecated.

## July

### July 1st

-   Added structs for each geometry for storing the data.
-   Some minor fixes for original data type point_t.

### July 2nd

-   storing all the data parsed to the respect vectors.
    -   Except polyline is a bit tricky, not done yet.

### July 3rd

-   Added polyline struct and the storing part.
-   Added code for passing circle entity information to openscad and
    openscad draw it.
    -   Having trouble with compilation.

### July 4th

-   Added arc, line, points, lwpolyline.
    -   Still have some problems with lwpolyline.

### July 5th

-   fix lwpolyline.
-   Added ellipse.
-   Found problem with mesh.

### July 8th

-   Trying to fix mesh

### July 9th

-   Change the structure of the entire code to use the code of dxfdata
    to fix the mesh problem
-   The code still not able to produce the correct polygon yet.

### July 10th

-   Fix the mesh problem and now the code can properly import a single
    dxf file.
    -   For some reason, the data is store and fill in the next polygon
        if the second dxf is imported.

### July 11th

-   Fix the data leakage between document.
-   Now the code is passing all the test file except nothing decimal
    comma and transform insert.
    -   the reader has an issue with insert entity

### July 12th

-   Trying to figure out how to fix the insert.
-   Learning the insert spec from dxf manual

### July 14th

-   Fix the block list and curr_block is not storing value properly
-   There is an infinite loop caused by the file offset in the
    process_enitites_unknown
    -   It jumps to the previous line but does not jump back
-   Continue on fixing insert

### July 15th

-   Clean up most of the commented code in dxf.cc and dxf.h
-   fix the curr_block memory issue by using a global variable indx
    that indicate the position of the block in block_list
-   Continue on fixing insert

### July 16th

-   Adding back_file_offset to state_data to have the program jump
    back
    -   Still getting the wrong result, the geometries are scattered but
        shapes are the same.
-   Continue on fixing insert

### July 17th

-   replace all memory allocation function related to insert with new
    and delete
    -   valgrind now output no error or warning
-   Continue on fixing insert

### July 18th

-   Download and build brlcad to test out what's the difference and if
    it can output the correct result
    -   There is no problem with the curr_state-&gt;file_offset
-   Continue on fixing insert

### July 19th

-   Found that the brlcad xform is different than my version.
    -   Can't figure out why it's different
-   Continue on fixing insert

### July 20th

-   Found the BU_LIST_POP actually assign curr_state to the last
    element of the list
    -   This fix the infinity loop and remove back_file_offset.
-   Continue on fixing insert

### July 21st

-   By switching the push_back and new_state = curr_state this fix
    the xform problem.
    -   Insert is fixed but it looks there is an issue with different
        compiler

### July 22nd

-   Cleaning up dxf.cc, import-dxf.cc, dxf.h.

### July 23rd

-   Finished cleaning up dxf.cc, import-dxf.cc, dxf.h.
-   Make [\#pr3005](https://github.com/openscad/openscad/pull/3005) to
    test in various platform.

### July 24th

-   Fix scale, xyorigin, layername problem.
-   Test result [3](https://github.com/openscad/openscad/pull/3006)

### July 25th

-   Starting working on spline entity.
-   Reading spline related code on QCAD.
-   Learning dxf spline entity spec.

### July 26th

-   QCAD is using an external library opennurbs to deal with the spline.
-   Reading spline related code on BRL-CAD.
    -   BRL-CAD code can be implemented on openscad.

### July 29th

-   Replicate and integrate brlcad spline code to openscad.

### July 30th

-   Continue integrating blrcad spline code to openscad.

### July 31st

-   Testing brlcad code with openscad, comparing with brlcad and qcad.
    -   Creating test cases using AutoCAD.
    -   Both brlcad and qcad seems to not supporting the spline created
        by autocad properly due to dxf version problem.
    -   brlcad encounter segmentation fault with one of the spline test
        cases.

## August

### August 1st

-   Switch to reading LibreCAD spline related code.
    -   LibreCAD 2.x version is using their own code.
-   Also reading openscad bezier curve related code.

### August 2nd

-   LibreCAD can handle the spline created by autocad unlike brlcad and
    qcad.
-   OpenSCAD code can handle degree 2, 3 normal spline(Beizer curve)
    properly.
    -   Starting adding openscad code to import_dxf.

### August 3rd

-   Modified openscad code and integrated it to import_dxf.

### August 4th

-   Testing the spline import of openscad
    -   Able to import 3 control points for degree 2 spline and 4 for
        degree 3 spline.
    -   Fail to generate continuous bezier curve.

### August 5th

-   Trying to figure an algorithm or a way to generate continuous bezier
    curve like this
    [article](https://www.algosome.com/articles/continuous-bezier-curve-line.html).

### August 6th

-   OpenSCAD is now able to import degree 1-3 spline with certain
    numbers of control points.
    -   spline knots, weights, fit points are ignored.

### August 7th - 14th

-   Family trip.
-   Originally from 7th-12th, due to the riots in Hong Kong airport and
    the typhoon in Osaka, flight got cancelled and delayed. \*\* Due to
    the typhoon, updated flight time is 16th.

### August 15th

-   Starting working on polyline entity.

### August 16th

-   Rearrange code and fix error in storing polyline vertex in the
    importer.
-   On the flight home

### August 17th

-   Integrate 2D polyline entity to openscad ignoring 3D polyline
    features and curve-fit.

### August 18th

-   Improve polyline with the spline-fit flag, can generate by both
    spline vertex and control points.
-   Test polyline.
-   Add test cases to the test suite.