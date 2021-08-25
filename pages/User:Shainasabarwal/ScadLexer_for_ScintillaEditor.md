## Personal Information

-   **Name**: Shaina Sabarwal
-   **Email-address**: iamshainasabarwal@gmail.com
-   **IRC username**: shaina
-   **Contact Number**: +917837091321
-   **Blog**: shainasabarwal.wordpress.com

## Background Information

-   Computer Science Engineering student at Guru Nanak Dev Engineering
    College, Ludhiana, Punjab, India. Presently studying in 4th year.
-   I have worked in C++, Qt, Wt, HTML, CSS, Javascript, Ruby on rails,
    flex and Bison and Wordpress.
-   Have worked with OpenSCAD in 2014 on project UI Brushup of OpenSCAD
    that was about enhancing the interface for users of OpenSCAD by
    adding QScintilla Editor and its various features, Toolbars with
    small 2D icons. Options to choose color scheme of the solid models,
    and launching screen of OpenSCAD.
-   I am active member of Linux User Group, Ludhiana where the students
    are made aware about the open source technologies and motivated to
    contribute in them.

## Project Information

### Title: SCAD lexer for QScintilla Editor

This project aims to make lexer specifically for SCAD language.
Currently, QScintilla is using CPP lexer, which cause syntax problem as
CPP language is very large as compared to SCAD language of OpenSCAD.
With this, some scintilla and GUI related issues will also be solved.

