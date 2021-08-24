# Development Logs

## Community Bonding Period

-   Read OpenSCAD source and test files.
-   Learnt some important Qt classes used in OpenSCAD.
-   Explore different editors that can be integrated into OpenSCAD
    editor.
-   Discussed with community about the editor and finalized QScintilla.

## Development Period

### Week 1

'''''19th May Worked on Detachable rendering window.

'''''20th May Read about QScintilla integration after discussion with
community

'''''21st May Completed the task of Detachable window and made a pull
request in branch detatchrenderwindow of OpenSCAD.

'''''22nd May

-   Submitted patch for detachable render window, which my mentor said,
    can be a good addition to
    <https://github.com/openscad/openscad/pull/787>.
-   Discussed about the integration of editor.
-   Added class Qscintilla and make two separate objects of QTextEditor
    and QScintilla classes in Editor class.

'''''23 May

-   Removed errors and Added some built in functions of QScintilla class
    so that its minimal functionality can be seen.
-   Discussed about it with mentors and I got that two separate classes
    should be made say legacyEditor and ScintillaEditor which will
    inherit QTextEdit and QScintilla classes respectively and an
    Interface class Editor will be used to call the functions of both
    these classes.

'''''24 May

-   Refactored some code and made two separate classes as discussed.
-   More code need to be refactored yet.

### Week 2

'''''26 May

-   Searched about how to change the color of rendered model.
-   Checked rendersettings.cc renderer.cc preferences.cc. Preferences.cc
    has color scheme for preview but not for rendered model.

'''''27 May

-   The functions defined in legacyEditor.cc can be called in mainwin.cc
    by object of interface class i.e. Editor.

'''''28 May

-   Still not able to find the code that affects the color of rendered
    model. Struggling for it.
-   Facing a segmentation fault because of toPlainText() function call
    in mainwin.cc at some places. Trying to solve it.

'''''29 May

-   Completed the editor class as interface and defined virtual
    functions into it using which the derived class functions can be
    called into the mainwin.cc

'''''30 May

-   The size of the editor is creating problem. It is not fitting into
    the DockWidget. Read about size hint, size policy and customizing Qt
    widgets.

'''''31 May

-   Cloned new openscad as a lot of changes are made by the developer
    and installed required libraries. Build OpenSCAD with Qt5 and remove
    errors caused to old libraries versions. My mentor suggested me to
    shift to Operating system Ubuntu 14.04 as 12.04 is not supporting
    new libraries required by OpenSCAD.

### Week 3

'''''2 June

-   Installed QScintilla editor API and read its example to understand
    how to it can be integrated into OpenSCAD.
-   Made Scintilla class derived from Editor class.

'''''3 June

-   Install OS Ubuntu 14.04 lts.
-   Cloned OpenSCAD and build required libraries
-   Scintilla editor is not working. Trying to figure out the problem.

'''''4 June

-   As the editor is removed from MainWindow.ui file, the editor defined
    as object of legacyEditor is facing some size issues. Trying to
    figure out how to set its size equal to its parent
    editorDockContents.

'''''5 June

-   Integrated QScintilla editor into openscad with minimal
    functionality.

'''''6 June

-   Solved size problem of legacy and scintilla editors successfully.
    Now they are occupying the full editorDock widget space.

'''''7 June

-   Read and became familiar with QScintilla documentation to add new
    features into the scintilla Editor.

### Week 4

'''''9 June

-   Made a wiki page showing what features need to be implemented in
    editor
-   Line numbers at the margin.
-   Brace Matching.
-   Auto Indentation

'''''10 June

-   Included line wrap and flags at wrapping to make the editor
    responsive to the window size.
-   Add margin width to the line numbers so show the full line number,
    previously it was showing just the last digit.

'''''11 June

-   Discussed with mentors, how to add error indicators. This was bit
    confusing, as with scintilla editor we are not using the existing
    highlighter class which is used for highlighting and error
    indicating

'''''12 June

-   Understanding how to do error indicating using qscintilla functions
    provided in documentation.

'''''13 June

-   Error indicator is implemented
-   Facing problem in unhighlighting when the user solve the error
-   Finally implemented error indicators with marker at line number
    which will help to identify line having error in case there is no
    line wrapping

'''''14 June

