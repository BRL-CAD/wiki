## Community Bonding Period (May 6 - May 27)

### May 14

Discussed about sharing of mock-up code and prototypes with mentor

### May 15

Developed a prototype for gui implementation of multi-tab feature.
[Prototype1
Code](https://github.com/RomitKumar/openscad-prototype/tree/master/prototype1)

### May 16

Implementing prototype in openscad codebase

### May 17

Implemented the prototype in openscad codebase. Made [PR
\#2949](https://github.com/openscad/openscad/pull/2949). This pr will
act as a sandbox for prototyping and sharing of coding with mentor.
Discussion about integrating pre-available editing features in all tabs

### May 18

Implemented the comment feature using signal dispatcher as suggested by
mentor. Made the pr.

### May 19

Studying the openscad codebase to look for implementation of saving
feature for each tab.

### May 20

Implemented the feature of saving of tab contents in prototype code.
Main Window name updates on switching tab.

### May 21

Discussed about correctness of signal dispatcher.

### May 22

Implemented signal dispatcher in a separate class. Made the
[pr](https://github.com/openscad/openscad/pull/2949/files#diff-99feea0b406e34be128d4299fafad187R2732).
Discussed about implementation details of multi-tab feature. Decided to
implement the feature in a separate TabManager class.

### May 23

Studying the openscad codebase for feasibility of implementation of
TabManager class.

### May 24

Studying openscad codebase.

### May 25

Made a prototype project with similar gui features as multi-tab.
Implemented those features using with a separate TabManager class as
suggested by mentors. [Prototype2
Code](https://github.com/RomitKumar/openscad-prototype/tree/master/prototype2)

### May 26

Implement basic gui(opening and closing of tabs) of multi-tab in
openscad code. The feature in implemented in a separate TabManager
class. Made the [pr
\#2955](https://github.com/openscad/openscad/pull/2955)

## Coding Period (May 27 - Aug 19)

## Week 1 (May 27 - June 2)

### May 27

Discussed about possibility and various method of integration of Simple
and QScintilla Editor with multi-tab editor.

### May 28

Implemented the code for integration of pre-available editor features
with multi tab. There are some issues that need to be handled like
checking the undo state, highlighting of error in multiple files.

### May 29

Removed support for legacy editor and corrected the keyboard mapping for
zoom in/out. Pushed commits
[cfa32da](https://github.com/openscad/openscad/pull/2955/commits/cfa32dab32175ef6e591abfab757d8b95034cf05)
and
[1ad0f53](https://github.com/openscad/openscad/pull/2955/commits/1ad0f53653a5922abe1d66911f9eacbc1ea9af93)
to pr [\#2955](https://github.com/openscad/openscad/pull/2955).

### May 30

Corrected the updation of undoState and windowModified. Now these states
behave correctly for multi-tab environment. Realised that stl exports
and enable status of parameterWidget are not behaving correctly.

### May 31

Corrected the behaviour of stl exports and enable status of
parameterWidget. Running some basic tests to check the correctness of
work done till now.

### June 1

Discussed with mentor about behaviour of Customizer widget and animation
on changing tabs. Implemented those behaviour in codebase of openscad.
Pushed the commits to pr
[\#2955](https://github.com/openscad/openscad/pull/2955)

### June 2

Run basic tests on gui implemented so far. Discovered that Find, Find
and Replace are not behaving correctly for multi-tab.

## Week 2 (June 3 - June 9)

### June 3

Correcting the behaviour of Find, Find and Replace for multi-tab

### June 4

Implemented the correct behaviour of Find, Find and Replace for
multi-tab. Pushed commit
[23129ba](https://github.com/openscad/openscad/pull/2955/commits/23129ba51dfe1f62ed8333fe84fd15a63bb0db71)
to pr [\#2955](https://github.com/openscad/openscad/pull/2955/). Found a
bug related to previous implementation of Find. Raised issue
[\#2962](https://github.com/openscad/openscad/issues/2962). Discussed
about implementing save feature for multi-tab and naming of new tabs and
tabs that have same file names.

### June 5

Studying the openscad codebase for implementation of save features in
multi-tab.

### June 6

Working on implementing the open feature for multi-tab.

### June 7

Removed the option for single file QScintilla Editor. Instead now
multi-tab editor will not show tabs in case of single tab, effectively
giving the feeling of single file QScintilla Editor. Implemented this
feature in multi-tab editor. Pushed commit
[d594980](https://github.com/openscad/openscad/pull/2955/commits/d594980fb192da2871dcc1c442ac521624d54b19)
to pr [\#2955](https://github.com/openscad/openscad/pull/2955)

### June 8

Continuing the work to implement open feature in multi-tab.

### June 9

Completed the work of implementing Open(File menu option, Recent Files,
Examples), Save, Close feature for multi-tab. Pushed the corresponding
commits to pr [\#2955](https://github.com/openscad/openscad/pull/2955/).

## Week 3 (June 10 - June 16)

### June 10

Started testing of code submitted.

### June 11

Changed the behaviour of Open and Open Tab as suggested by mentors. Made
commits
[6a0a1d1](https://github.com/openscad/openscad/pull/2955/commits/6a0a1d169be25db80da5f5d9cb9e91251f2414b5)
and
[e3ff4d9](https://github.com/openscad/openscad/pull/2955/commits/e3ff4d90ef3828a01652d25a15d7fea546f2dcaf)
in pr [\#2955](https://github.com/openscad/openscad/issues/2955).

### June 12

Testing and cleaning of code.

### June 13

Done cleanup of code. This includes renaming variable/function, removing
redundant function, removing mdi checkbox from Preferences/Advanced,
correcting implementation of reload, prevention of double emission of
currentChanged signal for first tab. Pushed commits
[0e92308](https://github.com/openscad/openscad/pull/2955/commits/0e923084003f16c1050aa6ea3ff04c25f0efec52)
and
[cdaee5e](https://github.com/openscad/openscad/pull/2955/commits/cdaee5ea6d226efb963b9f38a839fc74e6cad911)
in pr [\#2955](https://github.com/openscad/openscad/issues/2955).

### June 14

Implemented the Save All feature. Pushed commit
[b0c95e8](https://github.com/openscad/openscad/pull/2955/commits/b0c95e89f7e5028be18ca8e71d5016eb579e7e46)
in pr [\#2955](https://github.com/openscad/openscad/issues/2955).
Corrected the enabling of Parameter Widget on file load and opening of
Recent Files and examples in empty tab. Pushed commits
[35e3fe0](https://github.com/openscad/openscad/pull/2955/commits/35e3fe083656fc9d952506f9f0bfdbcc2ce95ba7)
and
[acc3123](https://github.com/openscad/openscad/pull/2955/commits/acc3123308cbe169afbc4134d7a17268307b66a3)
corresponding to the changes. Discussed with mentor about the idea of
Tab Header spanning the whole window.

### June 15

Working on Tab Header spanning whole window length.

### June 16

Implemented the feature of Tab Header spanning whole window length.
Pushed commits
[087359f](https://github.com/openscad/openscad/pull/2955/commits/087359f3b3ca6b6e2835fc8fb9cdeaf77a0aeebd)
and
[c59df44](https://github.com/openscad/openscad/pull/2955/commits/c59df4498160f8fd5aaadc8b480b82c2263da479)
in pr [\#2955](https://github.com/openscad/openscad/issues/2955).

## Week 4 (June 17 - June 23)

### June 17

Shifted Tab Header implementation from dock widget to toolbar. This
toolbar clings to editor dock widget when it is undocked. Pushed commits
[fd93e57](https://github.com/openscad/openscad/pull/2955/commits/fd93e57691f272c8f5322eb9d5c8e057b2e49e63),
[a50fd61](https://github.com/openscad/openscad/pull/2955/commits/a50fd610d0d63f4e11e2adf9bb53a2f8939c1591)
and
[689292c](https://github.com/openscad/openscad/pull/2955/commits/689292c2c53678cf106cb442b0a09315ea204ec1)
in pr [\#2955](https://github.com/openscad/openscad/issues/2955).

### June 18

Testing multi tab implementation

### June 19

Continuation of testing of multi-tab implementation. Looking and
exploring various methods for auto completion feature.

### June 20

Posted in mailing group inviting users for testing of multi-tab feature.
Going through the codebase at pr
[\#2889](https://github.com/openscad/openscad/pull/2889) to understand
details of auto completion feature.

### June 21

Updated implementation of tab tool bar such that it is hidden when a
single tab is present. Pushed commit
[dff9b9b](https://github.com/openscad/openscad/pull/2955/commits/dff9b9be7afafdf17b0fcc874cc0460076918362)
in pr [\#2955](https://github.com/openscad/openscad/issues/2955).

### June 22

Looking at web resources available to understand auto-completion in
qscintilla.

### June 23

Made a new pr [\#2975](https://github.com/openscad/openscad/pull/2975)
implementing auto-completion of openscad keywords. The commit is
[bdc8e10](https://github.com/openscad/openscad/pull/2975/commits/bdc8e10ef54d78e8702f72d10a01872c1a36240b).
Also pushed commit
[7cda02a](https://github.com/openscad/openscad/pull/2975/commits/7cda02a796664e45df2abc8af46c8c994b8a7e5e)
to enable qscintilla in travis check. Discussed with mentor about
various options of providing keyword list for auto-completion.

## Week 5 (June 24 - June 30)

### June 24

Implemented ctrl+insert shortcut to display template list. Pushed commit
[10bfc3f](https://github.com/openscad/openscad/pull/2975/commits/10bfc3f8278278b6efd67870c9f55c9ee629ba63)
in pr [\#2975](https://github.com/openscad/openscad/pull/2975)

### June 25

Checking the plausibility of making keyword list for auto-completion at
Builtin class.

### June 26

Discussed with mentor about implementation details for auto-completion
keyword list in Builtin class.

### June 27

Pushed commit
[77dfcc5](https://github.com/openscad/openscad/pull/2975/commits/dc1146bcb41a3c466dcee836491dd546eee4653f)
in pr [\#2975](https://github.com/openscad/openscad/pull/2975)
implementing registering of keywords in Builtin class.

### June 28

Pushed commit
[dc1146b](https://github.com/openscad/openscad/pull/2975/commits/dc1146bcb41a3c466dcee836491dd546eee4653f)
in pr [\#2975](https://github.com/openscad/openscad/pull/2975) replacing
qt structures with std structures in core classes.

### June 29

Pushed commit
[a3e8950](https://github.com/openscad/openscad/pull/2975/commits/a3e8950788e79cf2293293cecdc2a6989e12460c)
and
[d1dc26f](https://github.com/openscad/openscad/pull/2975/commits/d1dc26ffe48b6c6ed17de8a651de1e008e3bd658)
in pr [\#2975](https://github.com/openscad/openscad/pull/2975) adding
other keywords in keyword list. Discussed with mentor regarding html
formatting of calltips.

### June 30

Working on html formatting of calltips.

## Week 6 (July 1 - July 7)

### July 1

Made a separate Keyword class for storing information about keywords.
Pushed commit
[1eefb4a](https://github.com/openscad/openscad/pull/2975/commits/1eefb4a762185eba6b9adc297f893c49cf0328b4)
in pr [\#2975](https://github.com/openscad/openscad/pull/2975). Checked
about possibilty of html formatted string for calltips. It seems that
QScintilla does not support formatting of strings in html form.

### July 2

Pushed commit
[d9246dd](https://github.com/openscad/openscad/pull/2975/commits/d9246dd06047f2a90b8e599ffa2c1068828fd2ba)
in pr [\#2975](https://github.com/openscad/openscad/pull/2975) modifying
the structure of Keyword class. Discussed with mentor about final
structure for implementation of keyword auto completion.

### July 3

Working on implementation of mentor suggested approach.

### July 4

Applying the approach for primitives keywords.

### July 5

Completing the primitive keyword autocompletion.

### July 6

Pushed commits
[6836128](https://github.com/openscad/openscad/pull/2975/commits/6836128ede8f072399483286d14d5c55b3d18452)
and
[0720ea1](https://github.com/openscad/openscad/pull/2975/commits/0720ea124f5a5eed93ac4f1c482ef4ef0f29f71d)
in pr [\#2975](https://github.com/openscad/openscad/pull/2975)
implementing auto completion for all keywords.

### July 7

Pushed commit
[65676bf](https://github.com/openscad/openscad/pull/2975/commits/65676bf72d721183c509ddb85c45cdd947a5d3e1)
in pr [\#2975](https://github.com/openscad/openscad/pull/2975) adding
remaining non-registered keywords in auto-complete list.

## Week 7 (July 8 - July 14)

### July 13

Pushed commit
[12c605f](https://github.com/openscad/openscad/pull/2955/commits/12c605f2902a3013fef91d6661d0542093d7547a)
in pr [\#2955](https://github.com/openscad/openscad/pull/2955)
correcting implementation of opening of files in empty editor tab. Also
pushed commit
[30085ff](https://github.com/openscad/openscad/pull/2955/commits/30085ff06972de21da09753feecd50472d39950c)
so that files with & are shown correctly.

### July 14

Pushed commit
[a99d689](https://github.com/openscad/openscad/pull/2955/commits/a99d689ab9315b0559d5a10e9a315e934bf9abb1)
in pr [\#2955](https://github.com/openscad/openscad/pull/2955) resolving
merge conflict caused due to merging of pr
[\#2989](https://github.com/openscad/openscad/pull/2989) in master
branch.

## Week 8 (July 15 - July 21)

### July 19

Discussed with mentor about overall feedback of work done till now. Get
to know about feedback message on multi-tab regarding multi-tab.

### July 20

Pushed commit
[87a58ca](https://github.com/openscad/openscad/pull/2975/commits/87a58ca5c9b5f4798e92be8e6bc11228eea364b3)
in pr [\#2975](https://github.com/openscad/openscad/pull/2975)
implementing templates being read from json file. Discussed about
possible improvements in template feature and calltip format. Pushed
commit
[606f743](https://github.com/openscad/openscad/pull/2955/commits/606f743232dd97914955b8b4945f866119428b75)
in pr [\#2955](https://github.com/openscad/openscad/pull/2955)
initializing tabCount variable.

### July 21

Working on improvements of template feature discussed.

## Week 9 (July 22 - July 28)

### July 22

Discussed with mentor about possible placeholder of cursor in templates

### July 23

Pushed commit
[a378b23](https://github.com/openscad/openscad/pull/2975/commits/a378b236a1bca112dbcf216be1ac648918bb6c88)
and
[92c8b2e](https://github.com/openscad/openscad/pull/2975/commits/92c8b2e0ffe8c70eb3595fe2cc7bc2e2c840d5e9)
in pr [\#2975](https://github.com/openscad/openscad/pull/2975)
implementing improvements in template feature as discussed with mentor.

### July 24

Working on deciding a calltip format for auto-completion feature

### July 25

Pushed commit
[b280d9e](https://github.com/openscad/openscad/pull/2975/commits/b280d9e7103e3e10787e9ee16c857fa5132bcf06)
in pr [\#2975](https://github.com/openscad/openscad/pull/2975) updating
the calltip format for some keywords.

### July 26

Pushed commit
[d6a2eec](https://github.com/openscad/openscad/pull/2975/commits/d6a2eec860833270667f2341512159bec46f3274)
in pr [\#2975](https://github.com/openscad/openscad/pull/2975) adding
settings in Preferences to enable/disable autocomplete and character
threshold.

### July 27

Pushed commit
[92eaaae](https://github.com/openscad/openscad/pull/2955/commits/92eaaae0655dfb6297da5f630fb77f276ec02164)
improving handling of file drops, commit
[a3fe6d2](https://github.com/openscad/openscad/pull/2955/commits/a3fe6d228e326f7c0707371eed44f4abcf802e5c)
enabling opening of multiple file from open dialog box and commit
[94eac67](https://github.com/openscad/openscad/pull/2955/commits/94eac673e9c33bfd090573b6a0794b9ecb52d84c)
preventing opening of same file in different tab in pr
[\#2955](https://github.com/openscad/openscad/pull/2955)

### July 28

Going through the code to analyze the possibility of extending error
handling and allowing switch to tab / opening tab with error location

## Week 10 (July 29 - August 4)

### July 29

Continuing reading code base for extending error handling. Discussed
with mentor about calltip format

### July 30

Pushed commit
[464ac3c](https://github.com/openscad/openscad/pull/2975/commits/464ac3c867ed344ab54af55f57df5736388f9f03)
in pr [\#2975](https://github.com/openscad/openscad/pull/2975) improving
calltip format

### July 31

Made pr [\#3022](https://github.com/openscad/openscad/pull/3022) adding
never option in reload confirmation dialog box

### August 1

Discussed with mentor about hotspot feature of use'd/include'd files

### August 2

Going through the QScintilla documentation, trying to find a way to
implement hotspot feature

### August 3

Still going through the documentation. Realized that this task can be
achieved by indicator. After discussion, decided to stick to hotspot

### August 4

Found a bug in reading of Preferences settings. Made pr
[\#3028](https://github.com/openscad/openscad/pull/3028) removing this
bug. Discussed with mentor regarding hotspot feature, and decided to
look into parser for it. A bug was reported in pre-filled file name in
export dialog box.

## Week 11 (August 5 - August 11)

### August 5

Made pr [\#3029](https://github.com/openscad/openscad/pull/3029)
correcting file name shown in export dialog box.

### August 6

Studying the codebase and looking for possible approach to implement
hyperlink.

### August 7

Going through the QScintilla documentation looking for possible clues.

## Week 12 (August 12 - August 18)

### August 12

Discussed with mentor about a possible idea to implement hyperlinks.
Planning to pass on line and column number information of use's file
name in FileModule::registerUse.

### August 13

Going through lexer.l and parser.y files, trying to understand their
working and finding a way to pass line and column number data of use'd
file.

### August 14

Found LOC macro in parser.y. It appeared to be promising. However, it is
giving strange results. Besides the location information changes on
different preview even though there is no change in file. The code
showing this behaviour is
[here](https://github.com/RomitKumar/openscad/tree/temp). Checking if I
have done something wrong.

### August 15

Discussed with mentor and decided to skip the location information part
of use'd file, assuming it provides correct data, and implement the
remaining hyperlink part.

### August 16

Reading about the implementation of hotspot to achieve hyperlink. It
seems that the ScadLexer should be a sub-class of QsciLexerCustom, if we
want hotspot links, however that is not the case. Decided to drop
hotspot for hyperlink.

### August 17

Reading about Indicators to implement hyperlink.

### August 18

Working on code to implement hyperlink feature via Indicators.

## Week 13 (August 19 - August 25)

### August 19

Completed the code for hyperlink feature. Made pr
[\#3045](https://github.com/openscad/openscad/pull/3045). Now the part
left is regarding correct implementation of character location of use'd
files. This feature also needs to be extended to include'd files.

### August 20

Discussed with mentor about possible solution for the erroneous behavior
of Parameter Widget.