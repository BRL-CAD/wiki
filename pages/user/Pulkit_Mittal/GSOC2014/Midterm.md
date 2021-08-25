# Making Step Libraries Thread Safe

## Brief Progess Report

I have been working on making the Step Libraries thread safe as a part
of Google Summer of Code program. The libraries which I have targeted
are (in the following order)

-   *cllazyfile*
-   *clstepcore*
-   *cleditor*
-   *cldai*

I am done with making *cllazyfile* thread safe. I also have covered
around 6K lines of codes of *clstepcore* library.

Considering the fact *cllazyfile*, *cleditor* & *cldai* all contain on
avg \~3K lines of code and *clstepcore* contains \~17K lines of code. It
can be safely said that I am 35% done with the thread safe objective.
Its clear that I am lagging behind (ideally it should have been around
50%), but my progress is not disappointing either.

## Work Done

Most work uptill now has been done by using a (Test-Driven Development)
TDD approach. Under this approach I create a test first and in it invoke
the features I wish to make thread-safe. Sometimes the classes /
functions are very small or the change require to make them thread-safe
is trivial. In such cases to save time I don't follow the TDD approach
and I directly jump to the development part.

### Testing Methodology

Each of my unit test checks multiple features of a class for
thread-safety. For a particular feature, the unit test typically consist
of 3 parts.

1.  An instance of the class is created. The feature/s (same or
    different) to be checked are called twice in serial manner.
2.  Another instance of the class is created. This time the feature/s
    (same or different) to be checked are called in parallel by
    different threads, with the same load as in step 1. The load is
    kept-heavy so that the operations by the two threads overlap in time
    domain.
3.  Both instances are compared for any disparity. Harmless differences
    like order of occurrence, of various entities inside the data
    structures, are ignored. For checking the internal data structures,
    already available public API's are used. However wherever needed new
    API's have also been created for this purpose.

The step 2 & 3 are repeated multiple times. If a disparity is found it
is immediately reported and the check fails.

### Development Methodology

The features which were targeted were the public APIs. *e.g.* For
cllazyfile library the functions of the class *lazyInstMgr* were
targeted as it was the only class which was meant to be visible to the
user of that library. The code changes can be roughly divided into 2
parts.

##### Pre-Processing

This part mainly consist of code refactoring. These changes by
themselves do not make the code thread safe, however they make the job
of making code thread safe much easier. No mutex (or equivalent) is
invoked in this part. Couple of examples where I needed preprocessing
are:

-   *gennodelist* and *gennode* classes: This link-list structure was
    difficult to make thread-safe in its original form. This was because
    an operation on one node could change the state of another node. The
    classes were modified so that a node could modify state of another
    node only through its parent list.
-   ExpDict.h/.cc/.inline.cc files: These contain multiple classes which
    were similar and not thread-safe. Hence another class was created
    which would contain all the features and act as superclass. Now only
    this new superclass was needed to be made thread safe. Lot of
    duplicated code was removed this way.

##### Thread-Safety

A feature could be thread-unsafe due to the following reasons.

1.  It does file I/O.
2.  It modifies the state of a thread-unsafe data structure / counter.
3.  It modifies the state of multiple data structures / counters which
    should be consistent at all time.
4.  It provides a reference to a read unsafe data structure to the user.

For 1. & 3. the only way out was using fat lock. For 2. I had an option
of using a fat-lock or making the structure itself thread safe. I chose
the latter in cases where many classes were taking dependency on the
same data-structure. Structures described in 4. were found in
*cllazyfile* library. Whenever such a feature was invoked, clones of
that data structure were made.

For locking either a *std::mutex* or a *std::recursive_mutex* was used.
The changes also included invoking the HAVE_STD_THREADS macro in the
cmake files.

### The Grey Area

I started this project with literally no knowledge of *cmake* files. But
in-order to compile my changes I had to modify some of the existing
cmake files. Unlike my C++ coding, I am not very confident about these
modifications. They should be looked into carefully in future before
merging the branches.

## Amount of Coding Done

I regularly commit my code to
[*hj/thread-safety*](https://github.com/stepcode/stepcode/tree/hj/thread-safety)
branch in the github repository. One can see my changes
[here](https://github.com/stepcode/stepcode/compare/hj/thread-safety#files_bucket).
In short I have modified / added 43 files, done 1949 additions and 622
deletions. About 1100 of the additions are due to new unit tests. To see
my daily logs do visit [logs](logs/md).

## The *Other Works*

Apart from participating in GSOC this year I am also doing the following
work.

-   M-Tech Project: I also started M.Tech Project this summer. I am
    continuing the work started by a senior. In order to prevent my work
    from getting monotonous I switch back and forth between my M.Tech
    Project and GSOC Project (giving 85% of the time to the latter). I
    will have a kick-off meeting on July, 3rd with the company which is
    funding my project.
-   TA'ship: Since I was staying in the college for summers, I opted for
    being a TA in one of the summer courses. Its a nice experience.
    However the TAship duties demand 4-5 hrs of my working time on
    Wednesdays. The summer course will end by July, 10.