-   Today's task was to work towards syntax highlighting. Qscintilla has
    different lexer classes such as QsciLexerCPP, QsciLexerJava etc for
    highlighting syntax of different languages. But all the keywords
    used in openscad are not supported in single language. Planning how
    to tackle this problem.

### Week 5

'''''16 June

-   A new class ScadLexer is made that is inherited from QsciLexerCPP
    class, which contain the enum having labels for different style IDs.
-   A keyword method in QsciLexerCPP is overridden in ScadLexer to
    define Openscad set of keywords.

'''''17 June

-   DefaultColor function of QsciLexerCPP is overridden in ScadLexer
    which return colors for different sets of keywords defined in
    keyword method in the same class.
-   Preference syntaxhighlight string is called to know the current
    value of Edit/Preference/Editor set by the user in the openscad
    window.
-   Provide different colors to keywords according to dark, light or no
    background color.

'''''18 June

-   Unable to change the syntax color when the user changes the
    settings.
-   The defaultColor method in ScadLexer and setHighlightScheme method
    in ScintillaEditor needs to be connected somehow. Tried some methods
    getting ideas from existing Highlighter class for legacyEditor.

'''''19 June

-   The idea of DefaultColor method is dropped because it is
    automatically called by the lexer and two such functions for
    different backgrounds can't be defined.
-   The inbuilt lexer function setColor is used in setHighlightScheme
    function to provide colors to different keyword sets, operators,
    numbers etc according to their style IDs mentioned in
    qscilexercpp.h.

'''''20 June

-   Appropriate colors to the keyword sets are given using to monokai
    color pallete.
-   Set editor utf8 for supporting unicodes.
-   provided inconsolata font.
-   Committed my changes for the mentor's review.

'''''21 June

-   Explored about adding custom toolbar having most usable actions.
-   Downloaded and edited required Icons.
-   Made toolbar at the top of the MainWindow

### Week 6

'''''23 June

-   Reviewd toolbar from mentor but due to a Qt bug, toolbar styles were
    not supported at every platform.
-   Explored for different option how to get user's desktop settings.

'''''24 June

-   Regenerate all the icons in black color.
-   The icons will be black if the default desktop setting as light gray
    color and white if it has dark color as default settings.

'''''25 June

-   Made more icons for wireframe and surface
-   Tested all icons by adding them in light gray toolbar

'''''26 June

-   Made two different toolbars one at editor side and other at glView
    (rendering window) side.
-   Added more suitable icons

'''''27 June

-   Some actions like showaxes, showedges in toolbar are not working.
    Trying with different methods.
-   Added direct actions and icons in mainwin.cc instead of ToolBar
    class and it worked.

### Week 7

'''''3 July

-   Read about the color theory and tried to modify existing themes of
    rendering window of openscad

'''''4 July

-   My mentor suggested that I should add new themes with new names
    rather than modifying existing one. So tried to made new ones

'''''5 July

-   Added icons for preview, perspective. orthogonal for both dark and
    light default color scheme.

'''''6 July

-   Added icons for animate and cross hairs for both dark and light
    default toolbar color scheme.

'''''7 July

-   Improved syntax highlighting color scheme.
-   Improved new added rendered model themes and provided them new
    names.

### Week 8

'''''8 July

-   Committed and pushed themes
-   Started working towards adding run time option for switching editor
    from legacy to scintilla

'''''9 July

-   Added combo box in Preferences.ui with the help of designer and
    added both editors as different options.
-   Tried to get the current value of selected editor option in
    preferences in mainwin.cc but it is causing some errors.

'''''10 July

-   Successfully got the value of selected editor option in mainwin.cc
    and changed editor in mainwindow according to the user's selected
    editor option.

'''''11 July

-   Solved the problem of not showing previously selected editor option
    in Preferences dialog box.
-   Solved the problem of showing unnecessary warning for save changes
    even when nothing has been modified in scintilla editor.

'''''12 July

-   Decided what should be done next with mentors and planned to work
    towards making launching screen for openscad.
-   Started working towards making mock up of launching screen design.

### Week 9

'''''14 July

-   Looked at launching screen of few famous software for inspiration

