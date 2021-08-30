## Project Title

Improvement of OpenSCAD Text-Editor Features
Organization: OpenSCAD

## Abstract

OpenSCAD is a free and open-source software for creating solid 3D CAD
objects. The application provides its own set of instructions/command to
create a 3D model. These instructions include various pre-defined
functions, keywords and a syntax to use them. While there are some
external editors that facilitate the writing of code for OpenSCAD, its
integrated editor lacks many of the desired features.

As modern OpenSCAD usage has advanced, it now makes more extensive use
of libraries consisting of many files, and the editor features have not
kept pace with this more advanced workflow. The goal of this project
will be to add different IDE-like features to the integrated text editor
thus advancing its usage. This will make the editor more user-friendly
and easier to handle large codes. Currently, the editor supports
features like syntax highlighting, bracket matching, numbering of lines,
besides others. I will work on implementing multi-file editing support
to the editor and autocompletion of OpenSCAD keywords.

## Detailed Description and Implementation

The project can be listed down to two major subtasks:

#### Phase I - Multi-file Editing

The editor currently supports editing of one file in a window. Whenever
a new file in opened, a new window opens with that file. I will work
towards adding the tabs to the editor. This will allow opening multiple
files, one at each tab, in a single window. This will include:

i\) **Implementing a GUI**
A GUI support for Tab Document Interface. The QScintilla editor is
contained in editorDockContents widget by using its addWidget()
function. Instead an object of QTabWidget can be made and passed for
addWidget() function of editorDockContents. Each tab of the QTabWidget
can hold a widget of QScintilla editor. The tabs will of course be
movable and closable. An option for creating new tabs will be added in
the File menu.

ii\) **Making GUI functional**
Writing code to handle opening and closing of tabs. New tabs can be
created using the addTab() function of QTabWidget. Similarly, closing of
tabs can be handled by catching tabCloseRequested() signal or
equivalent. Drag and Drop features will be re-implemented to open a new
tab instead of another window.

iii\) **Attaching features to each tab**
The editor already supports features like indenting, commenting and
various others. These features need to be extended to all tabs of
editor. Besides, functionalities like preview or rendering need to be
attached to current active editor tab such that whenever preview/render
is clicked, code of current active tab(or as discussed in the community)
is compiled. This can be done by making a separate QScintilla object for
each tab. Whenever a tab is changed, the editor object(whose member
method has implementation of the functionalities) can point to currently
active tab’s QScintilla object.

iv\) **Saving of changed files**
Whenever a editor tab is closed, it is needed to check the change status
of file and to provide a dialog box to ask for saving the changes.
Again, this can be implemented by implementing tabCloseRequested()
signal of each tab. Similar checks need to be performed on closing the
window. This can be done by checking the change status of each open tab.

The expected GUI should look like the following, generated with mock-up
code:

(../../img/Image3.png)

Any changed files will be marked by asterisk(\*)

(../../img/Image4.png)

Changes in file menu

(../../img/Image2.png)

#### Phase II - Keyword Autocompletion

The current editor has no mechanism of suggestions for autocompletion
based on already typed text. The aim of this phase will be to add
features to provide suggestions based on prefix-matching of typed text.
The suggestions will only consist of OpenSCAD keywords. This feature has
a prototype at [PR
\#2889](https://github.com/openscad/openscad/pull/2889). My
implementation of the feature will be influenced by the prototype. It
primarily consist of:

i\) **Implementing QsciLexer and QsciAbstractAPIs**
It includes maintaining a list of OpenSCAD keywords and using them to
implement the functions lexer and api class. The actual implementation
part can be done by subclassing QsciLexer and QsciAbstractAPIs classes.
This provides us with the lexer and api objects. The keywords and the
related templates will be hard-coded in the subclassed files. This can
be later(not in scope of project) expanded to write all the keywords in
a separate json/xml files and the subclassed codes can read the keywords
from those json/xml files.

ii\) **Integrating with editor**
The QScintilla editor object requires the api and lexer objects for it
to suggest for autocomplete keywords. Once the lexer and api objects are
attained, they can be attached to the editor object. This gives the
editor functionality of autocomplete with behaviour defined in the lexer
and api class.

iii\) **Autocompletion Settings**
This includes options to set enable status of autocompletion feature and
the time delay before the suggestions appear. This can be implemented by
storing the settings in QSettings class. The option can be made
available in Edit - Preferences - Editor.

