## Project Title:



STEP LIBRARIES

# Detailed project description

-   Most of my fellow participants are working on how important it is to
    keep your code in working order and adding functionalities to it,
    but hardly anyone ever really cares about keeping the container for
    your code in working order.
-   STEP is the current standard for exchange of CAD data between
    different software packages. BRL-CAD makes use of the NIST STEP
    Class Libraries code to support its step-g converter, but this
    source code was written before many current C++ standard practices
    and libraries were finalized. As a consequence, it needs both
    cleanup and performance enhancements.
-   There is already an existing STEPcode repo at
    <https://github.com/stepcode/stepcode> which needs to be modernized
    and improved.
-   Right now, I am learning about STEP libraries and studing the
    directory.

<!-- -->

-   Improvement is needed for

::\*\*LIBRARY PERFORMANCE

::\*\*CODE MAINTAINABILITY

::\*\*better DOCUMENTATION for the STEP libraries.

::\*\*Resolving some issues

## Library Performance

-   The biggest performance problems are related to reading files.
-   src/cleditor (especially the STEPfile class) contains the old code
    for reading and writing Part 21 files. There are probably some small
    improvements that could be made here, but I'd focus on the newer
    lazy loading code as per Mark's advice.
-   src/cllazyfile implements lazy loading (it scans a file for
    instances, but doesn't load them into memory until necessary). Mark
    Pictor wrote it last fall and winter. It's much faster but there is
    still room for improvement. It works for the files he had tried it
    on, but it doesn't do everything it claims to do. Under his
    guidance, I am willing to work on this problem. We would test it
    much more thoroughly, and some parts would be refactored so that
    unit testing becomes easier (there are violations of the Law of
    Demeter, for example).

## Code Maintainability

-   Duplicate files and functions still exists (like Issue 47 down),
    though most dead code and most inaccurate comments have been
    eliminated.
-   The testing isn't nearly as thorough as it should be, as lcov
    shows - <http://stepcode.org/lcov/> . Ideally, we'd have C++ unit
    tests that would cover everything. As it stands, probably 99% of our
    coverage is from Part 21 files. Tests in C++ would make it far
    easier to locate the source of problems.
-   There are also classes like DirObj that are used, that should
    probably be eliminated.
-   If dead code exists in src/cldai or src/clstepcore, care should be
    taken - most of that code is mandated by STEP Part 22 or Part 23,
    the Standard Data Access Interface.
-   src/clprobe-ui is the remnants of a very old GUI. The only reason it
    hasn't been removed from the repo is that it is an example of the
    use of STEPcode. Hence much attention need not be paid to it.

## Documentation

-   Mark always wanted to write a script using doxygen, and possibly
    doxyassist, to create documentation that is split up logically. Like
    the v0.5 docs (
    <http://mpictor.github.io/scl/0.5/doc.StepClassLibrary/doxygen-html/index.html>
    ), but with fewer tabs - perhaps one for parsing express (express,
    exppp, fedex_plus, fedex_python), one for uses of STEPcode (tests,
    clprobe-ui, SCView, BRL-CAD's stepg
    (http://stepcode.org/stepcode-use-doxygen/dir_d0040508ea657d1100a6aec0fcb59f22.html),
    etc. He hasn't moved past the planning stage. This sounds like
    something I would like to work on. Doxygen has many features that he
    hasn't delved into; some might help us.
-   There are a lot of comments in the code discussing things that
    aren't implemented or aren't implemented completely. I would try to
    make a list of them. If they can be tagged such that Doxygen creates
    a page specifically for unimplemented features, its great.
-   Adding more examples on the stepcode wiki.

## Issues that needs to be solved

-   I went through some issues related to cleanup and part21 and would
    like to contribute fixing them. I am particularly addressing and
    reviewing these issues and help them getting organized-

<!-- -->

-   -   [Issue 227](https://github.com/stepcode/stepcode/pull/227):
        Merge major BRL-CAD SCL changes into stepcode
        -   Very little work to do (in case of any differences only)

<!-- -->

-   -   [Issue 90](https://github.com/stepcode/stepcode/issues/90):
        Statistics from p21read
        -   This issue is almost complete with few things left such as
            counting the instances, doing a few calculations, and
            printing some info near \#L164 of
            src/test/p21read/p21read.cc

<!-- -->

-   -   [Issue 204](https://github.com/stepcode/stepcode/issues/204):
        fedex_plus: add doxygen-style comments to the generated C++
        -   Nothing has been done on this issue. Figuring out how
            fedex_plus and libexpress work can be challenging, and I
            would need some understanding of the EXPRESS language,which
            people claim to be quite different from other languages.
            This might take upon some time.

<!-- -->

-   -   [Issue 197](https://github.com/stepcode/stepcode/issues/197):
        error handling - option to summarize errors in p21read,
        fedex_plus
        -   Nothing has been done on this issue also. Something related
            that can be done is like to have numbered errors, similar to
            how MSVC does it. This would make it easy to sort or search
            the output of fedex_plus. It could be visualized after it
            that P34 would be a parser error or warning, while F12 would
            be a fedex_plus error or warning.

<!-- -->

-   -   [Issue 170](https://github.com/stepcode/stepcode/issues/170):
        STEPfile::MakeBackupFile() is inefficient
        -   This is a trivial issue

<!-- -->

-   -   [Issue 21](https://github.com/stepcode/stepcode/issues/21):
        cppcheck 1.49 issues report
        -   This requires re-running cppcheck. That tool is probably
            better now, and STEPcode has changed considerably since the
            report was generated. There are other tools as well, which
            may report different problems. clang-analyzer is good for C
            but doesn't check C++ thoroughly.
            [Oink](http://daniel-wilkerson.appspot.com/oink/index.html)
            sounds impressive and deserves to be given a try.

<!-- -->

-   -   [Issue 47](https://github.com/stepcode/stepcode/issues/47):
        files with identical name and similar content
        -   This one is the first issue I have started to work and using
            as a tool to learn the basics.
        -   Partially, the work has been done and I have learn a lot
            many things which I was completely unaware of before.
        -   I realized how important is the ability to read and examine
            the ERRORS. I have never encountered the errors related to
            large codebase before. For the next week or two, I will be
            focusing on understanding how to read and interpret the
            errors. I am discussing them with other potential developers
            on IRC and having hold upon it and getting the pattern in my
            mind would be one of the best things I will learn. This is
            the most basic skill upon which I want to have a better
            grip.
        -   Next are the COMPILER WARNINGS which I used to ignore before
            thinking them to be harmless and hence useless. Now, I have
            got a reason to ponder upon if its useless, why is it
            actually there. The compiler wants to drag my attention to
            some syntatically correct but semantically incorrect code
            which might have some logic bug. I will try to figure out
            the reason behind WARNINGS.
        -   Also, I realized that on LARGE CROSS-PLATFORM projects, it
            is not sufficient if checked on just one platform. The code
            should be designed and modified with utmost care such that
            it does work well on other platforms also.
        -   Some terms like call-stack now seem to be familiar. Right
            now I am having an error saying it couldn't look up for
            vtable in the process of linking. I am devoting some time
            nowadays to understand the process of how calls are made and
            linked with libraries.
        -   I also installed a new diff and merge tool MELD to find out
            differences between two similar files and used them for
            diffs between pair of 13 similar files.
        -   In this issue, except for two files, there is almost similar
            set of files in src/fedex_plus and src/clstepcore from
            which the other copy need to be kept and the first one
            should be removed carefully such that the build system is
            not broken at any point.
        -   I have down the differences in that files using MELD tool.
            Now decission has to be taken to untangle calls, replace
            them, move them, delete them or refactor them in the
            clstepcore.
        -   Taken care of 11 similar files. Known about how
            CMakeLists.txt is organized to include necessary headers,
            libraries and executable.
        -   Also, refreshed some concepts about virtual, pure classes,
            friend classes etc. related to cpp.
        -   Learnt and used practically some basics of git- to commit,
            add, remove, push, pull, make branch, switch between
            branches, going back to a commit, setting head, log ,etc.
            Installed gitk and used it.
        -   Taking care of line-endings - CRLF (windows)
        -   Ran the gdb debugger for the first time on such a large
            -codebase. Used command-line uptil today. Now, installed
            KDevelop IDE as it has a nicer gdb GUI wrapper integrated.
        -   Known other GUIs like kgdb,ddd and insight.

## IRC bot

-   Most of the famous IRC channels have a bot which keeps various
    information and provides functionalities like !logs (on \#brlcad),
    !next (on \#gsoc), etc.
-   There exist an IRC channel \#stepcode, but without a bot. No way to
    give some news related to stepcode.
-   Mark and I are planning to have a bot which keeps track of the logs.
-   It would have one more feature of displaying detailed description
    about an issue when typed issue number.
-   For this, till now I have made a bot - STEPbot, which is quite
    hardcoded now with messages on '!test', '!hello', '!areyoubot?' and
    '!bye'.
-   There is one more drawback. It doesn't function 24\*7 . It works
    only when I turn it on. With my going offline, the bot also leaves
    IRC.
-   Hoping to have a superb STEPbot.

<!-- -->

-   Still I am not completely done with this and would be updating this
    proposal as and how I understand and get directions.

# Why Refactoring Is Needed ?

-   Poorly designed code usually takes more code to do the same things,
    often because the code quite literally does the same thing in
    several places. By eliminating this duplicates, we ensure that the
    code says everything once and only once, which is the essence of
    good design.
-   Mostly, when the developers are trying to get the program to work,
    they are not thinking about that future developer. It takes a change
    of rhythm to make changes that make the code easier to understand.
    Refactoring helps to make the code more readable. A little time
    spent refactoring can make the code better communicate its purpose.
-   As the code gets clearer, one can see things about the design that
    he could not see before because its difficult to visualize all this
    in head. Thus, refactoring is just wiping the dirt off a window so
    you can see beyond.
-   When I myself did some projects on making my own shell, implementing
    malloc and some data structure projects, I realized, while I’m
    studying code I find refactoring leads me to higher levels of
    understanding that otherwise I would miss out.
-   Reducing and refactoring the amount of code does, however, make a
    big difference in modification of the code. The more code there is,
    the harder it is to modify correctly. Hence, this needs to be done
    as early as possible as everyday developers are working and adding
    new and new code to it.

<!-- -->

-   The above is what I intend to do as part of GSoC.
-   It is not just about 3 months of GSoC, I want to be committed with
    this code for years. I will keep contributing even after that as
    thing is an endless job-new codes are definitely going to be added
    and that in-turn would also require code reducing and refactoring.
    Moreover, by the end of 3 months, I believe, I would have hacked the
    entire source code so well that I can work on other projects also
    and contribute in making BRD-CAL more awesome!

# My Development Reports

[Click here to see logs](Reports.md)

# Links to any code or algorithms you intend to use

ALGORITHM I intend to use:

-   Step1:Select one or more defect to review.
-   Step2: Mark as claimed and being worked on.
-   Step3: if ( More than three lines of code ) goto step 4 else Change
    according to my Judgment
-   Step4: If ( More than in a file ) then goto step 5 else goto step 8
-   Step5: If ( More than a directory ) then goto step 6 else goto step
    7
-   Step6: Probably warrants a new function in the highest common
    library and goto step 11
-   Step7: Create function, add declaration to private header and goto
    step 11
-   Step8: If ( In a library ) then goto step 9 else goto step 10
-   Step9: Create hidden/static function or macro in the same file and
    goto step 11
-   Step10: Create static function or macro in the same file and goto
    step 11
-   Step11: If it warrants a regression test the goto step 12 else goto
    step 13.
-   Step12: Add regression/ unit test and commit and goto step 14.
-   Step13: If it is user visible goto step 14 else goto step 15.
-   Step14: Update TODO and goto step 15

/\* Here check once again for was it good code to change and leaves back
no duplication, has a regression or unit test if warranted and it passes
and all docs were updated like TODO, deprecation.txt, doc-book, doxygen
comments etc \*/

-   Step15: Commit and mark as 'Needs Review' and goto step 16
-   Step 16: Estimate impact, update severity and goto step 17.
-   Step 17: Record in the ledger and goto step 1.

# Problems I would encounter and how will I solve them ?

-   The task of code refactoring and reducing is very critical as it
    play around with most of the folders and files present in the source
    folder and will modify and delete and add some new lines as per the
    requirements. There is huge possibility of changing the
    functionality of the program and make it behave in a bad manner.
-   So, what I have though is I would compile after every change.
-   BRL-CAD's step-g converter will serve as a test for the
    functionality of the library and compiler will be set to strict
    flags.
-   Moreover, I will run unit test and test with that there is no run
    time error also and the behavior of code remains the same.
-   Rest, Google, my best friend who knows everything is always with me
    and will help me in every situation.

# Deliverables

-   Modernize the C++.
-   Improve library functionalities
-   Make code more readable and maintainable
-   Document it using doxygen system
-   Create Reusable code.

# Importance of the Project:

-   Improving Design :As people change the code to realize short term
    goals, the code will lose its structure and program will decay.
-   Makes Software Easier to Understand : Still compiler taking a few
    more overheads and delivering output a few milliseconds later is not
    of huge concern to most of us. But, what worries us is that a new
    developer will have to spend a week figuring out the part he wants
    to change which would be actually job of an hour if the code was
    well managed.
-   Easier to add new Features

# Time availability:

-   My availability for the project would be possible for the specific
    GSoC period as I would be having my summer break from 1st May to
    last week of July. Since in August the new semester would have just
    begun, I would be able to spare enough time to work on the project
    as I am not involved in anything else which would be a hindrance.
-   In September I have a 3 days in-sem evaluation at university. It is
    compulsary to have a \*present\* marked for it, but its weighage is
    just 10-15% in the total evaluation for the semester which is quite
    negligible. Except for these 3 days, I am available in September
    also.
-   I will also work on Sundays if needed needed to cope-up in-case if I
    am unable to meet with my development schedule due to unavoidable
    circumstances.
-   Even after GSoC period I will get enough time to continue
    contributing to STEPcode and BRD-CAL.

# Development schedule:

//\* Pre-GSoC Period \*/

-   -   April 19- 22 : Downloaded Source-code and made one initial
        patch.
    -   April 23-30 : Final End-Semester Exams at University.
    -   May 1-3 : Submit some more patches to showcase my work.
    -   May 4-21: Ensure Build Environment is working fine, stay in
        constant contact with the mentor to discuss efficient ways and
        asking them questions and make some more patches.

/\* GSoC period Starts \*/

## PHASE I: Analysis and Design Period

-   May 25- June 20 :
    -   Getting familiar with the code
    -   Examine the existing STEPcode repo at
        <https://github.com/stepcode/stepcode> and create a list of
        tasks that need to be done.
    -   Fix some small issues like \#21, \#123, \#200 ,\#204, \#233
    -   At the end of this period : A finalized plan to proceed for the
        development of the library.

## PHASE II: Development Phase

-   June 20 – September 11
    -   June 20 – June 30 - Write two script using doxygen (or
        doxyassist possibly) to create documentation which is split up
        logically.- one for parsing express (express, exppp,
        fedex_plus, fedex_python) and other for uses of STEPcode
        (tests, clprobe-ui, SCView,[BRL-CAD's
        stepg](http://stepcode.org/stepcode-use-doxygen/dir_d0040508ea657d1100a6aec0fcb59f22.html))
    -   July 1- July 5 :Read the code related to lazy loading
    -   July 5- July 9 : Make appropriate interface of src/cllazyfile
        and add \#TODO comments
    -   July 9 - August 15 - Work on completing those todo's. Writing a
        function, test it and document it in a cyclic manner.
    -   August 15 – August 24 - submitting and some more review and
        updating if it is necessary.
    -   August 24- August 26- Check minutely, if its not leaving behind
        some bugs.
    -   August 26 – August 30 - Making mid-term report and completing
        the task left.
    -   At the end of this period : src/cllazyfile with all
        functionalities and all of them having been tested at unit
        level.

## PHASE III :Testing, Cleaning and Wrapping Up

-   August 30 - September 27
    -   August 30 - September 9 - Testing it on other platforms
    -   September 9-September 15 - bugs fixing, review to be ready for
        submitting the final result. Solving some small open issues on
        github if time permits.
    -   September 10- 22 -Pencils down ,Code clean up , Documentation
        (wiki pages)
    -   Sept. 23 – 27- Final evaluation and Submit code to Google
    -   At the end of this period: Deliverable mentioned would be
        successfully be completed.

# My preparation for the Project:

-   Joined IRC channel \#brlcad
-   I have mailed in the mailing list of BRL-CAD talking about my
    interests and planning for near future.
-   Surfed through previous year projects where I found one similar
    project. I am also in contacting with that candidate who would guide
    me and share her experience with me.
-   Cloned the source-code into my system.
-   Opened some src files, saw some codes and found huge cod repition
    over there. \*As my first step, I had modified the file
    /src/libbn/plot3 and reduced some amount of code.
-   I didn't have previous experience with SVN version control system.
    Made an account on sourceforge.net and submitted my first
    [patch.](https://sourceforge.net/tracker/?func=detail&atid=640804&aid=3611485&group_id=105292)
-   <Right now>I am checking out STEP Libraries and how it functions.
-   Due to the burden of final exams I am afraid that I couldn't work to
    my maximum potential till 30th April. But from 1st May to May 3rd, I
    am planning to submit some more patches to show my work.

# Why me?

-   The reason why I am a suitable candidate for "Code Refactoring"
    project is because most importantly, I love programming in C and C++
    and figuring others code looks quite fascinating job to me.
-   Moreover, I had won 3rd and 1st position respectively in "i-code and
    C-debugging contest" organized by IEEE as a part of I-Fest at
    DA-IICT in 2012 and 2011 respectively.
-   I have been certified as excellent C and C++ coder with A++ grade by
    Centre for Development and Advanced Computing(CDAC), Pune, India.

# Why BRL-CAD?

-   The code is entirely written in C, the programming language in which
    I am the stongest.
-   Also, I chose BRL-CAD because I think it's great to work on such a
    powerful Open Source modeling system.

I promise that if given this opportunity, I will work with full
dedication, give my 100% efforts, leave no stones unturned and reduce
the code and make it more readable.
