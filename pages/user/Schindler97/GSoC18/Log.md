### Development Logs

#### Community Bonding Period

Progress through the community bonding period

-   Week 1
    -   Reviewed and understood Kanzure's implementation of python
        bindings : <https://github.com/kanzure/python-brlcad>
    -   Read about ctypesgen and understood it's short-comings and
        advantages
    -   Went through chapters 1-3 of mged tutorials
-   Week 2
    -   Reviewed and understood nmz787's implementation of python
        bindings : <https://github.com/nmz787/python-brlcad-tcl>
    -   Delved into understanding how tcl scripts are parsed by mged
    -   Implemented the ell primitive following nmz's methodology :
        <https://github.com/Killthebug/python-brlcad-tcl/commit/a0973c5b42615e0ef53ba9c876ee14992e1df937>
-   Week3
    -   Had a discussion with Sean about introducing procedural geometry
    -   Went through OpenSCAD's workflow and tried to understand how
        they work with procedural geometry
    -   Went through chapters 4-6 of mged tutorials

#### Coding Period

Progress through the coding period.

Ctypesgen Project Repo : <https://github.com/Killthebug/python-brlcad/>

TCL Project Repo :
<https://github.com/Killthebug/python-brlcad-tcl/commits/master>

-   Week 1
    -   **14 May**Introduced bindings and examples for primitives :
        arb4, arb5, arb7
    -   **15 May**Introduced bindings and examples for primitives : tec,
        trc
    -   **16 May**Introduced bindings and examples for primitives : rhc,
        rec
    -   **17 May**Introduced bindings and examples for primitives : ehy,
        epa
    -   **18 May**
        -   Introduced primtive : ell1
        -   Going through libged to figure out how the 'in' command
            works. Edit : Found it, thanks to Cezar :)
        -   Reading through the code of the ell primitive in librt to
            understand how primitives behave at a ground level. There's
            a lot going on, might take me a while to figure everything
            out.
        -   Sean recommended going through the various READMEs scattered
            across the code, will start on those too and log progress
            here.
    -   **19 May**
        -   Introduced the primitive : part
        -   Trying to understand how certain parts of the pipe()
            function have been handled by nmz's code.
    -   **20 May**
        -   Introduced bindings and example for : tor, eto & grip
        -   Going through to libged/typce.in to understand how it works?
            Seems good so far.

<!-- -->

-   Week 2
    -   **21 May**
        -   Introduced bindings and example for the primitive : half
        -   I've understood how typec.in functions
        -   We're trying to figure out the ??? in : tcl -&gt; .g .
            src/mged/setup.c (converts tcl to c commands) -&gt; ???
            -&gt; include/rt/db_io.h -&gt; .g
        -   I learnt about opendb, which calls the f_opendb() function
            defined in src/mged/mged.c. to open and create new
            databases, this will be handy in our pipeline.
    -   **22 May**
        -   Fixed primtive examples for arbx and sph
        -   Did mged tutorials 6-8
        -   Went through libged to understand how it work
    -   **23 May** :
        -   Went through Hacking-BRL-CAD, I really wish I had found this
            document way earlier!
        -   Couldn't get a lot of work done because of a research paper
            deadline I'm working on.
    -   **24 May** :
        -   I've started documenting the project so far. The major
            subtopics I'm documenting are :
            -   What is python brlcad?
            -   How to setup python brlcad?
            -   How do the different parts of the code work?
            -   Creating geometry using existing primtives
            -   Introducing and experimenting with primitives
            -   Further Work
    -   **25 May**
        -   Continuing work on the documentation.
        -   I'm still not able to build a page using doxygen, I've
            dropped a message on Zulip and hope to get it resolved soon
            :)
    -   **26-27 May**
        -   Took the weekend off to travel to the beach nearby, Last two
            weeks have been really hectic with GSoC work and my research
            paper deadline nearing up on the first of June!
    -   **28 May - 4th June**
        -   No major GSoC work was done during this period because of an
            external submission deadline at a research conference.

