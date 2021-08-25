# Community Bonding Period

-   Wrote code for new scadlexer in scadlexer.h and scadlexer.cpp files.
-   Fetch the colors in scintillaeditor.cpp file for new scadlexer and
    it is successfully working
-   Wrote functions on highlighting keywords and highlighting comments.
-   Tested with Qt4 as well as Qt5
-   Wrote function for highlight multiline comments
-   Wrote function to highlight numbers
-   Trying to search any better way for lexing approach using
    QSciLexerCustom class.

# Coding Period

## 25 May

-   Discussed and researched about different tools that can be used in
    scad lexer.

## 26 May

-   Chosen lexertl to be used for scad lexer.
-   Started reading lexertl documentation

## 27 May

-   Lexertl in boost is not the latest version, so as per its latest
    documentation it doesn't work, trying to read code of lexertl
    included in boost

## 28 May

-   Contacted Ben Hanson, the person who wrote lexertl and its
    documentation and he suggested to use the latest version of lexertl
    and not that included in the boost, because the latest version has
    some bug fixes and it also supports unicode. Also it is header file
    library so, we won't be needing to make any change in installation
    script
-   Discussed about this with my mentors
-   Added lexertl header files in openscad new branch lexertl

## 29 May

-   Read lexertl documentation and examples at
    <https://github.com/BenHanson/lexertl/tree/master/examples> and
    tried to add something into scadlexer files to test its working.

## 30 May

-   Added rules for numbers, operators etc and divide code into tokens.
-   Wrote the code for lookup table.

## 1 June

-   Successfully started highlighting keywords using lexertl tool in
    scadlexer.

## 2 June

-   Added rules for single line and multi line comments.
-   Multi line comments are not working as expected.

## 3 June

-   Read more about regular expression to have an efficient rule for
    single line and multi line comments.

## 4 June

-   Editor became slow. Trying to figure out what's the problem with it.
    May be the styleText function is being called again and again and so
    with it all rules of lexer are being called again and again on
    making any change in the editor by the user.

## 5 June

-   Discussed with mentors and defined all the rules in constructor
    instead of styleText function and this way, editor got its normal
    speed.

## 6 June

-   Discussed with mentors about problems in comments and keyword
    highlighting and started writing tests.

## 8 June

-   Wrote a C++ program using lexertl library with simple rules as
    testing.

## 9 June

-   Get the tests written checked by mentors and made more improvements.

## 10 June

-   Preparation for viva-voce in college, generating report and
    presentation

## 11 June

-   All day spent in college for waiting and delivering presentation to
    teachers and students

## 12 June

-   Read more in lexertl documentation to write comments as another
    state machine.

## 15 June

-   Discussed with mentors about writing tests, ie, reading scad script
    from an input file, mark the keywords, numbers etc and then put the
    output in another file.

## 16 June

-   Wrote test in C++ using lexertl library, defining various rules,
    which puts in the output in output file and get it checked by the
    mentors.

## 17 June

-   Compiled test suite of openscad and read its documentation.
-   Wrote lexertest in openscad test suite.

## 18 June

-   Made a new class Lex that can be used commonly by the tests as well
    as the scadlexer.
-   Added lexer rules in the class but it is not resulting any kind of
    highlighting.

## 19 June

-   The new syntax of stl vector class used to push all elements in one
    line could only be compiled using C++11 reference, so it didn't work
    while making openscad tests. The default syntax of pushing elements
    will increase a lot of line of code as a lot many elements need to
    be inserted.

<!-- -->

-   To solve above problem simple C style array are used to store all
    elements.

<!-- -->

-   Keyword lists in scadlexer were removed as now it will be using the
    arrays defined in lex class.

<!-- -->

-   Still not resulting highlighting.

## 20 June

-   lex file object is added in lexertest of openscad.
-   lex.cc file reference is added in CMakeList and solved reference
    error.
-   Removed the vectors defined in tests, as it will also be using the
    arrays defined in lex class.

## 22 June

-   Number of elements in each array is calculated by sizeof function
    and put in defineRules function of lex class as an argument.
-   Added more rules in lex class
-   Solved more errors and highlighting of different tokens start
    working using lex class.

## 23 June

-   Put the while loop which is reponsible for highlighting tokens
    according to the defined rules into the Lex class so that it can
    also be used commonly by lexertest test and scadlexer class.

## 24 June

-   Made LexInterface as abstract class to call the highligting()
    function of different classes(scadlexer and lexer in lexertest file)
    in Lex class.
-   Removed errors in lexertest file and compiled the tests
-   Discussed with mentors about writing the test cases

## 25 June

-   Wrote 2 test cases and write the file path in CMakeFile.txt file to
    pass them to add_cmdline() function so that respective python
    script that take those files and input, run the lexertest and
    generate respective output.
-   Pass both tests

