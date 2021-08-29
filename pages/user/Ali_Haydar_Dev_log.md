# Community Bonding Period

1.  Setting up the environment installing ubuntu in dual boot and
    rebuilding the project in windows and ubuntu
2.  Working on bugs:- the annotation is pointing to the origin fixed and
    patch submitted the drawing of numerical annotation results in no
    annotation working on it and notice that after constructing the
    numerical annotation you can't draw anything in the graphical screen
    until writing the Z command in MGED or reopening the database.
3.  Using the code to modify the Vlist to draw a box around the label it
    is like a hack, not a real function just an experiment, it makes me
    realize that the label drawing should not start from the reference
    point but a little bit further so the box doesn't touch the label.
4.  Contacting with the mentors and asking about there opinions.

#### This page is will be edited to include what I've learned so far and served as a log for the coming development.

# Coding period

-   May 27 start reading the annotation code and trying to understand
    the problem in the opengl depiction in Wgl and ogl display managers
-   May 28-29 failing to have any result with OpenGL and keep trying the
    logic exists in dm-X display manager but I am failing to copy it
    with OpenGL functions. the program is using OpenGL in immediate
    mode.
-   May 30 learning how to manipulate vector lists
-   May 31 the annotation vlist is complete when it exists in
    drawVlist() function in dm-wgl.c starting from the third point we
    can obtain the coordinates to the label vlist and use them to
    construct the box around the label
-   June 1 learning opengl immediate mode the projection wanted by the
    society is like the one produced by Glortho() but it is not giving
    the wanted results
-   June 2 working on the short annotation bug when you have a short
    annotation like one number or one letter it is not drawn in the
    graphics window one fix suggested by a fellow programmer is
    commenting the line 79 in vlist.c but this fix isn't approved by the
    society.
-   June 3 write the function ant_label_box() which draw the box
    around the annotation it was good but we have to optain a pointer to
    the segments inside the annotations and decide which segments have a
    box around it and which is not
-   June 4 one day off didn't do anything just read some code.
-   June 5 reading how the properties of line seg and text segment are
    entered and read by the annot_in function
-   June 6-9 structural dynamics exam didn't do much. and didn't pass
    the exam :(
-   June 10 I am working on the short annotations bug starting in
    bn_vlist_bbox() we will see what happen today and update.

June 10 the solutions I proposed is not accepted because it is changing
the calculations of the bounding box for lines and triangles

-   June 11 trying another approach in solving short annotation problem
    which is another way of calling bn_vlist_bbox() in bound_solid()
    may be changing the matrix flag in cmd\[0\]=15 to cmd\[0\]=12 so the
    annotation is treated as one point which is the point that is in
    model coordinates not in display coordinates.
-   June 12 submitted a patch to solve the short annotation problem but
    it didn't solve the long annotation problem because of the long
    annotation vlist hase multiple chunks.

June 12 trying to add a third segment to the annotation static one
defined inside annot_in() with its parameters to see if it will be
converted correctly to vlist.

-   June 13 the patch was good and I submitted another one to solve the
    problem of bbox() in long annotations when the annotation vlist is
    constructed from more than one chunk the display mode is not
    memorized thought the iterations
-   June 14 I managed to draw a circle segment between the annotated
    point and the reference point replacing the text segment by a carc
    segment I am working on the entring logic for three segments of the
    annotation.

June 14 now the annotation contains three segments a leader line, text,
and static arc segment I defined it inside the annot_in() function. the
annotation is imported correctly and all the segments are converted
correctly to vlist.

![](../img/15.png)

-   June 15 working on the problem of the bounding box, the solution is
    to change the bbox() function
-   June 15 prompt the user if he wants a carc segment in his annotation
    it seems like the annotation construction will be so hard on the
    user

![](../img/Pasted_image_(1).png)

-   June 16 send the patch of the new bbox() function it needs some
    modifications
-   June 16 the society suggested making an annotation editor using the
    existing code of sketch editor so I am learning tcl/tk
-   June 17 added the annot choice in creat menu and found where to
    assign the callbacks for classes in tcl/tk script which is done
    using auto_mkindex command and creats a script called tclindex.tcl
-   June 18 after copying the sketch_editor class in skt_ed.tcl and
    make annot_editor class the menu button still not recognizing the
    annotation, maybe this is happening because the mged_make()
    function doesn't now about the annotation so know we will make them
    meet each other :).
