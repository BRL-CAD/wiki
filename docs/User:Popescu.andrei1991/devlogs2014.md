# GSoC 2014 development logs for Object-oriented C++ Geometry API project

## Week 1

Nothing

## Week 2

Nothing

## Week 3

2nd June - Nothing

3rd June - brush up on sph implementation, research eqn
meaning/behaviour, complete sph patch

4th June - finished sphere implementation

5th June - fixed identation, copyright, added extra constructor,
integrated with DB

6th June - fixed comparison issues for isValid, polished patch to final
form. Began talks for next primitive

7th June - further sketch primive interface talks, rough interface
implementation

8th June - break day.

## Week 4

Milestone week 4: finish sketch implementation, have a good start with
extrude

9th June - wrote Sketch interface for all subelements, untested.

10th June - wrote Sketch interface (itself) implementation. reread
previous patch.

11th June - reworked Sketch class, investigated about what role
rt_curve plays in sketch.c

12th June - break day

13th June - working on Sketch subelements implementantion, ConstSegment
and Segment

14th June - continued working on the same subclasses, not much progress.

15th June - break/minimal work

## Week 5

16th June - waited for Sketch review, discussed with Daniel, started
working on Sketch based on new header

17th June - completed Sketch interface, researched sketch.c
implementation, worked on Line class in Sketch.cpp

18th June - feedback from Daniel improved my understanding of Sketch,
research how rt_geom.h should connect to coreinterface. Modified header
file, implemented Line, Arc and Nurb.

19th June - implemented Bezier, asked for feedback on previous work,
meanwhile reasearching/implementing Sketch class itself

20th June - read through feedback, worked on Sketch subelements
according to it

21st June - break.

22nd June - fixed compilation errors, implemented Arc and Bezier.

## Week 6

23nd June - finished Nurb, wrote Get methods for Sketch, researched on
how to implement Insert/Append Segments

24th June - wrote Google midterm, wrote several simple Sketch
methods(such as NumberOfSections), planned the rest of sketch
implementation

25th June - wrote midterm post

26th June - wrote Sketch class

27th June - researched BoT; nothing;

28th June - nothing

29th June - researched & wrote BoT interface

## Week 7

30th June - nothing

1st July - rewrote interface

2nd July - nothing; issues regarding thesis; discussed on IRC/Mail

3rd July - rewrote interface according to feedback, researched
implementation details

4th July - reviewed feedback, started working on implementation

5th July - worked on BoT implementantion, investigated bot.c code.
discussed on IRC bot.c/rt_bot_internal questions, feedback provided.
should be able to implement a large part of bot now.

6th July - implemented vertex handling (Add, remove, swap) functions,
researched face index aspect.

## Week 8

7th July - Implemented Face, continued working on bot methods.

8th July - finished working on both face and bot, however, having
multiple issues that need discussion.

9th July - reviewed bot, discussed issues on IRC, rewrote several
aspects according to Sketch feedback. moved back to Sketch.

10th July - nothing; medical condition - fever; I ll do my best to
recover(the work) the following days. I am starting to feel better

11th July -worked on new Sketch implementation(provided by Daniel as
review), multiple issues with making code compile succesfully, sent mail
to ask for help.

12th July - investigated sketch compiling and implementation issues.

13th July - worked on sketch implementation;

## Week 9

14th July - finished Sketch, several issues to be adressed. Will move to
BoT

15th July - worked on bot, by looking at new sketch.

16th July - discussed latest sketch version; nothing;

17th July - nothing;

18th July - worked on bot.

19th July - nothing;

20th July - modified Sketch, fixed some sketch typo's/bugs; modified
BoT; finished bot bar constructors and Face object getter.

## Week 10

21st July - rereviewed Bot;

22nd July - worked on BoT. finished AppendFace and Get; issue about
InsertFace;

23rd July - discussed bot issues; worked on InsertFace, constructors;
looked into Pipe

24th July - nothing;

25th July - wrote Sketch DeleteSegment, finished InsertFace, fixed
AppendFace, wrote deleteFace, wrote constructors. researched how to
write bot_copy

26th July - wrote copy functions; thought and worked on face normals
functions

27th July - waited

## Week 11

28th July - discussed bot, sketch, implemented sketch;

29th July - rewrote Normal, SetNormal for bot, finised bot, wrote pipe
interface

30th July - worked on pipe interface, researched pipe code

31th July - nothing

1st August - worked on pipe, researched;

2nd August - worked on pipe, but mostly a "nothing" day

3rd August - nothing;

## Week 12

4th - break/ intermitently worked on Pipe

5th - break/ intermitently worked on Pipe

6th - break/ intermitently worked on Pipe

7th - break/ intermitently worked on Pipe

8th - break/ intermitently worked on Pipe

9th - break;

10th - worked on pipe, finished some compilation errors, will be
finished on 11th

## Week 13