## 27 June

-   Multiline comments were causing problem in main lexing, as the value
    of start becomes the start of the line when some changes are made in
    particular line.
-   Trying to figure out more such problem in lexing.

## 28 June

-   To test this multiline commenting thing in lexertest, the value of
    the start is made changed but currently, it is not affecting the
    output of the test.

Trying to figure out the problem.

## 29 June

-   In highlighting function, the start was supposed to be used to
    change the pointer from where the file start to be changed. But
    recently, the variable start was not used in the function at all, so
    it was not causing any change.
-   Trying to figure out, how will it be used in the function

## 30 June

-   Trying to use the seekp function to put the start pointer at
    different location, but as the highlighting function is being called
    again and again at every token whereas the start is remained fixed.
    It is not giving the expected result.
-   Trying with more functions to generate the expected output.

## 1 July

-   Use tellp to check the current location of pointer, it is more than
    start, then highlight it otherwise, right the script as it is.
-   But it didn't behave same as openscad qscintilla editor. Discussed
    with mentors about the problem that, whole source string need to be
    divided into substring starting from start.

## 2 July

-   Divide the source string into substring started from start, but
    still the index of token in lexertest is different than in openscad
    editor because of tabs as openscad editor take tab as number of
    space tokens whereas lexertest takes tab as single token.
-   Change tab to spaces in lexerinput file, now editor and tests are
    behaving same, having same token index.

## 3 July

-   Scad Lexer is facing the problem of multiline comments, as the start
    variable in scadlexer is the start of current line, instead of start
    of document. So some changes are made within multiline comments, it
    gets highlighted again according to other rules instead of being the
    part of comment.
-   The behavior of the keywords are also not so good. Discussed with
    mentors about these problems and tried to find out the solution.

## 4 July

-   The problem of unusual behavior of highlighting of keywords with
    context to other text has been solved by calling highlighting
    function for variables with lexer rule id 9.
-   Wrote a new test named syntaxtest to check the style of all possible
    tokens in the openscad script.

## 6 July

-   A lexer rule for special variables in openscad starting with $ has
    been defined and highlighting function has been called for it.
-   Also read about modifiers and tried to highlight them, but talked to
    mentor about its highlighting style as it should be highlighted just
    as a single character or as multiline comments.

## 7 July

-   It is decided to highlight modifiers just as single character until
    the multiline comment problem is solved.

<!-- -->

-   Trying to read the documentation of scintilla
    <http://scintilla.org/ScintillaDoc.html> to find something useful
    for multiline comment highlighting successfully.

## 8 July

-   Read Qscintilla existing lexer such as LexMSSQL to get the idea of
    how these lexers are handling multiline comments.
-   Also get the concept of multi state for handling multi line
    comments.

## 9 July

-   SCI_GETSTYLEAT function has been found to get the style at a
    particular position.
-   SCI_GETCURRENTPOS function will be using to get the location of
    cursor.
-   Wrote code in the scadlexer to get the style at cursor position
    whenever user make any change in the script.

## 10 July

-   Used debugger to solve the problem of highlighting function being
    called again and again for some tokens. The problems was missing
    break statement in switch statement in some cases.

<!-- -->

-   Crashing of the application solved by removing additional setStyling
    statement in highlighting function and put that in if condition.

## 11 July

-   Used multi state feature of lexertl and changed the state of
    statement having existing style as comment or style at starting
    location as comment to comment with statement "results.start = 1",
    means like telling the lexer to highlight a statement inside /\* and
    \*/ as comment and not as regular text and keywords.
-   With this the problem of multiline comments has been solved.
-   Moving forward to apply same feature for highlighting modifiers.

## 13 July

-   Reading about different modifiers, so that they can be styled,
    obvious to the regular user.
-   Defining state for different modifiers \*, %, !, \# in lexer.

## 14 July

-   Wrote lexer rules for all modifiers but it is not being highlighted
    as expected.

## 15 July

-   Made the modifier rules working in the lexer.
-   Defined different rules for single line modifiers and block of
    modifiers.

## 16 July

-   Added new values in enum of scadlexer.h for modifiers
-   Also called different style for modifiers in scintillaeditor.cc

## 17 July

-   Defined highlighting colors for modifiers in all color scheme of
    editor which are written in json format in colorschemes/editor
    directory.

## 18 July

-   Started reading about adding options to change the toolbar icons by
    user.
-   User may also be able to add his own iconset.

## 19 July

-   Reading the existing code of listing the 3D View and Editor options
    in Preferences windows to get the idea of how can the iconset be
    listed.

## 20 July

-   Reading about the boost different libraries used in OpenSCAD such as
    filesystem, shared_ptr, property::tree that can be used to list the
    iconset and change the icon as selected.

## 21 July

-   Added new option for Icons
-   Also added new page for listing icon sets through QListWidget in
    Preferences window.

