### Development Logs

#### Community Bonding Period

Due to my semester end exams (Apr 26 - May 17), my time spent during
community bonding period was less but I still managed to do the
following:

-   Week 1
    -   Prepared a flowchart to understand how the execution of the
        rtcheck program works :
        [rtcheck_flow](../../img/Rtcheck_flow.jpeg)
    -   Was introduced to 'gdb' which helped me a lot to analyze the
        flow.
    -   Understood how the front-end portions of rt and back-end
        portions are connected by linking the view\*.c files

<!-- -->

-   Week 2
    -   Read the documentation to understand the RTUIF API :
        <https://brlcad.org/wiki/Developing_applications>
    -   Understood the origins of libanalyze functions.
    -   Discussed some ideas on how to implement the libanalyze
        function, all were bad ideas because they all involved calling
        the rtcheck program using execvp() as they usually end with
        exit().
    -   Was suggested a basic plan on how to proceed.
    -   Understood how libanalyze functions were used by an example :
        libged/voxelize.c and libanalyze/voxels.c

<!-- -->

-   Week 3
    -   Complied a version of the rtcheck program by just copying the
        relevant files to libanalyze/overlaps/.
    -   Discussed the plan related to rtcheck in detail.
    -   Understood the concept of using contexts and callback functions.
    -   Tried out callback functions, implementing a basic callback
        function that alters an int.

#### Coding Period

##### Week 1

-   14/05/18
    -   trying to build a new rtcheck command by stripping down the
        non-necessary parts of the front-end, so that the code is easier
        to understand.
    -   discussed a lot of issues with mentor.

<!-- -->

-   15/05/18
    -   started working on the design of the libanalyze function
    -   all parts of rt/main.c and do_ae() done

<!-- -->

-   16/05/18
    -   added do_frame(), do_run() and grid_setup() to libanalyze.

<!-- -->

-   17/05/18
    -   added worker() and do_pixel()
    -   used a worker_context to pass data to worker using the void
        pointer for bu_parallel
    -   when I ran the command I was getting segfault at rt_gettrees,
        thought I'd fix it next day

<!-- -->

-   18/05/18
    -   figured out the problem but it meant moving a lot of content to
        libanalyze
    -   I did it anyway out of curiosity and it fixed the problem with
        rt_gettrees still it crashed at rt_shootray!
    -   At the end of the day after a lot of debugging and trials, found
        out that rt_shootray was calling the hit sequence of gqa :O,
        not sure why.
    -   A quick rename of the hit sequence of libanalyze to check_hit
        solved the problem.
    -   Still need to figure out how to call rt_gettrees without moving
        all function calls to libanalyze.

<!-- -->

