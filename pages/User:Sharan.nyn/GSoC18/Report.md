## **Project Report : Check Command and Overlaps Tool**

-   The work done for the project can be split into the following parts:

### libanalyze function -- analyze_overlaps and libged command -- check_overlaps

` NOTE: This was later replaced with better code, check it out `[`here`](https://brlcad.org/wiki/User:Sharan.nyn/GSoC18/Report#new_libanalyze_API_and_check_command_that_uses_this_API)

-   The main goal behind adding a check_overlaps command was that
    libged's rtcheck command acted as a wrapper for the rtcheck program,
    and ran the rtcheck program with execvp command -- this was not
    desired as the execution was done in a different process.
-   I added the check_overlaps command which had the same options as
    rtcheck command and the logic behind shooting of rays was done in
    libanalyze.
-   The overlaps were processed on libged side with callback functions.
-   The submitted patches were committed by Daniel --
    -   [r70995](https://sourceforge.net/p/brlcad/code/70995/)
        [r71008](https://sourceforge.net/p/brlcad/code/71008/)
        [r71402](https://sourceforge.net/p/brlcad/code/71042/)
    -   [r71050](https://sourceforge.net/p/brlcad/code/71050/) -- this
        was later reverted by me
        ([r71059](https://sourceforge.net/p/brlcad/code/71059/))
-   I was given commit access to the repo :) and I did the following
    commits:
    -   [r71063](https://sourceforge.net/p/brlcad/code/71063/)
        [r71065](https://sourceforge.net/p/brlcad/code/71065/)
        [r71066](https://sourceforge.net/p/brlcad/code/71066/)
        [r71067](https://sourceforge.net/p/brlcad/code/71067/)
        [r71103](https://sourceforge.net/p/brlcad/code/71103/)
        [r71108](https://sourceforge.net/p/brlcad/code/71108/)
-   Documentation work related to check_overlaps --
    [\#497](https://sourceforge.net/p/brlcad/patches/497/)

### rtcheck based on libanalyze's analyze_overlaps function

` NOTE: This was later replaced with better code, check it out `[`here`](https://brlcad.org/wiki/User:Sharan.nyn/GSoC18/Report#new_libanalyze_API_and_check_command_that_uses_this_API)

-   Since the logic for shooting the rays was in libanalyze function
    analyze_overlaps.
-   My next task was to refactor rtcheck program to use
    analyze_overlaps.
-   [\#495](https://sourceforge.net/p/brlcad/patches/495/) was
    submitted.

### libanalyze function for grid generation

-   Function that sets the ray starting point and ray directions in a
    grid form was added.
-   This helped reduce the parameters passed to analyze_overlaps -- all
    grid related functions and data was passed in two variables.
-   The following commits were done -
    -   [r71117](https://sourceforge.net/p/brlcad/code/71117/)
        [r71118](https://sourceforge.net/p/brlcad/code/71118/)
        [r71160](https://sourceforge.net/p/brlcad/code/71160/)
-   Later triple grid support and refining was added -
    -   [r71200](https://sourceforge.net/p/brlcad/code/71200/)
        [r71201](https://sourceforge.net/p/brlcad/code/71201/)
        [r71204](https://sourceforge.net/p/brlcad/code/71204/)

### overlaps tool based on check.sh

-   One of the main goals of the project was to remove the need of the
    check.sh because it was a bash script it meant it didn’t work for
    windows system.
-   The same functionality was added with help of a .tcl file.
-   The following commits were done -
    -   [r71106](https://sourceforge.net/p/brlcad/code/71106/)
        [r71107](https://sourceforge.net/p/brlcad/code/71107/)
        [r71149](https://sourceforge.net/p/brlcad/code/71149/)
        [r71150](https://sourceforge.net/p/brlcad/code/71150/)
-   How it looked:
    [overlaps_tool.gif](https://brlcad.org/wiki/File:Overlaps_tool1.gif)

<!-- -->

-   I started to work on better object selection to make it like the
    prototype image I created during the application period
    ([image](http://brlcad.org/wiki/File:CheckGUI.png))
-   The following commits were done -
    -   [r71151](https://sourceforge.net/p/brlcad/code/71151/)
        [r71152](https://sourceforge.net/p/brlcad/code/71152/)
        [r71153](https://sourceforge.net/p/brlcad/code/71153/)
        [r71154](https://sourceforge.net/p/brlcad/code/71154/)
        [r71155](https://sourceforge.net/p/brlcad/code/71155/)
-   Better object selection:
    [better_object_sel.gif](https://brlcad.org/wiki/File:Overlaps_tool2.gif)
-   Final image:

<!-- -->

-   ![](img/Overlaps_tool_final.png)

<!-- -->

-   Documentation was done --
    [r71498](https://sourceforge.net/p/brlcad/code/71498/)

### new libanalyze API and check command that uses this API

-   The goal behind this task was to combine the geometry analysis tools
    -- rtcheck, gqa and glint into one command.
-   A libanalyze API was discussed that contained the backend logic of
    these commands in one place.
-   The check command has sub-commands for - overlaps, mass, volume,
    surface area, gaps, adjacent air, exposed air and unconfined air.
-   This task involved many commits. For list of commits please refer to
    *week 10 - week 12* in my daily log available here
    -[Log](http://brlcad.org/w/index.php?title=User:Sharan.nyn/GSoC18/Log#Week_10)

<!-- -->

-   Since I added a better command for checking overlaps (*check
    overlaps \[options\]*). I removed the old check_overlaps and
    analyze_overlaps function.
-   And adapted the code for the new check overlaps command. For commits
    refer to week 13's log -
    [Week-13](http://brlcad.org/w/index.php?title=User:Sharan.nyn/GSoC18/Log#Week_13)

<!-- -->

-   I also wrote some bash scripts to compare the outputs of check vs
    rtcheck/gqa --
    [r71355](https://sourceforge.net/p/brlcad/code/71355/)
-   Documentation and man page for check command was added -
    [r71374](https://sourceforge.net/p/brlcad/code/71374/)
    [r71393](https://sourceforge.net/p/brlcad/code/71393/)

### rtcheck and gqa based on the libanalyze API

-   Since the backend logic of gqa and rtcheck lives in
    libanalyze/api.c. The duplicated code in gqa and rtcheck can be
    removed.
-   rtcheck and gqa were changed to use the libanalyze functions.
-   work related to rtcheck and gqa can be found in the public Google
    Drive Folder linked below

### Files

This public Google Drive folder contains all the files which I worked on
almost exclusively during the coding period -

-   [saran_narayan-gsoc18-brlcad](https://drive.google.com/drive/folders/1WueiX-Cg21SpQ4lYmkhO6Qo40fwZSaaH?usp=sharing)

### Logs

-   [Daily
    Logs](http://brlcad.org/w/index.php?title=User:Sharan.nyn/GSoC18/Log)
-   The log also contains links to all my commits and patches.
