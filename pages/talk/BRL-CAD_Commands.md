This page would be much better if it was formatted similar to [MGED
Commands](MGED_Commands.md), marking commands to their purpose
or categorizing them or something. As is, it's incomplete and redundant.
--[Ssd](../user/Ssd.md) 09:42, 15 November 2009 (EST)

------------------------------------------------------------------------

Agreed. Though with over 400 commands, the task really begs for
automation and scripting or a plugin.. or some serious OCD editing.
Ideas on ways to streamline the process? --[Sean](../user/Sean.md)
14:11, 15 November 2009 (EST)


If you just want an alphabetized list, your best bet is to use the
category system to do the heavy lifting and forget marking by purpose
(or categorizing different purposes in different categories). If you
want a list sorted by function, just gotta plug at it one by one...like
putting all the image conversion functions in at once or something.
Where is the documentation for these things anyway?
--[Ssd](../user/Ssd.md) 08:27, 18 November 2009 (EST)

<!-- -->



I think we'd want to first at least have complete documentation for all
commands. How they are indexed and categorized isn't nearly as
time-consuming as creating a page per command, though both tasks are
exceptionally valuable (and tedious). The availability of docs depends
on the command type, but most are either in manpage format (throughout
the source tree, [example
here](http://brlcad.svn.sourceforge.net/viewvc/brlcad/brlcad/trunk/src/rt/rtshot.1?revision=33538&view=markup),
or in docbook format
[here](http://brlcad.svn.sourceforge.net/viewvc/brlcad/brlcad/trunk/doc/docbook/system/man1/en/).
At least, that's the case for the ones not already imported. --
[Sean](../user/Sean.md) 02:43, 19 November 2009 (EST)

Guess I misunderstood the question. I'd use the categorization as a
vechicle to drive the manual labor of getting the information in.
However, automation is good too. When I'm done with MGED commands, I'll
look for the docs you linked above and perhaps automate importing them.
I suppose I should automate the categorization I'm doing now (have you
looked? does it look ok?), but I'm reading the pages as I go, and
finding a few typos and things on the way too. By the way...is there a
reason why the MGED debug\* commands are not marked as developer
commands? --[Ssd](../user/Ssd.md) 02:17, 21 November 2009 (EST)
