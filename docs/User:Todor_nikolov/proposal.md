## Personal Information

------------------------------------------------------------------------


Name: Todor Nikolov

Email: tosemkd@gmail.com

IRC name:todor_nikolov

### About Me


I am a student in my 3-rd year in computer science and engineering, at
the faculty of Computer Science and Engineering in Skopje, Macedonia.

The focus of my studies is parallel programming and high performance
computing, also I have a fondness for embedded systems and low power
computing.

Along side this I also take classes in computer graphics and animation,
partly because it is connected to the previous fields, but mostly
because it is fun and quite challenging.

<!-- -->


My hobbies include gaming and learning new ways to torture all the
processors in my PC. :D

### Previous Experience

:\*2 months working on a social network as part of an internship,
february-march 2013 , in this project I used php with the codeigniter
framework, my tasks were implementing the messaging system and
configuring sphinxsearch to match the requirements of the design.

:\*A small app in android as part of a teamwork class, its still work in
progress.

## Project Proposal

------------------------------------------------------------------------

### Project Title


BRLCAD Raytracer library optimization

### Brief project summary


Currently most of the optimizations in BRLCAD's raytracer library are
based around the low level math libraries, the space partitioning of the
scene, and possibly the primitive detection functions. Also there is
already an extensive performance measuring and data collecting framework
in the application itself.

The first half of the project will be dedicated to determining
optimization opportunities and exposing them through documenting and
aiming tests at them, to help others involved in the project notice
them. The second half will be aimed at implementing some of these
optimizations and testing their feasibility and success.

The analysis and optimizations I plan are not only meant to provide
immediate benefit, but also support and promote further speedup and
porting to other technologies like GPGPU.

### Detailed project summary


The raytracer in brlcad calculates around 100k-1M rays/sec meaning a
render on a current screen (1920x1080) takes 1 - 15 seconds. The new
archer editor supports much quicker edits, meaning having a quicker
response by the renderer will improve the workflow and feel of the
application.

<!-- -->


The other use of the raytracer is queuing multiple traces in a script
file for the purpose of either animation or multi-view rendering can
take minutes to hours depending on the complexity of the scene and the
amount of frames taken.

<!-- -->


There are endless possibilities for the scope of the optimization, but
the most promising are:

-   Bundling rays in groups to reuse static data and enable
    parallelization.
-   Split raytracing routine to enable pipelining.
-   Locating pipeline hotspots and tighten their execution.
-   Research algorithms used in said hotspots and try to find and
    eliminate unnecessary computations.
-   Find and remove expensive and unpredictable operation like memory
    allocations on fast paths.

### Deliverables

:\* Graphical analysis and paper of the current state of the project
with additional scripts meant for testing and benchmarking separate
parts of the library

:\* Coding several optimization in the raytracer or object intersection
functions

:\* or preparing the pipeline for the purposes of further optimization
and possible porting to GPGPU

### Timeline

:\*May 15 - June - 10 - Analysis of code, getting familiar with
interacting with the program and creating test scripts and benchmarks.

:\*Rest of June - Finishing the Report on the current state of the
program, and building a prototype/ first optimizations being finished.

:\*July 1 - July 15 - Testing of code and removing bugs introduced in
the pipeline

:\*July 15 - August 15 - Iterating on what has been done so far, or
working on other parts of problem.


Basic principles that I will follow during this project:

-   Steer based on intuition, Do based on numbers.
-   10% increased code complexity defeats 10 times speedup
-   Document before doing, report after doing
-   Stay in contact, stay commiting

### Plans after finishing this program

:\#Rest and Relaxation

:\#Examining the current state of raytracing and possible research in
this field as part of graduation paper. Implementing that research as
part of an existing open source project is not out of the question.

### Why me

I have deep and intuitive knowledge of current CPU-SIMD and GPU
architecture, as well as their memory subsystems and their influence on
code execution speed. I also know how to identify code structures that
can be barriers to parallelization and speed even if they seem like
improvements.

### Why get involved in open source

I have always wanted to get involved in open source, even before
starting my studies. But up until now, my lack of experience and
confidence in my skills as well as my life situation prevented me from
making the commitment necessary for fruitful engagement in open source
projects.

### Why you

You have a complex and promising software that gives me a chance to
learn more about graphics, and programming than anything I have
encountered before. Also you have a good documentation and structure I
feel will help me fit in fast.