<!-- -->

-   Week 3
    -   **5 June**
        -   Resumed GSoC work. Had a conversation with @Sean and updated
            him regarding the lag in project.
        -   Revised through libwdb and some sample scripts in src/shapes
            and src/proc-db to get a hang on how .g files can be made
            using libwdb.
        -   The plan now is to introduce a new primitive name "script"
            in librt. As a part of creating it, I'm going to have to
            define the syntax of the scripts that the primitive will
            parse.
    -   **6 June**
        -   Major part of workday so far has been on understanding
            libged/typein.c that deals with the **in command**. I feel
            like we can incorporate a script keyword in this file
            itself. Also, waiting to hear from the mentors about what
            they think of this idea vs incorporating a new primitive.
    -   **7 June**
        -   I've modified scripts in proc-db to better understand how to
            interact with libwdb's API.
        -   I'm also trying to figure out where the logic for the main
            'script' parser would go. I feel like putting it inside
            libwdb would be a logical choice.
    -   **8 June**
        -   SVN has been acting weird today for me, despite multiple
            attempts (20+), I've been unable to checkout the repo. It
            seems to be an issue with my university proxy server but I'm
            not sure yet. I've been messing around a lot and have broken
            something which I can't seem to fix and hence am attempting
            to pull the latest build.
        -   I've been scanning through libged and mged to figure out how
            file upload works in mged. That'll be the first challenge in
            working with the 'script' parser.
        -   Discussion with Sean today is going-on. [To be
            updated] (To_be_updated.md)
    -   **9 June**
        -   Today was majorly spent understanding the ctypesges approach
            as proposed by Kanzure.
        -   ctypesgen seems to be automatically generating bindings for
            the c code and feels like a neat approach.
    -   **10th June**
        -   Sean assisted with a path to fix some installation errors in
            the ctypegen code. It was due to certain missing header
            files.
        -   We were facing issues in installations but once Sean
            explained about how lib_bundles work, I was able to get
            everything running.
        -   I also wrote and submitted a script that does what
            proc-db/wdb_example.c does using the tcl (nmz) approach and
            have submitted it for review. We will not decide whether to
            go ahead with the tcl approach or the ctypesgen one.

<!-- -->

-   Week 4 : Evaluation Period.

<!-- -->

-   Week 5
    -   **17th June**
        -   src/tcl/generic/tclParse.c seemed like a good place to
            understand how tcl scripts are parsed. Spent the entire day
            reading this code and trying to understand it.
    -   **18th June**
        -   tclParse.c is very very complicated and I feel like it'll be
            less of a challenge to write the parsing script from
            scratch. I plan to use pyparsing (lib) to create the parser.
        -   Spent the day learning how pyparsing works and going through
            it's tutorial series.
        -   pyparsing requires a BNF of the script format to work with.
        -   I'm planning to use tcl scripts as input for the procedural
            geometry because they are already in use in the BRLCAD
            ecosystem and I don't want to introduce a new file format.
        -   Creating a BNF for tcl is turning out to be a complicated
            job
        -   I've been at this for hours now and finally, I've come
            across this on the TCL website : <http://wiki.tcl.tk/1643>.
            Essentially you cannot have a BNF for TCL.
    -   **19th June**
        -   I'm just going to write a vanilla parser and add
            functionality as modules slowly.
        -   Basic TCL script parsing is working now.
        -   **The script parser works with python-brlcad (ctypesgen) to
            read tcl scripts and creating corresponding .g objects**
    -   **20th June**
        -   Changed the structure of the code and refactored it a bit.
        -   Right now arguments in scripts are being passed as constants
            but having variables would be an integral part of procedural
            geometry too.
        -   Changed the primitive creation code so that variable parsing
            can be introduced later.
    -   **21st June**
        -   Some primitives are still remaining in the script parser.
            Adding those and making some finishing touches.
    -   **22nd June**
        -   Introduced arbn and pipe primitives. All primitives are now
            accounted for.
        -   Introduced the ability to parse variables. Procedure
            geometry is all about re-using procedures and creating
            complicated objects easily. Such an approach would require
            the use of variables. Currently variables can be given a
            value and while making shapes these variables are swapped
            out for their values.
        -   I'm handling variables as they're used by tcl scripts.
    -   **23rd June**
        -   Now comes the tough part. I've have to introduce procedures.
            A procedure is any "function" that draws one or more shapes
            and may (usually has) have arguments passed to it that are
            used during shape creation.
        -   After a fair amount of reading, I've decided to go with
            tcl's procedures (http://wiki.tcl.tk/463) definition to
            procedures in the script.
