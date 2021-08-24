## Personal Information

**Name:** Pulkit Mittal
**E-Mail:** *bhangarval@gmail.com*
**IRC Nick:** *hoiji*
**GitHub:** *hoiji09*

## Project Introduction

### Project Title

STEP Libraries: Improving thread safety and performance

### Motivation

*STEP* is the current standard for exchange of *CAD data* between
different software packages. A *STEP-File* (also called Part21 file) is
the most widely used data exchange form of STEP. Part21 files may be
very huge (hundreds of Mb). These files are known to be heavily resource
consuming (in terms of computing time or memory consumption) when being
imported. The computing time taken by the processing of such files can
be significantly reduced by using multi-thread programming techniques.

However before incorporating multi-threading into the STEP-Libraries we
must ensure that the libraries are thread safe or else we might run into
data races which are hard to debug leading a detrimental impact on
development.

### Project Summary

The Project can roughly divided into 3 major tasks. A detailed
description of each is given in the following sections.

**Improve Thread Safety:** This is the first priority for this project.
Starting with *cllazyfile* STEP library, I would introduce thread safety
in the *cleditor*, *clstepcore* & *cldai* respectively in that order.

**Introduce Multi-threading into the STEP Libraries:** This task is
highly dependent upon the first task. Once the concerned library has
been deemed to be thread safe, we can start taking advantage of it to
boost performance. As a proof of Concept, I intend to at-least one
multi-threaded task.

**Performance Tweaks in Single Threaded Code:** This is a kind of a
filler task. Since the 1<sup>st</sup> task would involve going through
and understanding the code written in the aforementioned libraries. I
would use that opportunity to point out, discuss and implement small
tweaks which would increase the performance of the single threaded code.

## Improve Thread Safety

### Approach

The STEP Class Libraries consist of around 20K lines of code. I will
first scan through the Documentation and ReadMe files and then review
the code. This will help me figure out what resources could be possibly
be shared by multiple threads. Once I have found the critical data /
global variables, it would be easy to find critical sections and apply
appropriate locking or other means of mutual exclusion. This also
includes spotting calls to library functions which are thread unsafe and
moving to their thread safe counterparts. Using mutexes would be the
last resort. All changes to the code will be well commented, the major
ones would also be documented. Care will be taken to take dependencies
on only those C++ libraries which are supported by MSVC as well.

**Shared Resources:** Apart from the *std containers*, the STEP Library
also take dependency on resources (*i.e* data structures) defined in
*src/base/judy/\** & *src/clutils*. In order to improve thread safety
without hitting performance, some knowledge of the thread safety
properties offered by the by the above data structures will be needed.
Some examples of the utilization of such information are as follows.

-   **Judy Arrays:** A Judy Array is a data structure that has high
    performance, low memory usage. They are extensively used in lazy
    loading. The lazy loading code itself is designed to help avoid
    using huge amounts of memory unless there is an actual need to map
    various properties in *lazyInstMgr.h* (Lazy Instance Manager). They
    are neither *concurrent read safe* nor *concurrent write safe*. In
    order to make a judy object concurrent write safe a mutex need to be
    allocated. The same can be done to make the judy object thread safe
    for concurrent read accesses. But this is bound to hit performance
    in cases where the Judy-Array is used as read-only object once it
    has been initialized. An alternative way to support concurrent read
    access would be by cloning the Judy object with *judy_clone* for
    use by each thread.
-   **STL-Containers:** STL containers like vectors are used in various
    places inside the code. These are concurrent write unsafe but
    concurrent read safe. Thus, they will need mutexes similar to
    read-write locks.

**Creating Unit Tests:** Since all the existing units tests are for a
single threaded code, I will create new tests which will spawn multiple
threads to check the thread safety of libraries. This can be done by
asking the threads would to read/write files in different threads
simultaneously. These test will help me identify any deadlocks or
data-races that might have crept in the code. Further, these test will
be of use to any future developers too.

### Initial Progress and Findings

-   Introduced myself and discussed about the project in the *scl-dev*
    mailing List and the *\#stepcode* IRC channel. (IRC is a savior. I
    realized that it is the quickest way of communicating with fellow
    developers.)
-   Forked the stepcode project on github to my handle and cloned it on
    my local machine.
-   Gone through the source code of *src/cllazyfile*. I have read the
    appropriate documentation of the *src/cleditor* to get a fair idea
    of its functionality.
-   Read about thread safe properties of *judy arrays* and *std
    containers*.

### Deliverables

-   Modify STEP Class Libraries for a more readable, maintainable and
    *thread safe code*.
-   Modify the Documentation to reflect any major design changes
-   Wherever required, Unit Tests will be made for checking thread
    safety.

## Multi-Threading Speedups

### Approach

Once I have finished *part one* of the project, I can start making STEP
Libraries multi-threaded. Their could be possibly many ways of improving
performance by taking advantage of multi-threading. However as ensuring
the *thread safety* can potentially take the majority of the GSOC
duration, I plan to implement only one feature which would demonstrate
the advantage of using multi-threading in lazy-loading. If time permits
I can try adding other multi-threading features as well. For every
feature I add there will be appropriate documentation and unit tests.

### Deliverables

-   **A Module for Parsing and Processing data in different threads:**
    Multi-threading can be used in Lazy-Loading by reading a file in one
    thread and storing the related data into in-memory structures using
    another thread. This approach might even improve performance on a
    single processor.
