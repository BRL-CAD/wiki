# GSOC 14 Summary

## Week1

This week I am scheduled to implement the following

-   ARS
-   SUPERELL
-   BINUNIF

'''''May 19th

-   I implemented ARS.
-   Also implemented Ctypes Adapter to handle 2D Array

'''''May 20th

-   Initiated witting test for ARS.
-   Stuck in errors.

'''''May 21th

-   Tried with different approaches to handle the array but with little
    success.

'''''May 22th

-   Took a break off from ARS and implemented HALF runs properly. (tests
    also compile).

'''''May 23th

-   Relooked at ARS, dug the C code, found some error and the way ars
    data should be sent.
-   But the error still persists. although corrected my approach for
    sending data to mk_as

'''''May 24th

-   Corrected the error after a call with Csaba, The error was related
    to freeing the memory from brlcad-C code and also python code.
    Hopefully this experience helps me solve future problems

## Week2

This week's plan is to come in sync with the time line.

'''''May 26

-   Implemented superell.
-   Also made two patches in accordance with the brlcad C
    repository(main).

'''''May 27

-   Sent a pull request for the code to be merged.
-   Also worked on metaball. Metaball has some internal functions which
    are to be modified. thus figuring out a way to do it.

'''''May 28

-   Looked a Pipe primitive of brlcad and its implementation in python.
    Metaball has similar traits but there are further challenges. The
    data in metaball doesn't have number of points. Therefore this is
    tricky.

'''''May 29

-   Implemented Metaball.
-   Though there was an issue with the fastf_t \*verts\[5\], and I keep
    getting a very funny error :: expected LP_c_double_Array_5
    instance instead of LP_c_double_Array_5
-   Therefore for now my implementation works with fastf_t \*\*verts.

'''''May 30

-   Started working on EBM.
-   Learned brlcad image-processing tools. (They are quite good :-))
-   Also getting this strange error "test framework quit unexpectedly"

'''''May 31

-   Some strange behavior with my set-up.
-   Re-set up everything.
-   finally it turned out that all my executables in the brlcad C repo
    where 0 sized.

## Week3

'''''June 2

-   Created EBM primitve.
-   Used Ychar image given in the example.
-   works well

'''''June 3

-   Found a tricky error in BRLCAD C repository. The last argument in
    mk_metaball()
-   Submitted patches \#278 on the sf site to correct that.
-   Also corrected the metaball implementation and found a better way to
    terminate the list argument.

'''''June 4

-   Was away most of the day.
-   Accommodated changes suggested by Csaba.

'''''June 5

-   Implemented Grip.
-   Explored Bot and Constraint,
-   Constraint need not be implemented for now because its api is not
    mature.
-   Bot is an interesting primitive. Chalked out a way for it.

'''''June 6

-   Spent my time figuring out issue with bot.

'''''June 7

-   Added bot primitive.
-   The current version only creates a bot with plate mode.

## Week4

'''''June 9

-   Started working on a new primitive.
-   Apparently found an error in submodel primitive.
-   Reported it to the core developers team
-   Worked on modularizing the bot primitive.

'''''June 10

-   Contd. working on BOT.
-   Tried different approaches.
-   Modularizing a complex primitive as BOT has turned out to be tricky.
-   Finally created a module wherein facility of adding faces in a bot
    is different
-   Also each method has a different stub altogether.

'''''June 11

-   Cleaned the Bot code.
-   Wrote few tests cases of different methods. This will also serve as
    examples
-   Also finished working on submodel primitive.
-   Created a different file in the resource directory for the tests.

'''''June 12,13,14, 15

-   Traveling (informed Csaba)

## Week5

'''''June 17

-   Corrected ARS api to make it python friendly. The changed api only
    requires curve information.
-   Modified ctypes array2d to make it more robust.

'''''June 18

-   Started implementing pnts.
-   Pnts has different parts, thus implementing them using different
    classes.
-   Spent my time archetecting the pnts primitive.

'''''June 19

-   Bryan merged my code and indicated an error in metaball tests
-   Halting pnts implementation and focusing on correcting metaball.
-   Found a strategy to work such the mk_metaball is not required.
-   Also I dont know why BU_LIST_INIT is not wrapped automatically!
    (Thus implemented it seperately as a ctypes adaptor)
-   Now this doesnt require usage of mk_metaball function. Tests run on
    the current version of brlcad c-repository.

'''''June 20

-   There are 3 primitives which are left to be wrapped PNTS, BINUNIF
    and DSP.
-   Today I tried to understand the requirements of all three.
-   Went through the c code in libwdb (dsp,binunif) and typein(all
    three).
-   I am sure by the end of next week till which the stipulated time
    finishes I will have finished these primitives.

'''''June 21

-   Worked on DSP primitive created dsp followed dsp tutorial.
-   Got accumulated to the process of dsp creation.
-   Understood the v5 method of creation in typein.

## Week6

'''''June 23

-   Implemented DSP primitive.
-   Used a different approach, because the mk_dsp doesn't have the
    required parameters
