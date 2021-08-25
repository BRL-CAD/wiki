# Development Logs

## Community Bonding Period

-   Compiled working version of BRL-CAD with OpenCL on Ubuntu 18.04
-   Got familiarised with the MGED commands and the sequence of code
    being called from the build
-   Checked out other primitives which have been parallelized and their
    structure

## Weekly update

-   Week - 1 (June 1 - June 5)
    -   June 1: Working on getting ARBN primitive parallelized via
        OpenCL
    -   June 6: Submitted patch for review (June 6)
-   Week - 2 (June 8 - June 12)
    -   June 8: Working on getting PIPE primitive parallelized via
        OpenCL
    -   June 9: Worked on discont_radius_shot() function
    -   June 10: Worked on bend_pipe_shot() function
    -   June 12: Worked on linear_pipe_shot() function
-   Week - 3 (June 15 - June 19)
    -   June 15: Worked on pipe_start_shot() and pipe_end_shot()
        function
    -   June 17: Assembled all in pipe_shot() function
    -   June 19: Fixed a few bugs in pipe_shot() file
-   Week - 4 (June 22 - June 26)
    -   June 22: Submitted the PIPE patch file in sourceforge
    -   June 23: Started working on Dispalcement Map primitive
    -   June 24: Worked on dsp_in_rpp() function
    -   June 26: Worked on recurse_dsp_bb() function
-   Week - 5 (June 29 - July 03)
    -   June 29: Got stuck in recurse_dsp_bb() function
    -   July 1: First Evaluation Feedback

// Kept DSP primitive on hold owing to it's complex structure. Once I
get used to the simple primitives, I'll be in a better position to work
on DSP primitive. Hence, have kept it for the last month.

-   -   July 3 : Started working on Volume primitive

-   Week - 6 (July 6 - July 10)
    -   July 6: Completed rt_vol_shot() and rt_vol_norm() function
    -   July 8: Resolved few bugs
    -   July 9 - 10: Took a break for travelling to hometown owing to
        Covid-19

-   Week - 7 (July 13 - July 17)
    -   July 13: Submitted patch for Volume primitive
    -   July 14: Started working on Metaball primitive
    -   July 15: Converted secondary function:
        rt_metaball_point_value_iso()
    -   July 16: Converted secondary function:
        rt_metaball_find_intersection()
    -   July 17: Implemented rt_metaball_shot() in metaball_shot.cl
        file

-   Week - 8
    -   **July 20**: Completed rt_metaball_norm() function. Read about
        the inline functions being used here and it's possible
        counterpart and usage in OpenCL. I think I'll merge
        rt_metaball_norm_internal() into the norm method.
    -   **July 21**: Seems like there were two versions of the
        algorithm, only one of which was being used. Have removed the
        old version code from metaball_shot.cl file to remove
        redundancy.
    -   **July 22**: Submitted metaball primitive here:
        <https://sourceforge.net/p/brlcad/patches/548/> . I made a typo
        mistake while developing a patch, I've resubmitted it. Use the
        latest patch in comments section. Onto EBM primitive now!
    -   **July 23**: The -z flag worked FINALLY! I though of giving it a
        try once again today and it worked. I'd to change the
        FindOpenCL.cmake file locally to ensure it catches the correct
        path of OpenCL directory. This has indeed solved a big problem
        of mine. I'll revisit the previous patches now and update them
        accordingly. Will also include a detailed documentation of the
        commands and resolution of the errors I faced for future
        reference soon.
    -   **July 24**: Submitted patch for FindOpenCL.cmake file here:
        <https://sourceforge.net/p/brlcad/patches/549/> . Debugged the
        ARBN primitive patch files to remove the compile-time errors and
        typos! Moved on to VOL primitive, couldn't find relevant
        rendering command.

-   Week - 9
    -   **July 27**: Debugging METABALL primitive. Looking into
        plausible ways of passing extra parameters r_min and r_max
        from metaball_shot() to its rt.cl declaration.
    -   **July 28**: While compiling previously converted primitives
        like ELL and ARB8, I got compilation error - "failed to set
        OpenCL kernel arguments". On running the code, I found a bug in
        master branch itself. There was a mismatch between uchar2 and
        uchar3 in clt_frame() function in primitve_util.c and all it's
        related functions. I've updated the code, will include a patch
        for this. All primitives are rendering successfully now! Yayyyy!
    -   **July 29**: Submitted patch for the above bug resovled here:
        <https://sourceforge.net/p/brlcad/patches/551/> . Moving on to
        removing errors in PIPE primitive. Most of the compile time
        errors were related to Global-Private conversion, hence made all
        struct inside functions global as well. It is now compiling
        error-free but not rendering. Gotta deep dive more!
    -   **July 30**: Looking for possible options to print inside OpenCL
        kernel to see where it might be failing. Can't find any
        previously converted primitive with bu_log in it. Maybe, I'll
        import bu.h and give it a try!
    -   **July 31**: Worked out communication issues with Sean and came
        up with a measurable criteria going forward. Going to be
        chatting progress a lot more going forward in Zulip! Also,
        documented the details of issues I faced in Dev Logs for future
        reference. With this evaluation, the second month of the GSoC
        comes to an end. Onto the final phase now!

