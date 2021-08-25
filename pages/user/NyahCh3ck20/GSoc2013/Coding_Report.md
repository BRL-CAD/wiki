#### Coding Log Report for GSoc 2013

Daily log:

### PROJECT SUMMARY

This year's GSoC was my first and most exciting projects given the fact
that I'm working on my first opensource project and contributing for my
first time to a great software and organization like BRL-CAD.

For the past three months I worked on implementing a pull routine
which reversed the effects of a push on a CSG tree. This project
focused on reversing the effects of the push command available in
BRL-CAD and also pulling up and unpushed node. While following my
implementation outline as described in my [Design
Document](Design_Document.md), I kept modifying the plan as needed and
tried updating my [logs](Coding_Report.md) daily especially when I
initially had no stable Internet access.

Before the Mid-term Evaluations, I studied the push and xpush routines
seeing how the matrices were pushed down the tree in respective commands
and started implementing and finished implementing the pull_comb()
routine which pulls the matrix transformations in a combination node.
Submitted patches on sourceforge for review. I tested various parts of
the routine and made sure routine works perfectly will continue testing
and fixing bugs if any post GSoC to make sure command is complete. Also,
I wrote tests for the poly.c routines and submitted patches on
sourceforge; tested the bn_mat_inverse() routine implemented for
BRL-CAD and proposed new routine which are still awaiting review by
mentors.

Post Mid-term evaluations, I studied the various primitives trying to
figure out how to implement the pull_leaf() routine for each primitive
which was later disproved by Sean as a bad design choice which led to my
implementing of the pull_leaf() using the AABB's of primitives which
enabled me to pull translation components successfully. I also developed
the pull interface, wrote regression tests, created the man pages and
other documentation which will integrate command fully into BRL-CAD.

During Final Days and Post-GSoC I plan to finish implementing the
pull_leaf routine which pulls both the scale and rotation components of
primitives for BRL-CAD completing the pull routine and any other new
projects as needed.

This was one of the most exciting summers of my life.

Cheers! Nyah

### Test Results

-   Pulling unpushed object pulls matrix transformations up the tree.