-   19/05/18
    -   Added code to fill the overlap list passed through callback
        data.
    -   Using \`gedp-&gt;ged_wdbp-&gt;dbip\` to get the db name instead
        of asking it before objects.

<!-- -->

-   20/05/18
    -   Fixed printing of the overlap list.

##### Week 2

-   21/05/18
    -   Clean-up of the libanalyze function :
        -   Fixed a derp with setting default values of width and height
            in libanalyze instead of libged.
        -   Removed redundant header files.
    -   Read code for libged/gqa.c
    -   Prepare patch for the work done in first week.

<!-- -->

-   22/05/18
    -   Submitted the
        patch:[\#488](https://sourceforge.net/p/brlcad/patches/488)
    -   Did follow up and submitted v2.

<!-- -->

-   23/05/18
    -   Didn't do much today : Read the checker.tcl file for
        understanding.

<!-- -->

-   24/05/18
    -   Updated the patch and submitted v3.

<!-- -->

-   25/05/18
    -   Discussed the plans for refactoring rtcheck.
    -   Started work on rtcheck.

<!-- -->

-   26/05/18
    -   Added plot file output option.
    -   Fixed check_overlaps command not showing up in Archer.
    -   Submitted patch
        [\#491](https://sourceforge.net/p/brlcad/patches/491/) fixing
        some minor issues with the accepted patch \#488.

<!-- -->

-   27/05/18
    -   Added old_way of processing stdin.
    -   Added command driven way of processing stdin.
    -   Have to test the changes, it compiles fine.

##### Week 3

-   28/05/18
    -   Couldn't code in the morning hours. My cousin brother came and
        played games on my PC all day!
    -   Added getting objects from view feature to ged_check_overlaps
    -   Tested rtcheck executable for matflag inputs.

<!-- -->

-   29/05/18
    -   Trying my best to get the display of overlaps working for
        ged_check_overlaps.
    -   Okay it worked but I used temp file so that I could use two
        inbuilt functions pdv_3line and rt_process_uplot_value. But
        using them is not needed. So as suggested by Daniel, I will try
        to merge them together and remove the file dependency and
        buildup the list in my overlapsHandler.
    -   With it I found one more bug with yesterday's work, that if do
        draw g4 and do checkover_laps g4 then it would consider g4
        twice! :/. To solve this Daniel suggested to not consider
        visible objects if objects are mentioned with command.
    -   Success! all worked out with so much minimal code, just 5 lines
        instead of my initial work that involved 25 lines.

<!-- -->

-   30/05/18
    -   Fixed bug with overlays considered as visible object on second
        run.
    -   while testing matflag for rtcheck:
        -   fixed a bug in tree command.
        -   added parsing of az/el in degree/radians values for cm_ae.
        -   fixed issue with Multiview giving segfault.
    -   Added -r, -R flag to rtcheck.
    -   Added -d flag to rtcheck and check_overlaps to print some debug
        information.

<!-- -->

-   31/05/18
    -   Fixed a major flaw in the overlapsHandler giving the same data
        for both reg1 and reg2.
    -   Fixed issue of getting first row of plot file as W 0 0 0 0 0 0
    -   Added feature to check_overlaps for getting view information
        from gedp.

<!-- -->

-   1/06/18
    -   Fixed scrambled overlays from check_overlaps.
    -   Experimenting with bu_list for overlaps list.

<!-- -->

-   2/06/18
    -   Using bu_list for overlaps_list in rtcheck
    -   Didn't do much other than that, spent some time with family :)

<!-- -->

-   3/06/18
    -   Submitted v2 patch for check_overlaps changes
        [\#491](https://sourceforge.net/p/brlcad/patches/491)
    -   Fixed bug with multiview caused by handling overlapList in main,
        moving to do_frame solved it.
    -   Submitted patch
        [\#494](https://sourceforge.net/p/brlcad/patches/494/) fixing
        again some issues with \#491 :D

##### Week 4

-   4/06/18
    -   Adapting archer to use check_overlaps instead of rtcheck to
        libged/rtcheck.c
    -   Applied fix for fix-me comment as suggested by Daniel.
    -   Figured out why wireframes weren't displayed in Archer, turned
        out to be not compiling with openGL.

<!-- -->

-   5/06/18
    -   Submitted patch
        [\#495](https://sourceforge.net/p/brlcad/patches/495/) for
        rtcheck program.
    -   Continuing work on adaptation of archer.
    -   Finally figured out how to deal with pane data in archer, spent
        hours to figure it out and it was a really simple thing xD. Just
        needed to use to_view_func instead of to_pass_through_func
        in tclcadobj.c
    -   with that I think I am done with adapting check_overlaps and
        ready to remove libged/rtcheck.c

<!-- -->

-   6/06/18
    -   Started documentation works, it is not much fun :/ so didn't do
        much.

<!-- -->

-   7/06/18
    -   Changed check_overlaps behavior to get objects only from view,
        updated the related documentation too. \*REVERTED\*
    -   Added handling for when the user mentions duplicate objects for
        rtcheck
    -   Submitted patch adapting check_overlaps to archer and mged
        [\#496](https://sourceforge.net/p/brlcad/patches/496/)

<!-- -->

-   8/06/18
    -   Completed documentation.
    -   Submitted patch for documentation
        [\#497](https://sourceforge.net/p/brlcad/patches/497/).

<!-- -->

-   9/06/18
    -   Had to revert adaption patch because we can't remove rtcheck
        without deprecation.

<!-- -->

-   10/06/18
    -   Fixed a bug with check_overlaps and rtcheck allocation of
        memory for region names. committed -
        [r71063](https://sourceforge.net/p/brlcad/code/71063/)
    -   compared the outputs of old rtcheck program and new rtcheck
        program.
        -   got it to match finally after small tweaks

##### Week 5

-   11/06/18
    -   reapply reverted changes for adaption of check_overlaps to
        archer.
        -   committed the changes -
            [r71065](https://sourceforge.net/p/brlcad/code/71065/),
            [r71066](https://sourceforge.net/p/brlcad/code/71066/) and
            [r71067](https://sourceforge.net/p/brlcad/code/71067/)
    -   Had a hard time fighting with sourceforge to push the commits :/
    -   reworked the documentation because of removal of rtcheck without
        deprecation.

<!-- -->

-   12/06/18
    -   fixed MGED's overlap tool -
        [r71068](https://sourceforge.net/p/brlcad/code/71068/)
    -   Just read through the checker.tcl file.

<!-- -->

-   13/06/18
    -   Continued reading.
    -   Fixed rtcheck and matched output with new rtcheck

<!-- -->

-   14/06/18
    -   Nothing much done today, made a plan to proceed further.

<!-- -->

-   15/06/18
    -   Started work on porting check.sh to a Tcl file.
    -   Now able to print the list, need something to store the values
        efficiently.

<!-- -->

-   16/06/18
    -   Storing the overlaps as objects of a class, which is stored in a
        list.

<!-- -->

-   17/06/18
    -   Took some rest and spent time with family ^_^.

##### Week 6

-   18/06/18
    -   Continued work on overlap tool.
    -   Added check for if the objects actually exists.
    -   Showing status on what the tool is doing.
    -   Better sorting done.

<!-- -->

-   19/06/18
    -   Using simple lists now in overlap tool instead of using classes
        and objects which made everything complicated.
    -   Fixed a bug with check.sh
        [r71093](https://sourceforge.net/p/brlcad/code/71093/)

<!-- -->

-   20/06/18
    -   Using Itcl and Itk for overlap tool.
    -   Added progress bar.

<!-- -->

-   21/06/18
    -   Read documentation of Itcl and Itk to get idea on how to use it.

<!-- -->

-   22/06/18
    -   Added overlap menu with options to browse, create new overlaps
        file and run check
    -   Integrated everything together

<!-- -->

-   23/06/18
    -   Read gqa related code, since I was waiting for the feedback on
        the above works.

##### Week 7

-   25/06/18
    -   Trying to fix bugs with check_overlaps and gqa with havoc.g.

<!-- -->

-   26/06/18
    -   Added comments to the tcl file for overlaps menu.
    -   Cleaned up the overlaps menu code.

<!-- -->

-   27/06/18
    -   Didn't do much work, just discussed about the issues with
        havoc.g.
-   28/06/19
    -   trying to visualize gqa using geogebra with the coordinates
        printed out with -d option.
    -   fixed a small bug with gqa :)
        [r71101](https://sourceforge.net/p/brlcad/code/71101/)

<!-- -->

-   29/06/18
    -   Bind return key to check overlaps button and take focus to text
        entry in overlaps file tool.
    -   Fixed a bug with loading of overlaps.
    -   Browsing is restricted to '.overlaps' file.
    -   Add a validity check to check if the browsed overlaps file is a
        valid one.

<!-- -->

-   30/06/18
    -   Didn't code.

<!-- -->

-   1/07/18
    -   Changed the looks of the overlaps menu.
    -   Added hints for the user.

##### Week 8

-   2/07/18
    -   Committed :
        [r71106](https://sourceforge.net/p/brlcad/code/71106/) and
        [r71107](https://sourceforge.net/p/brlcad/code/71107/) for
        overlaps_tool
    -   Discussed next task.

<!-- -->

-   3/07/18
    -   Fixed check_overlaps crash on windows build.
        [r71108](https://sourceforge.net/p/brlcad/code/71108/)
    -   Trying to figure out the arguments of the grid generator such
        that it is suitable for both check_overlaps and gqa.
    -   Thanks to Daniel, I have a good plan to proceed! Will get
        started on grid generator tomorrow.

<!-- -->

-   4/07/18
    -   Added grid generating function to libanalyze.
    -   Reduced the parameter list to analyze_overlaps, now it just
        uses a grid structure and a grid shooting function.

<!-- -->

-   5/07/18
    -   Made changes to gqa and made it use the grid generating
        function.

<!-- -->

-   6/07/18
    -   Update rtcheck to use the new grid generator function.
    -   Committed the changes to repo :
        [r71117](https://sourceforge.net/p/brlcad/code/71117/),
        [r71118](https://sourceforge.net/p/brlcad/code/71118/) and
        [r71119](https://sourceforge.net/p/brlcad/code/71119/)

<!-- -->

-   7/07/18, 8/07/18
    -   Discussing the next task to do.

##### Week 9

-   09/07/18
    -   Started the next task of "Better object selection in overlaps
        tool"
    -   Added geometry browser in the overlaps tool
    -   Split the overlaps menu and overlaps file gen as two separate
        files.
    -   Improved object selection
    -   Added listview for selected objects

<!-- -->

-   10/07/18
    -   Added ability to add/remove manual entry of objects.
    -   Can add/remove objects using wildcards.

<!-- -->

-   11/07/18
    -   Added doxygen comments for grid-generating functions -
        [r71147](https://sourceforge.net/p/brlcad/code/71147/)
    -   Fixed a bug with gqa -
        [r71148](https://sourceforge.net/p/brlcad/code/71148/)
    -   Committed the whole progress into multiple commits :)
        -   [r71149](https://sourceforge.net/p/brlcad/code/71149/)
        -   [r71150](https://sourceforge.net/p/brlcad/code/71150/)
        -   [r71151](https://sourceforge.net/p/brlcad/code/71151/)
    -   Restore handling visible objects -
        [r71152](https://sourceforge.net/p/brlcad/code/71152/)
    -   No need to check the objects again -
        [r71153](https://sourceforge.net/p/brlcad/code/71153/)
    -   Add clear selection button -
        [r71154](https://sourceforge.net/p/brlcad/code/71154/)
    -   Code cleanup -
        [r71155](https://sourceforge.net/p/brlcad/code/71155/)

<!-- -->

-   12/07/18
    -   Just went through the code.
    -   Discussed the gqa bug.

<!-- -->

-   13/07/18
    -   Add the 3 axis grid support to check_overlaps.
    -   Discussed about the API design.

<!-- -->

-   14/07/18
    -   Tried to write a header file for public API for rtcheck and gqa.

<!-- -->

-   15/07/28
    -   Attempted to add az/el supported to gqa(3 axis) but couldn't
        find a good solution.
    -   Spent the most of the time with family, but hey it was weekend
        ;)

##### Week 10

-   16/07/18
    -   Started work on the check command.
    -   Added processing of the sub-commands given like overlaps,
        volume, weight etc
    -   Added the parsing of the options.
    -   Added object parsing -- visible and cmd-line.
    -   Added az/el for single grid.
    -   Added single grid setup.

<!-- -->

-   17/07/18
    -   Added triple grid related functions to libged and libanalyze.
    -   Added a general libanalyze function.
    -   Made the check overlaps sub command to work.
    -   Submitted for review on zulip.

<!-- -->

-   18/07/18
    -   Fixed grid refining, now it works perfect.
    -   Added overlay and plot file saving to check overlaps.

<!-- -->

-   19/07/18
    -   Nothing done today.
    -   Still working on the plan. Once it is set would go at full speed
        ;)

<!-- -->

-   20/07/18
    -   Committed triple grid functions and refining
        [r71200](https://sourceforge.net/p/brlcad/code/71200/)
    -   Options parsing from libged to libanalyze using bu_hash_tbl
        implemented.
        -   the benefit of using hash_table is that we can pass key
            value pairs and just grab those options that are set. The
            other options can have meaningful defaults.
    -   Removed some global variables in libanalyze/api.c and used
        options passed from libged.
    -   Added single grid and az/el functions in libanalyze/api.c.

<!-- -->

-   21/07/18
    -   lots of work done on both check.c and api.c
    -   Got check overlaps and check volume ready.
    -   Removed hash_table for parsing the options.

<!-- -->

-   22/07/18
    -   Added exp_air sub command (needs testing)
    -   Committed all the work done so far:
        -   [r71204](https://sourceforge.net/p/brlcad/code/71204/)
        -   [r71205](https://sourceforge.net/p/brlcad/code/71205/)
        -   [r71206](https://sourceforge.net/p/brlcad/code/71206/)
        -   [r71207](https://sourceforge.net/p/brlcad/code/71207/)
    -   Added check gaps command.
        [r71208](https://sourceforge.net/p/brlcad/code/71208/)
    -   Cleaned up some code:
        -   [r71209](https://sourceforge.net/p/brlcad/code/71209/)
        -   [r71210](https://sourceforge.net/p/brlcad/code/71210/)
        -   [r71211](https://sourceforge.net/p/brlcad/code/71211/)
        -   [r71212](https://sourceforge.net/p/brlcad/code/71212/)
        -   [r71213](https://sourceforge.net/p/brlcad/code/71213/)
        -   [r71214](https://sourceforge.net/p/brlcad/code/71214/)

##### Week 11

-   23/07/18
    -   Added check adj_air -
        [r71217](https://sourceforge.net/p/brlcad/code/71217/)
    -   Bug fixes to api.c -
        [r71218](https://sourceforge.net/p/brlcad/code/71218/)
        [r71219](https://sourceforge.net/p/brlcad/code/71219/)
    -   Added check weight -
        [r71220](https://sourceforge.net/p/brlcad/code/71220/)
    -   Code cleanup -
        [r71221](https://sourceforge.net/p/brlcad/code/71211/)
        [r71222](https://sourceforge.net/p/brlcad/code/r71222/)
    -   Passing bu_vls struct for verbose and debug information -
        [r71223](https://sourceforge.net/p/brlcad/code/71223/)
    -   Fix a derp with check_overlaps -
        [r71224](https://sourceforge.net/p/brlcad/code/71224/)
    -   rename weight to mass -
        [r71225](https://sourceforge.net/p/brlcad/code/71225/)

<!-- -->

-   24/07/18
    -   Added moments and centroid -
        [r71240](https://sourceforge.net/p/brlcad/code/71240/)
        [r71241](https://sourceforge.net/p/brlcad/code/71241/)
    -   Added check surf_area
        [r71247](https://sourceforge.net/p/brlcad/code/71247/)

<!-- -->

-   25/07/18
    -   Updated api.c for single_grid -
        [r71253](https://sourceforge.net/p/brlcad/code/71253/)
    -   print per-region stats is now working for volume and mass -
        [r71258](https://sourceforge.net/p/brlcad/code/71258/)
    -   Add -i option to check overlaps -
        [r71259](https://sourceforge.net/p/brlcad/code/71259/)
    -   Add quiet missed report and required number of hits to check
        command and libanalyze api -
        [r71260](https://sourceforge.net/p/brlcad/code/71260/)
    -   Discussed about surf_area and tried to fix it.

<!-- -->

-   26/07/18
    -   Not much work done today, had to visit college.
    -   Read glint to add features of glint to libanalyze API
    -   Improved surface area algorithm, thanks to Daniel for suggesting
        the trick.

<!-- -->

-   27/07/18
    -   Committed the surf_area algorithm -
        [r71279](https://sourceforge.net/p/brlcad/code/71279/)
    -   Tried to understand the differences in the grids of check and
        glint.

<!-- -->

-   28/07/18
    -   Placement training classes (26/07 - 28/07) is over -- back to
        full speed :)
    -   committed [r71289](https://sourceforge.net/p/brlcad/code/71289/)
        to get correct grid size.
    -   changed the signature of overlaps_callback function pointer -
        [r71290](https://sourceforge.net/p/brlcad/code/71290/)
    -   start work on glint analysis options -
        [r71291](https://sourceforge.net/p/brlcad/code/71291/)
    -   bug fix for surf_area -
        [r71292](https://sourceforge.net/p/brlcad/code/71292/)
    -   added glint analysis functions and variables -
        [r71293](https://sourceforge.net/p/brlcad/code/71293/)

<!-- -->

-   29/07/18
    -   Did not work.

##### Week 12

-   30/07/18
    -   Added unconf_air sub-command -
        [r71300](https://sourceforge.net/p/brlcad/code/71300/)
    -   Move all the left globals to current_state -
        [r71301](https://sourceforge.net/p/brlcad/code/71301/)
        [r71302](https://sourceforge.net/p/brlcad/code/71302/)
    -   Added some more verbose messages -
        [r71303](https://sourceforge.net/p/brlcad/code/71303/)
    -   Added functions for total moments, volume, mass and centroid -
        [r71305](https://sourceforge.net/p/brlcad/code/71305/)

<!-- -->

-   31/07/18
    -   Added functions for per-region status and total values of
        surf_area -
        [r71317](https://sourceforge.net/p/brlcad/code/71317/)
    -   Add a new variable gridRatio to set uneven grid cells for
        rtcheck - [r71320](https://sourceforge.net/p/brlcad/code/71320/)
        [r71322](https://sourceforge.net/p/brlcad/code/71322/)
    -   bug-fix for api.c -
        [r71321](https://sourceforge.net/p/brlcad/code/71321/)

<!-- -->

-   1/07/18
    -   after struggling to understand what aspect does -- added a
        variable aspect because there was no way around it
        [r71337](https://sourceforge.net/p/brlcad/code/71337/)
    -   replace getfromview by setviewinformation -
        [r71338](https://sourceforge.net/p/brlcad/code/71338/)

<!-- -->

-   2/07/18
    -   get rtcheck working with libanalyze/api.c as base.
    -   wrote scripts to test check command with gqa and rtcheck.

<!-- -->

-   3/07/18
    -   Uploaded the final scripts to the repo -
        [r71355](https://sourceforge.net/p/brlcad/code/71355/)
    -   Updated the check overlaps printing style -- now like rtcheck -
        [r71359](https://sourceforge.net/p/brlcad/code/71359/)

<!-- -->

-   4/07/18
    -   started work on documentation of check command.
    -   small fix for check overlaps --
        [r71372](https://sourceforge.net/p/brlcad/code/71372/)
    -   documentation work related to check command done -
        [r71374](https://sourceforge.net/p/brlcad/code/71374/)
    -   small build error pointed by Cezar fixed -
        [r71377](https://sourceforge.net/p/brlcad/code/71377)

<!-- -->

-   5/07/18
    -   Took a break and did not work :)

##### Week 13

-   6/07/18
    -   Start removal of check_overlaps.
    -   Removed from Archer; Added check command -
        [r71388](https://sourceforge.net/p/brlcad/code/71388/)
    -   Small fix in api.c -
        [r71389](https://sourceforge.net/p/brlcad/code/71389/)
    -   make use of check overlaps in overlaps_tool -
        [r71391](https://sourceforge.net/p/brlcad/code/71391/)
    -   Add grid size option to check and api.c -
        [r71392](https://sourceforge.net/p/brlcad/code/71392/)
    -   Updated the doc -
        [r71393](https://sourceforge.net/p/brlcad/code/71393/)
    -   Update archer for the new option -
        [r71394](https://sourceforge.net/p/brlcad/code/71394/)
    -   Update overlaps_tool for the new option -
        [r71395](https://sourceforge.net/p/brlcad/code/71395/)

<!-- -->

-   7/07/18
    -   removed libged/check_overlaps.c --
        [r71412](https://sourceforge.net/p/brlcad/code/71412/)
    -   removed libanalyze/overlaps/analyze_overlaps.c --
        [r71413](https://sourceforge.net/p/brlcad/code/71413/)
    -   started work on gqa.c

<!-- -->

-   8/08/18
    -   added function to get grid summary --
        [r71439](https://sourceforge.net/p/brlcad/code/71439/)
    -   some w/s and comments in libanalyze/check_options.c --
        [r71440](https://sourceforge.net/p/brlcad/code/71440/)
    -   Add some comments in libanalyze/api.c --
        [r71441](https://sourceforge.net/p/brlcad/code/71441/)

<!-- -->

-   9/08/18
    -   fix overlaps_tool not able to run checker tool --
        [r71467](https://sourceforge.net/p/brlcad/code/71467/)
    -   Fix indentation of the overlap_tool.xml file --
        [r71470](https://sourceforge.net/p/brlcad/code/71470/)

<!-- -->

-   10/08/18
    -   Start work on the final project report.
    -   [Report](Report.md)

<!-- -->

-   11/08/18
    -   Had a busy day -- college works and family took up most of my
        time.

<!-- -->

-   12/08/18
    -   Update the documentation for overlap_tool -
        [r71498](https://sourceforge.net/p/brlcad/code/71498/)