-   Week 10
    -   **August 3**: Took a break owing to some personal work!
    -   **August 4**: While checking CLINE primitive patch for
        debugging, I found it's shot function was missing. That being my
        first patch, I might have missed out on doing "svn add" of that
        cline_shot.cl file. Will have to redo again.
    -   **August 5**: Completed the cline primitive conversion, looking
        for documentation for making this in MGED window so that I can
        render and test if it is working as expected. Couldn't find any
        proper documentation for this!
    -   **August 6**: Trying to see best practice to import/define
        bn_distsq_line3_line3() in the OpenCL version of this from
        libbn repository. Found out that for making cline primitive in
        MGED, "in" command doesn't work. We have to use "make" command
        for that purpose. The full command would be "make cline.s
        cline".
    -   **August 7**: Defined the bn_distsq_line3_line3() in rt.cl
        and used it in cline_shot.cl . It is now compiling error-free.
        I've updated the patch with latest code. Tried using printf
        command, but the rendering gets stuck somehow because of it.
        Gotta deep dive more!

-   Week 11
    -   **August 10**: There seems to be some issue in memory allocation
        pieces of code. Since printf command was not working, I'd a
        tough time narrowing it down. I'm trying with the simplest of
        the primitive now - SUPERELL to find out more about why
        previously present primitives are rendering and newly converted
        one aren't!
    -   **August 11**: Giving printing in OpenCL another try for
        debugging purpose. Converted bu_log() in rt.cl to see if it
        works. No progress! Including stdio.h header in _shot.cl gives
        "stddef.h file not found" error.
    -   **August 12**: The Superell patch is not rendering, though it
        was one of the simplest one. I think I am missing out on
        something trivial but can't figure out what. I want to re-do
        SUPERELL primitive from scratch.
    -   **August 13**: Turns out, I missed one variable while passing it
        from .c file to .cl shot file - variable 'n'. It is now
        rendering, although not exactly the same. Gotta ask Sean on
        this!
    -   **August 14**: Documented here in the wiki logs all MGED
        commands to render various primitives for future purpose.

-   Week 12
    -   **August 17**: I'm unable to make superell primitive with "in"
        command. It throws error:
        rt_db_external5_to_internal5(superell.s): unable to import
        non-BRL-CAD object, major=255 minor=35 . Deep diving into this
        for possible bug. It is accepting none of the abc/ne parameter
        values. Even with e=n=1 where it should form Sphere or ellipsoid
        with n=2.
    -   **August 18**: That seemed to be a random error. I cloned a
        fresh repository and started again. The C rendering of the
        Superell worked with normal parameters. Don't know why it didn't
        work in previous repository. No luck with _shot.cl file though!
    -   **August 19**: Gave HYP primitive a try as well. This is also
        one of the simpler primitive to work on. And it worked. Both the
        C and OpenCl renderings of the primitive match and with better
        performance in OpenCl. Hurrray!
    -   **August 20**: Submitted the patch for HYP primitive here:
        <https://sourceforge.net/p/brlcad/patches/553/> . Moving back,
        it seems I'm facing issues with memory allocation in OpenCL
        versions of other primitives I worked on which is why they don't
        render as expected. Looking into possible solutions!
    -   **August 21**: Did a quick pixdiff to ensure both the renderings
        are similar or not. Couldn't understand the usage of pixdiff in
        BRL-CAD MGED terminal, so tried via OpenCV package in python.

-   Week 13
    -   **August 24**: It is officially the last week of GSoC. Gotta
        devote my time in documentation and logging details for future
        references. Also, turns out, we can hit pixdiff command in the
        way discussed in Issue 4 below.
    -   **August 25**: Started the documentation process. Decided to use
        BRL-CAD wiki instead of Google Doc or GitHub page for this
        purpose. Took screenshots of rendering logs for performance
        measure and the images of primitives rendered.
    -   **August 26**: Ensured all the patches submitted work smoothly
        with the latest version of the BRL-CAD repository!
    -   **August 27**: Working on the final report, using performance
        and testing.
    -   **August 28**: Completed the report, submitted to Sean for
        reviewing!
    -   **September 1**: Nirt command probably needs a more detailed
        looking into. It should ideally have -z flag as well. Will look
        into it later. And so, the GSoC season ends.. Until next time!