-   Week 6
    -   **24th June**
        -   Some basic changes in variable parsing. Resolved errors that
            were creeping in due to line spacing/indentation.
    -   **25th June**
        -   Writing an interpreter seems to be far more difficult that I
            had imaged. I've been at this for hours now and I can't
            figure out a good enough flow (sequence) in which I should
            parse the different parts of a script.
        -   The major issue seems to be with handling expressions and
            variable substitution within procedures at run-time. To
            tackle this, I've decide to encode each procedure (proc in
            the script) as an object of the procedure class
            (proc_interpreter.py) and initialize it with all the global
            and local variables it might require.
        -   On run-time then expressions would be executed based on the
            arguments passed and the final values would be substituted
            then.
        -   <https://compilerdesignblog.wordpress.com/> Has turned out
            to be very helpful. Not directly, but in a way guides you on
            how to tackle the problem.
    -   **26th June**
        -   Introduced proc_finder, responsible for extracting exact
            procedure strings from the script. Used the generic closed
            parenthesis calculation using a stack.
        -   Introduced basic-bone structure for the proc_interpreter.py
    -   **27th June**
        -   Argument extract from procedures done so far.
    -   **28th June**
        -   I'm trying to create a BNF so that the syntactic parser can
            execute expressions containing variables and constants.
            Though, I've never understood how BNFs work. Time to read
            up! There is a set of tools, called parser generators, which
            accept a grammar as an input and automatically generate a
            parser for you based on that grammar.
    -   **29th June**
        -   Work has started on the arithmetic syntax parser. It will be
            used to evaluate mathematical equations (BODMAS expressions)
            in the procedural scripts.
        -   Introduced a bare bones structure with functionality to add
            and subtract.
    -   **30th June**
        -   There was in issue with white spaces being present in the
            equations, fixed that today.
-   Week 7
    -   **2nd July**
        -   I wake up on Monday to resume working. Start reading what
            I've written and I feel like : <https://imgur.com/a/DSQNWPt>
        -   Nonetheless I start adding comments and working finishing
            the parser. I've added functionality to divide and multiple.
        -   Parenthesis are now being taken care of! :)
    -   **3rd July**
        -   I just realized about a massive blunder I've made. I can't
            account for negative or floating point numbers :\|. Start
            frantically working on it. Difficult to think around it but
            fairly easy to implement I'd say.
        -   The arithmetic parser is ready. I now import it into the
            script parser and write code to extract "mathematical
            expressions" from the script and feed it to the parser.
        -   Feel like I should document my functions better. Add basic
            description to major functions in script.py
    -   **4th July**
        -   I've found a bug in how proc structures are being extracted
            from the script. Fixing it should be easy.
        -   Turns out, isn't easy. Still working on a fix (without
            breaking a lot of other things).
    -   **5th July**
        -   Skipped today, didn't do much work today :/
    -   **6th July**
        -   YES! Procs get extracted properly. The bug was fixed by
            finding the last line of proc-definition, and then using it
            for further tasks.
    -   **7th July**
        -   Now we're extracted procs, time go get started on parsing
            them.
        -   Global variable substitution : Done
        -   Local variable substitution : Done
