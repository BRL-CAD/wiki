## PROJECT DETAILS

Project Title : Implementation of a heart primitive.

Name: Isaac Kamga.

IRC Name (Handle): Izak

e-mail: u2isaac@gmail.com

Phone : +237 74 10 62 97

## Introduction

This page will contain logs of the work I will be doing during and after
the summer of code period.

## From June 3rd to June 7th

-   Compiled and ran BRL-CAD from source (in 26 minutes) as well as used
    mged command interface.

<!-- -->

-   Studying /src/librt/primitives/\*/\*.

<!-- -->

-   Revising red-black trees in "Introduction to algorithms",third
    edition book by Cormen.

## From June 10th to June 14th

-   Fixing rb_delete.c to effectively delete nodes.

## My Development Pictures

## From June 17th to June 21

June 17

-   Finished working on rb_delete.c .

June 18

-   Edited raytrace.h by defining ID_HRT 43 ,incrementing ID_MAXIMUM
    and ID_MAX_SOLID to 44 as shown in this patch .

<!-- -->

-   Added the DB5_MINORTYPE_BRLCAD_HRT 42 define to db5.h as shown
    here .

June 19

-   Hoped to do this today : Need to look at the "Metaball" paper on
    using the blobby method , read volume rendering by Drebin et al and
    edit magic.h and rtgeom.h to include the heart primitive .

<!-- -->

-   However, took ill ( of malaria ) so undergoing treatment .

June 20

-   Ill of malaria so undergoing treatment .

June 21