**QsciLexerCustom inherited lexer** In my project UI brushup of
OpenSCAD, I added QScintilla editor and used its CPP lexer class
QsciLexerCPP for syntax highlighting. It worked fine. But after testing,
some issues arises as SCAD is small and simple language as compared to
CPP. In this project, we found the solution of the problem - Writing a
lexer specifically for SCAD language. QScintilla library has a class
QsciLexerCustom
(http://pyqt.sourceforge.net/Docs/QScintilla2/classQsciLexerCustom.html)
which can be used as a base class for new language lexers. The advantage
of using this class is that it doesn't require to make any change in
QScintilla code or to re-compile it. This will be inherited by our new
class for Scad lexer and its virtual functions will be redefined.

**Defining style index for SCAD language** SCAD language includes
various categories of keywords including mathematical functions, solid
primitives as defined: <http://www.openscad.org/cheatsheet/> ,Operators,
Numbers, Comments - single line as well as multiline, single quoted and
double quoted strings, parenthesis and variable names. The lexer firstly
requires to index the styles of different keywords for the purpose of
syntax highlighting using functions of qsciLexerCustom. This indexing
can be done using an enum as <code>

`enum {`
`       Default = 0`
`       Keyword = 1`
`       Comment = 2`
`       Operator = 3`
`}`

</code>

**Syntax Highlighting** Syntax highlighting is very important feature of
an editor as it improves the readability of the code and context of
text. QScintilla editor in OpenSCAD as used CPP lexer, caused problems
in highlighting as <https://github.com/openscad/openscad/issues/1172>
Writing lexer for SCAD language will solve such problems. For this,
different functions for highlighting of keywords, operators, numbers,
mathematical functions etc will be defined in the lexer.
For Example
<code> void highlightKeywords(const QString &source, int start){

`   foreach(QString word, keywordsList) {    //iterate keywords`
`       if(source.contains(word)) {`
`int p = source.count(word);    // consider joining`
`           int index = 0;    // begin to consider the indices `
`           while(p != 0) {`
`               int begin = source.indexOf(word, index);    //consider an index entry`
`               index = begin+1;    //give point of reference for next iteration`
`               startStyling(start + begin);    //begin to style with an index entry`
`               setStyling(word.length(), Keyword);    //for the length of a given style word.length Keyword`
`               startStyling(start + begin);    //finish styling`
`               p--;`
`           }`
`       }`
`   }`

}

</code> As shown, the function is using respective style index 'Keyword'
for styling. The complete DEMO for keyword highlighting is:
<https://github.com/shaina7837/Scad-Lexer-demo>

**Different Color scheme** Not every color suits to everyone. People
like to have choices specially in case of colors, so it is very
important to have different color schemes as options in preferences to
be selected by the user. This feature helps to improve the usability of
software a lot. It will require checking the selected scheme and define
style index accordingly.

**Issue \#1108 Customizable Icon set** I liked the idea that user may
add its own icon set for toolbars. It will require user to add his/her
icons in a file such as icons/icon.svg and openscad will fetch and put
them onto toolbar instead adding them into mainwin.cc code directly.

**Issue \#1056 Toolbar Buttons** Toolbars requires more icons as
demanded here <https://github.com/openscad/openscad/issues/1056>

**Issue \#1172 Syntax highlighting: \# affects the whole line** As
presently, qscintilla uses CPP lexer, so it takes the whole line as
preprocessor directive, started with \#. With writing lexer specifically
for SCAD language, this problem will be tackled.

**Issue \#905 AutoComplete/ Calltips for QScintilla Editor** Many times,
a programmer makes mistakes while writing syntax which can cause
irritable errors and reduce productivity. In this case, auto completion
or call tips helps a lot, which is considered as a great feature of an
editor. As a first step, only the functions defined in the scad language
will be added to be shown in call tips. Further after the feedback of
the community, names of the modules related to current project can be
added.

**Issue \#1075 Add multi-line, nested list '\[' '\]' indentation and
tree folding to QScintilla Editor** The feature of multi line, nested
indentation and folding can be added into the scad lexer using functions
like setFoldAtElse(), setFoldComments() etc.

**Issue \#915 Scintilla Editor issues** The remaining issues such as
auto scroll to error line after compilation, convert tab into spaces and
highlighting the folded region will be solved.

## MILESTONES

**Community Bonding Period**

-   Talk to the community Members
-   Start reading understand existing code of scintillalexer of openscad

**Week 1(25th May)**

-   Get started and solving issue \#1056 Toolbar buttons

**Week 2(1 june)**

-   Read and get confortable of qscilexercustom and its base class
    qscilexer to understand its virtual functions that will be defined
    in scad lexer
-   Start writing scad lexer

**Week 3(8 june)**

-   List all keywords, operators, mathematical functions, solid
    primitive functions

etc of the SCAD language and define their style index.

**Week 4(15 june)**

-   Start redefining the functions of qscilexercustom in scad lexer
-   Define function to color keywords.
-   Define function to color comments.

**Week 5(22 june)**

-   Define function to color Operators.
-   Define function to color solid primitive functions
-   Define function to color mathematical functions

**Week 6(29 june)**

-   Define function to color transformation functions.
-   Read about existing color scheme code in scintilla editor code in
    openscad and try to understand how to add those color scheme option
    through new scad lexer.

**Week 7(6 july)**

-   Define various color scheme options for users.
-   Read and improve code.

**Week 8(13 july)**

-   Solve scintilla related issues listed in issue \#915
-   Add autocomplete feature solving issue \#905

**Week 9, 10(20 july)**

-   Find a way to fetch icons from a icons file rather than directly
    coded in mainwin.cc
-   Solve issue \#1108 i.e. allow users to add its own icon set.

**Week 11, 12(23 july)**

-   Solve issues \#1075 and \#1172

**Week 13(6 August)**

-   Solve the remaining errors.
-   Get feedback by mentors and other community members
-   Test on various platforms

**Week 14(20 August)**

-   Improve code and testing before final submission of code.

## Deliverable

-   A special lexer for SCAD language with syntax highlighting and other
    features.
-   A file to add custom icons by users.
-   More icons for toolbar
-   Improvement of scintilla editor by removing its issues.

## Communication

### Time Availability

I will be available for 40 to 48 hours / week, can spend more, if
required.

### Email/Mailing list

My email address is iamshainasabarwal@gmail.com, I have subscribed to
both brlcad and openscad mailing lists. I have been in contact through
these mailing lists with other community members.

### Real-Time Contact

I can interact with the mentors through OpenSCAD's IRC
channel(\#openscad) on freenode. My nickname on IRC is shaina. I am also
comfortable with talking to my mentor via telephone if need arises.
**Contact Number**: +91 7837091321

### Code Review

I already has commit access to openscad respository at
<https://github.com/openscad/openscad>. I will push my code in separate
branch of same repository and send pull request so that mentors can
review my code and then merge it up in master branch after testing.

## Why OpenSCAD?

OpenSCAD is an open source CAD software application used to make 3D
solid models. It has various applications in mechanical, civil,
electronics and designing hardware tools for research and education
purposes. The software has potential to be used by the large number of
professionals and hardware developers. I have already contributed in
this community and worked in UI brushup of OpenSCAD as my last year GSOC
project. I have very good interaction with mentors and community members
of the community as I also attended Reunion at California in 2014. I
feel very confortable to discuss and come up with new ideas.

## Why SCAD lexer project?

I came up with this idea of adding scad lexer as gsoc project, because
last time, I, in my project 'UI brushup of OpenSCAD' used QsciLexerCPP
as a base class for SCAD lexer class. But as the CPP is very large
language as compared to SCAD so it is causing various issues, which I
came to know later. In this year, I want to solve all those issues by
writing a lexer specifically for scad lexer.

## Why Me?

As we have very less number of women in technical study as compared to
men, I want to be the part of technical community and spread awareness
about women in tech in our society. I learnt a lot being the part of
this community and want to contribute more through this program and
afterwards. I also shared idea of improving the website of OpenSCAD but
that couldn't be the part of this project, so I have plans to do so
after completion of this project.