-   Week 8
    -   **9th July**
        -   Expression evaluation within procs using global and local
            variables done.
        -   There is still a bug that creeps in during argument
            substitution (when a proc is called), working on a fix now.
        -   Things are looking good. The entire script parser should be
            ready in a day or two!
    -   **10th July**
        -   Implemented the python version of sgi.sh
        -   &lt;&lt;Evaluation Period has started! Eeek!&gt;&gt;
    -   **11th July**
        -   Worked on reducing the size of the sgi.py (Made it under 100
            lines)
        -   My approach was not right, better abstractions are expected.
    -   **13th July**
        -   Rounded_rcc procedure implemented and pushed.
        -   Discussion with Sean regarding how the procedural scripts
            will be interacted with.
-   Week 9
    -   **16th July**
        -   Basic Sanity Checks for the Rounded_rcc procedure are in
            place.
        -   Work to couple the script primitive with the pythonic parser
            starts today!
    -   **17th July**
        -   Made changes as required to rename files and libraries.
        -   Updated files, tests and examples.
        -   Tested files to make sure nothing is breaking on new build.
    -   **18th July**
        -   Made the spreadsheets that investigate which wdb functions
            are on the python side and which are currently not. Pushed
            this to github as well.
        -   Started work on rt_script_describe(). Reading previous
            primitives and understanding how files work.
    -   **19th July**
        -   Sean has nicely given instruction on what do and they seem
            to be straightforward. I'm having issues with parsing
            strings, I'm using a character array but I'm sure there has
            be a better way.
        -   Modified typein.c to take appropriate input
    -   **20th July**
        -   I've found something called bu_vls which seems to be
            handling scripts.
-   Week 10
    -   **23rd July**
        -   Finished work on the excel sheet (added list of primitives
            with mk_primitive function)
        -   Discussion with Sean regarding re-writing my file printing
            code snippet.
    -   **24th July**
        -   The (null) printing was fixed.
        -   Mged now though crashes with Segfault 11 when executing the
            in command for creating script.
        -   Re-wrote the code snippet to modify l describe to print file
            contents.
        -   Can now print file contents with hardcoded file path but
            cannot store file name.
    -   **25th July**
        -   Today's work was more about failing to do a lot of things
            rather than actually being able to do them.
        -   I thought that I was having a problem with the bu_vls
            struct so tried to use a char array to store the filename in
            typein.c.
        -   I then started looking at the code and debugging line by
            line and found the bug. It was occurring because in
            src/librt/primitives/ell.c, fname could not be read from the
            rt_ell_internal struct
    -   **26th July**
        -   I also spent a considerable amount of time reading through
            import5() and export5() function in dsp.c and ebm.c to
            understand how they handle input strings. A lot of doubts
            were cleared by debugging using bu_log. Have a few major
            doubts, have shared them on the IRC.
        -   The best resources :
            <https://docs.python.org/3/extending/extending.html#calling-python-functions-from-c>,
            <https://www.linuxjournal.com/article/8497>
        -   Learnt to debug using lldb and also caught my first
            initialization error!
        -   Explored include/bu/file.h to see file opening options.
            bu_temp_file() as Sean suggested is a \*possible\* way to
            go.
        -   \[Minor Task\] Compiled and shared list of primitives not
            implemented in python brlcad.
    -   **27th July**
        -   Started working on fixing the script primitive, but even
            there, I'd constantly get a seg fault. I thought they were
            initialization issues and I tried to fix them here and there
            but nothing worked
