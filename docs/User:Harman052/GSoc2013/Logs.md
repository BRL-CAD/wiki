Proposal Link: <http://brlcad.org/wiki/User:Harman052>

# Daily Progress

### June 17 2013

I go through the project flow, checked milestones and time period to do
specific tasks. I mentioned various JavaScript libraries in the proposal
so was trying to sort out which I should start with. I compared them
with each other but later on with some Internet searches, it was found
that webGL is not fully supported on all devices and browsers. I already
compared webGL and HTML5 during proposal submission but now it is
confirmed that I will go with HTML5 canvas for this project. Also
learned about its various capabilities and features.

### June 18 2013

Tried tutorials of HTML5 to build base for the project implementation.

### June 19 2013

I decided to submit a patch and selected a feature request of directing
the mged output to journal file. Currently, only user inputs can be
written in it. I tried by searching for files that I need to edit but
failed. I was searching for bu_log_add_hook() that doesn't pointed me
to files that I could start with. Later I got useful and detailed hints
from IRC to look into src/mged. I will look into it.

Also discussed about project scope with Sean.

### June 20 2013

Conclusion of discussion was that many aspects of project are still
unclear to developers. Although it was very painful to know that
developers have doubts about my proposal but anyway I started with
visualization. Different steps can be visualized as 2D HTML5 entities.
The results of intersection can be visualized as not displaying the
non-overlapping part as soon as user clicks on 'Intersect' button using
javascript's "onclick" event handler. But mathematical visualization
will not there.

### June 21 2013

Searched for solutions for unclear aspects of project. Searched about
wireframes, why wireframes are used? It is just because they are fast to
calculate but didn't find any anything useful specific to BRL-CAD for
reply.

### June 22 2013

I searched and collected lot of information that can be very useful for
BRL-CAD. I am compiling it now, and as it completed, will share with
developers.

### June 23 2013

Found more useful information. Will share on mailing list, once
summarized. Took break.

### June 24 2013

Worked on patch. Studied the f_journal function, its various
components. Some doubts are still not cleared. Will try to finish by
tomorrow.

### June 25 2013

-   Prepared a detailed email and sent to mailing list about what I
    found for Sean's questions. Expecting new directions.
-   Designed basic layout of interface.

### June 26 2013

-   As told by mentor, I studied WebGL and tried WebGL demos. I would
    use mixture of HTML5 and WebGL.

### June 27 2013

-   As suggested by Charlie Stirk, I reviewed <http://shapesmith.net/>.
    I tried it by downloading and installing locally. 3D objects can be
    easily created and edited. Moreover, it can produce josm files than
    can be easily parsed and used to make script of MGED commands. It
    will be wonderful if we use its interface.
-   Got reply from Sean, suggesting to shift from making geometry editor
    to geometry viewer.

### June 28 2013

I was suggested to focus on making online geometry viewer. I just posted
on dev-mailing list whatever I did in this context.

### June 29 2013

-   Used facetize command to convert implicit primitives into bot
    format. However it failed to run on brep objects.
-   Searched for web technology that could support NURBS geometry
    directly.
-   Posted details about today's progress on mailing list.

### June 30 2013

-   Explored source files to fix the facetize command. I found code for
    facetize command in two files, one in src/libged/facetize.c and
    other in src/libged/wdb_obj.c. Currently facetize.c is working.

### July 01 2013

Wasn't able to do much work due to some un-expected urgent work.

### July 02 2013

Looking into wdb_obj.c as it controls BRL-CAD database, it may be
helpful in reading file from browser.

### July 03 2013

-   Completed the task of summarizing the things discussed on mailing
    list into an wiki article.
-   Working on layout.

### July 04 2013

Explored src/libged/facetize.c and src/libged/wdb_obj.c files. From man
page, found "t" option of facetize command and for corresponding to this
option, found nmg_use_tnurbs flag in src/libged/facetize.c and
src/libged/wdb_obj.c files. But I didn't found any relevant code that
can be hooked to make the command working in desired way.

### July 05 2013

-   Trying to figure out solution. Ask for solution on IRC.

### July 06 2013

-   Post problem on mailing list.
-   In the mean time, I worked on patch. Tried to add "-r" option (for
    response) under f_journal function in history file. Now just need
    to figure out where to add hook in this file.

### July 07 2013

