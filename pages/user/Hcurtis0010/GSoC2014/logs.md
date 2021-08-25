## Week 1

**Monday, May 19**

I re-read the Hacking file, and that led me to do research on binaries,
regression testing, and other topics. Also, I had a good IRC
conversation with my mentor, Sean Morrison, about how best to interact
with one another and what I will need to do to succeed during GSoC.

**Tuesday, May 20**

Sean and I had an enlightening IRC conversation in which he pointed out
the danger of relying too much on examples when dealing with code.

Afterward, I wrote some programs involving arrays. Although I finished
the first one, I ran into problems with the second. I did some research
as I attempted to solve it; the topics I investigated included dynamic
allocation, vectors, and heaps. Sean had asked me to create the programs
in order to learn more about dynamic and stack memory and be able to
apply that knowledge to future GSoC activities.

**Wednesday, May 21**

I am happy to say that I learned a lot today. One of the more memorable
things I learned was that I should not put the "using namespace"
construct in my programs. I conducted research to find out why. Also, I
read about malloc(), pointers, sizeof, and the differences between ANSI
C, C99, and C++.

I showed to the community the program that I completed yesterday, and I
received feedback on it. That evening, I worked on the second program,
the one that had been giving me problems. In it I used malloc() for the
first time. At first it wouldn't compile, and later it would compile but
would crash at runtime. However, I finally got it to work after a fellow
GsoCer, raj12lnm, told me what I was doing wrong.

The work I did today is preparing me to address problems with BRL-CAD’s
fast4-g.c program as well as produce the conversion library that will be
the focus of my GSoC proposal. We'll see how it goes.

**Thursday, May 22**

I converted yesterday's C++ programs to C. At first, they refused to
compile, but after some research and a little trial and error, I was
able to get them to work. A fellow GSoC student, oana_, helped me
remedy a problem with one of them. The process was a good lesson. One
interesting thing I learned was that I should avoid using certain code
elements such as conio.h, getch(), and scanf_s because they work solely
in Microsoft compilers and thus would make my programs less portable.

Next, I will create a version of my dynamic allocation program that uses
functions from BRL-CAD’s libbu library API instead of those of the
standard library. As I do so, I am sure that I will use plenty of what
this week’s C++ and C exercises have taught me.

**Friday, May 23**

Today, I worked on a version of my dynamic allocation program that
features libbu elements in place of stdlib functions. This is one more
activity will help prepare me to tackle the fast4-g task. Unfortunately,
I ran into a problem: I could not get the compiler to locate all of the
interdependent header files that the program needs in order to run.

**Saturday, May 24**

I re-read the GSoC checklist to identify the items on it that I have not
yet done. Also, I re-read and analyzed BRL-CAD’s fast4-g.c program and
worked on my plan to improve it.

**Sunday, May 25**

Today, I continued to analyze the fast4-g.c program and work on my plan
to improve it. As a part of this, I researched elements in it that I was
not familiar with. This process is teaching me skills that will help me
complete my GSoC project.

Also, I read the online document "How To Ask Questions The Smart Way."
It taught me how to ask well-researched questions when requesting other
developers' help with problems.

## Week 2

**Monday, May 26**

I read more about pointers, malloc, and other topics in order to
understand them better. Also, I continued to analyze fast4-g.c so that I
could put myself in a better position to improve it.

**Tuesday, May 27**

Unfortunately, I became stuck while working on fast4-g.c In order to get
out of that rut, I asked myself new questions about the task as part of
a fresh approach to it. Then, I continued to analyze the program as well
as the problem I was attempting to solve.

**Wednesday, May 28**

Today, I continued to work on the fast4-g.c issue. I found evidence that
I might be going down an incorrect path in my approach to the problem.
With some additional work, I will know for sure whether this is true.

**Thursday, May 29**

I had a good IRC conversation with GSoC mentors Sean Morrison and Erik
Greenwald this evening about my progress. Because of a prior commitment,
I was not able to work on GSoC tasks as much as I would have liked.
However, I will make up for that tomorrow.

**Friday, May 30**

Today, I read information about and practiced using my virtual machine
and my developer tools. I have realized that I need to increase my
proficiency with them in order to continue making progress.

**Saturday, May 31**

I continued to research and work with my developer tools and virtual
machine. I ran into problems when I tried to install a software update
for the VM, but I managed to solve them.

**Sunday, June 1**

What I did today was read the install file and the Contributors' Guide
to BRL-CAD. It served as preparation for another try at making my
dynamic allocation program work using BRL-CAD functions.

## Week 3

**Monday, June 2**

