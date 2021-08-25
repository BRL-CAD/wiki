### Development Logs

#### Community Bonding Period

-   Explored the Qt's documentation for different shortcuts declaration
    styles.
-   Made myself comfortable with Qt Programming\[By following
    tutorials\].
-   Cleaned the code for an existing PR on Shortcut Configuration

#### Coding Period

-   June 1-June 7:
    -   Complete GUI Form \[continued work from Bonding Period\]
    -   Add the GUI in preferences.
    -   Made the GUI Functional and interactive
    -   Added the support for writing the shortcuts to config-file.

<!-- -->

-   June 8-June 14:
    -   Code Cleaning
    -   Add Seach-Box in GUI
    -   Made search efficient.

<!-- -->

-   June 15-June 21:
    -   Add more functionality, like reset to defaults
    -   Got first feedback
    -   Worked on feedback changes

<!-- -->

-   June 22 - June 28:
    -   Changed existing QShortcuts to QActions
    -   Minor fixes

<!-- -->

-   June 29 - July 3:
    -   Received good feedback from the mentors.
    -   Removed bugs from the GUI like multiple Shortcut Catcher Dialog
        boxes while searching.
    -   Gave special attention towards the undefined behavior due to
        unassigned pointers, Rule of 0/3/5 inconsistencies.

<!-- -->

-   July 4 - July 12:
    -   Started Working on the Number-Scroll via mouse feature.
    -   Skimmed through the code for the existing Scintilla Editor Code.
    -   Wrote the code for handling the mouse wheel events.
    -   Stuck on the abrupt jump of the number on scrolling.

\[Bug- when I scroll the wheel one time then the wheel event is
triggered twice.\]

-   July 13- July 19:
    -   Talked with mentors regarding the bug.
    -   Fixed the bug by installing event filter on the viewport()
    -   Added an option to modify the step-size in the Preferences.

<!-- -->

-   July 20 - July 26:
    -   Encountered a new bug causing abrupt jump of caret while
        changing the most significant digit.
    -   Added an option to choose modifiers in the Preferences.
    -   Fixed the bugs.

<!-- -->

-   July 27 - July 31:
    -   Started working on feedbacks for Number-Scroll PR,
    -   Made some changes in the Shortcuts-GUI PR for fixing more bugs,
        which my mentors bring into the attention.

<!-- -->

-   Aug1 - Aug 9 :
    -   Fixed anomalous primary shortcut bug.
    -   Add appropriate access modifiers to the ShortcutConfigurator
        Class.
    -   Few more GUI enhancements in Shortcuts-GUI like changing column
        according to search.
    -   Started working on Error-Log Feature.
    -   Added initial GUI for Error-Log in the form of a Dockable Widget
        in MainWindow.
    -   Add a new output_handler for Error-Log.

<!-- -->

-   Aug 10 - Aug 16:
    -   Continuous Discussion with mentors and community regarding the
        need to remove old PRINTB() like macro expansion from the
        source-code, and replace it with a new LOG() statements.
    -   Added a MessageClass for messages of all types in the
        application and a new LOG() function.
    -   Started Replacing the 380+ PRINTB,PRINT,PRINT_DEPRECATION
        statements with new LOG() statements.

Aug 17 - Aug 23:

-   -   Continued replacing the old statements with a new one. \[Took
        more than expected, because of my mistake and
        misinterpretation\]
    -   Figured out why, echo tests are failing.
    -   Worked on the failing tests.

Aug 24 - Present:

-   -   Finished up the work with failing tests,
    -   Implement Jump to Error Location.