Refer gif at [PR \#2889](https://github.com/openscad/openscad/pull/2889)
to see the expected result

Changed GUI at Preferences-Editor

(../../img/Image1.png)

## If Time Permits

If the outlined work is completed before time, I will like to further
extend the feature set of editor. Below are the optional features which
can be included to the current scope of project:

-   Implementing CTRL+TAB key combination for cycling among tabs in
    editor
-   Automatic completion of closing brackets in editor

## Deliverables

-   Complete support of multi-file editing. Users should be able to
    create and close multiple files in a single window and can access
    any files in any order. Each file should be able to extend already
    available editing features. Options for saving and content modified
    marker will also be available for each file.
-   Autocomplete suggestions of all OpenSCAD keywords. The editor will
    provide keyword suggestions along with various parameters of
    functions. The suggestions can be chosen through arrow keys and
    selected by pressing enter.

## Timeline

#### May 6 - May 26 (Community Bonding Period)

-   Familiarize myself with the code and community
-   Learn and explore Qt Framework - using documentation, books
-   Learn and explore QScintilla

#### May 27 - June 2

-   Choose among various options to implement multi-file editing
-   Implement a GUI to support multiple file editor in a single window
-   Add option in File menu and Editor dock to open a new file in same
    window

#### June 3 - June 9

-   Write code to implement multi-file editing
-   Handle opening and closing of file tabs from GUI buttons
-   Code to open a new file in same window from file menu and editor
    dock
-   Migrate the support of opening file in new window to different gui
    option

#### June 10 - June 16

-   Extend already available editor features(indentation, commenting,
    colour-scheme, undo/redo, etc) to each new file in a window
-   Mapping preview and rendering functionality to currently active tab
    or as discussed in the community
-   Provide drag-and-drop support for opening new file in same window

#### June 17 - June 23

-   Extensive testing of multi-file editing feature
-   Solve any issues encountered while testing

#### June 24 - June 28 (Phase I Evaluation)

-   Take suggestions and feedback of work done till now
-   Implement changes based on suggestions
-   Based on stakeholder feedback, reassess and adjust remaining project
    scope in an agile manner if needed.

#### June 29 - July 7

-   Go through the OpenSCAD documentation and create a list of its
    keywords
-   Develop template of keywords and related function signatures

#### July 8 - July 14

-   Code to implement auto-completion feature
-   Use lexer and api class of QScintilla to implement the feature
-   Explore the prototype for autocomplete calls

#### July 15 - July 21

-   Extensive testing of auto-completion feature
-   Solve any issues encountered while testing

#### July 22 - July 26 (Phase II Evaluation)

-   Take suggestions and feedback of work done till now
-   Implement changes based on suggestions
-   Based on stakeholder feedback, reassess and adjust remaining project
    scope in an agile manner if needed.

#### July 27 - August 4

-   Add GUI to set enabling/ disabling of autocomplete feature
-   Add GUI for autocomplete character threshold
-   Code to implement enable status of autocomplete feature

#### August 5 - August 11

-   Code to implement autocomplete character threshold
-   Look for possible optimization and clean up of code
-   Resolve any issues encountered

#### August 12 - August 19

-   Buffer week for any unforeseen circumstances

## Further work based on project

I will like to continue my contribution to the OpenSCAD organization
even after the GSoC period. There are certain list of features that I
have in mind and will love to add to the editor. These features include:

-   Autocomplete suggestions of user-defined variable/function/module
    names
-   Add shift+scroll trigger to change numeric values
-   Functionality to add tab-triggered templates and related gui options

## About Me

I am an undergraduate student in my third year pursuing Computer Science
and Engineering from National Institute of Technology, Durgapur (West
Bengal, India). I have experience with Java, C++, Python, SQL, and
LaTeX. As per my academic curriculum, I have undergone courses on Basic
of Programming in C, Data Structures, and Object Oriented Programming in
C++. Besides, I have also done a few self projects which are available
on my github.

**Contact Information**:
Name: Romit Kumar
University: National Institute of Technology, Durgapur
Email: romitkumar1705@gmail.com
Github: <https://github.com/RomitKumar>
IRC Username: RomitKumar
Gitter Username: RomitKumar
Country: India
Timezone: Indian Standard Time (GMT+5:30)