'''''15 July

-   Tried making different designs but still not satisfied :(

'''''16 July

-   Made a good launching screen design mock up and showed to my mentor
    to get review for further improvements.

'''''17 July

-   Made new class LaunchingScreen in openscad and added basic widgets
    using Qt designer.

'''''18 July

-   Added background and colors to the buttons in launchingscreen of
    openscad.

'''''19 July

-   LaunchingScreen is added in the scope of MainWindow but this way
    launching screen get showed up on every new window. Need to have
    some different logic.

### Week 10

'''''21 July

-   LaunchingScreen is added in openscad.cc but it is showing launching
    screen even when a filename is given at command line.

'''''22 July

-   A bool variable is added that checks if the file size is 0 at cmd
    line or not and shown launching screen accordingly.

'''''23 July

-   Tried adding signal slots of new, open and help buttons in
    openscad.cc but it is creating a mess there because the slots are
    defined in mainwin.cc. Need to adopt some different way.

'''''24 July

-   To have better and clean code, LaunchingScreen object is defined in
    mainwin.cc but the launcher is shown in openscad.

'''''25 July

-   Added recent files in List Widget but currently it is not working on
    clicking the file name.

'''''26 July

-   Added recent file path instead of just name and added a button Open
    Recent, by clicking which, the selected item in List Widget will
    open up in the editor.

### Week 11

'''''28 July

-   Disable Open Recent button if nothing selected.
-   Added TreeWidget for examples parallel to Recent List Widget with
    the help of designer.

'''''29 July

-   Added Categories names as top level elements in treeWidget.
-   Got the names of the examples in show_example() function in
    mainwin.cc and added in treeWidget.

'''''30 July

-   Examples are not working after clicking on them so added button Open
    Example using the same logic of Open Recent button.
-   Examples are still not working on opening the currentItem.

'''''31 July

-   Gave full path of example instead of file name as parameter to
    openFile function and now examples are working :)

'''''1 August

-   Made the check box work to hide the launcher and save the user
    settings.
-   Made an option in Preferences/features to show the launcher again.

'''''2 August

-   Made the size of the launcher dialog box fixed.
-   Pushed the code for reviewing

'''''3 August

-   Wrote the blog post about the major contribution of the project to
    openscad software
    <https://shainasabarwal.wordpress.com/2014/08/03/gsoc-project-ui-brushup-of-openscad/>

### Week 12

'''''4 August

-   Read about the Monokai theme for our new QScintilla Editor
-   Set the monokai theme for Qscintilla Editor and provided its option
    in Preferences box

'''''5 August

-   Read about the Solarized theme.
-   Set the Solarized theme for QScintilla Editor and also provided the
    option in Preferences.

'''''6 August

-   The find and replace functions are not working into the QScintilla
    Editor. Studying for how to implement these functions.

'''''7 August

-   Read the QScintilla documentation and find various function to
    implement find and replace in our new editor.
-   Made the find, replace, and find next operations working in the
    qscintilla editor but there is no function available for find
    previous.

'''''8 August

-   As we have editor interface for both editors - Legacy editor and
    QScintilla editor. So it is required to make the common function for
    find and replace operations for both the editors.
-   Discussed with mentors about this.

'''''9 August

-   Made the common functions for find, replace, find next in the editor
    interface for both editors.

### Week 13

'''''11 August

-   Hide the options of indent/unindent comment/uncomment from the Edit
    Menu when the QScintilla editor is on as these options are no more
    required in the qscintilla editor.

'''''12 August

-   Trying to find the way how to implement find previous and replace
    all options in the scintilla editor

'''''13 August

-   Tweaked some icons in the toolbar. Shifted render icon in rendered
    window toolbar from editor toolbar and removed some icons that are
    less often used.

'''''14 August

-   Worked towards making the font and size options in preferences
    window working for the qscintilla editor.

'''''15 August

-   Font and size can be changed in qscintilla editor through preference
    option.
-   Removed the problem of articrafts in open Example and open Recents
    buttons.

'''''16 August

-   Cleaned up code of branches scintillaeditor and launchingscreen

'''''17 August

-   Working towards changing the launching screen checkbox text from
    "show me everytime" to "Don't show again" on suggestions of mentors.