-   Waiting for reply.
-   Found function history_journalize that actually writes data in
    journal file and where the log hook is required to be added. With
    the help of grep, I found details about bu_log_add_hook() in
    bu.h. Need to figure out how to implement.

### July 08 2013

Was looking at similar implementation of bu_log_add_hook() in
src/libged/log.c and util/pl-dm.c to figure out to redirect data to
file. Both these files have same bu_hook_t function. I tried to
implement in similar way, but it didn't worked.

### July 09 2013

-   Looked at the source of
    <http://www.ibiblio.org/e-notes/Splines/models/parrot.html> since it
    is much similar to our requirement. They are using CanvasMatrix.js
    library (http://www.ibiblio.org/e-notes/webgl/CanvasMatrix.src.js)
    for matrix calculations as webGL does not have this support.
    However, CanvasMatrix.js is provided by Apple Inc. and its terms of
    use seems favorable to me but some expert person must check.
-   Model is taking input just like an ordinary webGL application i.e.
    in the form of vertices and faces, so we can easily provide that
    with OBJ file.

### July 10 2013

-   I read about WebGLU. Even they didn't specify the support for
    visualizing trimmed NURBS.
-   However they have partial .obj parser implemented to load objects.
    But they said, they support object hierarchies. If I got it
    correctly then it mean we can show sub components of regions and
    combinations.
-   Found 'glMatrix', another Javascript Matrix and Vector library.

### July 11 2013

-   Found a performance benchmark for different matrix libraries:
    <http://stepheneb.github.io/webgl-matrix-benchmarks/matrix_benchmark.html>.
-   Still not clear which library is suitable.
-   Talked to Sean on IRC about the code that's to be hooked in
    facetize.c. Have to move quickly.

### July 12 2013

-   Did some experiments with B-rep objects. My motive was to see how
    B-rep objects are represented in database file. First I made an
    implicit object and convert .g file to .asc then from .asc back to
    .g and it was successful. Then in new database file, made another
    object and made its brep object and converted file to .asc. In asc
    file I got message, "a Tcl output routine for this type of object
    has not yet been implemented" which means brep object was not
    described in .asc file. When this file converted back to g, all
    entities (one Implicit and one brep) were lost.
-   Not much work done.

### July 13 2013

-   Reviewed glMatrix and WebGLU matrix library to see if they can
    satisfy our requirements.

### July 14 2013

-   Asked questions on webGL IRC about various matrix libraries.
-   Prepared summary as told my Sean of his last email.
-   After seeing reply, many things got cleared which I took other way
    earlier.

### July 15 2013

Understanding the basics of various geometry representation forms to
know more how they are used in graphics.

### July 16 2013

Learned concepts behind Bezier curve and other basic things like control
points, degree, basis function.

### July 17 2013

Explored about NURBS and maths part behind its working. How control
points and their weights played their part in making curve, purpose of
knot vector. However, it need sufficient time to grasp all that
completely. But now I have basic understanding to NURBS geometry.

### July 18 2013

-   Tried a basic NURBS specific example in OpenGL to see what basic
    functions are required to be ported to JavaSctipt(WebGLU).
-   Tried example in SWIG to convert C code int Python but later came to
    know it does not support JavaScript. :-(
-   Looking into GLU's source code and looking for some other converter.

### July 19 2013

-   Found Emscripten: <https://github.com/kripken/emscripten>. From its
    description and demos, it looks promising and suitable for my work.
-   Working on it.

### July 20 2013

-   Received mail from my mentor on mailing list having instructions
    about how to proceed further in project. So finally I will visualize
    polygonal OBJ files on browser, no need to use Emscripten.
-   Started reading about how to read data from g file.

### July 21 2013

Took break.

### July 22 2013

-   Successfully retrieve name of database file, title, version, units
    from g file using pointer to db_i struct.
-   Working out to retrieve names of entities from g file.

### July 23 2013

-   Made wire frame of layout.
-   Prepared flow and implementation summary of project.
-   Nothing found. Still working on same task of retrieving names of
    objects.

### July 24 2013

-   Making a small prototype of web models. Searched the Internet and
    found good examples of displaying OBJ files using ThreeJS.
-   Basic scene is setup but getting problem with loading OBJ file.
-   Tried to get solutions from IRC and Stack OverFlow, but not
    succeeded.

### July 25 2013

-   Made prototype of how BRL-CAD models will be interactively displayed
    on browser.
-   <http://devplace.in/~harman/geometry_viewer/cylinder.html>
-   <http://devplace.in/~harman/geometry_viewer/mug.html>

### July 26 2013

-   After little struggle, applied materials to models.
-   But models are not rendering on Sean's browser in the same way as on
    mine. He is getting problem in viewing models after I assigned
    materials. Following are screenshots from my system:

<http://screencloud.net/v/4lpO>

<http://screencloud.net/v/2sOA>

### July 27 2013

-   I checked models on different browsers and systems. They are viewed
    differently on different machines but the browser version is same.
    Some are getting lines (tessellation lines) and some not.
-   In the mean time, I successfully retrieve names of objects from
    database file.

### July 28 2013

-   I started moving towards making web interface. I found a ready made
    editor in ThreeJS source code.
-   Reviewed the editor, used it to see what tasks similar to what I
    purposed in mock ups it can perform. It seems promising.
-   Send email to BRL-CAD dev mailing list, expressing my interest in
    using this editor as base for project.

### July 29 2013

No work done, due to some college related work.

### July 30 2013

-   Looked for different method of file uploading. I wanted to start
    with Drag n Drop support, but later I choose simpler method of
    browsing the files just to complete the overall flow. Made file
    upload feature. Drag n Drop support will be added at the time of
    actual interface implementation.
-   Made and share future plans and ask for suggestions on mailing list.

### July 31 2013

-   Started with adding file upload option. I was planning to make this
    feature as drag n drop, but later I decided to first go with simple
    solutions.
-   Added entity list display on browser.

### August 01 2013

-   Following mentor Rai's suggestions, added feature of generating OBJ
    files of first five entities as the file uploads.
-   Now I need to pass value from PHP to JavaScript so as to finally
    display OBJ file on browser. I suspect Ajax can be the solution.

### August 02 2013

-   I used PHP redirection to redirect to model display page.
-   Now as the file upload finishes, model displayed on browser
    (although only first entity at the moment). So, at least the flow
    has been completed.
-   Tested with all models that shipped with BRL-CAD source code. It
    worked perfectly with all files except those who have modeling
    errors. However, it look lot of time for files that have large
    number of entities (2000+) such as havoc.g but once OBJ files
    created model displayed successfully. I will recheck and discuss in
    detail on mailing list once I finished with setting up demo.

### August 03 2013

-   Added CSS to first page.
-   Adjusted camera position and added additional directional light to
    light up the scene.

### August 04 2013

-   Changed the code so that in case if file already exists, it will
    directly display the models rather than uploading the same file and
    making OBJ files again.
-   Removed unnecessary files and created repository on GitHub and
    pushed all the code.

### August 05 2013

-   Fixed problem of test.g file in the demo. Tested on different
    systems.
-   Took break.

### August 06 2013

-   Took break.

### August 07 2013

-   Went to college for documents related work. Some documents are still
    left. Need to visit tomorrow. Too tired. :-(

### August 08 2013

-   Submitted the documents to college. Work finished.
-   Looked into patch \#183. Tried to reduce code of those two functions
    into one. But I suspect about the functionality and purpose of those
    two functions. Looks like a wrong step taken. Need to concentrate on
    other patch.

### August 09 2013

-   Searched for various similar implementations in brlcad src to see
    how to use hooks for bu_log output. Found in mged/cmd.c,
    util/plot-dm.c
-   Studying how they are working.

### August 10 2013

-   With the help of example given in bu.h, I implemented error logging
    feature in journal command. It successfully logs output of bu_log
    to text file.
-   Testing changes. With option that I added, on running journal
    command in MGED in classic mode (using -c option) it displays
    nothing. On quitting MGED it quits successfully. Looking into the
    problem.

### August 11 2013

-   On testing, found other problems that are introduced due to my
    changes. Although most of them are small and serious problem is only
    when BRL-CAD crashes on running "ls -A" command after reopening
    journal file in same MGED instance.

### August 12 2013

-   Called in the college. There was misunderstanding in the documents.
    Fixed it.
-   I noticed that the problem of patch in classic mode is the same case
    when we redirect output / error to a text file using "&gt;" and
    "2&gt;". It redirects all output, and at that time nothing shows on
    screen.

### August 13 2013

-   Posted summary of efforts of this week to mentors.
-   Decided and planned what to do and how to do next in the project.
-   Took break.

### August 14 2013

-   As per my plan, I have to start with on-demand rendering option.
    Firstly, I sort out different aspects of this option on paper so
    that I could see the complete flow and what intermediate things I
    have to add to achieve this functionality.

### August 15 2013

-   Improved existing code as per HACKING file. However, need to inspect
    carefully before committing.
-   Started working on on-demand rendering option as it makes an
    important part of project.
-   Set layout according to mockups. Added divs.

### August 16 2013

-   Getting problem with onclick event handler. On clicking the link,
    function is not being called. Getting error that function not
    defined, but it is actually defined. Looking into it.

### August 17 2013

-   Still stuck at same problem.
-   Took short break.

### August 18 2013

-   Finally, "onclick" problem solved. It was a scope problem.
-   Added "View" and "Hide" links corresponding to each entity name.
    Working on implementing their corresponding backend functions.

### August 19 2013

-   Working on "on demand renderer". It has two parts: "On demand
    drawing" and "on demand deleting". Getting problem with entity
    display.

### August 20 2013

-   "On demand draw" part done. Actually, earlier I was taking it other
    way. But looking at some problem on Stack Overflow an idea came that
    I implemented and it worked. If I did what I planned earlier, no
    doubt it worked but it would consume more resources and might be
    less efficient.
-   Now working on "on demand delete" part.

### August 21 2013

-   Still stuck at "on demand delete" problem. As such it is very small
    problem but till now unable to find any solution. Explored over the
    Internet and found one solution but that's not much efficient. Now I
    asked on Stack Overflow. Here is the link:

<http://stackoverflow.com/questions/18357529/threejs-remove-object-from-scene>

### August 22 2013

-   No useful response on Stack Overflow.
-   Found one solution of my own but that's not much efficient. Actually
    in this solution, user can delete entities in reverse order as they
    are drawn. Before actually implementing it, looking for more
    efficient one.

### August 23 2013

-   Expanding that "inefficient" solution into useful one finally, "on
    demand delete" option done in a small standalone application. Now
    user can delete entities in random order. Next step is to implement
    it into actual application after testing. :)
-   Solved few small issues that I got while testing. However, needs
    more intensive testing. Will share on mailing list once implemented
    into actual application.

<!-- -->

-   Not feeling well.

### August 24 2013

-   Solved various small issues that came up during implementation of
    "on demand delete option" into application. Now need to use AJAX to
    call "createOBJ" function (PHP) at a "onclick" event of "view"
    button.
-   Fixed issues related to coding standards.
-   Again not feeling well.

### August 25 2013

-   Working on AJAX request problem. Looking into the documentation.
    After this has been done, work of demand rendering facility will be
    finished.

### August 26 2013

-   Took break.

### August 27 2013

-   On demand entity draw / hide facility implemented.
-   Now Next plans are to add sign-up / sign-in feature so that every
    user have his / her account and could access and manage uploaded
    files. Further I'll be adding attractive GUI for easy user
    experience. But before that, I would test whatever I did till now.
-   I was successfully able to draw Goliath.c of goliath.g but found few
    issues.

### August 28 2013

-   While testing with BRL-CAD's default .g files, I noticed various
    points that needed to be considered to give user a better
    experience. I'll share them on mailing list.
-   Now working on sign-up / sign-in feature.

### August 29 2013

-   Searched for sign-up modules on the Internet so that I could change
    / merge them into one that would be useful for this project.
-   Found many, but need to combine them and reduce unnecessary features
    and code.
-   Sign up feature is implemented, entry is being saved in database.
-   Working on email verification.

### August 30 2013

-   Email verification is done.
-   Created login page, landing page, and implemented sessions
    variables.
-   Sign-up module is ready. Need testing.

### August 31 2013

-   Now the user is able to create account, login and logout
    successfully.
-   Module tested successfully.

### September 01 2013

-   To make actual use of user accounts, I changed the code so that as
    soon as the user clicks on confirmation link (to activate account),
    the user directory (same as that of username filled while signing
    up) is created and a subdirectory "obj" (to store obj files) is also
    created.

### September 02 2013

-   Getting problem when user uploads a file. After upload, all entities
    of .g file erased. This was due to path problem. Actually the
    uploaded file was not being moved to desired directory and instead
    new empty .g file created in user directory having the same name as
    that of uploaded file. Anyway, this has been solved. Now the
    uploaded file is successfully saved in user's directory and with
    this sign-Up / sign-In work completed.
-   Testing.

### September 03 2013

-   Testing the application after integrating with signup module.
    Identified possibilities where improvements can be done; will be
    added to TODO list.
-   Added bootstrap CSS and custom CSS to improve look and feel.

### September 04 2013

-   Visited various sites similar to this application to get idea of
    perfect GUI. My main focus is to first work on the page where user
    see models and then change other pages accordingly as that page is
    main focus of this project. I think I need to add few more features
    to help user to view models in convenient way and since I noticed a
    lot of scope of this project so I need to discuss with developers
    about what to be added and what not within the GSoC period.

### September 05 2013

-   Took break.

### September 06 2013

-   Working on feature to enable the user to manage / access uploaded
    files, load old files from his dashboard.

### September 07 2013

-   Updated todo list on GitHub repository.
-   Just finished with two new features: Now as the entity added to
    scene, it gets a random color. Now models look more colorful. At
    this moment colors being assigned to entities are random, in future
    this will be brought under control of user.
-   <http://screencloud.net/v/d2zN>
-   <http://screencloud.net/v/va61>

<!-- -->

-   Secondly, now models are drawn horizontally. Earlier, models drawn
    tilted (one side raised), were difficult to examine so fixing this
    just improved usability.
-   <http://screencloud.net/v/yUpN>

### September 08 2013

-   Worked on patch to calculate and compare volumes of implicit objects
    and their brep versions.

### September 09 2013

-   Still working on patch (the shell script), testing, improving it.

### September 10 2013

-   Submitted patch.
-   Implemented grid in geometry viewer as suggested by Sean.

### September 11 2013

-   After reading Sean's reply, got many ideas about how the requested
    features can be implemented. Before actually start coding, I want to
    plan about how the options of such features will be provided to
    user. Like, if we implement wireframe feature, how user will use it,
    i.e. whether it should be like each entity should clickable to draw
    wireframe. Even if the entity is clickable, which button it should
    be clicked with, right or left. If it is right button, should it
    have some context menu with many other options?

<!-- -->

-   Other case may be to have single checkbox option which when clicked,
    all entities in the scene will get their wireframes.

<!-- -->

-   Also these wireframes can be drawn from left side panel (list of
    entities) when user hovers an entity.

<!-- -->

-   Similar possibilities are also there for transparency option. Need
    to discuss.

### September 12 2013

-   Assuming that we would have a combination as whole of what I devised
    yesterday I started working on making entities clickable to get
    wireframes.
-   Able to get wireframes on built-in geometry on a user click in a
    simple standalone application.

### September 13 2013

-   Wireframes implemented on OBJ objects but currently they are very
    inefficient. The major problem is that sometimes, user clicks at one
    place, and action is performed somewhere else. That's annoying.
-   Other problem is, in case if the object is a combination of simpler
    entities, wireframe cannot be drawn on the whole object with single
    click; one has to click each component entity to draw its wireframe.
-   Here is the example: <http://screencloud.net/v/ozjo>
-   Earlier lighting was not proper. One side of model always remained
    in dark. I attached light to movement of camera, so now models are
    more enlightened.
-   Added key bindings to see: top(T), bottom(B), left(L), right(R) of
    model; giving out more touch of BRL-CAD.

### September 14 2013

-   Took break.

### September 15 2013

-   Implemented wireframe option. Now black wireframe appear by default.
    On pressing "S", model will be shaded with random colour and on
    pressing "W" wireframe will appear again on whole model.
-   <http://screencloud.net/v/lSaK>
-   <http://screencloud.net/v/1wDg>
-   Earlier I reported a problem about slow performance of big / heavy
    models. Actually, this is not a problem of ThreeJS. Earlier on my
    Chrome browser canvas renderer was enabled that was not fully able
    to handle such models. I enabled webGL in settings and tried that
    heavy model (Goliath.g) once again, and now it is working perfectly
    just like tiny models.

### September 16 2013

-   Urgent work out of station.

### September 17 2013

-   Urgent work out of station.

### September 18 2013

-   Urgent work out of station.

### September 19 2013

-   Improved GUI of model_display.php.

### September 20 2013

-   Improved CSS of sign-in / sign-up pages and landing page.