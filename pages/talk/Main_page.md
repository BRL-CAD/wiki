Hello and welcome, X Tin Basher! The edits to EBM and elsewhere are more
than welcome, thanks!

Cheers! --[Sean](../user/Sean.md) 10:48, 23 November 2010 (EST)

------------------------------------------------------------------------

I've started having fun with BRL-CAD, but I notice that this wiki needs
some TLC. I'm an old hand at mediawiki, so if nobody objects, I'm going
to start making massive changes here. For starters, I can:

-   categorize every page, looks like there's quite a few untagged pages
-   relabel the stuff in [:Category:MGED] (:Category:MGED.md) to
    remove the prefix so it looks nicer (this is a huge job unless it
    gets automated)
-   Eventually, I'd like to make a page for (almost) every executable in
    brlcad/bin; some already have pdfs or pages and I'd start by finding
    and categorizing these.

If there are no objections, I'll get started when I have time.
--[Ssd](../user/Ssd.md) 08:40, 12 November 2009 (EST)

------------------------------------------------------------------------

Hi Ssd, no objections whatsoever! The wiki could absolutely use lots of
TLC. Let me know if there are things I can do to help you out. If you're
really up for a challenge, one of the things we were working on over a
year ago (that never got off the ground) was a way to keep our Docbook
XML sources fully synchronized with Mediawiki so you could perform
bidirectional editing and have changes to one update the other. The
basic idea was a Mediawiki plugin that staged wiki changes to an SVN
checkout with Docbook-to-wiki and wiki-to-Docbook conversions happening
on the fly.

Something to perhaps think about, but even without that, the Wiki still
needs massive TLC. The categorization and filling in of missing content
will be greatly appreciated!

Cheers! --[Sean](../user/Sean.md) 08:48, 12 November 2009 (EST)

------------------------------------------------------------------------

It also annoys me that none of the PDF's have a table of contents, but
that's not somethign I know how to fix so easily.
--[Ssd](../user/Ssd.md) 09:02, 12 November 2009 (EST)

------------------------------------------------------------------------

Lots of great updates earlier today! As for the table of contents, are
you referring specifically to PDF indices? Otherwise, the big documents
(Vol II - Intro to MGED and Vol III - Principles of Eff. Modeling) have
tables of contents (on pages vii and iii respectively). They're also
part of the larger migration to Docbook as the central document
management format so that the PDF files can be continually updated and
regenerated, and the documents can be output in different formats (e.g.
directly integrated with the wiki or even if just as static html dumps).
-- [Sean](../user/Sean.md) 15:26, 12 November 2009 (EST)


Lots of updates...yes, and did you see the time frame? Those were the
easy ones. The rest will take longer, especially as I might actually
have to write and/or research the content. As to the PDF's...the
document has a toc obviously, but the PDF does not. Yes, I mean the pdf
toc/index/bookmark thingie. Very annoying to try to find stuff in there
without one. I take it that the docbook material is not yet in the wiki.
Has anyone started work on a wiki translator for it? The bidirectional
gateway thing sounds interesting but dangerous.
--[Ssd](../user/Ssd.md) 00:58, 14 November 2009 (EST)

## BRL-CAD Primitives

I got annoyed that I couldn't find a comprehensive list of primitives,
so I started filling out [BRL-CAD
Primitives](/wiki/doc/BRL-CAD_Primitives). I'm sure I missed a few, and
the few that are there don't all have complete information. It would be
nice to add a description/title, and a link to relevant documentation
(and page) for those that need it.

Anyone wanna help fill in the blanks? --[ssd](../user/Ssd.md)
05:39, 31 December 2009 (EST)


Of relevance to this work, there is <http://brlcad.org/tmp/primitives/>
which includes grouping and visuals for most of the production-ready
primitives. --[Sean](../user/Sean.md) 14:20, 25 March 2010 (EDT)

I suggest utilizing this work for categorization of primitives - we've
been working on how to group these things for a while, and we have an
ordering that's based on a combination of the mathematical nature of the
primitives and the type of data they use:

<http://bzflag.bz/~starseeker/geometric_primitives.txt>

CY (starseeker in irc)

Note that this categorization doesn't include a few "work in progress"
primitives like metaballs and superell - metaballs in particular might
need a little thought to categorize it - perhaps composite implicit


Great stuff! So brl-cad DOES have a revolve primitive! I'll have to play
with that I guess. I still hate the sketch editor, so unless I start
importing sketches, I might just stick with pipes. I added a few more
from your list to the list. Your categorization closely fits mine
already. A few discrepancies... First, in what way is a halfspace
polyhedral? It doesn't even seem bounded. Also, I can't find support for
sweep or brep. I assume they aren't supported in my version. (Do we need
to tag new primitives with version numbers?) Also, a lot of your "hard
to categorize" things I just stuffed in an "other" category; although
the order I put them in still groups them about the same as you do, even
within the other group. --[ssd](../user/Ssd.md) 17:10, 31 December
2009 (EST)

How about a category for meshed primitives? This would include (please
correct me!) ars, bot, spline, nurbs, and maybe metaball?
--[ssd](../user/Ssd.md) 01:58, 1 January 2010 (EST)


The only truly meshed primitives are the BoT and NMG primitives. ARS is
presently implemented as a polygonal surface, but that is mostly an
implementation detail (it could just as easily be a NURBS surface).
Similarly, spline, nurbs, and metaballs aren't meshed. With the
exception of metaballs, all the rest have one trait in common in that
they are primitives with an explicit boundary representation. Metaballs
are an implicit boundary representation primitive.
--[Sean](../user/Sean.md) 14:20, 25 March 2010 (EDT)

Hello Sean. Glad I haven't upset anyone yet with my edits. I'm a bit OCD
about English grammar. Don't expect any amazing code or anything similar
from me; I'm an ex-mechanical engineer, and computer programming is
definitely not my forte. Nor am I mathematically gifted. But, BRL-CAD
seems to fit my needs for a combined Cad-Modeller-Renderer. Bit of a
steep learning curve, though...
