# Reports

## Week 13 (August 15th to August 22th)

1.  Used BCP tool to compress Boost to \~50MB (svn version is \~ 100MB)
2.  Wrote a script that compiles the bundled libraries (except LLVM,
    which we assume to be already instlled)
3.  Tests made on different machine (Ubuntu 10.04) is crashing when
    running the oslc application from OSL.

## Week 12 (August 8th to August 15th)

1.  Started adding osl dependencies to a separated svn repository.
2.  Added ilmbase, openexr, oiio and osl, though boost and llvm
    libraries are too big to be added (\~500MB and \~250MB
    respectively).

## Week 11 (August 1st to August 8th)

1.  Implemented a multi-sample mode (similar to increasing mode, but it
    keeps the average of the sampled pixels and always uses full
    resolution)
2.  Implemented a random shoot mode, but it seems there's a bug with
    rendering in unbuffered mode
3.  Investigated the bug with the unbuffered mode, still without
    success.

## Week 10 (July 25th to August 1st)

1.  Studied OSL code in order to discover how to use it with a ray
    tracer.
2.  Implemented a simple mode for ray tracer, but I don't know how to
    add reflection and refraction to it. I intend to come back to it in
    the future.
3.  Studied BRL-CAD code to design the new framebuffer mode (similar to
    incremental).

## Week 9 (July 18th to July 25)

1.  \[19/07\] Implemented a basic texture shader written in OSL.
2.  \[20/07\] Stopped using the hypersampling option (-H) and added a
    loop in the sh_osl to avoid shooting the same ray many times.

## Week 8 (July 11th to July 18th)

1.  Implemented a thread-safe version of sh_osl, though no advantages
    were being taken from parallelism.
2.  Studied some OSL code to figure out how to use it with multiple
    threads
3.  \[07/18\] Implemented a new thread-safe version of sh_osl with less
    blocking.

## Week 7 (July 4th to July 11th)

1.  Wrote a small tutorial on how to use OSL in BRL-CAD
    ([link](User:Kunigami/GSoc2011/OSL_Tutorial "wikilink"))
2.  Ported BRL-CAD cloud shader to OSL
    ([screenshot](http://dl.dropbox.com/u/1399996/GSoC/RT_OSL_cloud.png))
3.  Ported BRL-CAD checker shader to OSL
    ([screenshot](http://dl.dropbox.com/u/1399996/GSoC/RT_OSL_checker_glass.png))
4.  Implemented support for group of shaders

## Week 6 (June 27th to July 4th)

1.  Implemented support for reflection and refraction in the OSL Shader
    that is used by rt
2.  Implemented support for refraction in the stand alone application
    that uses BRL-CAD shooting system to render BRL-CAD scenes with osl
    shaders
    [screenshot](http://dl.dropbox.com/u/1399996/GSoC/OSL_RT-Refraction-Corrected-2011-06-30.png)
3.  Started getting errors due to different version of libpng. BRL-CAD
    uses 1.4 and OIIO used 1.2. Recompiled OIIO to use 1.4 and the
    problem was solved.

## Week 5 (June 20th to June 27th)

1.  Implemented an osl shader, which seems not to give correct results
2.  Implemented a stand-alone application to render BRL-CAD scenes with
    OSL shaders
    [screenshot](http://kuniga.files.wordpress.com/2021/06/osl-rt-2011-06-25.png)

## Week 4 (June 13th to June 20th)

1.  Discovered that the crashing was due to multi-threaded issues. I'm
    currently using -P 1 on my tests.
2.  Re-defined the OSLRenderer interface, so that it considers recursion
    rays needed for reflection and transmission
3.  Start studying how the rt application works.

## Week 3 (June 6th to June 13th)

1.  Adapted the OSL raytracer so that it can be called by the osl
    shader.
2.  The rt application is currently crashing. Inspecting with valgrind I
    suspect that it is due to memory leaks.

## Week 2 (May 30th to June 6th)

1.  Not very productive week. With the help of the mentors I managed to
    solve the compile error.

## Week 1 (May 23th to May 30th )

1.  Implemented a (poor) polka dot for BRL-CAD, to get familiarized with
    the shaders syntax. [polka dot
    goblet](http://kuniga.files.wordpress.com/2021/05/goblet1.png)
2.  Trying to compile the OSL raytracer outside OSL build, but getting
    compile errors, that I have no idea on how to solve. I've emailed
    the dev list asking for help.

## Week 0 (Community Bonding)

1.  Compiled OSL sources both in Ubuntu 10.10 and Mac OS X Snow Leopard.
    (had trouble with 11.04, mainly due to LLVM)
2.  Found a raytracer developed by Erich Ocean and Brecht
    [1](https://groups.google.com/forum/#!topic/osl-dev/B-JrY8KBo7I/discussion)
    that uses OSL-written shaders. It currently renders refraction
    wrongly.
    [screenshot](http://kuniga.files.wordpress.com/2021/04/image2.png)
3.  Discovered the cause of the above error: I was using the wrong
    shader for glass. Now, the image is correctly rendered.
    [screenshot](http://kuniga.files.wordpress.com/2021/04/testrender_closures_fixed_refraction.jpg)