-   ***(If Time Permits)* A Module for Creating Multiple objects in
    Parallel:** This module would take a list of objects as input and
    create multiple in-memory objects for each in parallel. This would
    especially increase performance on a multiprocessor leading to
    quicker loading.
-   ***(If Time Permits)* A Module for Loading Multiple Files in
    Parallel:** This could benefit some upcoming STEP capabilities such
    as the use of External Element References\[1\] to some entities in
    separate STEP files. So loading these files in parallel and
    supporting the references between them would increase performance of
    those applications that will take advantage of this capability.

## Performance Tweaks in Single Threaded Code

### Approach

This involves identifying inefficiencies in the code and and discussing
them with my mentor. If I am not behind schedule I would also implement
small patches which would remove the inefficiencies and increase
performance. This part of the project I plan to do concurrently with
*part one* of my project. As *part one* involves lot of reviewing of the
code, this will increase my familiarity with the code. Also I intend to
run and profile some already made tests which will help me identify the
bottlenecks.

### Initial Progress and Findings

-   I have made a small modification the lazy-loading module. The code
    has been merged with the main code and gives a 1.5x speedup in
    lazy-loading. The main idea for the modification was to buffer an
    already read data in one portion of the code. This buffer prevents
    the reading of the same data from the disk twice.

## Time-Line

### Availability & Commitments

-   **Pre-GSOC:** My college semester ends on 12<sup>th</sup> May. As
    this period would also require a good amount of commitment towards
    my college activities (tonnes of assignments, projects and exams). I
    will be able spend only around 10-20 hours a week on an average to
    prepare for my GSOC project.
-   **Early/Mid-GSOC:** My summer vacations would last till
    20<sup>th</sup> July. As I have no prior-commitments during this
    period, I will able to spend around 45-55 hrs per week on my GSOC
    project. In case I find that I am lagging behind, I am willing to
    spend up to 70 hrs per week for the project.
-   **Late-GSOC:** After my college reopens on 21<sup>st</sup> July,
    up-till the GSOC pens down date *i.e* 18<sup>th</sup> August, I will
    be able to spend 35-45 hrs per week on the GSOC Project.

### Milestones

-   **Current - April, 15:** Review the source code of *src/cllazyfile*,
    test the single threaded version and start working towards making it
    thread safe.
-   **April, 15 - April, 30:** Thread safety for *src/cllazyfile*. (As
    mentioned before, making Unit Test to check thread safety is
    implied)
-   **May, 1 - May, 12:** College Exams!!
-   **May, 13 - May, 26:** Thread safety for *src/cleditor*.
-   **May, 27 - June, 30:** Thread safety for *src/clstepcore*. I may
    have to give a large time to this library as it is huge!
-   **July, 1 - July, 10:** Thread safety for *src/cldai*.
-   **July, 11 - July, 31:** Implement multi-threading in lazy-loading.
-   **August, 1 - August, 18:** Buffer.

## About Me

I am a 4<sup>th</sup> year *Dual Degree CSE* student studying in *Indian
Institute of Technology (IIT) Delhi, India* (UTC+05:30). (Dual Degree in
IITD is a 5 year course, in which students obtain their Bachelor’s as
well as their Master’s degree in Technology in the area of Computer
Science and Engineering.)

### Skills

**Programming:** I have coded a lot in *C, Java, Perl, Bash and PHP*. I
am also familiar with *C++, C\#, Python, SML, VHDL*. I have used
open-source softwares such as *svn, gdb, llvm, gprof, qemu* etc.

**Interest Spectrum:** My interest spectrum is quite large and varies
from software systems (multi-threading, concurrency bug analysis,
compiler optimizations, security) to hardware-software interface
(multiprocessor programming, high performance architecture). I never
miss a chance of making my program more efficient (in terms of computing
time) and later brag about it!

### Major Coding Experiences

**Internship:** In summer 2013, I did an internship at *Microsoft, India
Development Center, Hyderabad*. The team to which I was assigned to
there, was impressed with my work and even extended me an offer of
joining them as a Full-Time employee once I have completed my degree!
(*i.e.* in 2015).

## Miscellaneous

### Why Us?

Frankly, I was searching for a open source project in which I could put
my experience with multi-threaded programming to practical use. Thats
how I spotted the STEPCode project of ensuring thread safety and improve
performance. Owing to the friendliness of my potential mentors, their
quick and encouraging responses to my queries, I got started on my
project in no time. I have learnt lot about open source programming from
the comments of the people who reviewed my patch. This STEPCode project
nicely fits into the my interest domain. It gives me an opportunity to
polish my multi-threading concepts and learn about the caveats
associated with them. Also I believe the prospect of increasing
performance of the code (via single thread tweaks, multiple threads)
would increase my motivation further!

### Why Me?

-   Thread Safety is an intricate topic, and through my experience I
    know how painful it is to debug data-races. I will make sure that no
    fellow developer who takes dependency on STEP Libraries faces that!
-   I agree that I can make mistakes, but am I willing to learn from
    them.
-   I have some experience in dealing large code-bases (courtesy
    assignments, internship), but since this is the first time where I
    will be contributing to an open source project, I am very
    enthusiastic about it.

# References

\[1\] <http://www.cax-if.org/documents/rec_prac_ext_ref_v21.pdf>