-   June 19 made some changes on the new bbox() function, the annotation
    editor is working now but failing to save the annotation,
-   June 20 the error in saving the annotation was in the function which
    writes the annotation to the database
-   June 21 the new bbox() function is accepted solving all the
    problems, now I am working on modifying the Gui of the annotation
    editor
-   June 22 facing a problem with drawing a line to the same point from
    the annotation editor and from the in command
-   June 23 made the user able to enter the annotated point and store it
    in V which will be the origin of coordinates to draw the hall
    annotation
-   June 24 the annotation editor stores the chosen vertex twice I don't
    know why. still working on the Gui to make the user able to enter
    the label of the annotation and the text placement coordinates work
    going very slow the placement of the widgets in the window is making
    me crazy.

![](../img/Pasted_image_(2).png)

-   June 25 now its the time to make a method to create the txt segment
    in tcl script but whenever I add a new method to the script the
    whole editor goes down.
-   June 26 submitted the patch for the bbox() it is correct but
    contains a lot of mistakes in the indents and white spaces, I am
    working on making a unit test for the code I wrote.
-   June 27 reading the unit tests in bn library it appears there is a
    file called bn_test.c which calls the test functions and it exists
    in the configured project I.e the build file you generate using
    Cmake , I have added the test file that I will write in, to the list
    of bn_test_srcs in cmakelist in test file of libbn .
-   June 28 still working on the unit test program the main function is
    automatically generated based on the test file name, I have added
    the tests also to the cmakelist file the program will test the
    bn_vlist_cmd_cnt() function in vlist.c which returns the number
    of commands in a vlist so we have to invent a list and send it to
    the function to see if it works properly.
-   June 29 the vlist is a doubly liked list so we have to obtain a head
    for the list and start adding elements I am thinking to put a for
    loop which adds points to the vlist depending on the test command in
    cmakelist file I will use RT_ADD_VLIST macro on the created head
    to add points to the list. also worked a little on the annotation
    editor but still not good the new methods I add breaks the hall
    script I don't know why. at the end of the day the test file works
    and the main function is called correctly from bn_test program.
-   June 30 I have a problem building the test program because of using
    RT_ADD_VLIST the error is unresolved external RTG which is from
    the type rt_g defined in global.h, maybe it is a link error to
    librt, because I noticed that the RT_ADD_VLIST macro works in
    files which is existed inside librt maybe I am wrong ,
-   July 1 the same link error still keeping me from going ahead I tried
    to define rt_g RTG; object inside the test file and the build is
    okay but when executing the macro the program get BU_ASSERT error I
    don't know why I asked the mentors to learn me how to link to librt
    and i tried a solution by making a function inside annot.c to add
    the points to the vlist now my new function is the unresolved
    external object.
-   July 2 the same link error we linked librt to the test file the
    function works but when you use RT_ADD_VLIST inside it you get the
    BU_ASSERT error and when using RT_ADD_VLIST inside the test
    program you get the unresolved external error when building the
    code.
-   July 3 found the solution by adding two lines to the test program
    which is 1- rt_g RTG; 2- BU_LIST_INIT(&RTG.rtg_vlfree); this
    solution is you need a free list to use the vlist which I learned in
    a hard way wasting 3 days searching online how to link a library to
    your code in cmake system.