-   But it creates a issue while freeing it.
-   Tried resolving it but with no success.

'''''June 24

-   Re-looked at the issue of DSP.
-   Used GDB to get the backtrace. Pasted it in the channel. Waiting for
    reply.
-   Also committed the code in a different branch in dsp_primitive.
-   Also resolved issues notified by Csaba in the code.

'''''June 25

-   Corrected DSP.
-   Also added calloc support to brlcad_new to initialize the allocated
    memory to 0.

**MidTerm Summary**


Mid Term Summary is
[here](User:Krajkreddy/GSOC14/midterm-summary "wikilink")

## Implementation of Brep and OpenNurbs

### Quick Summary

-   python-brlcad uses ctypes. Since ctypes can only talk to C
    functions, We need to provide declaring classes with extern "C".
    This requires a lot of changes to main repository brlcad. making it
    clumsy.
-   Other options which I have explored to wrap c/c++ code in python are
    boost library, swig and sip.
-   Bryan (kanzure) has done an experiment with swig code for python
    wrappers. His code is available
    \[here\|<http://diyhpl.us/~bryan/irc/opennurbs/brlcad-opennurbs2.zip>\].
    This misses some brlcad and doesn't work appropriately.
-   Boost library provides a wonderful seamless wrapping. But it
    requires change in c++ code. It uses a special python header in the
    c++ code with different wrapping schemes.
-   sip is one of the better tool I found to wrap python code. details
    can be found
    \[here\|<http://pyqt.sourceforge.net/Docs/sip4/index.html>\].
-   other tool which can parse c++ automatically is clang find the
    details
    \[here\|eli.thegreenplace.net/2011/07/03/parsing-c-in-python-with-clang/\]

### Plan

To wrap the brep/opennurbs code as a python module. And use it in
brlcad-python project.

'''''July 21

-   Played with PyBindGen. This tool is promising in wrapping with C++
    code which has inner classes.
    <http://pybindgen.readthedocs.org/en/latest/apiref/>

'''''July 22

-   Since most tools which wrap c++ code doesn't have a automatic
    parsing of c++ headers like ctype-gencore.
-   today I found a parser for c++ headers.
    <https://pypi.python.org/pypi/CppHeaderParser/2.4.3>
-   With in this week I am planning to write code which generates
    automatic config files using the c++ headers.

'''''July 23

-   Learnt to deal with PyBindGen. A nice tool to wrap c++ code for
    python library.
-   Implemented small dummy c and c++ code.
-   Couldnot run the automated script because of some issues dont know
    why they are errupting. Apparently a symbol "config_t" is not
    available in the module.

` File "`<input>`", line 1, in `<module>
` File "/home/raj/.local/lib/python2.7/site-packages/pybindgen/gccxmlparser.py", line 598, in parse`
`   pygen_classifier, gccxml_options)`
` File "/home/raj/.local/lib/python2.7/site-packages/pybindgen/gccxmlparser.py", line 693, in parse_init`
`   self.gccxml_config = parser.config_t(**gccxml_options)`

AttributeError: 'module' object has no attribute 'config_t' '''''July
24

-   Relooked at PyBindGen code. It seems good. I think we can either
    develop this tool further (if it fails to work as it is currently)
-   Also looked at how we can solve this.

'''''July 25

-   Looked at various dependencies like gccxml and pygccxml and saw
    there version numbers.
-   Apparently the config_t symbol was deperecated.
-   Changed this and in the PyBindGen. Reported the bug in thier issue
    tracker. Personally contacted the author who is traveling and will
    change it later.
-   created a dummy example of the code and it works fine.
    <https://github.com/raj12lnm/TryPyBindGen>

'''''Summary : Have the ability to parse a C++ header and create a
wrapped library for it. Next I will move to wrapping the Giant .. the
OpenNurbsLibrary in Python. :D

'''''July 26

-   wrote a c++ example in the pybindgen example. Looks like this is
    working fine.
-   Tried parsing C++ header of OpenNurbs using pybindgen.
-   looks like there is some issue here.
-   The issue currently is as follows.

There are multiple symbols in different headers and gccxml is not able
to gather information regarding the ones which depend on each other. For
example the paste here <http://tny.cz/8008c460> tells us how when
parsing a file has given issues.

'''''July 28 (Monday)

-   Found that Pybindgen requires a single header.
-   Instead of automating it, used a frugal way by concating the header
    files in such a way that the order is topologically sorted in the
    dependency graph.
-   While Parsing the header using Pybindgen I get an error.
-   There is a bug at which I am stuck <http://tny.cz/be8180ca>.
-   Since the header file is several lines(&gt;65K) long all, Thus the
    parsing takes a long time. And the bug is somewhere at the end. All
    my efforts went in vain today.
-   I have added the repository here
    <https://github.com/raj12lnm/OpenNurbs-Python>
    -   Installing the repository
        -   Install Pygccxml 1.0 from here
            <https://launchpad.net/ubuntu/+source/pygccxml/1.0.0-4> (1.0
            is supported by PyBindGen)
        -   Install Pybindgen bzr checkout
            <https://code.launchpad.net/~gjc/pybindgen/trunk>
        -   use python mymodule_gen.py &gt; mymodulegen.py
        -   mkdir build
        -   python setup build
-   Currently build will be successful but not correct, some symbols
    will be mismatched.

'''''July 29 (Tuesday)

-   Continued to work on the error using breakpoints and manual code
    outputs. But failed to find the part of the header file which is
    producing this error.

'''''July 30 (Wednesday)

-   Found the issue in the header file which prompts the above error.
-   It is just the NULL default value for an integer type pointer.
-   I have created a small example here
    <https://github.com/raj12lnm/TryPyBindGen>
-   On digging the code although I could not find the exact issue but it
    has something to do with ctypes. Also, other pointers with 'NULL'
    default works fine.
-   So know I have details of all the classes, methods their parameters,
    enums etc.
-   Next step is to create a cpp file from this information and build
    the library.

'''''July 31 (Thursday)

-   I get numerous build errors
-   I have listed them here <http://tny.cz/896562a1>
-   Looks like there are some issues to handle private keyword in
    pybindgen.
-   I tried to look at the internal of the code and it turns out that
    pybindgen ignores private and protected methods.
-   Reported the error to pybindgen developers.

'''''August 1 (Friday)

-   Debugged the setup files and corrected the error for unitialized
    variables.
-   On further looking, PBG has a way to ignore private and protected
    methods of classes, but it is somehow failing in the case of
    OpenNurbs's case.
-   Also, Discussed about provisisons to initiated a way to wrap
    important classes of OpenNurbs in Python with Bryan(kanzure) on IRC.

'''''August 2 (Saturday)

I have sampled all the errors from the build <http://tny.cz/802fe6f9>.

The build mainly contains following types of errors from PBG(PyBindGen).
They are :

-   ‘retval’ was not declared in this scope : In some functions/methods
    the sudo retval is not declared.
-   Private methods are wrapped
-   error: assignment of read-only variable :
-   Call of overloaded functions.
-   cannot find members in some struct which are used.

I tried to get into PBG source code to find the reason for these. But it
looks like I will require some more time to understand PBG. Also In the
meanwhile I notified the developers of PBG regarding the status.

'''''August 4 (Monday)

-   Worked with one of the developer of PBG.
-   Now one of the error where const double and float pointers were
    causing errors are solved.

'''''August 5 (Tuesday)

-   Worked on two errors which PBG is causing for C++ code.
    -   Inability to wrap overloaded functions
    -   wrapping of private methods.

All though couldnot understand how private method wrapping can be
avoided by PBG. But there are few overloading functions. My plan is to
manually change the overloading functions in the produced cpp file.
(Although this might cause an issue because of large number but cannot
find an alternative.)

'''''August 6 (Wednesday)

-   I spend my time today mainly working on the issue of overloaded
    functions.
-   As suggested by the PBG developer(by personnel email), I checked the
    pybindgen.gccxmlparser module but could not find any issue.
-   Later on diging the code of OpenNurbs I found that all the
    overloaded functions which were causing the issue were private
    constructors mainly used for singleton pattern
-   Also Interestingly all these private constructors didnt have
    definitions as well.
-   Thus I removed them manually from the auto generated c++ file.

'''''August 7 (Thursday)

-   One of the error I the PBG was regarding retval which is an internal
    parameter in many functions. This was an error in PBG. Now resolved.
-   Errors have majorily shrinked now by taking care of the above
    issues.
-   Now the major errors are here <http://tny.cz/2ed6eadc>
-   There are main two types of error left.

1.  1.  Accessing of symbols from union which is not supported by PBG.
    2.  Also overloading functions in string class of opennurbs.

'''''August 8 (Friday)

-   While Compiling I received many errors related to overloading of
    functions.
-   I have seen that these are in ON_String and ON_wString class.
-   These are mainly created due to excessive overloading of methods.
-   I have removed some redundant overloaded functions from these
    classes and now these work.

'''''August 9 (Saturday)

-   Since Union is not supported by PBG, therefore the generated file
    creates error issues while compiling.
-   In OpenNurbs library there is an instance of union in a struct
    MAP_VALUE
-   I have contacted the developer of PBG. They have suggested on
    mannually changing the generated c++ code.
-   I have thus manually changed the c++ code wherever there are
    instances of the struct.
-   And thus now the struct errors are eliminated.

'''''August 11 (Monday)

-   Now everything compiles perfectly.
-   But on loading the compiled library in a python shell I lot of
    symbols are not defined.
-   I found that BRL_CAD main repository removes the OpenGL
    dependencies thus I also removed them
-   The problem on diagnosis turned out that, some functions in
    OpenNurbs have only declarations and lack definitions. This is
    indeed a common practice by c++ developers.
-   But Since pybindgen only scans header files thus the undefined
    symbols creep in.
-   I have removed such declarations. And it works well.

**Suggested 'pencils down' date**

End term summary is
[here](User:Krajkreddy/GSOC14/end_term_summary "wikilink")