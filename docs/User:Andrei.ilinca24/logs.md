# Webpage for development logs for GSoC 2015

## Community Bonding Period

**TODO list**

-   figure out if there is any major difference between .csg and .scad,
    except of expressions and modules
-   figure out what parser to use (if it’s yacc/bison or re2c or any
    other, I’ll get involved and research what benefits does each offer)
-   figure out how to use it, have a very simple demo set up within
    BRL-CAD build hooks

**15 May Update**

\- made wiki pages for account, proposal, logs

\- reread participation expectations and HACKING

\- came up with the following grammar for parsing group() functions:

expr -&gt; group_begin token group_end

token -&gt; group_content token \| expr

where group_begin is "group() {"

token is \[a-z\]+ "("\*")";

and group_end is "}"

\- looked over other BRL-CAD importer re2c lemon parsers ( wfobj and
dom2dox) in order to understand how to integrate mine into BRL-CAD but
with no luck so far

\- currently investigating perplex tool and how is it used and
integrated over the re2c layer

**17 May**

\- dom2dox is not compiling with the rest of BRL-CAD's code so its
CMakeFiles can not be used as an example of an integration of a re2c
lemon parser

**18 May**

\- cleared some empty holes in my understanding of the .csg OpenSCAD
files format due to a thread on their mailing list regarding just that;
it seems that there will be a new function added to the language soon,
called trace() and also OpenSCAD2 will implement some changes in the
existing methods

\- got some help compiling dom2dox from Kalpit

**24 May**

\- today was my birthday and I celebrated by erasing BRL-CAD and rebuilt
it from svn sources to have a fresh start of Coding Period

## Coding Period

**Week 1**

25 May : read about the lemon parser, tried to develop some simple
numerical calculations in order to attain some skill using it

26 May : applied Cliff's csg makefile integration patch to my machine,
built BRL-CAD successfully