-   Week 11
    -   **30th July**
        -   Created the Tutorial folder in github
            (https://github.com/Killthebug/python-brlcad/tree/master/Tutorial)
            It has currently two files which explain how to create
            shapes procedurally.
        -   abstract_tutorial.py : Uses the draw_primitive file to
            create geometry. Advantage of using it is : better naming of
            functions and easier handling of arguments that are passed.
            This file is tested and complete and creates all shapes.
        -   core_tutorial.py : Used the actual wrappers, without an
            intermediate file. This file is not totally tested and hence
            might break. Will be fixed in the next commit.
    -   **1st August**
        -   Primitives missing from the scene were introduced : bot,
            grip, superell, submodel, ebm.
        -   I tried to create ars and metaball but there seem to be
            issues popping up. I'm fixing them. The issue with metaball
            is something that is followed on from GSoC'14. Look at May
            29 Entry :
            [Krajkreddy/GSOC14/summary](/wiki/user/Krajkreddy/GSOC14/summary.md)
        -   With ars and metaball there's some issues on the binding
            side. There was an issue with the fastf_t \*verts\[5\],
            Error :: expected LP_c_double_Array_5 instance instead
            of LP_c_double_Array_5.
        -   Re-arrangements in the scene take up a little more time than
            expected but that's not a major issue.
    -   **2nd August**
        -   Learnt to work with sketch, extrude and revolve in mged.
        -   Moved a few shapes (3) from the z-orientation to the
            y-orientation.
        -   Browsed code to create the script primitive in the python
            API and found what "I think" are some errors. I've changed
            the code a bit and I've almost managed to get it to work. I
            know exactly what to change further (hopefully) and it
            should be up and running in the next commit.
    -   **3rd August - 5th August**
        -   Finally, the scene (with most of the primitives is close to
            completion)
        -   The scene is now along the x-y plane, growing vertically
            along the z-axis.
    -   **6th August**
        -   Refined the arb\* constructions in the scene by better
            orienting some and re-drawing some to improve viewing
            angles.
        -   Superell and ebm introduced in the scene.
        -   Progress done on the script primitive front. I've now
            understood that there are 3 different ways to pass arguments
            to the script primitive. Figuring out the exact parameters
            for the points and vertices didn't take very long (\~1.5
            hours because in python data-types are not defined and
            experimenting with logging requires re-installing the entire
            package again and again).
-   Week 12
    -   **7th August**
        -   Even though I was able to figure out (hopefully) what sort
            of data was required, there are some errors arising in terms
            of unexpected size of params and a clash due to
            multiple-variables coming in with the same name. I was able
            to debug this eventually, though I've had to change the
            original code.
        -   Even after all the arguments are passed, the three
            approaches get stuck at the same place when they try to
            create the curves :
            <https://hastebin.com/unapohiduq.coffeescript>
        -   File :
            <https://github.com/Killthebug/python-brlcad/blob/cd3ed94705933600f2a94f9e7ccde2e2ddd69497/brlcad/primitives/sketch.py#L408>
    -   **8th August**
        -   The sketch primitive binding (on the ctypesgen end) was
            broken/out-dated.
        -   Although I was able to figure out how to pass arguments,
            there were issues with respect the modules involved.
        -   Thanks a ton to Cezar for pointing out some deprecated
            features, but the errors just won't stop.
    -   **9th August**
        -   Spent some time figuring out the sketch primitive but then
            eventually gave up.
        -   I started writing the describe function for the script
            primitive.
    -   **10th August**
        -   A little into today and I've completed the describe
            function.
        -   There's an issue in rt_script_export5(). This is with
            regard to the space allocated for the buffer
            (ep-&gt;extbytes).
        -   Also, 4 characters seemed to be creeping into the struct
            (rt_script_internal \*) script_ip-&gt;s_type variable.
            For now I've handled them by copying the bu_vls to a char
            array and then chopping off the first 4 characters in the
            char array.
        -   script_ip-&gt;s_type still remains to be fixed, but I
            imagine the fix would be minor.
    -   **12th August**
        -   Blog post for python brlcad is up :
            <https://medium.com/p/990e3c286a63/edit>