I worked on the libbu task (the one that involves using BRL-CAD
functions like bu_malloc to run my dynamic allocation program). Also, I
conducted research as needed; part of that was a good IRC conversation
with Sean during which I learned the correct way to use some important
virtual machine commands.

**Tuesday, June 3**

Today I continued to make progress on the libbu task. As a part of this,
I read about CMake and how it locates libraries.

**Wednesday, June 4**

I read about CMake and how to write a CMakeLists.txt file. Afterward, I
attempted to write one.

**Thursday, June 5**

During the first half of today's work session, I read more about CMake
and worked on my CMakeLists.txt file. However, when I communicated with
Sean later that day, he told me that for now I should use GNU Compiler
Collection (GCC) commands instead of a CMakeLists.txt file to compile my
program. He said that it is important that I build manually at first so
that I can learn what the GCC options mean and how compilation and
linking work.

Incidentally, a problem I have is how long my system takes to build
BRL-CAD. I hope that I can find a way to shorten the time.

**Friday, June 6**

I continued trying to enable my dynamic allocation program to use
BRL-CAD headers. As a part of this, I read about GCC and its commands.

**Saturday, June 7**

Today I was able to compile my dynamic allocation program. However, that
gave rise to new issues that had to do with linking. I researched some
possible solutions and tried them, but I did not have much success. I
will keep trying.

**Sunday, June 8**

I had a good IRC conversation with Sean about the dynamic allocation
task. Afterward, I was able to both build and link my program, but it
would not run. The error message it gave said that it could not locate
the shared object file. I began investigating the problem, and I learned
a lot.

## Week 4

**Monday, June 9**

During our conversation in the \#brlcad IRC channel, Sean gave me
helpful feedback on the GCC options I was using to compile my dynamic
allocation program. However, even after I incorporated his suggestions,
I received an error message when I attempted to run the code. I will
continue to search for a solution.

**Tuesday, June 10**

I kept researching and trying different ways to enable my dynamic
allocation program to use BRL-CAD functions, but unfortunately, none of
them worked. At least my efforts did allow me to rule out an incorrect
file path in my compile line as the cause of the error message.
Incidentally, my laptop overheated and began running slowly, so I had to
turn it off and let it cool before starting it again and rebuilding
BRL-CAD.

At the very end of the night, I finally solved the problem with my
dynamic allocation code. I was very happy.

The technique that worked involved my adding the path of the library I
needed to my system’s /etc/ld.so.conf file. In the process, I used the
editors vi and nano for the first time.

**Wednesday, June 11**

I resumed work on the fast4-g task that I had first attempted several
days ago. I researched and analyzed the problem, and then I began
designing the changes I planned to make to the code.

**Thursday, June 12**

I continued making corrections to fast4-g. However, I was not able to
dedicate a lot of time to GSoC today because of a prior commitment.

**Friday, June 13**

I worked some more on the fast4-g task. I ran into some problems in
dealing with parts of the program that I do not understand well. I might
need to consult with a mentor before I can continue.

**Saturday, June 14**

Today I closely reexamined and conducted further research on the parts
of fast4-g that I do not understand well. I was able to answer some of
the questions I had about this task, but I am still stuck. Tomorrow I
will discuss the situation with my mentors and show them the code I have
written.

**Sunday, June 15**

I conversed over IRC with a fellow GSoC student, andrei__, about my
fast4-g task. His comments were helpful. Also, I continued working on my
corrections to the code.

## Week 5

**Monday, June 16**

In an attempt to become "unstuck" and resume making satisfactory
progress, I experimented with different features within the fast4-g code
I had written. I found the process beneficial.

At the end of the night, I had a good conversation with Sean. He
provided feedback on the work I had done on the libbu dynamic allocation
task. Also, he gave me excellent advice on how best to ask for
assistance in the \#brlcad channel.

**Tuesday, June 17**

Today Sean gave me very helpful feedback on the code I had written for
the fast4-g task. I worked on rewriting the code.

**Wednesday, June 18**

In order to deepen my understanding of the fast4-g task, I reread my
notes and identified the most important and helpful pieces of
information.

Afterward, I finished and posted a new draft of my code converting the
program's region list from stack allocated to dynamic. I thought it was
a step in the right direction, and hopefully, I will soon be able to
submit a patch.

One unfortunate fact that is impeding my progress on this task is that I
do not have a fully clear picture of how fast4-g converts geometry from
the fastgen4 format to the BRL-CAD format. I have tried hard to examine
the program and research the parts of it that I do not understand. Even
so, I am having a hard time knowing what corrections to make in order to
solve the problem at hand.

My lingering questions are as follows:

-   How do I know when the heap memory allocated for the group_head
    needs to be resized?