## 22 July

-   Added code to list the name of iconsets in Preferences's Icons page
    through boost::property tree, but it is listing the path of iconset
    folders instead of just names. Need to extract the name of iconset
    from the path.

## 23 July

-   Changed the way to get the path of iconsets from property::tree to
    DIR using dirent.h
-   Also the name of iconsets has been shown in the list instead of
    paths.

## 24 July

-   Wrote code to use the name of iconset in mainwin.cc to use the
    iconsets in the toolbar.
-   Added slot in preferences to change the icon when the iconset has
    been changed by the user in Preferences Window.

## 25 July

-   Added function in mainwin.cc to get the name of iconset from the
    path mentioned and change the icon in the toolbar.
-   Also changed Icons's icon in Preferences Window
-   Make Icons option checkable to solve the problem of not being shown
    as selected when clicked.

## 27 July

-   Changed the icon of Icons option to a free image. Last one was not
    free.
-   Changed the path of images of toolbar icon in openscad qrc file and
    mainwin.cc
-   Added list of flaticons to be changed on selecting from the list of
    iconsets.

## 28 July

-   Divide the iconset into dark and light folders for different
    background colors at different platforms.
-   Make the flaticons as default icon set and provided option to add
    new icon set by user just by adding a new folder inside images
    folder.

## 29 July

-   Working on highlighting modifiers but it is having very strange
    behavior that is affecting the color of text below the current
    modifier when some change is made in it.
-   Trying to figure out the problem by writing tests.

## 30 July

-   Cleaned some code of lexertl rules.
-   Debug the code and lexer states in a file to understand the behavior
    of modifiers, but everything seems fine other than behavior of
    modifiers styling.

## 31 July

-   Discussed with mentors about modifiers problems and try to
    understand the theory of states and lexer rules.
-   Found that lexer state goes to 0 at every lookup call, so rule that
    is moving from current state to initial state is not being called.
-   Trying to figure out the solution for it.

## 2 August

-   Made changes in lexertl rules to solve the problem of modifiers.
-   Call the user id at each rule to get lexer feedback more often about
    style of the text. This solve the problem a bit, but still it is
    affecting the next modifier styling.

## 3 August

-   Use the logic of multiline comments for modifiers, change state by
    checking the state of pos, one less than start position, and it
    worked well.
-   As the modifier \* is also a mutliplier and modifier % is also the
    sign of MOD, so the later also get styled as former in both cases.
-   Discussed this problem with mentors and got that this problem can be
    solved by parsers.

## 4 August

-   Compiled autocomplete branch to start working on autocomplete
    scintilla feature, but it having some errors. Trying to figure out
    the reason of these errors.

## 5 August

-   Discussed about other features that are missing with latest lexer
    and were present in CPP lexer that are auto indentation and folding.
-   Trying to find out how these features can be added in our current
    lexer.

## 6 August

-   Read scintilla documentation to know how to implement folding and
    auto-indentation for braces.
-   Tried different methods but it didn't work as required.

## 7 August

-   Tried different methods and finally folding start working
    successfully for braces.
-   Tried different methods for auto-indentation but it didn't work
    well, causing infinite indentation on setting indentation of next
    line of opening brace.

## 8 August

-   Implemented folding for square brackets as well as multiline
    comments.
-   Used blockStart and blockEnd functions of Qscintilla for
    auto-indentation.
-   BlockEnd function takes only single character to unindent, so
    auto-unindent for } braces worked well but not able to implement
    auto-indent for square brackets.

## 10 August

-   Tried adding auto-indentation for square brackets by using the logic
    of folding for code block started and ended with square brackets but
    it did't work as expected.

## 11 August

-   The window is made to be auto-scrolled in case of any compilation
    error using scitilla function SCI_LINESCROLL fed with the error
    line.

## 12 August

-   As the window gets scrolled skipping the number of lines at every
    F5, so the logic is changed to set the cursor to error position and
    scroll the window to show the cursor position in case of any
    compilation error. In this way, the cursor remains that the error
    position in case of repeatedly running the same script.

## 13 August

-   Wrote the summary of project in github wiki page
    <https://github.com/openscad/openscad/wiki/GSOC-2015-Project---ScadLexer>

## 14 August

-   Made some changes, added images in the project summarization.
-   Also wrote the documentation for the features of scintilla editor
    <https://github.com/openscad/openscad/wiki/Scintilla-Editor-Features>

## 17 August

-   Started testing various added features in scadlexer for quality
    purpose.

## 18 August

-   Started writing tests for different start value, mentioning the
    value of start in the input file only.

## 19 August

-   Shift reading file from highlighting function to main function of
    lexertest as to pass the required pass parameter to lex_result
    function.

## 20 August

-   Use examples shipped with openscad to write tests to test their
    behavior and performance.