[pull_unpushed_obj](http://brlcad.org/wiki/File:Pushed_pulled_object.png)

-   Pushing object after pull restores original matrix conditions.

[push_pulled_obj](http://brlcad.org/wiki/File:Pushed_pulled_object.png)

## 17 June - 23 June

Coding Begins for GsoC working on codepatch to be uploaded to brlcad
uploaded the sourcefile for new push routine which supports the -x
option for xpush but still needs further testing and modifications.

18 june 2013 Added a new functionality to new push routine where the
push would recognise the the xpush case even in a case where the -x
option is ommitted or ignored.

Tested the new routine and extracted patch to be uploaded to sourceforge
replacing the previous push file I uploaded.

To discuss with mentors whether there is an implementation of the
Inverse of a 4x4 matrix in the brlcad source code.

Looking at the implementations of the Inverse of the matrix in BRL-CAD

## 24 June - 30 June

-   Monday June 24

Looked at the definitions for the inverse of a 4x4 matrix as defined in
/src/libbn/mat.c. However, i realised orthogonal matrices were not taken
into consideration. So added functionality to determine inverse faster
for othogonal matrices and to upload patch to sourceforge shortly.

Started creating structures for the pull routine that is ( pull_obj and
p_solid) structures to hold objects to be pushed and solids currently
being pushed on a CSG tree. Code to be added to sourceforge Shortly.

re-read the HACKING file to make sure i conformed with the coding
standards for BRL-CAD.

-   Tuesday June 25

Further tested the bn_mat_inverse routine(src/libbn/mat.c) and
modified patch that was to be uploaded yesterday but failed due to poor
network connection.

Looked at the libbn library especially mat.c which would be useful for
implementing the pull.

Studied the vmath.h header and discovered the transform.c file which
could be applied in creating the pull routine.

Uploaded the pull.c first patch and bn_mat_inverse patches due to
failure in network for them to be uploaded yesterday. [Inverse Matrix
support for orthogonal
matrices](https://sourceforge.net/p/brlcad/patches/202/)

Will need some clarification from mentors concerning my design strategy
for the pull routine.( The necessary functions i would need to create or
call from the source) in order to implement a complete pull
routine.(Asked on mailing list.) still to continue work on push and
xpush merger.

Saw the importance of magic numbers in taking note of visited nodes
along the CSG tree. Also, thought of checking the matrix transformations
for each node to determine if node has been visited but since magic IDs
were used in the push then i could use both in pull when performing the
inorder walk from the leaf(solid) nodes.

Moreover, for objects in database, dp-&gt;d_uses was used but not safe
as defined push.

-   Wednesday July 26

Earlier part of the day used for preparation for and wrote an
Information System test before working.

Added the new pull routine to the setup.c(/src/mged/setup.c) interface
and included the new command into the CMakeLists.txt
file(/src/libged/CMakeLists.txt) in the brlcad source

These patches also included the removal of the xpush command to support
the new push and xpush. Patches to be uploaded to sf.

Added new pull routine declaration(ged_pull(struct ged \*,int, char
\*\[\])) to the ged.h header so it can be accessed by other files.
patches to be uploaded to sf.

Added new pull to tclcad_obj.c file(/src/libtclcad/) although with
support of more than one arguments i'll first of all try to test with
only one argument then see how far it goes;this is so that it's
available in the internal database interface.

Added tentative ged_pull() function definition to the pull.c file to
enable it to be accessed by files calling function.

However since ged_pull() routine does not compile code can't compile
due to unused variables so will create some dummy operations just to see
how blank routine works and get it started.

Well just realised that the orthogonal matrix consideration in the
bn_mat_inverse routine in mat.c is causing the benchmark tests to
fail. Gotta sit on it and fix the bug. [Pull
Patch](https://sourceforge.net/p/brlcad/patches/206/)

-   Thursday 27 June

Travelled to Douala and spent the whole day trying to cash the prepaid
GSoC deposit. However, tried working on a bug in the mat.c
file(/src/libbn) where the inserted code patch for orthogonal matrix
support is giving wrong answers during the benchmark test. Discovered a
little error calling the bn_mat_mul2() routine and now code passes 3
benchmark tests and fails 3.Will perfect code and upload codepatch
tomorrow on sf.

-   Friday 28 June

Looking at the bn_mat_inv() routine and performing some tests to
ensure all benchmark tests succeed.

Checked the orthogonal matrix support and code still fails 3 regression
tests after testing and checking need some assistance for this. Started
a detail analysis and study of the push command from the ged_push()
routine. This is to enable me understand perfectly the implementation
hacks of the push in order to implement a push correctly especially when
it comes to dealing with the points and matrix transformations at the
node and leaf levels on the CSG tree.

To check all reviews from code patches so as to start working on them
tomorrow. [Modified push](https://sourceforge.net/p/brlcad/patches/190/)
[Modified
bn_mat_inv](https://sourceforge.net/p/brlcad/patches/202/)This patches
passes some regression tests; but i don't understand why it still
doesn't work perfect. Don't really see the problem here

## 1 July - 7 July

-   Monday 1 July

Well did not code because of Preparations to attend the Google Student's
Ambassador's Summit in Nairobi, Kenya for Africa. This summit goes on
for the whole week. But will try to fix problems with my code patches
while at the summit.

-   Tuesday 2 July 2013

Boarded Kenyan Airways flight from Douala Int'l to the Jomo Kenyatta
Int'l in Nairobi which took about 5 hours; then registered with the GSA
team.

-   Wednesday 3 July 2013

Attended the First day of Summit where we had talks with Google
Engineers about being a good ambassador. Presentations were given by Mr.
Obum Ekeke , Tayib Fall and others about opportunities at Google.

-   Thursday 4 July 2013

Second Day of Summit focused on Google products like Adwords, Adsense
and other products; also, Engr. Giacomo(Googler) gave a presentation on
Webmaster tools and Google Search in general.

-   Friday 5 July 2013

Third day of Summit where we focused on making greater impacts on our
communities in Africa; with awards given to Star GSAs of the previous
years. Shared ideas and experiences for the Moonshot idea competition
organised as per country we emerged 3rd after South Africa and Kenya.
Developed plans to execute our moonshot idea as we returned home after
the summit

-   Saturday 6 July

Preparing for return trip to Douala Int'l and went round Nairobi for
shopping and other stuffs.

-   Sunday 7 July

Returned from Nairobi to Douala and after meeting family travelled to
Buea to prepare for coming week.

## 8 July - 14 July

-   8 July 2013

Wrote a report to be submitted to the Vice Chancellor concerning my
experiences on Google Student Ambassador's summit and preparing for a
Numerical Analysis Exam Took further look at source code(/src/push.c) to
see how the matrix transformations are applied to the coordinate points
of the node so as to determine a way of extracting the original matrix
transformation or almost exact matrix transformation for source code.

Glad the Dean of the faculty of Science authorized the installation of
Internet in the CS so we can have 24/7 Internet access

-   Tuesday 9 July

Wrote my Numerical Analysis exams and to finish with exams tomorrow so i
can focus on GSoC full time.

-   Wednesday 10 July

Finished writing exams today and started preparing previous code
patches(mat.c,push.c,pull.c) so that when the Internet access is
available all files will be uploaded so as to get commit access.

-   11 July 2013

studied the brlcad primtive internals like(torus, spheroids, toruses
(torii), spheres, ellipsoids, pyramids) so as to be able generate the
original transformation matrix. Torus, struct rt_tor_internal
Centerpoint, point_t v, is obviously the translation. The orientation
and scale is defined by vect_t h, and radiuses by fast_t r_h and
fast_t r_a. Because of symmetries, the original transformation matrix
must have contained a translation of v, and a rotation that brings
vect_t h to an axis

Spheres and ellipsoids, struct rt_ell_internal Centerpoint is at
point_t v, which again is obviously the translation done.There are
three vectors, point_t a, point_t b, and point_t c, that describe the
spheroid axes. This means that I can construct the transformation matrix
that transforms the unit sphere to this sphere directly.

for Truncated general cones, struct rt_tgc_internal Centerpoint is at
vect_t v, with vect_t h describing the axis. The base of the cone is,
I think, described by the vectors vect_t a and vect_t b, and the top
of the cone by vectors vect_t c and vect_t d. This implies that aÂ·b=0
and cÂ·d=0, but they may not be perpendicular to h, since the base and
top of a general cone may be cut along any direction. v is the
translation, and h should be along an axis (probably z axis). This
yields three vectors (h, f, g), that along with the translation vector v
define the transformation matrix just like in the ellipsoid case.

Also, looked at data type for Pyramids: struct rt_arb8_internal This
data type contains between four (tetrahedron) to eight vertices as
point_t variables. Pyramids and tetrahedra have the apex vertex
perpendicular and center to a face. This can be taken as the face
vector. The second vector is one that bisects an edge (the longest
edge?) of the face perpendicular to the apex. The third vector is their
cross product, and is either towards a vertex (a tetrahedron) or halves
another edge of the face perpendicular to the apex (a pyramid). These
three vectors can be used to regenerate the initial transformation
matrix, with e.g. the base on the XY plane, and the apex along the Z
axis.

To look at wedges, Boxes, and convex polyhedra tomorrow.

-   12 July 2013

Prepared complete patches and uploaded to sf to replace the existing
patches for new push routine(push.c), pull routines(pull.c) and
bn_mat_inverse routine(mat.c) with orthogonal matrix support. Since
there is no internet connection, I could not create these patches with
the current svn checkout.

Continued study of implementation of push.c so as to see what happens to
coordinate points of the node, to determine how some form of the
original matrix transformation is stored so as to ease restore during
the pull routine.

-   13 July 2013

Did no work because of a long meeting( in my capacity as Auditor of
Computer Engineering students Association) of over 5 hours with the Dean
of Faculty to draft modalities for new student union body and draft
constitution and mission to govern association.

Will start implementing the pull leaf function as from Monday which will
extract the matrix transformations from the primitives(solid) or leaf
nodes.

## 15 July - 21 July

Monday 15 July

-   Implemented the pull_leaf routine which build a linked list for
    object's tree which would be used in extracting matrix
    transformations in leaf_mat() routine I am to start working on
    tomorrow.
-   continued with the implementation of the ged_pull by adding -d
    option to command to enable a debug of command as in push -d

Todo: To ask on mailing list how to generate a Magic ID since its needed
for the pull.

Tuesday July 16 2013

-   Further worked on the pull_leaf routine to make sure list is
    properly built and created loop to free up list if errors occured
    during the list build like pulling unpushed nodes.

<!-- -->

-   Started working on a loop to move through the nodes of the linked
    list making the necessary mat_t changes while moving upwards
    modifying the current matrix transformation as it encounters a new
    leaf when necessary calculating and storing the inverse matrices up
    the tree till it reaches the root. This will then be followed by
    writing these changes to the database.

TODO: Ask on mailing list how my current working model solves the method
so as to make the necesary changes in approach and continue.

Wednesday July 17, 2013

-   Finished writing loop that moves backwards on the newly built list
    of nodes on the tree, performing inverses as necesary,storing the
    changes on the node, writing to database and setting the matrix
    transformations for primitives(leaves) to identity as necessary.

<!-- -->

-   Wrote loop that frees up built list and returns result of object
    pull.

<!-- -->

-   started testing of pull command and to continue fixing bugs. Till
    command is ok before adding support to pull more than one object.

<!-- -->

-   Performed another benchmark test for the orthogonal matrix support
    for bn_mat_inverse() in mat.c

<!-- -->

-   Uploaded code patches for mat.c and combined push and xpush to
    sourceforge.

Todo: fix all problems with with currrent and past patches and upload to
sf for mentor review.

Thursday July 18, 2013

-   Started working on compile time errors of the pull.c by fixing some
    pointer casts and others.

Friday July 19, 2013

-   Finished debugging compile errors and started testing routine.

<!-- -->

-   Tested for improper use of command(pull 'no object'), returned
    correct errors

<!-- -->

-   Tested for pulling a primitive.(returned correct error message).

<!-- -->

-   Tested for pulling an object which has not been previously
    pulled.(mged crashed due to segmentation fault) to start working on
    bug next week.

Will be taking tomorrow off since its my birthday and start working on
bugs and patches next week.

## 22 July - 28 July

Monday July 22, 2013

-   Added -x option to push.c to support new xpush command(recreated and
    tested new push command). Spent whole day debugging and still have
    not succeeded in removing bug causing the

loss of options to push command.

-   Created new patch for pull command and patch applies cleanly but
    command still further development and debugging.

Tuesday July 23, 2013

-   Installed Internet in the CS Lab so as to increase efficiency for
    BRL-CAD.

<!-- -->

-   Started downloading latest svn checkout for BRL-CAD source

<!-- -->

-   Set up account on bz.bzflag.bz server and Started downloading
    tutorials on how to use ssh and GNU Screen

<!-- -->

-   Upgrading my SL 6.2 distro so as to start further work on patches
    tomorrow.

Wednesday July 24, 2013

-   Enabling pull routine to be able to pull a non leaf node; that is
    routine is able to pull geometric transformations from any node up
    to the root.(as @Sean adviced me on mailing list.)

<!-- -->

-   Found bug in code which returns error when pulling non-leaf node.
    Started fixing

<!-- -->

-   Prepared patch to stub pull routine unto brlcad using svn
    diff(Uploaded to sf
    [Here](https://sourceforge.net/p/brlcad/patches/215/)

<!-- -->

-   Tests of pull routine
    shown[here](http://brlcad.org/wiki/File:Pulling_non_leaf_objects.png)

Thursday July 25, 2013

-   Tested new algorithm for bn_mat_inverse() which used only Uses 100
    multiplications and 61 additions or substractions.

<!-- -->

-   Tested new algorithm for bn_mat_determinant which requires only 34
    multiplications and 20 additions or substractions, saving 6
    multiplications

and 3 additions or substractions compared to the previous one.
Integrated code into brlcad and tested. new passed all benchmark tests.
Created patch and uploaded to
[sf](https://sourceforge.net/p/brlcad/patches/216/)

-   Wrote Tests to compare runtime of old_determinant against new
    determinant routine which returned the following results below:

<!-- -->

-   Wrote Tests to compare Inverse of Old matrix inverse routine and
    new_matrix Inverse routine which returned the following results:

` CPU: Pentium(R) Dual-Core  CPU      E5500  @ 2.80GHz`
` Compiler used: gcc 4.4.6-3)`
` Compiler command: gcc -W -Wall -O3 -fomit-frame-pointer`
` Kernel: Linux localhost.localdomain 2.6.32-220.el6.i686 #1 SMP Sat Dec 10     17:47:51 EST 2011 i686 i686 i386 GNU/Linux`

` ./determinant`
` My implementation:`
`          98 cycles minimum`
`         112 cycles median`
` libbn implementation:`
`          84 cycles minimum`
`          84 cycles median`
` Results (relative differences of calculated determinants):`
`   -3.836070396965505e-14 minimum`
`   0 median`
`   2.152181998793086e-13 maximum`

` ./inverse`
`  Example:`
`  My implementation:`
`   [  0.803558  0.065957  -0.31977  0.174422 ]-1   [  1.105838 -0.352959   0.306948 -0.191398 ]`
`   [  0.178270  0.764400 -0.477912  0.560214 ]     [ -0.546125  0.959763  0.471464 -0.743848 ]`
`   [  0.567903  0.641359  0.602482  0.639353 ]   = [ -0.461005 -0.688994  0.868583 -0.088937 ]`
`   [  0.000000  0.000000         0  1.000000 ]     [  0.000000  0.000000         0  1.000000 ]`
` libbn implementation:`
`   [  0.803558  0.065957  -0.31977  0.174422 ]-1   [  1.105838 -0.352959  0.306948 -0.191398 ]`
`   [  0.178270  0.764400 -0.477912  0.560214 ]     [ -0.546125  0.959763  0.471464 -0.743848 ]`
`   [  0.567903  0.641359  0.602482  0.639353 ]   = [ -0.461005 -0.688994  0.868583 -0.088937 ]`
`   [  0.000000  0.000000         0  1.000000 ]     [  0.000000  0.000000        -0  1.000000 ]`
`  My implementation:`
`         462 cycles minimum`
`         490 cycles median`
`  libbn implementation:`
`         434 cycles minimum`
`         546 cycles median`

Friday July 26, 2013

-   Added -x option to push command. But command fails to read options
    in mged. Tried (Pd:x) and Pdx as arguments to bu_getopt() but
    command fails to read options. Continued testing and debugging.

<!-- -->

-   Changed the call of pushx(formerly ged_xpush to take as args
    gedp,dp so as to proceed to xpushing of object. Still testing
    routine.

<!-- -->

-   Debugged push command to support -x option, made
    [patch](https://sourceforge.net/p/brlcad/patches/217/) and submitted
    on sourceforge. However command can push only an object at a time so
    further work needs to be done to added support for multiple objects.

<!-- -->

-   Some tests on command
    [Here](http://brlcad.org/wiki/File:Testing_new_push_routine.png)

TOD0: Add support for multiple objects then clean up xpush in BRL-CAD.

Saturday 27 July, 2013

-   Added support to Push routine to push multiple objects. Created
    patch and modified patch uploaded to sourceforge.

<!-- -->

-   To clean up xpush routine from source code and make all new
    references to new push.

## 29 July - 4 August

Monday July 29, 2013

-   Started studies on ssh, irssi, and GNU Screen, succeeded in
    uploading some of my code patches to bz.bzflag.bz.

<!-- -->

-   Downloaded code to bzflag and compiled code although there is a
    small in bug in current code repository.

<!-- -->

-   Started working on tests for some of the /src/libbn/mat.c routines
    using the modified test Sean gave me on bn_mat_inverse and
    bn_mat_determinant.

Tuesday July 30, 2013

-   Started looking at the BRL-CAD Numerics library for tests and
    started wrote a unit test for the bn_poly_multiply() routine.

<!-- -->

-   Tested for very large and small values and answer was correct.

<!-- -->

-   Integrated test into BRL-CAD, created patch and submited code on
    [sf](https://sourceforge.net/p/brlcad/patches/221/).

<!-- -->

-   Filled the Mid-Term Evaluation form for participants.

To continue work on poly.c routines tomorrow.

Wednesday July 31, 2013

-   Wrote the unit test for bn_poly_scale(), bn_poly_add(),
    bn_poly_sub(), bn_poly_synthetic_division() routines and
    uploaded code patches to source forge.

Will continue writing tests for the other poly.c tomorrow and finish by
the end of the week.

Thursday Aug 1, 2013

-   Wrote the unit test for bn_poly_quadratic_roots() routine and
    uploaded patch on
    [sourceforge](https://sourceforge.net/p/brlcad/patches/226/)

<!-- -->

-   Spent day debugging test and doing some further extreme test.

Friday Aug 2, 2013

-   Wrote and tested the unit tests for the bn_poly_cubic_roots and
    bn_poly_quartic_roots() routines. Created patches and uploaded to
    sourceforge.

<!-- -->

-   To modify patches include source of known test values( Use Octave or
    maxima) since mathportal.org doesn't give clear math solver.

<!-- -->

-   Modifying patches to match reference values from Octave.

Saturday Aug 3, 2013

-   Spent whole day debugging all unit test patches making sure tests
    failed when expected and produced the right results and outputs.

<!-- -->

-   uploaded codes to sourceforge.

## 5 August - 11 August

Monday Aug 5, 2013

-   Started working on the pull routine making sure non-leaf objects
    could be pulled.

started by building a linked list. and there is a bug lurking in there
somewhere in. Spent whole day here; will continue work on it tomorrow
after i finish moving the comments. starseeker talked about.

-   will upload latest patch to sf which should apply cleanly

Tuesday Aug 6, 2013

-   had to continue debugging pull.c but persistent problems with
    patches forced me to continue working on the libbn unit test patches
    I submitted on sourceforge.

<!-- -->

-   Currently fixing patches with Erik so they can apply cleanly.

Will be travelling home tomorrow and resume on Monday next week; So i'm
to finish with these patches and get commit access so I could work
freely on my project.

## 12 August - 18 August

Monday Aug 12 2013

-   Finished correcting indentation errors on libbn unit tests for
    polynomial routines.

<!-- -->

-   Continued test of pull routine; since tree fails to build linked
    list and discoved that the problem actually lied in the fact that I
    was testing on invalid input so linked list was not built. Trying
    appropriate objects.

Tuesday Aug 13 2013

-   Continued testing of pull routine on non leaf nodes like regions and
    combinations and this kept reporting a segmentation fault. To
    continue debugging

Wednesday Aug 14, 2013

-   continued working on the pull or matrix transformations up one level
    but work halted due to lights out for the rest of day.

Thursday Aug 15, 2013

-   Fixed patch on bn_poly_add() test and uploaded code to
    sourceforge, continued debugging bn_poly_synthetic_division()
    routine but error kept coming from bn_poly_synthetic routine
    itself as traced by gdb. Continue working on it.

<!-- -->

-   Resolved an issue with test but seg fault still lurks somewhere in
    code; been starting for over an hour and still getting nowhere. Will
    look at that tomorrow.

Friday Aug 16, 2013

-   Fixed the bn_poly_synthetic_division() unit test and uploaded
    code to sourceforge.

<!-- -->

-   Started looking at the db_preorder_traverse() routine ( although
    its not clear what struct db_traverse is since i don't see
    definition in source code) and how I could use it in implementing
    pull routine.

<!-- -->

-   To ask about definition of db_traverse since i don't see in source
    code.

Saturday Aug 17, 2013

-   Reworked the accepted patches and submitted patch on sourceforge.

<!-- -->

-   Fixed the bn_poly_quadratic_roots() routine and submitted code on
    sourceforge.

<!-- -->

-   Started working on plan to implement pull using the
    db_preorder_traverse() which will need some routines to work with
    combinations and extract matrix transoformations from primitives

ToDo: To start working on the leaf_mat() routine which extracts matrix
transformation from primitive.

## 19 August - 25 August

Monday August 19, 2013

-   Started reworking the pull_leaf routine to use db_functree instead
    of db_preorder_walk but may still use later to extract matrix
    transformation from primitives and continue walking up the tree.
    Still to ask on mailing which primitives to support first.

<!-- -->

-   Wrote the comb_enter_func() which restores the matrix
    transformations of a combination but is still dependent on
    pull_leaf() which is to deal with various primitives. To ask sean
    how to store changes on a combination matrix.

ToDo: Continue implementing pull_leaf() adding support to pull matrix
transformation from torus then, spheres, ellipsoids and in that order.
Still wondering why commit access is not coming!

Tuesday August 20, 2013

-   Finished Writing the pull_comb() routine together with the
    pull_comb_mat() routines. Discussed with Sean about test driven
    development. Will start writing unit test for routines tomorrow

<!-- -->

-   Looked into BRL-CAD source on how to write pull_leaf() routines
    which will support various primitives in the pull process since they
    don't have matrix transformation as such. Still to look at
    pull_leaf to actually see how they dealt with primitives

Wednesday August 21, 2013

-   Started looking at test provided by Sean to use of db_walk_tree so
    as to be able to create a similar for pull_comb using
    db_functree() but faced problems calling functions in BRL-CAD's
    libraries. So i'll continue working on test tomorrow

<!-- -->

-   Continued adding some functionalities to pull_leaf() routine.(still
    crude) will continue work on pull_leaf after testing pull_comb()
    perfectly

Thursday August 22, 2013

-   Started and finished writing pull_comb() unit test. But there is
    actually a seg fault which prevents the cur_mat() pointer from
    being inverted. Probably NULL.

<!-- -->

-   Will continue debugging and finish testing pull_comb() tomorrow
    then move on to pull_leaf()

Friday August 23, 2013

-   Finished debugging pull_comb() and tested routine. Works perfectly.

Any way to note changes made on combination. pulled matrix is stored on
comb_leaf-&gt;tr_l.tl_mat.

-   Created patch to stub empty pull routine into brlcad. then continue
    working on pull_leaf() routine tomorrow.

<!-- -->

-   Waiting for mentors to apply patch so i could create patch which
    adds pull_comb() routine into BRL-CAD.

## Aug 26 - Sept 01

Monday 26 August 2013

-   Started implementing the pull_leaf routine which extracts the 4x4
    matrix transformations for a primitive. Succeeeded in implementing
    the pull_leaf for an ellipse, sphere, EPH, elliptical parabola,
    elliptical torus, extrude, hyperbola, and a particle.

<!-- -->

-   started testing function and will continue debugging tomorrow before
    continuing with the addition of the superellipse, metaball,
    arbitrary complex polyhedra, arb8, rhc, rpc, and pipe.

Tuesday 27 August 2013

-   Finished debugging pull_leaf() but routine is incomplete since I
    don't currently support all primitives. Will follow Sean's
    instructions and start developing pull interface from tomorrow by
    adding synopsis, docs, full integration and test cases.

<!-- -->

-   Added support for truncated cones in pull_leaf() but a bug hangs in
    there. Will take a peek tomorrow or finish this night before going
    to sleep.

Wednesday August 28, 2013

-   Started developing the interface by adding the stubbing the pull to
    archer interface.

<!-- -->

-   Added the pull routine to the tclscripts, libtclcad, and wrote the
    pull documentation in brlcad/doc/ directories.

Still to finish writing the regresssion tests before moving on to adding
support for pulling primitives on BRL-CAD.

Thursday August 29, 2013

-   Started and finished writing the regression tests for the pull
    command.

<!-- -->

-   Tested and compiled code but pull does not appear on the command
    line when regression tests are ran. Will ask on IRC for assistance
    here.

Todo: When done with developing the pull interface, I'll dive into
writing the pull_leaf routine for all primitives.

Friday August 30, 2013

-   Tested regression tests for pull and added manual pages and
    documentation for pull successfully such as in man pages, appropos
    library for pull

<!-- -->

-   To create patch and submit on sourceforge, also tried adding pull to
    archer but found a little problem. To discuss with mentor on how to
    proceed.

TodO: After approval of man pages, to continue adding support for all
primitives into pull command. and fix bn_poly_sub() test patch.

Saturday August 31, 2013

-   Finished testing regression tests and uploaded code to sourceforge

<!-- -->

-   Continued looking at the primitives such as arb8, arbn so as to
    continue working on primitives for pull.

## Sept 02 - Sept 08

Monday Sept 02

-   Started looking at the other primitives; left to complete the
    pull_leaf() routine. Saw many complications with many primitives.
    Will need the Assistance of Sean in extracting the matrix
    transformations from them.

Tuesday Sept 03

-   Fixed bug in bn_poly_sub() unit test; uploaded code to
    [sourceforge](https://sourceforge.net/p/brlcad/patches/224/).

<!-- -->

-   Succeeded in pulling the following primitives(TGC, REC, PARTICLE,
    EPA, EHY, HYP, ETO, EXTRUDE). Still left with about 26 primitives to
    be pulled in order to complete the pull_leaf() routine.

Will need some directions on how to implement pull_leaf() since using
switch case statements is not a good design choice.

Thursday05 - Sunday 08

-   Took a break so as to recover from malaria.

## Sept 09 - Sept 15

Monday 09 October

-   Started looking at AABB bbox routines in BRL-CAD. Still to develop
    simple algorithm that automatically processes the translation from
    bbox return vectors to determine original translation.

<!-- -->

-   Read some online wiki pages on AABB bounding box of objects.

ToDO: To start writing routine and unit test tomorrow

Tuesday 10 October

-   Started and finished writing tranlate routine which extracts and
    sets the translation component from the bounding box minimum and
    maximum points from the bounding box routine.

<!-- -->

-   To integrate general bounding box calculating function for every
    primitive.

Wednesday 11 October

-   Started testing pull_leaf routine using the rt_functab bbox
    routine and successfully pulled some translations assuming object's
    centrepoint was translated from the origin(0,0,0). But still waiting
    on Sean for some clarifications on the math.

<!-- -->

-   To look at confirmation from sean and perfect the pull_leaf
    routine, completing the pull routine and running through valgrind.

Thursday 12 October

-   Perfected math on moving bounding box and primitive to origin before
    extracting translation. But will start testing tomorrow.

Friday 13 October

-   Successfully wrote the pull_leaf routine which pulled the
    translation components of the primitive.

<!-- -->

-   Tested routine together with the pull_combination routines and
    successfully moved the matrices right up to the root of the tree.
    but still unclear with cases where the matrix transformations for
    the combinations is NAN.

<!-- -->

-   Submitted [patch](https://sourceforge.net/p/brlcad/patches/215/) on
    sf and awaiting review before moving on to porting command to archer
    since i've not been granted commit access.

## Sept 16 - Sept 22

Monday Sept 16,

-   Started re-testing the pull routine starting from the pull_leaf
    which pulled correctly.

<!-- -->

-   Discovered a bug with the pull_comb() routine which pulls matrices
    which are not symmetric;so will fix bug tomorrow.

<!-- -->

-   Started stubbing pull to archer but had an error will try to fix
    problem tomorrow or post question on mailing list and see what comes
    up.

Tuesday Sept 17

-   Continued testing the pull_leaf and realised NAN values were being
    pulled from the primitives which are to be set to zero in such
    cases.

<!-- -->

-   Started fixing bug.

Wednesday Sept 18

-   Continued fixing pull_leaf routine but realised pull_comb()
    routine pulled matrix transformations having NAN as values. to ask
    mentors about this problem if it persists.

<!-- -->

-   Was in a meeting with the Vice Chancellor as Google Student
    Ambassador and explained my Vision for the University during my
    tenure.

Thursday Sept 19

-   Started preparing for my upcoming exams next week; and had a meeting
    with the Public relations Officer of the University concerning my
    recent appointment as Google Student Ambassador and plans for the
    University community.

Friday Sept 20

-   Attended the Interview at the University Media House( Chariot FM)
    where I explained my GSoC experience and current work as Google
    Student Ambassador.

Saturday Sept 21

-   Wrote the Project summary and continued preparing for my exams next
    week.

## Sept 23 - Sept 28

1.  Monday Sept 23

Started looking at the BRL-CAD documentation spreadsheet posted by
Harmanpreet and summarising all documents on the list. Requested for the
script from Harmanpreet that automates the summary of the documents.

@Will finish summarising documents tomorrow; since I have to prepare for
some of my exams coming up from tomorrow.