27 May : small progress on the lemon
[tutorial](http://souptonuts.sourceforge.net/readme_lemon_tutorial.html)
, been occupied with school exam

28 May : finished the lemon tutorial, got some understanding of how
lemon parsing is done, I have now a fully working calculator parser

29 May : not much work done today, posted an email on the mailing list
with conclusions regarding the last few days work on lemon parser
calculator

30 May : prepared for Monday school exam, no work done for GsoC today

31 May : got response from Cliff on mailinglist and cleared what I have
to do next which is adding some simple parsing grammar for 1-2 csg
functions (group() ,multimatrix() ) to the newly integrated parser in
src/conv; started working on it

**Week 2**

1 June : worked on grammar, got some compiling errors, fixed a few, hope
to have some valid parsing by tomorrow

2 June : more work on grammar, restrained the errors to just 1:

home/andrei/buildbrlcad/src/conv/csg/csg_scanner.c:1:0: error: ISO C
forbids an empty translation unit \[-Wpedantic\]

I posted on mailinglist the error and the patch with the code that I
wrote today.

3 June : prepared for next exam, did nothing for GSoC

4 June : further investigations on the empty translation unit error, not
much progress , stayed on IRC

5 June : did not feel very well (headache and flu), did nothing for GSoC

6 June : got Cliff's mail response on my small grammar compiling error,
applied the changes and it compiled well; segmentation fault at
execution and gdb says the error is in PERPLEX_LEXER_private;

7 June : worked out the error and finally had group() parsed well

**Week 3**

8 June: just some code cleanup, prepared for tomorrow's exam

9 June: been at school for exam all day, did nothing for GSoC

10 June: tested and sent a [valid csg parser
patch](https://sourceforge.net/p/brlcad/patches/375/) for "group() {" ;
started working on parsing "group(){ "some content" }"

11 June: worked on bonding group_content and group_end tokens with the
existing grammar, almost done

12 June: the grammar that I proposed for group_content and group_end
parsing is good but there seems to be a problem with the perplex scanner
code; further investigations

13 June: prepared for Monday's exam, no work for GSoC

14 June: prepared for tomorrow's exam, no work for GSoC

**Week 4**

15 June: been at school for exam almost all day, did some small research
on lemon grammar

16 June: started reworking on group() parsing, it seems that the latest
patch didn't applied cleanly

17 June: sent the new patch which applies very well on my clean
checkout; did some more work with the group_content parsing

18 June: further work on group_content parsing

19 June: finished the last exam, more work on group_content parsing,
resolved some of the errors, hope to come up with a valid patch soon

20 June: finalised group_content and group_end parsing, made a
[patch](https://sourceforge.net/p/brlcad/patches/383/), tested it on a
clean checkout, posted it on sourceforge and sent a mail to the list
with project updates

21 June: last patch got committed by Cliff, added tokens for all the
functions/methods that can appear in a .csg file, started working on
grammar for union() and difference()

**Week 5 (pre-Midterm)**

22 June: further work on the functions token, trying to expand the regex
for group_content to cover all the functions formats in a .csg file and
also trying to expand the grammar

23 June: made token for parsing dimension parameters for cube(),
sphere(), cylinder() and polyhendron(), linked it with the existing
grammar

24 June: designed non-terminals for assignation of parameters ( for
example for parsing things like "convexity = 1" or "size = \[3,4,5\]")

25 June: heavy work on the csg grammar, lots of tests, working on edge
cases, almost done & ready for a patch submission

## Midterm Evaluation Period

At the beginning of the coding period I haven't had anything related to
lemon and re2c integrated into BRL-CAD. I decided to take some time to
study how to use this parsing tools before getting to the actual writing
of the code. Because of my summer exam session, my progress was little
in the first few weeks and, after working out some simple calculators
using lemon, I finally started working on the .csg grammar. Initially, I
though I could gradually parse and interpret functions and methods but I
soon realised that having a fully functional grammar first is a better
idea. With lots of help from Cliff and Andrei Constantin Popescu, I
managed to finish the grammar just 2 days after the Midterm Evaluation
Period opening and have it merged.

To run my code, just go in build/src/conv/csg , write an input file with
some .csg text in it (or save a .csg there) and then just run ./csg
input.txt output.txt . It should print on the screen various messages
containing the tokens matched in the parsing process.

26 June: sent a [patch](https://sourceforge.net/p/brlcad/patches/386/)
regarding the .csg grammar which is almost complete , needs some work in
the priorities section to be just right

27 June: filled midterm form on melange, worked on priorities

28 June: sorted out the priorities section, changed some of the internal
structure of the grammar to parse imbricated functions better, added a
new rule for assignation, made a [new
patch](https://sourceforge.net/p/brlcad/patches/388/) with the complete
grammar and sent a mail to the list with the latest updates

29 June: talked with teepee from OpenSCAD about the conversion from
.scad to .csg, found out how to properly test the proposed grammar
(running the OpenSCAD test suite) and also got some insight about the
functions that generate the .csg from the .scad ( toString for
[primitives](https://github.com/openscad/openscad/blob/master/src/primitives.cc#L610)
and [special
functions](https://github.com/openscad/openscad/blob/master/src/transform.cc#L190)
)

30 June: did nothing for GSoC

1 July: tested my grammar using some .csg files provided by OpenSCAD,
modified it to also parse "group();" , not only "group() {...}", added
DEBUG macro and tried to print some matched functions using
bu_vls_addr(&A-&gt;value) but with no luck

2 July: further work on printing matched functions, renamed some tokens
in the grammar for a clearer code

## Coding Period (2nd half)

3-6 July : had a mental breakdown because of the lack of progress and
sleep in the last few days, took some time to organise my days and get
back on track with everything

**Week 6**

7 July : restarted reading dom2dox code to learn about interpreting
lemon grammar, understood some basic principles

8 July : cleared some confusions about the "END_TEXT;" macro after a
discussion with Sean on IRC, decided not to use macros to prevent
complexity issues

9 July : found the /doc/parsers/writing_perplex_lemon_parsers.doc and
also the templates in there and read through them , they seem well
explained and detailed

10-11-12 July : not much progress, tried a different approach by
modifying the grammar to match functions as 1 token to reduce the number
of terminals, ended up not parsing the function parameters

**Week 7**

did nothing for GSoC

**Week 8**

20 July : got Sean's mail about communicating more and staying more on
IRC, tried to install tmux to be 24/7 on IRC but failed due to some
incompatibility issues, decided to stick to XChat

21-23 July : documented about perplex, re2c and lemon in order to
understand better what is not working and why and asking the right
questions

24 July : sent an email to Sean and Isaac with questions about why
fprintf(appData-&gt;outfile, "%s", bu_vls_addr(&A-&gt;value)) does not
print anything but the token is matched, about the generated tree and
also discussed updating deliverables

25 July : more work on sending matched strings to main, restrained the
problem to a memory allocation issue