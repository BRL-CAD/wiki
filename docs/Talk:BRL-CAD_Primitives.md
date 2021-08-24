Other sources for information:

-   <http://brlcad.org/wiki/A_Survey_of_Implicit_Constraints_in_Primitives>
    which also could use some filling out
-   <http://bzflag.bz/~starseeker/geometric_primitives.txt>
-   scattered through all brl-cad manuals
-   source (last resort I hope!)

I've partially filled in the info for each primitive as I found it and
as I've had time. Feel free to improve this page! Many of the primitives
listed here are not fully implemented (present in *in* or *create* but
absent from *make* or without a form when it should have one, etc.), it
might be useful to add version numbers to indicate when the object was
introduced or when it was completed, especially if there are older
compiled binaries on the website that don't yet support them.


??Whoever wrote this should have signed it??

## Revision of Introduction (5/27/13)

As a tech writer who is new to BRL-CAD, I'm finding that my study of it
is being hampered by the current state of its documentation--so I
decided to work on improving it. My first step was going to be revising
the introductory section of this article to more completely describe the
MGED commands for not only creating but also viewing and editing the
properties of geometric primitives. But I decided all such information
more properly belonged elsewhere, so I:

-   moved the information on creation methods to a new article,
-   retitled the old articles on determining and changing the properties
    of primitives to be consistent (leaving redirects in their old
    locations),
-   added links to those three articles to the introduction to this one,
    and
-   began reworking those three articles.

Of course, I also anticipate improving the rest of this article as time
permits.

[JoelDBenson](User:JoelDBenson.md)
([talk](User_talk:JoelDBenson.md)) 20:22, 27 May 2013 (UTC)

Joel, impressive how you were able to gather all of our myriad
documentation and developer notes that are scattered about. Your cleanup
and improvement efforts are very much appreciated, thank you in spades.

One of our long-term goals has been the cleanup and restructuring of the
documentation like you've started, with our online documentation fully
synchronized with our developer resources. From a developer-centric
perspective, this means bridging a technical gap between the software
and the ease of use of wiki-style online editing. This is because the
code is constantly changing and we need some way to keep our
documentation as up-to-date as possible, ideally as fast as the code is
changing and ideally as easy to edit as possible (obviously).

Towards the technical end, most of our most current documentation is now
in the XML Docbook format (html-style markup) in our repository. The
intent (which is not yet actualized) of getting that content
synchronized onto the website.

My goal for many years now is to get bidirectional round-trip editing
set up whereby our XML documents are published to the web and as
developers change the docs, the website is updated. Similarly, any user
can go to one of the website pages (like you've been doing on the wiki)
and those changes actually get staged for commit into our repository.
How this will eventually happen is obviously a major technical
challenge.

Again, that setup is not yet in place but you will find remnants and
information about it strewn about just like everything else. I mention
it only so you are aware of the long-term plan, not to derail your
current (excellent) goals of cleaning up what we do have.

One piece of information you may not yet have come across is a [table of
contents](TOC.md) that I recently pulled together. That includes
a massive Documentation section that I would greatly appreciate feedback
on from your tech writer perspective. I'd like to build up a consistent
vision for where the website as a whole is going with an emphasis on
organizing and cleaning up our absurdly extensive and poorly organized
documentation. You wouldn't know it but we actually have several
\*thousand\* pages (million+ words) of documentation when you add it all
up!

[Sean](User:Sean.md) ([talk](User_talk:Sean.md)) 11:31,
31 May 2013 (UTC)

Sean—

Thanks for the encouragement! I'll provide some feedback (especially on
your TOC) via your Talk page, when I get time (that's always the rub,
isn't it!

By the way, I've noticed some technical problems with this Wiki.
Specifically:

-   The libMagick.so.9 component is reported to be missing, so it's not
    possible to have the Wiki resize images on the fly—check the
    downloaded images page for evidence of this.
-   Also, attempting to access the authoring help pages fails because
    "the Class 'XMLReader' is missing". Fortunately, much of what I've
    learned via other Wikis does seem to work here. Still, it would be
    nice if this site's authoring help worked.

[JoelDBenson](User:JoelDBenson.md)
([talk](User_talk:JoelDBenson.md)) 04:40, 10 June 2013 (UTC)

## Completion of ARBs section

I have concluded that keeping this article to a reasonable length will
require moving the kinds of details I had included for rpps and boxes to
companion *Creating and editing ... primitives* articles. I created two
such articles, one for arb8s and one for arbns and moved info that had
been here into them. If the arbn article proves sufficiently short, I
might combine them into a single *Creating and editing arb primitives*
article—time will tell.

Having done that, I was able to complete the text of the Arbs section of
this article as a true overview. I do plan on adding some illustrations
as soon as I have time.

[JoelDBenson](User:JoelDBenson.md)
([talk](User_talk:JoelDBenson.md)) 04:40, 10 June 2013 (UTC)

On further reflection, I think I've gone overboard in reducing the
extent of this section. I need to include details on how the vertices of
arb8s, arb7s, etc. have to be defined so that they are recognized as
such. Plus the illustrations, of course.

[JoelDBenson](User:JoelDBenson.md)
([talk](User_talk:JoelDBenson.md)) 15:03, 10 June 2013 (UTC)