-   Ill of malaria so undergoing treatment .
-   Uploaded some patches
    [here](http://sourceforge.net/p/brlcad/patches/191/).

June 22

-   Recovering from brief illness....

<!-- -->

-   Updated GSoC 2013 Accepted projects page on the wiki .

## From June 24th to June 29th

June 24

-   Re-read the Patch submission guidelines in the HACKING file .

<!-- -->

-   Read the research paper titled "Volumetric shape description using
    the blobby model" which was used to implement the metaball primitive
    ( by the second method). Since the above method is used with two
    sphere primitives to create a metaball , I am considering using this
    same method alongside two spheres ( for the heart lobes ) and an
    elliptical parabola - epa (for the lower portion of the heart ).
    Need to verify the correctness of this design approach on the
    mailing list.

June 25

-   Studying the ray tracing geometry header ( rtgeom.h ) to write the
    heart primitive's internal representation (struct rt_hrt_internal)
    .

<!-- -->

-   Searching for more information on the key properties of the heart .

<!-- -->

-   Editing the magic numbers header ( magic.h ) which I have patched
    [here](https://sourceforge.net/p/brlcad/patches/203/) .

<!-- -->

-   Currently writing the struct rt_hrt_internal structure which I
    have kept [here](https://sourceforge.net/p/brlcad/patches/204/)
    .Also wrote the RT_HRT_CK_MAGIC(_p) macro in rtgeom.h for the
    heart .

June 26

-   Finished Modifying the magic header file
    [here](https://sourceforge.net/p/brlcad/patches/203/) which I
    earlier on submitted .

<!-- -->

-   Looking into the internal representations of the tor and the
    superell .

<!-- -->

-   Reading the rt_???_shot() functions in
    src/librt/primitives/tor/tor.c and
    src/librt/primitives/superell/superell.c to understand how they
    build up and evaluate formulae.

<!-- -->

-   Included the internal representation of the heart in the
    include/rtgeom.h file used by the ray trace geometry library .That
    is, added the ID_HRT section ( struct rt_hrt_internal ). Please,
    take a [look](https://sourceforge.net/p/brlcad/patches/204/) :)

<!-- -->

-   Editing the table.c file in src/librt/primitives .Declared a
    raytrace interface for the heart by RT_DECLARE_INTERFACE(hrt) .
    Edited the rt_functab\[\] array by providing an entry ID_HRT for
    the heart primitive. That is, add RT_FUNCTAB_MAGIC, "ID_HRT",
    "hrt",rt_hrt_\*, just to name a few. You are welcome to look at my
    [progress](https://sourceforge.net/p/brlcad/patches/205/).

June 27

-   Early in the morning I Left Buea, my home town to collect Google's
    welcome package in Douala. Collected some cash from the available
    ATM . Negotiating for Internet access and cool coding
    environment.Really tired.

June 28

-   Corrected and submitted the db5 header [( See db5.patch
    )](https://sourceforge.net/p/brlcad/patches/191/) based on
    guidelines given by mentors.

<!-- -->

-   Corrected and submitted the raytrace header [( See raytrace.patch
    )](https://sourceforge.net/p/brlcad/patches/191/) based on
    guidelines given by mentors.

<!-- -->

-   Corrected and submitted the magic header [( See newest_magic.patch
    )](https://sourceforge.net/p/brlcad/patches/203/) based on
    guidelines given by mentors. Still to correct the magic.c file to
    make these changes complete.

June 29

-   Editing the magic.c file to accommodate the heart primitive.
    Uploaded the [patch
    here](https://sourceforge.net/p/brlcad/patches/203/?page=1).

<!-- -->

-   Reworking the ray trace geometry header file (rtgeom.h) so that the
    internal representation of the heart will be accurate.

## From July 1st to July 6th

July 1

-   Working on struct rt_hrt_internal inorder to include the heart
    primitive into the include/rtgeom.h header. Reading wikipedia and
    Wolfram pages on heart symbol,Level set,cusps and epicycloids.

<!-- -->

-   Combined magic_h.patch and magic_c.patch into single
    [magic.tar.gz](https://sourceforge.net/p/brlcad/patches/203/?page=1)
    compressed file .

<!-- -->

-   Combined db5_h.patch and db5_types_c.patch into single
    [db5.tar.gz](https://sourceforge.net/p/brlcad/patches/207/)
    compressed file.

July 2

-   Still awaiting clarifications which I requested on the mailing list
    to develope the internal representation of the heart primitive in
    include/rtgeom.h.

<!-- -->

-   Corrected the
    [hrt_magic.patch](https://sourceforge.net/p/brlcad/patches/203/?page=1)
    file based on recommendations given by my mentor.

<!-- -->

-   Corrected the
    [hrt_db5.patch](https://sourceforge.net/p/brlcad/patches/207/) file
    based on recommendations given by my mentor.

<!-- -->

-   Awaiting some answers to questions posted on the mailing list in
    order to proceed with the editing of rtgeom.h and raytrace.h

July 3

-   Getting requisite authorization to connect Workspace at the Faculty
    of Science building to the Internet. Not easy dealing with a
    bureaucratic system in which every administrative decision has to be
    documented in letters.

<!-- -->

-   Downloaded subversion packages and source code to install. Need this
    to submit patches that apply cleanly.

<!-- -->

-   The above activities took the whole day. Could not do coding work.

July 4

-   Doing negotiations to get Internet access. This is a prerequisite to
    submitting perfect patches which are generated from the svn
    checkout.

<!-- -->

-   Pushing through with authorization for Internet access at my
    workspace .

<!-- -->

-   Presented the "Implementation of the heart primitive" proposal and
    progress reports to lectures and students of the Departments of
    Computer Science and computer Engineering.

<!-- -->

-   Did no coding work today as I was preparing a good environment for
    coding.

June 5

-   Did detailed mind maps to aid visualization of necessary editing of
    files to aid submission of logical patches. This will help see
    exactly how to group file changes like magic numbers , mirror
    support, mged support, etc.

<!-- -->

-   Got equipment ready for installations of Internet but could not
    install today due to rainy weather. Hoping to get a sunny window
    tomorrow morning for installation.

July 6

-   Awaiting the arrival of Head of Department from Bamenda. Discussed
    with him the need for authorization to install Internet at the
    laboratory by phone. He said we need to officially discuss it during
    office hours on Monday,July 8.

<!-- -->

-   Doing research on how to solve the sextic equation of the heart.
    Read some papers and observed that the sextic equation of the heart
    does not meet the conditions presented in the literature.

## From July 8th to July 14th

July 8

-   Yoopee:) My Head of Department discusses the need for GSoC students
    to temporarily install Internet at the laboratory with the Dean of
    the Faculty of Science.The Dean seconds the idea and writes to the
    Vice-Chancellor for final authorization. Waiting for the final
    authorization from the Vice-Chancellor within the week.This is the
    [letter](https://docs.google.com/file/d/0B4kEIUMOBbU-SlBaeEdqQ0Eta1U/edit?usp=sharing)
    I wrote to the Deputy Vice Chancellor .The Head of Department's
    letter through the Dean to the Vice-Chancellor can be viewed
    [here](https://docs.google.com/file/d/0B4kEIUMOBbU-b2xzMXl2Y2lyaG8/edit?usp=sharing).

<!-- -->

-   Modified the internal representation of the heart (struct
    rt_hrt_internal).

<!-- -->

-   Including an entry into the rt_functab\[\] array for the heart.

<!-- -->

-   Plan to generate the patches from the work done immediately Internet
    access is available.

July 9

-   Correcting my M.Sc. thesis in order to submit to supervisor until
    13:00 UTC.

<!-- -->

-   Finished working on the internal parameters of the heart solid in
    include/rtgeom.h .It now includes a center point, unit vectors in
    x,y and z directions and distance from center point to both upper
    and lower cusps.

<!-- -->

-   Added mk_hrt() routine and associated comments to the include/wdb.h
    header file and src/libwdb/wdb.c file.

<!-- -->

-   Added p_hrt\[\] array and hrt_in() routine to src/libged/typein.c
    so as to read heart parameters from the keyboard.

<!-- -->

-   Waiting for final authorization for temporal installation of
    Internet access to generate patches which I worked on using svn.My
    Head of Department says the Dean still awaits response from the
    Vice-Chancellor's office.

<!-- -->

-   Intend to test these edits tomorrow. Couldn't do these today because
    the Faculty building was very noisy today due to a staff meeting.

July 10

-   Had a two-hour entretien today with my supervisor and head of
    Department until 10:00 UTC.

<!-- -->

-   Created a hrt_magic patch file ( generated from diff -u for now
    ),the patch applied cleanly and BRL-CAD source compiled.

<!-- -->

-   Created a hrt_stub patch file ( also generated from diff -u for now
    ), patch applied cleanly and BRL-CAD source compiled.Realised that
    an empty heart primitive has NULL fields in its rt_functab\[\]
    array entry.

<!-- -->

-   Still Awaiting response to letter of authorization from the
    Vice-Chancellor :(

<!-- -->

-   For tomorrow's work, I intend to create a heart object which can be
    tested in the mged interface.

July 11

-   Debugged and compiled the int mk_hrt(struct rt_wdb \*wdbp, const
    char \*name, const fastf_t \*center, const fastf_t \*xdir, const
    fastf_t \*ydir, const fastf_t \*zdir, const fastf_t d) routine
    which was previously added to src/libwdb/wdb.c file.

<!-- -->

-   Debugged and compliled the p_hrt\[\] array and the hrt_in(struct
    ged \*gedp, char \*cmd_argv\[\], struct rt_db_internal \*intern)
    function which was previously added to src/libged/typein.c .

<!-- -->

-   Tested the compiled code by reading in the coordinates of a heart
    object using the keyboard on the mged interface as shown
    [here](https://docs.google.com/file/d/0B4kEIUMOBbU-ZUpmcXpxZlFzVXc/edit?usp=sharing).
    Feeling great!:)

<!-- -->

-   Still awaiting response from the Vice-Chancellor.

<!-- -->

-   Intend to finish any hacks of the mged interface and get into the
    difficult functions like rt_hrt_shot, rt_hrt_prep , etc.

July 12

-   Added case HRT to the solbld function in src/conv/asc/asc2g.c which
    parses the heart record and determines which libwdb routine to call
    in order to replicate it. Debugging asc2g.c.....

July 13

-   Started writing rt_hrt_shot() function for
    src/librt/primitives/hrt/hrt.c

## Monthly Summary

Work done

1\. Added magic numbers:

-   Defined RT_HRT_INTERNAL_MAGIC Ox6872743f in include/magic.h
-   Included a case RT_HRT_INTERNAL_MAGIC in src/libbu/magic.c
-   I ended up with hrt_magic.patch.

2\. Stubbed in an empty heart primitive

-   Defined DB5_MINORTYPE_BRLCAD_HRT in include/db5.h.
-   Incremented ID_MAX_SOLID and ID_MAXIMUM to 44 as well as defined
    ID_HRT as 43.
-   Added { DB5_MAJORTYPE_BRLCAD, DB5_MINORTYPE_BRLCAD_HRT, 1,
    "hrt", "Heart" } as entry for the heart primitive in
    src/librt/db5_types.c.
-   Added struct rt_hrt_internal{} to internally represent the heart
    and wrote the RT_HRT_CK_MAGIC(_p) macro .
-   Declared RT_DECLARE_INTERFACE(hrt) and edited rtfunctab\[\] to
    include an entry for the heart in src/librt/primitives/table.c .This
    entry had many NULL fields.
-   With this, I generated hrt_stub.patch.

3\. Added type in support for the heart (so as to read heart parameters
from the keyboard.)

-   Added mk_hrt() routine and associated comments to include/wdb.h and
    src/libwdb/wdb.c .
-   Added p_hrt\[\] array and hrt_in() routine to src/libged/typein.c
-   This gave birth to hrt_type.patch, which was compiled, debugged and
    tested in the mged interface (See July 11 on my Development log).

Future work

-   Start coding and testing the Intersection of a heart with a ray by
    writing int rt_hrt_shot(), void rt_hrt_norm, void rt_hrt_uv,
    etc

## From July 15th to July 20th

July 15

-   Studying how the quartic equation of the torus is built until the
    roots of this quartic equation is found by the root finder.

<!-- -->

-   Working on int rt_hrt_shot() function whereby a ray intersects
    with the heart.This yield a sextic polynomial in t with 7
    coefficients each with an average of 70 algebraic terms. The
    coefficient of t^6 has been computed while the coefficient of t^5 is
    being computed.

July 16

-   Working on the t^5 and t^4 coefficients of the sextic equation in
    the int rt_hrt_shot() function whereby a ray intersects with the
    heart.

July 17

-   Finished working on the coefficients of the sextic equation...
    Pretty tedious.

<!-- -->

-   Discussed today with my former mathematics professor who pointed me
    to the Rouche's theorem to locate complex roots of a polynomial .
    Researching on this Theorem to locate roots and solve sextic
    equation.

July 18

-   Following up the letter written to the Vice-Chancellor at the
    Central Administration. No coding work done today.

July 19

-   Finished writing the rt_hrt_shot() function which has to be
    debugged and tested.

July 20

-   Had a headache today. Did no coding work. Just did some planning and
    light observation of toroid and superell primitives in
    src/librt/primitives/.

# From July 22th to July 27th

July 22

-   Wrote the rt_hrt_parse\[\] array based on the internal properties
    of the heart.

<!-- -->

-   Corrected the hrt_specific structure.

<!-- -->

-   Wrote the rt_hrt_prep() function to prepare the heart object for
    ray shoting.

<!-- -->

-   Making sure that my patches compile, although not yet generated from
    svn diff -u .

July 23

-   Fixed my S.L. 6.2 system today after a crash. Lost the
    0rt_hrt_prep() function which I already wrote :(. Not a big deal
    though.

<!-- -->

-   Helped install Internet at the laboratory.

<!-- -->

-   Discussed on IRC with brlcad on setting up a bzflag account.
    Accepted the usage policy and rules. Got this account set up.

<!-- -->

-   Discussed with brlcad and Erik on IRC about correcting my
    communication (posting) style. Read the more academic
    [wikipedia](http://en.wikipedia.org/wiki/Posting_style) page and
    Erik's recommended
    [link](http://catb.org/jargon/html/T/top-post.html) in order to
    correct this.

<!-- -->

-   Checking my patches from A to Z.

July 24

-   Generated and tested the
    [hrt_magic.patch](https://sourceforge.net/p/brlcad/patches/203/?page=1)
    that it applies cleanly, independently and without any side effects.

<!-- -->

-   Generated and tested the
    [hrt_stub.patch](https://sourceforge.net/p/brlcad/patches/207/)
    that it applies cleanly, independently and without any side effects.

July 25

-   My mentor
    [accepted](http://sourceforge.net/p/brlcad/patches/203/?limit=10&page=1#836c)
    the hrt_magic.patch and
    [applied](http://sourceforge.net/p/brlcad/patches/203/?limit=10&page=1#a682)
    it to r56212. :)

<!-- -->

-   Doing changes to generate hrt_typein.patch.

July 26

-   Removing errors from the hrt_typein.patch

<!-- -->

-   My hrt_stub.patch file got
    [closed-accepted](http://sourceforge.net/p/brlcad/patches/207/?limit=10&page=1#99a9)
    status and
    [applied](http://sourceforge.net/p/brlcad/patches/207/?limit=10&page=1#f22c)
    to r56235.

July 27

-   Working on a test for the
    [rb_delete.c](http://sourceforge.net/p/brlcad/patches/191/)
    function.

# Pre-midterm evaluation summary

In order to prepare the BRL-CAD source code for the heart primitive , I
hooked the heart primitive into the BRL-CAD source by adding a magic
number for the heart in include/magic.h and src/libbu/magic.c, stubbing
an empty heart in include/db5.h, include/rtgeom.h, include/raytrace.h,
src/librt/db5_types.c and /src/librt/primitives/table.c and adding
typing support for the heart in the mged interface in include/wdb.h,
src/libwdb/wdb.c and src/libged/typein.c as can be seen
[here](https://docs.google.com/file/d/0B4kEIUMOBbU-ZUpmcXpxZlFzVXc/edit?usp=sharing).
As regards the ray tracing callback functions in
src/librt/primitives/hrt/hrt.c , I have built the hrt_specific
structure, written the rt_hrt_shot() and rt_hrt_prep() functions and
I am currently testing these.I intend to continue working on other
callback functions like rt_hrt_import(), rt_hrt_print(), etc and
finally hook the heart primitive to the mged and archer interfaces with
associated clean up and documentation.

# Mid-term Evaluation week

July 29

-   Fixed a typo ( V_vec instead of v_vec on line 286 of
    src/libger/polyclip.cpp ) and generated a
    [patch](http://sourceforge.net/p/brlcad/patches/218/) which was
    applied to r56306 by Mohit Daga.

<!-- -->

-   Working on the starting requirements of Google Developer Group (GDG
    Buea) : Created GDG Buea Google+ page with links to agents' pages ,
    GDG Buea google group,etc

July 30

-   Filled Mid-term evaluation form and submitted to google-melange.com

<!-- -->

-   Compiled and tested the int mk_hrt() routine and p_hrt\[\] array &
    the hrt_in( ) function in src/libwdb/wdb.c file and
    src/libged/typein.c respectively. Generated and uploaded this
    hrt_typein.[patch](https://sourceforge.net/p/brlcad/patches/220/).

<!-- -->

-   Had an IRC session where I discussed with mentors on the importance
    of paying attention to detail.

July 31

-   Worked on opening comment, bu_structparse rt_hrt_parse array and
    hrt_specific structure .

<!-- -->

-   Posed a question to other developers asking for help on writing
    rt_hrt_bbox() routine and testing callback functions in hrt.c

August 1

-   Presenting the work done to set up the Google Developer group Buea
    to staff of the Department of Computer Science.

<!-- -->

-   Doing some research on calculating the bounding box volume of an
    object.

<!-- -->

-   Going through a little irssi-ssh tutorial.

August 2

-   Correcting the rt_hrt_shot() function in
    src/librt/primitives/hrt/hrt.c

<!-- -->

-   Chatted with my mentor today : giving me recommendations for commit
    access.

<!-- -->

-   Working on a basic hrt/hrt.c

<!-- -->

-   Just passed the mid-term evaluations

# August 5th to August 9th

August 5

-   Correcting the bare bones
    [patch](https://sourceforge.net/p/brlcad/patches/228/).

<!-- -->

-   Building rt_hrt_prep() and rt_hrt_shot()

August 6

-   My operating system crashed due to some accidental system file
    deletes.Fixing my system , created coding environment and did fresh
    svn checkouts.

<!-- -->

-   Worked on the logo for the [GDG
    Buea](https://plus.google.com/100289274059280359416) Google+ page.

<!-- -->

-   Did no coding work today.

August 7

-   Wrote the rt_hrt_import() callback function for hrt.c.

<!-- -->

-   Uploaded hrt_import5
    [patch](https://sourceforge.net/p/brlcad/patches/230/) to
    sourceforge.net.

<!-- -->

-   A picture for the rt_hrt_import5 test on mged interface can be
    viewed [here](http://brlcad.org/~Izak/Import_test.png).

<!-- -->

-   Wrote the rt_hrt_export() callback function for hrt.c.

<!-- -->

-   uploaded hrt_export5
    [patch](https://sourceforge.net/p/brlcad/patches/229/) to
    sourceforge.net.

<!-- -->

-   A picture for the rt_hrt_export5 test on archer interface can be
    viewed [here](http://brlcad.org/~Izak/Export_test.png).

August 8

-   Have been granted commit access. :)

<!-- -->

-   Learned how to use svn commit, svn revert, etc.

<!-- -->

-   Ensured consistent bu_log("rt_hrt_xxx: not implemented yet!\\n");
    in calllbacks functions for hrt.c and committed to
    [r56694](http://sourceforge.net/p/brlcad/code/56694/).

# August 12th to August 17th

August 12th

-   Added hrt_invsq vector and hrt_invRSSR matrix to the heart
    structure in [r56745](https://sourceforge.net/p/brlcad/code/56745/).

<!-- -->

-   Added rt_hrt_print() routine and removed rt_hrt_??port4()
    routines pertaining to version 4 of database in
    [r56745](https://sourceforge.net/p/brlcad/code/56746/).

<!-- -->

-   Added rt_hrt_import5() routine to import the database format to
    the internal format in
    [r56747](https://sourceforge.net/p/brlcad/code/56747/).

<!-- -->

-   Added rt_hrt_export5() routine to export from internal format to
    database format in
    [r56751](https://sourceforge.net/p/brlcad/code/56751/)

August 13th

-   Went to the Cameroon GCE Board office to apply for duplicate
    certificate for my younger sister.

<!-- -->

-   Wrote rt_hrt_describe() routine to present the heart solid in
    human-readable format and committed changes to
    [r56791](http://sourceforge.net/p/brlcad/code/56791/).

<!-- -->

-   Pictures to demonstrate the working rt_hrt_describe() function
    using the l command in the mged and archer interfaces can be viewed
    [here](http://brlcad.org/~Izak/rt_hrt_describe_mged.png) and
    [here](http://brlcad.org/~Izak/rt_hrt_describe_archer.png)
    respectively.

August 14th

-   Working on rt_hrt_prep() routine but electric blackouts in my area
    halted work.

August 15th

-   Compiled hrt.c after writing rt_hrt_prep(). This routine calls
    rt_hrt_bbox() routine (which I am still to work on ) and some
    testing using the rt command. Will commit
    [rt_hrt_prep()](http://paste.kde.org/p20fbe4c6/) later.

<!-- -->

-   Worked on rt_hrt_ifree() to free the storage associated with the
    rt_db_internal version of this solid and commited to
    [r56876](https://sourceforge.net/p/brlcad/code/56876/).

August 16th

-   Working on rt_hrt_bbox() routine which needs some testing before I
    commit.

August 17th

-   Finished working on rt_hrt_bbox() routine today. Used the bb
    command to test this code in the
    [mged](http://brlcad.org/~Izak/rt_hrt_bbox_mged_test.png) and
    [archer](http://brlcad.org/~Izak/rt_hrt_bbox_archer_test.png).

<!-- -->

-   Committed changes in rt_hrt_bbox() and rt_hrt_prep() routines to
    [r56917](http://sourceforge.net/p/brlcad/code/56917/).Will do more
    work on rt_hrt_prep() function eventually.

# August 19th to August 24th

August 19th

-   Corrected spelling of polynomial in bn_poly_synthetic_div.c in
    [r56944](http://sourceforge.net/p/brlcad/code/56944).

<!-- -->

-   Wrote the rt_hrt_free() and rt_hrt_params() functions in
    [r56947](http://sourceforge.net/p/brlcad/code/56947/).

<!-- -->

-   Still working on rt_hrt_prep().

August 20th

-   Modified rt_hrt_prep() function and commited it to
    [r57004](https://sourceforge.net/p/brlcad/code/57004/).

August 21st

-   Working on rt_hrt_shot(). Still to commit.

<!-- -->

-   Modified comment to add new constant in rt_hrt_prep() in
    [r57023](http://sourceforge.net/p/brlcad/code/57023/) and
    [r57035](http://sourceforge.net/p/brlcad/code/57035/).

August 22nd

-   Modifying a comment by punctuating the word primitive in super
    ellipsoid primitive and commited to
    [r57058](http://sourceforge.net/p/brlcad/code/57058/).

<!-- -->

-   Understanding how to write the rt_???_shot() function for
    primitives.

<!-- -->

-   Adding rt_hrt_shot to intersect a ray with the heart in
    [r57068](http://sourceforge.net/p/brlcad/code/57068/).

<!-- -->

-   Tests in the mged using the 'rt' command givers this
    [result](http://brlcad.org/~Izak/rt_shot_test.png).

August 23rd

-   Removed unused variable polycurve and fixed function declarations in
    pc header

and committed to [r57097](http://sourceforge.net/p/brlcad/code/57097/).

-   Added rt_hrt_norm() function which Computes the normal to the
    heart given a point on the heart in
    [r57100](http://sourceforge.net/p/brlcad/code/57100/).

# August 26th to August 31st

August 26th

-   Experiencing an infection in my left eye so could not work
    throughout the weekend until today.Couldn't work with one eye.

August 27th

-   Researching on solving sextic equations. Found an interesting paper
    by Titus Piezas III.

<!-- -->

-   Correcting sextic equation in comment preceeding rt_hrt_shot()
    implementation in
    [r57180](http://sourceforge.net/p/brlcad/code/57180/).

August 28th

-   Reading papers by Piezas and Thomas Hagerdon to come out with
    algorithm to write bn_poly_sextic_roots.c.

August 29th - 30th

-   Consulting mathematician Titius Piezas for advice on how to solve
    the sextic equation for rt_hrt_shot() to do ray tracing. Piezas
    says the equation is solvable using numerical solutions with
    arbitrary accuracy but is not solvable with respect to radicals in
    Galois theory.

August 31st

-   Researching on root-finding algorithms which can be used to write
    bn_poly_sextic_roots.c

<!-- -->

-   Working on rt_hrt_plot to plot the heart.

# September 2nd to September 7th

September 5th

-   Working on roots_example.c to incorporate test for sextic equation.

September 6th

-   Changed 4 to BN_MAX_POLY_DEGREE in roots_example.c to avoid any
    further confusions in
    [r57469](http://sourceforge.net/p/brlcad/code/57469).
    roots_example.c actually solves a sextic equation now.

<!-- -->

-   Solved the implicit heart equation with x=y=z in order to substitute
    into the rt_hrt_shot sextic equation and use in roots_example.c

<!-- -->

-   Running rt command on a hrt object. Picture can be viewed
    [here](http://brlcad.org/~Izak/heart.png).

September 7th

-   Produced a [slideshow](http://brlcad.org/~Izak/Movie.odp) from
    images produced after running the 'rt' command on a heart object.

# September 9th to September 14th

September 9th

-   Getting my feet wet with plotting in the mged/archer interface :)

September 10th

-   Fixed the orientation of the heart and invalid implicit equation in
    rt_hrt_shot() in
    [r57533](http://sourceforge.net/p/brlcad/code/57533/).

<!-- -->

-   Getting better results from rt_hrt_shot in this [Heart
    movie](http://brlcad.org/~Izak/Heart.mpg).

<!-- -->

-   Observing the rt_ell_plot() functions to see how the
    rt_hrt_plot() can be written.

September 14th

-   Corrected rt_hrt_bbox() by Stretching the xdir vector to
    accommodate the heart and rt_hrt_norm() by Correcting Z component
    of the normal vector (partials of sextic equation) in
    [r57553](http://sourceforge.net/p/brlcad/code/57653/).

# September 16th to September 21st

September 16th

-   Had an entretien with my University's Vice- Chancellor and dean of
    Faculty of Engineering today talking about Summer of Code and
    approaching Doc Camp .

<!-- -->

-   Wrote a private helper function rt_hrt_24pts() for
    rt_hrt_plot(). Have written code to get 2 iso-contours. Still
    working on some bugs in archer.

September 17th

-   Following the stack trace which Sean opened my eyes to on IRC.

September 18th

-   Fixed the bumpy areas on the heart by correcting some code in
    rt_hrt_norm() in
    [r57728](http://sourceforge.net/p/brlcad/code/57728/).

September 20th

-   Corrected the rt_hrt_norm() function so that the default trace
    shouldn't be doing from high specular to dark shadows in
    [r57780](http://sourceforge.net/p/brlcad/code/57780/).

# GSoC 2013 summary

For the past quarter, I've been implementing a heart primitive for the
BRL-CAD package. This project focused on writing and testing callback
functions in the ray tracing library for the aforementioned
primitive.You are invited to read my diary on
<http://brlcad.org/wiki/User:Izak/GSOC_2013_logs>.

Despite the challenges I encountered such as the lack of Internet
connectivity for over 5 weeks before the mid-term evaluation period, I
hooked the heart primitive into the BRL-CAD source by adding a magic
number for the heart in include/magic.h and src/libbu/magic.c, stubbing
an empty heart in include/db5.h, include/rtgeom.h,
include/raytrace.h,src/librt/db5_types.c,src/librt/primitives/table.c
and src/librt/primitives/hrt/hrt.c as well as adding typing support for
the heart in the mged interface in include/wdb.h,src/libwdb/wdb.c and
src/libged/typein.c.

After the mid-term evaluations,I implemented ray tracing callback
functions for serialization (rt_hrt_??port), textual description
(rt_hrt_describe, rt_hrt_print) and ray tracing (rt_hrt_prep,
rt_hrt_shot and rt_hrt_norm).I also wrote a test to ensure that
BRL-CAD's root solver is stable for sextic equations and after
consulting some mathematicians, I learned that the heart's sextic
equation cannot be solved in radicals -- A pointer to which method does
not work :). Feel free to download a heart animation from
<http://brlcad.org/~Izak/HeartImages/Heart.mpg>. You can also look at
images of the heart from 360 different angles using
<http://brlcad.org/~Izak/HeartImages/>

As GSoC 2013 comes to an end, my passion to continuously contribute to
the open source community grows. I intend to finish the callbacks
functions for the heart primitive and hook the heart to the mged and
archer interfaces so the heart gets into the next BRL-CAD release :)

Feeling Great! :)