-   Once I have determined that, how do I know what new size it needs to
    be?
-   Why does the group_head array in fast4-g's commit 56495 hold 11
    elements in particular and not some other number of them?

**Thursday, June 19**

Today I continued working on my fast4g task. This included further
attempts to answer the questions I listed in yesterday's log entry.

Understanding the way pointers work is an important part of this
endeavor. I thought my familiarity with them was adequate, but I later
realized that I was mistaken. For example, I did not understand the
concept of pointer dereferencing as well as I should. Before continuing
to code, I read some information about pointers that was appropriate for
my skill level in order to improve my understanding of them.

Also, I began going back through fast4-g.c to look for clues to the
answers to my questions, but then I thought of a better idea. Since I
knew that the wmember variable called group_head was an important part
of the solution, I decided that I needed to focus on learning more about
that element in particular. In order to accomplish this, I examined the
functions and macros that are associated with it. It was a process that
I found worthwhile.

Incidentally, an additional question I now have is about the meaning of
the Ws in the variable name wmember and the header name wdb.h. I looked
for the answer but could not find it.

Near the end of the night, I read a BRL-CAD tutorial pdf called
"Converting Geometry Between BRL-CAD and Other Formats." It included a
section about FASTGEN-to-BRL-CAD conversion that helped me to better
understand the fast4-g task.

**Friday, June 20**

I worked again on the fast4-g task. One interesting thing is that last
night's research improved my understanding of the differences between
CSG and BREP. While FASTGEN4 is a BREP format, BRL-CAD is oriented more
toward CSG. Fast4-g.c's purpose is to convert FASTGEN4 to BRL-CAD.

Andrei_, a fellow GSoC student who has helped me before, offered me an
answer to one of the questions I had posted. Also, he gave me feedback
on the code I had written. It was kind of him.

Incidentally, I posted a new draft of my corrections. It is here:
<http://paste.lisp.org/+32AW>

I read some great information about structs and pointers. It will help
me to understand the parts of fast4-g.c that I am having trouble with
and to write high-quality code for my patch.

I have a new question: when I allocate memory for the group_head
wmember list in fast4-g.c, should I use bu_\*alloc() or bu_get()? I
researched this, but I could not find a clear answer.

I do know that bu_\*alloc() is right for items that are large or
infrequently needed. In contrast, bu_get() is suitable for small
pointers and is faster. Sean said that he would like fast4-g.c to be
faster, but maybe group_head is too large for bu_get() to handle.

**Saturday, June 21**

Today was another day devoted to fast4-g. I went back through the
program and traced the flow of all of the modules that involve the
variable group_head. My understanding of the code has never been
better; now I need to figure out exactly what form these stack-allocated
instances of group_head will take upon becoming dynamically allocated.

A question that I asked earlier this month in the \#brlcad IRC channel
is this: with what number do I replace 11, the subscript of the
stack-allocated version of group_head, once I make group_head
dynamically allocated? I think that I now have the answer.

Also, interestingly enough, I am realizing that understanding fast4-g.c
involves learning about the way linked lists function. There is a macro
called BU_LIST_INSERT in the program that works with group_head. The
comments accompanying the macro definition say, "To put \[a\] new item
at the tail of \[a\] list, insert \[the new item\] before the head."

This does not make sense to me. I thought that placing something at the
end of a list meant placing it after the list's head. I attempted to
find information that would clarify this, but I could not. I asked a
question about it in the channel to see whether anyone would be willing
to explain it.

**Sunday, June 22**

I made further progress toward my objective of converting elements of
BRL-CAD's fast4-g.c from stack allocated to dynamically allocated. I
finished and posted another draft of my code, asking for feedback as
always. This is a link to it: <http://paste.lisp.org/+32BJ>

The fact that I am more familiar with the program's features and its
flow than in the past has been beneficial. I might now be close to
creating a usable patch. By the way, the comments in BRL-CAD header
files such as list.h and wdb.h have helped me determine what to include
in my fast4-g.c corrections.

I would also like to mention something I found puzzling. The code in
lines 2943 and 2944 of fast4-g.c commit 56495 will always run because it
is in the main function, yet similar code in commit 56641 is restricted
by an if statement. I studied the program in order to understand why,
but I was unable to answer this question.

In the evening, I did some additional reading about pointers. Moreover,
I looked at some other information to refresh my memory on how to make
patches, and then I created a fast4-g.c patch.

The patch that I produced might not be acceptable because I based it on
commit 56495 and will probably need to use commit 60592 instead. At
least I know that I am able to make a patch. My best guess is that in my
final version of fast4-g.c, I will need to comment out the other
developer's corrections that Sean disliked; however, I must confirm
this.