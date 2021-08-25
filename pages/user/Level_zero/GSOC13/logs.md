# Development Logs

## Project Details

|                             |                                                                   |
|-----------------------------|-------------------------------------------------------------------|
| **Project Name**            | Consolidating and Adding the Image Processing Functions to LIBICV |
| **Project Sudent**          | Mohit Daga                                                        |
| **IRC(nick)**               | zero_level                                                       |
| **Google-Melange username** | zero_level                                                       |
| **Phone Number**            | +91 9783582684                                                    |
|                             |                                                                   |

## Introduction

This page will contain weekly targets and Updates about the work done.

### Pre Coding Period

'''''From 1st to 5th June

Will be unavailable on the internet, Visiting the meditation facility.

-   Targets during this time
    -   As per the proposal document I will be studying the Image
        Processing tools.

<!-- -->

-   Read Details regarding SVN.

'''''5th June to 9th June

-   Read Codes of the utilities from Group 1-8. Made Rough Notes for all
    theses utilities and working for an Implementation Plan.

'''''10th June to 12th June

-   Api Design and Posting them on BRLCAD website. It can be accessed
    from [here](Level_zero/GSOC13/api.md).

'''''12th June - 14th June

-   Working on conversion tools. Posted a patch for conversion of pix-bw
    and bw-pix.Patch can be found
    [1](http://sourceforge.net/p/brlcad/patches/188/).

### Week 1 (17-22 June)


**Structures**

-   Structure Definitions : This week structure and api definitions were
    designed. had good discussions with the mentors on the possibility
    of the design and finalizing it.

<!-- -->

-   Later during the end of week I read about high definition images.
    Familiarized myself with Openexr
    [2](http://www.openexr.com/ReadingAndWritingImageFiles-1.2.x.pdf)
    image containers. Also about how bmp, png handles them. About


**Depth Converters**

-   Bw-pix, pix-bw : I converted these two utilities to functions. These
    were important because these can help convert a grey level image to
    a colour image and vice versa. Saved as patch.


**Patches**

-   Wrote Doxygen comments for ICV Header file. Committed by \`\`Erik

<!-- -->

-   Revisited my pre-application ICV_LOAD patches. Improved them and
    posted. Waiting to be reviewed. (Patch 197).


**Cropping Functions**

-   Although Groups start from the second week. During Discussions with
    the mentors, I implemented functionalities of Group 1. icv_rect
    (cropping with rectangular box.) and icv_crop(cropping with skewed
    coordinates). Although these have to be re modified with the new
    structure definitions.


**bwhisteq**

-   I found a code redundancy while reading the utilities last week.
    Thus posted it. The mentors found issues with the compatibility of
    bwhisteq and its correctness. I checked and tested it on
    artificially uniform grad images, two color images with half dark
    and half light and natural images of lena, barbara. Turns out that
    this is fine.

*P.S. From next week onwards I will update on daily basis.*

### WEEK 2

'''''24th June

Worked on Operations(GROUP 2). Learnt the macro usage of vmath.h. This
provides nice macro definitions. Although these cannot be used for image
data. Designed new macro definitions for icv_data. Initiated a
discussion for keeping them in icv_math.h

'''''25th June

-   Tested three different structure definitions for the time. These are
    here [3](http://www.bzflag.bz/~mohit/interleaved.c)
    [4](http://www.bzflag.bz/~mohit/structure.c)
    [5](http://www.bzflag.bz/~mohit/seperatearrays.c)
-   checked the Crop, and rect as per the new struct defintion
-   Find out a plan to implement these structure on the existing use of
    a libicv in rt,libged and rmrt

'''''26th and 27th June

-   Wrote Functions to read, write, create Image and zero image.
-   Separate files have been made for each format. Added pix, bw format.
-   Links to these files are as follows


<http://www.bzflag.bz/~mohit/ICV/icv.h>

<http://www.bzflag.bz/~mohit/ICV/image.c>

<http://www.bzflag.bz/~mohit/ICV/icv_bw.c>

<http://www.bzflag.bz/~mohit/ICV/icv_pix.c>

<http://www.bzflag.bz/~mohit/ICV/fileformat.c>

-   Road ahead:- Incorporate them in rt/view.c rt/viewxray.c
    rt/viewedge.c and rt/do.c and libged/screengrab.c

'''''28th June

-   Converted the existing use of LIBICV in rt.
-   Added gamma_corr field in image for gamma correction when an
    image's data is converted from double to unsigned char type.

'''''29th June

-   didnt do any coding work today.
-   worked towards clarifying issues with my patches 171, 175, 176,
    178,188,192,197,198, 201.

'''''30th June

-   did some system Cleaning and Installed new operating System and
    packages.

### WEEK 3

'''''1 July

-   Did code regarding Filter Functions (Group 3) and use of Kernels.

'''''2 July

-   Improved the kernel functions. tried building a test function in the
    src/util folder.

'''''3 July

-   Instead of going further with Designing new functions. reiterated
    the use of icv functions in libged/screengrab.c Changed there
    functions as per the new writepixel functions. Tested load, save
    functions of icv library.

'''''4 July

-   Wrote testing function and programs similar to libbu. These will
    help in testing the functions of icv. Also changed current usage of
    libicv in rt, rmrt and libged.

'''''5 July

-   Wrote Color_space changers. This will be useful in saving RGB data
    in bw format and gray data in pix format.

'''''6 July

-   Wrote crop and rect functions for icv library. Crop accepts skewed
    parameters and can extract image in any quadrilateral, this then
    converts the image to rectangular using the nearest neighbour.
    Whereas rect extracts rectangular part of an image.

### **Milestones Reached**

The following milestones only include the completed code. Kernels and
operations have been started but are yet to completed, thus not included
in the milestone.

1.  Discussed with mentors about the image structures and API designs.
2.  Wrote save functions in new format. Implemented the following
    functions as per the new formats.
    1.  create_image,
    2.  load_image,
    3.  zero_image,
    4.  free_image,
    5.  write_pixel,
    6.  write_line
3.  Initiated a testing infrastructure for libicv. Wrote testing
    functions for loading and saving images.
4.  converted the existing use of ICV in rt,libged and rmrt.
5.  Implemented functions to crop image These include
    1.  Rect
    2.  Crop
6.  Implemented functions to change Color_space
    1.  rgb2gray
    2.  gray2rgb

This link takes you to the new ICV infrastructure written
<http://bzflag.bz/~mohit/libicv_7thJUL/>

### Week 4

'''''Monday (8th July)

Implemented testing routines in libicv/tests for color_space(rgb2gray
and gray2rgb), pixel writing(single pixel, and pixel line). Corrected
few errors in the routines. Tested color space changers with natural
image(lena of 512X512 in png format). Converted that to pix(png2pix).
Loaded pix image using implemented function. and converted it to gray
scale image, then saved to bw format. Used this bw image to create a pix
image using colorspace change to rgb. *P.S. All these things are done by
loading the image in double format data*

'''''Tuesday (9th July)

Implemented and tested splitting of color channels. Given a rgb image
this function can split the any color channel and produce a gray scale
image.

'''''Wednesday (10th July)

-   Implemented Pixsaturate as icv_saturate.
-   This implementation is a function which takes in the sat value and
    icv_image struct. This takes the double data.
-   Created a test routine for this implementation. Corrected few errors
    which crept in.
-   Compared the results with the original routine (pixsaturate)

'''''Thursday (11th July)

Started working on filter Again. This is a very tricky implementation as
a function. There are three routines pixfilter, bwfilter and
pix3filtter. Read there code along. Found some commonalities.

'''''Friday (12th June)

Implemented the filter routine for single channel images. This is a very
rough draft and will involve changing and updating the function.

'''''Saturday (13th June)

**Took a break : Invited friends for Iftikhar party**

'''''Sunday(14th July)

Only Tested the bwhisteq function for Method2. And updated status about
previous patches.

### Week 5

'''''Monday (15th July)

Improved the filter function with added generalization to dimension of
kernel and number of channels.

'''''Tuesday (16th July)

Finalized filter function. Tested it with natural images for lenna,
mandrill and barbara. This implementation is highly generalized and can
handle any number of channels. Also kernel dimension has been worked
with (Ensuring it accepts any size of kernel). Although this file will
need a relook for getting kernel coefficients of arbitrary size.

'''''Wednesday (17th July)

Implemented icv_hist function. Also tested this file. This
implementation has also been generalized for any number of channels.
thus an improvement over previous code. Also it was tricky implementing
this because the image data is converted to double. To deal with this
used the bins concept and converted to integer.

'''''Thursday (18th July)

Looked at plans for implementation of histeq for double data. By the
look of it looks very tricky to implement this for double data. I
believe I have to write it afresh.

'''''Friday (19th July)

Implemented histeq for single channel images. Also looked at stats
functions. Looked at Erik's suggestion for single functions like
icv_image_sum, icv_image_mean etc.

'''''Saturday (20th July)

Implemented stats function. Planning to merge hist functions in stats.c

### Week 6

'''''Monday (22 July)

Implemented bilinear interpolation as part of scale function. Next I
have to implement nearest neighbour function.

'''''Tuesday (23 July)

Completed scale function. Now it is a generalized implementation. It is
implemented as icv_scale accepts both gray scale(single channel) and
rgb images. Also it works with double data.

'''''Wednesday (24 July)

Implemented shrink function. This handles both pixshrink and bwshrink
and the api function looks as icv_shrink.

'''''Thursday (25 July)

Tested icv_scale and icv_shrink. Corrected the anomalies.

'''''Friday (26 July)

Committed the new icv structure. Incrementally Committing all the
functions and api's. Also working on a bug that crept in rt during
commit.

'''''Saturday (27 July)

Tried Fixing issue related to rtedge.

'''''Sunday (28 July)

Hostel Relocation.

### Week 7

'''''Monday (29 July)

Fixed few bugs which crept in during icv implementation in rt. Compiled
the src code on bz account. Ran several tests on multi processor machine
(bz server). Did benchmark testing. Went through large part of code in
rt. Also got acquainted to multi threaded process in brl-cad.

'''''Tuesday (30 July)

Tested and committed rect, crop, filter, filter3, fade api functions. My
local tree was sort of mismanaged.

'''''Wednesday (31 July)

Was planning to work on merging my tree in the source code, But
Apparently Benchmark Error showed up. :-( Wrote icv_writeline such that
now it doesn't allocate memory. This helps in putting in place the
semaphores again. Even Putting semaphore didn't help resolve the
benchmark issue. I took help of fellow gsoc students to get errors from
benchmark, And it turned out there was issue with fractions in double
data. Did some internal tests. And corrected the code.

'''''Thursday (1 Aug)

Segregated pix, bw from fileformat.c file. Added new flags and thus
modified my previous work on operations and icv_math.h Completed source
tree syncing.

'''''Friday (2 Aug)

Revisited to scale and shrink. Corrected pixshrink and bwshrink
utilities. Went out for TAX registration. Could not do much work. Will
make up on sunday.

'''''Saturday (3 Aug)

Implemented bilinear \[binterep(..)\] and nearest neighbour
interpolation \[ninterep(..)\] in sync with current format. Also added
BOX Average shrinking \[shrink_image(..)\] and under sampler
\[under_sample()\]

### Week 8

'''''Monday & TUESDAY (5th and 6th Aug)

-   Did Code cleaning. Visited my university regarding final year
    thesis. Now everything is set.

<!-- -->

-   Will Start working at a better pace from tomorrow. Targeting this
    week's deadline of groups.

'''''Wednesday to Sat (7th to 10th Aug)

-   **bw_save and pix_save** :- Modified such that now they can write
    to stdout or pipes refering to them
-   **bw_load and pix_load** :- modified such that now they can read
    from stdin or pipes.
-   **pixscale and bwcale** :- Doesnt show ioctl error now.
-   **bwrect** :- Converted a model for using libicv in the utilities.
-   **decimate** :- created a wrapper function namely icv_resize to
    handle the resizing functionality.
-   **stat** :- implemented mode, median, skew and variance
    functionalities.

### Week 9

'''''Monday (August 10)

-   modified bw_read and pix_read such that it can read from stdin and
-   Modified bw_read and pix_read such that it could save to stdout.
-   These two modiciations are useful for writting and reading images
    to/from pipes
-   Did some codecleaning by correcting messages.

'''''Tuesday (August 11)

-   Started converting utilities to use icv library.
-   Converted bwrect to use icv library.
-   Also leart bu_getopt and other function to handle the operators

'''''Wednesday (August 12)

-   Improved the nomenclature of icv library as per the mentor's advice

1.  icv_save -&gt; icv_write
2.  icv_load -&gt; icv_read
3.  icv_free -&gt; icV_destroy

'''''Wednesday (August 13)

-   Had discussions on IRC regarding the fate of the utiities. And other
    utilities option.

'''''Thrudsay (August 14)

-   corrected the documentation of bwrect as per the new modification.
-   Incorporated the use of icv in pixrect.
-   Wrote the docs for pixrect for icv.

'''''Thrudsay (August 15)

-   Added routines to read/write dpix images.
-   Also created icv_normalize function to handle the dpix images.

'''''(August 16 - August 22)

-   Taken a break for holidays. Independence day and RakshaBandhan

### Week 10

'''''August 23

-   Made provision for bw-pix to use libicv.
-   Pixfade also uses libicv.

'''''August 24

-   Reduced parameters of rgb2gray. This now takes the weights and the
    color combinations.
-   Added few macros for icv to covert rgb images into gray images using
    the standard weights.
-   Put some brain on the error related to sextic polynomials. Helped
    Izak_ (on IRC) to correct it.

### Week 11

'''''August 25 & August 26

-   icv_filter didnt take care of the boundaries till now. Finding a
    solution to correct this behaviour.
-   Also had a discussion related to minimal changes.

'''''August 27

-   Modified icv_filter to preserve boundary condition.
-   Incorporated libicv in bwfilter app. This now has an option to
    output to a specified file name. Also pipes can be handled.

'''''August 28

-   Encountered error in regress due to the latest changes in pix-bw
    utility.
-   Looking at regress and trying to study its functionality.

'''''August 29

-   Updated the man page of bwfilter with recent changes in libicv.
-   Added verbose in bwfilter as per the previous usage.
-   Added offset and kerndivision flag options in bwfilter.
-   Wored out the regress error. Also there was an error with expr in
    the regress. Helped in finding that out.

'''''August 30 and August 31

-   Improved bw_read and pix_read to read images without specifying
    the image size. Also updated the docs.
-   Used this improvement in pix-bw. Also changed at the instances
    pix-bw is used.
-   did some code cleaning in color_space utilities, bw-pix.

### Week 12

(Exam Week at home institute.)

-   Updated and restructured the mannual page for pix-bw

<!-- -->

-   Created a list of doubts in development of libicv. Had an
    informative discussion with Sean (brlcad) on irc related to
    development and task left for completion. Added all the points in
    src/libicv/TODO.