## Major Issues Faced

### Issue 1

-   -   **Issue**: -Z flag not working. Initially, I couldn't find
        proper documentation around -z flag and it's usage. I only found
        with command **man rt** that -z is used to compile with OpenCL
        function of that primitive. However, it always said printed
        "Raytrace Aborted" in the logs.
    -   **Solution**: I found that while doing the cmake compiling, it
        couldn't find the OpenCL library and it's version correctly. It
        detected library path as "/usr/" instead of the usual
        "/usr/lib/x86_64-linux-gnu/libopenCL.so" . So, I changed the
        cmake file where it detected OpenCL and submitted patch for
        FindOpenCL.cmake file here:
        <https://sourceforge.net/p/brlcad/patches/549/> . The commands
        are now as follows:

While doing the cmake, add the DBRLCAD_ENABLE_OPENCL flag

    cd brlcad-svn-trunk
    mkdir build
    cd build
    cmake .. -DBRLCAD_ENABLE_STRICT=NO -DBRLCAD_BUNDLED_LIBS=ON -DCMAKE_BUILD_TYPE=Release -DBRLCAD_ENABLE_OPENCL=ON

While compiling a primitive in mged window, use the following command:

     rt -z 1 -o primitive_cl.png

If you pass 0 to the -z flag, it'll compile the C version of the
primitive. So to say, passing 1 to -z flag defines the USE_OPENCL flag
inside primitive function to 1. -o flag outputs the primitive rendering
to an external file in the build folder.

### Issue 2

-   -   **Issue**: Primitives already present in the master branch of
        the repository were not rendering in their OpenCL version. It
        displayed error: "failed to set OpenCL kernel arguments".
    -   **Solution**: I found that the error was due to a mismatch
        between uchar2 and uchar3 data type of variable "o" in
        clt_frame() functions in primitive_util.c file. I made the
        variable uniform to uchar3 in all the places where this function
        was being used and they're now rendering as usual. The patch was
        submitted at the link here:
        <https://sourceforge.net/p/brlcad/patches/551/> .

### Issue 3

-   -   **Issue**: The MGED commands to render the primitives don't have
        a proper documentation. I faced issues while making them so that
        they can render properly because the values for some of the
        variables are highly constrained according to their logic
        implemented. While trying to render, it got "segmentation fault"
        error code
    -   **Solution**: I've started documenting the commands for most
        primitives here in the logs for future reference. I'll keep on
        adding more as and when I find them.

### Issue 4

-   -   **Issue**: Once the OpenCL version renders successfully, I
        didn't know the exact technical methods to follow to ensure both
        the C and OpenCL version are identical.
    -   **Solution**:

Method 1: Both the renderings of C and OpenCL version should look alike.
Check this via rotating in different angles in MGED window. Method 2:
Using pixdiff method.

    cd brlcad-svn-trunk
    cd build
    bin/pixdiff file1.pix file2.pix > out.pix
    bin/pix-png -o out.png out.pix > out.png

The details are in these link:
<https://brlcad.org/~nouhrasofat/man1/en/pixdiff.php> and
<https://brlcad.org/~nouhrasofat/man1/en/pix-png.php> . The images can
be stored in pix format via the -o flag in the MGED window itself!
Method 3: The CPU performance in the logs registered while rendering a
primitive should improve in OpenCL version compared to C version.

## MGED Commands to draw primitives

### ARBN

    in arbn.s arbn 8 1 0 1 1 -1 0 0 1 0 1 0 1 0 -1 0 1 0 0 1 1 0 0 -1 1 0.5 0.5 0.5 1 -0.5 -0.5 -0.5 1

### ARS

    in x.1 ars 4 6 0 0 3 1 1 3 1 -1 3 -1 -1 3 -1 1 3 1 1 1 1 -1 1 -1 -1 1 -1 1 1 1 0 -1 0 -1 -1 -1 0 -1 0 1 -1 1 0 -3 0 -1 -3 -1 0 -3 0 1 -3 0 0 -3

### CLINE

     make cline.s cline

### ELL

     in ell.s ell 0 0 0  0 -1 0  1 0 0  0 0 1

### HRT

     in hrt.s hrt 0 0 0 5 0 0 0 5 0 0 0 5 4

### RCC

     in rcc1.s rcc 0 0 0  1 1 1  0.5

### SUPERELL

     in ell.s superell 0 0 0  0 -1 0  1 0 0  0 0 1 1 3