-   July 4 rewrite the test file and adding all the expected cases of
    the function like Null pointer to no list and very long list. I have
    sent the file to the society to get opinions about the whole
    operation I think I finished it. Now looking to the bugs in the
    annotation we can notice that the annotation label is presented in
    the top-right position no matter what the position flag is I am
    working on this now and asked for the mentors to revise the goals of
    the project because the annotation editor is written in tcl/tk which
    will not be used in the new GUI this will make me do a lot of things
    that will not be useful. also, I have an exam on the 9th of June.
-   July 5 I couldn't do anything due to some problems in my sleeping
    schedule.
-   July 6 I found a bug in the annotation behavior which is the
    position of the label doesn't change whatever the user chose from
    the position flags I am working on this and I have sent a suggestion
    for a partial solution.
-   July 7 managed to make the case of the bottom right

![](../img/Pasted_image_(3).png)

-   July 8 I am preparing for structural dynamics exam tomorrow didn't
    do much I know I have to calculate the length of the label in the
    annotation.
-   July 9 I had an exam. didn't do much
-   July 10 I made some changes on the test program bn_test.c.
-   July 11 I found a way to calculate the dimensions of the label in
    the annotation by calling the function which converts the string to
    a vlist bn_vlist_2string() considering that the reference point is
    the text placement point.
-   July 12 working on the positions, the mentor's opinion is that the
    position flag should be related to a point of the text not related
    to the leader line but I think in this case it happens to be the
    endpoint of the leader line is the same point of the text placement
-   July 13 still working on the positions flage the function
    rt_pos_flag() always returns the value top-right I fixed it and
    now I think it is manageable to construct all cases
-   July 14 I managed to construct all the cases of the positions flage

![](../img/Pasted_image4.png)

-   July 15 still the discussion of position flag and I am working on
    making a new annotation type which is dimension line I am thinking
    of using the same primitive and prompt the user for the tow points
    of which the dimension line will exist. I fell very sick and I am
    planning to go to the hospital
-   July 16 I made the dimension line and send it to the mentors to see
    what they think

![](../img/DL.png)

July 16 the mentor's said this approach will not work because the line
had to be in model space and its label in display space I don't know how
to solve this issue, I think the line should have its own vlist and the
label also and each one should have different projection matrix

-   July 17 I was in the hospital and had minor surgery. the doctor told
    me you can set on the chair after tow days ): .
-   July 18-19 I didn't do any thing.
-   July 20 I am back to work I will fix the patches and try another
    approach for the dimenison line .
-   July 21 I managed to keep the label of the dimension line in the
    display space and the lines in model space but the result is not
    good yet
-   July 22 the solution for the dimension line is not accepted, now I
    will try to modify the annotation primitive and add more refrance
    points to the text segment and see what will result, before that I
    will try another approach

July 22 now it works the label of the dimension line is in display space
and the lines are in the model space, waiting for the society opinion.

-   July 23 now I will work on the text of dimension line, size,
    rotation angle, and placement flags.
-   July 24 still working on the dimension line I have modified the
    txt_seg but the new attributes (txt size, rotation angle) are not
    passed to the database I think I have to modify the export and
    import functions and the function which describe the annotation.
-   July 25 still struggling with exporting the txt_seg after adding
    the text size and rotation angle.

July 25 I fixed the error in importing and exporting the annotation but
still, there is an error in the label

![](../img/DL1.png)

-   July 26 working on the dimension line

July 26 as the current dimension line is not bad it could be used to
make a dimension line for a 3d object by changing the verts to 3d points
(fastf_t \*pointp_t) and this is not a problem for the vlist because
it is already can hold a 4d point I will see what the mentors say about
that

-   July 27 the dimension line in its current state is not accepted I
    will fix the position flag patch and the test program and get back
    to the dimension line.
-   July 28 took one day off.
-   July 29 I am working on the position flage patch and extending the
    text segment structure .
-   July 30 submitted a patch for fixing the position of the annotation
    based on the position flags and a patch to extend the text segment
    structure in the annotation to have a text size and text rotation
    angle parameters

![](../img/PF.png)

-   July 31 trying a new approach for the dimension line by adding a 3d
    verts to the annotation primitive which will be existed along with
    the 2d verts and will be used if the point index is negative. and
    trying to reproduce a bug in the l command when used with the
    annotation.
-   August 1 after extending the text segment the old annotations
    doesn't work anymore I am trying to make it compatible
-   August 2 there was some mistakes in the annotation's position flag
    patch I fixed them and I am working on a bug in the extended text
    segment structure and another one in the L command
-   August 3 fixed some previous errors in my code and still trying to
    find the problem in L command the problem is it works some times and
    some times don't even with short and long labels.
-   August 4 still unable to find a solution for importing the old
    annotation that doesn't contain a text_size and text_rotation
    angle in its structure because I didn't find a way to distinguish
    between the old one and the new one. also no result for the l
    command bug
-   August 5 I found a way to import the old annotation properly by
    reorganizing the order of pointers but as we know the old annotation
    doesn't contain the new parameter so they will be random values from
    the database, as I am playing by the import function the l command
    bug some times appear when I change somthing related to the label so
    the solution for both problems will be probably in the import
    function
-   August 6 there is some progress in the l command bug it is due to
    the exporting of label.vls_str structure the vls_len and vls_max
    has incorrect values but still doesn't know how to fix it
-   August 7 still stuck in the same problems, my findings are we are
    exporting the bu_vls structure which is the annotation label as a
    structure I don't know why the importing function assumes that it
    will import the string separated from vls_offset,vls_len,vls_max
-   August 8 I think this will be a solution for both problems the
    compatibility issue and the l command bug because the text segment
    is exported correctly but the import operation is not correct in my
    opinion I am still searching for a solution.
-   August 9 I found a solution which is importing the bu_vls as a
    whole by using bu_vls_strcpy() function and counting for the null
    terminator in the increment of the external buffer pointer this
    solves the l command bug.
-   August 10 I am working on extending the annotation structure to
    include 3d verts and waiting to see the society opinion of the l
    command fix.
-   August 11 by extending the text segment and using the solution of
    exporting the bu_vls as a whole it is compatible with the old
    version of the annotation.
-   August 12 the L command fix is correct and it needs more work on the
    size allocated in the exporting function and adjusting the import4
    and export4 functions working on that. also, the position adjustment
    of the annotation is good.
-   August 13 I am back to the dimension line and 3d verts I will see
    what I will get today.
-   August 14 I fixed some errors in previous patches and working on
    adding the 3d verts I have a problem with importing them the Z
    coordinate is always zero.
-   August 15 I fixed importing the 3d points and send a patch to see if
    we can use it in dimension lines.
-   August 16 now I am trying to use the 3d verts in the dimension line.
    I have a problem with the functions that use verts like
    seg_to_vlist it uses the verts array if I want to use verts3d
    array that I have added to the annotation primitive I may have to
    write a new function.
-   August 17 studying about 2d paper space used in cad programs.
-   August 18 fixing previous patches L command bug and annotation
    position adjustment.
-   August 19 working on the new dimension line approach with 3d verts
    the problem is if we want to use a negative index for the dimension
    line verts it is not logical because this index will be used in an
    array and negative indexing is a miss and undefined behavior in c so
    it needs a lot of work.
-   August 20 working on the open tickets and documentations.
-   August 21 I am making a new function seg_to_vlist to call in case
    of the dimension line to deal with 3d verts array that I have added
    to the annotation primitive.
-   August 22 still finalizing the open problems and working on the
    final report.
-   August 23 I reviewed the committed code and found a bug in drawing
    the annotation I have reported the bug and submitted a solution
-   August 24 working on the report.
-   August 25 made a new approach for drawing a box around the label.
    and some documentations.
-   August 26 Submitted the final evaluation.

GSOC 2019 is over it was a magnificent experience I have learned a lot
of new things and developed my coding experience. I am planning to
continue my contribution to open source and BRL-CAD. thanks to google
and my mentors for this opportunity.
