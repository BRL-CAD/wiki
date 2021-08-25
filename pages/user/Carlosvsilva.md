My name is Carlos Silva, and I'm from Portugal.

I would be delighted to improve BRL-CAD project under Google Summer of
Code 2009 program, so I submitted the following application to improve
the IGES converter importer/exporter.

I am getting familiarized with the source code and IGES documentation,
and i made my first patch:

-   <https://sourceforge.net/tracker/?func=detail&aid=2765379&group_id=105292&atid=640804>

## Project Proposal

### Project Title

IGES importer/exporter enhancements

### Project Goals

The main goal is to update the IGES converter importer/exporter to
version 5.3 (6.0 in the future) of the IGES standard, and producing
quality code ready to be included in svn mainline brlcad.

### Project Benefits

BRL-CAD project will support the latest 5.3 version (and later support
version 6.0) of the industry wide prevalent IGES standard to exchange
geometry data between CAD systems. The converter will be re-designed to
support multiple file formats when importing/exporting for full
compatibility with all existing projects and systems. The code produced
will be clean, stable, portable and maintainable, which will be of
utmost importance in a project as complex as BRL-CAD. BRL-CAD project
will be one of the best alternatives for workflows involving the 5.3
version of the IGES format and above.

### Project Tasks and Deliverables

I started the work on my BRL-CAD application based on the list of
changes for version 5.3 of the IGES standard. Since the current
converter in BRL-CAD is at version 5.1 level support, i will first need
to add the features/behaviour of the 5.2 version of the standard.

So, I propose the following precise schedule:

#### Phase 1 (April 21 - April 30)

Test the code for feature support and correct operation converting
to/from the 5.1 version of the standard, with different 5.1 version IGES
files covering the features detailed here:

<http://www.iges5x.org/archives/eco/eco-51.htm>

I already went through most resources, and there don't seem to be any
outstanding issues or problems with 5.1 version support.

#### Phase 2 (May 1 - May 15)

Continue getting myself up to speed with the brlcad/src/conv/iges source
code structure with the help of cscope, which I already started to do.
Continue researching BRL-CAD’s primitives and entities to understand the
mappings between IGES and BRL-CAD formats. Most of the mappings seem
direct so far.

#### Phase 3 (May 16 - May 31)

If there are any issues with version 5.1 support, fix them, debating any
bigger issue with the BRL-CAD dev team if needed.

Implement a command-line parameter to specify the version of the IGES
standard to import or export. Redesign the converter to use the code
specific for each version of the standard, in places where they differ.
Be careful to avoid duplication of code.

#### Phase 4 (June 1 - June 30)

Start implementing and testing for conformance the changes listed for
the 5.2 version of the standard, here:

<http://www.iges5x.org/archives/eco/eco-52.htm>

Some of the these changes are refinements of the wording of previous
versions of the standard. The changes that require code or behaviour to
be changed, will be implemented and then tested with hand-created IGES
5.2 files and with example files and other resources available from
www.iges5x.org.

The new attributes/entities (like Minimum Design Wall Thickness
attribute) will be matched with BRL-CAD's existing ones. If necessary,
new ones will be created for BRL-CAD, debating with the dev team on the
best path to take to develop them.

#### Phase 5 (July 1 - August 10)

With the official document of the IGES 5.3 standard, and its list list
of changes, begin to implement any new code behaviour required like the
"Change to Flow Associativity Entity", or implement new code to convert
new features of the 5.3 standard, like 'Add Attributes for Geometry of
Cataloged Parts".

Research BRL-CAD's support of Unbounded Lines in the Line entity, and if
there's no support, implement it, and then implement the code to convert
this feature.

Also implement the BREP Objects as CSG Primitives in the places
mentioned by the standard.

Consult with the BRL-CAD dev team for best practices in improving the
converter architecture and for information on this
standard/implementation, valuable for this project. By July 6, date of
mid-term student evaluations, work should have been started on this
phase, and preferably, at least half of the changes list should already
be implemented in BRL-CAD's IGES converter. By the end of this phase,
version 5.3 support will be complete, tested and documented.

#### Phase 6 (August 11 - August 17)

Test all the code produced and write the necessary documentation.

If time allows, implement the features of IGES 6.0 version of the
standard listed in <http://www.iges5x.org/archives/eco/eco-60.htm>

I'm happy i will be working directly on the trunk, without any
sub-branches involved, so I can get instant feedback on my work and
contribute faster, with higher quality code.

I have a lot of enthusiasm to contribute to the BRL-CAD project, and I
will implement this project teaming with my mentor and the BRL-CAD
developers to reach the best design decisions and create clean, stable,
portable and maintainable, release-quality code.

I will take advantage of the extensive C experience I got while
successfully working on the MSN protocol plugin in libpurple - it's part
of Pidgin \[1\] - under Summer of Code 2007 \[2\], and from other other
personal projects. I updated the C-based MSN protocol plugin
successfully to the latest version, reverse-engineering Microsoft's
official client encrypted network communications and reading unofficial
documentation of this closed protocol, that I found on-line. I had to
improve another student’s previous SoC work with hard to maintain code
to successfully complete this project. In 2008 i applied with Pidgin
again, because of the familiarity with the source code, and due to the
involvement with the project, i know which areas libpurple could benefit
the most from improvements. Even though my application was considered
solid by the team, i found out at the last minute that they have a
policy of not taking repeat students, in the spirit of GSoC. So i also
applied for FreeBSD's mtund, with a really short time-frame as best as i
could, but between the time available to the proposal, and FreeBSD not
being interested in all the projects of their ideas list, i wasn't
selected.

I believe i can accomplish this project for BRL-CAD successfully, and
bring in tested, release-quality code. I have no classes this semester,
only short papers without a deadline, and will be available and comitted
full time as soon as I'm accepted into the program. I will have a lot of
free time to work so I’m enthusiastic about it. After completing my
project I hope to continue contributing code and bug-fixes to BRL-CAD
project.

Hopefully I will grow as a software engineer, and gain real-word
experience with CAD systems design and interoperability.

### Personal Bio

I am a 25 year old student from the small town of Maia which is located
in the north of Portugal. I moved to the city of Braga to study
Informatics Engineering (CS) at one of the best universities in
Portugal, Universidade do Minho, and I’m a software engineer by heart.
I’ve been involved with the free software community since I started
using RedHat Linux 6 and I was involved in informal communities in
Portugal. I gave a lecture in high-school on how to install RedHat Linux
and have been to some IT conferences. In the past I used regularly BSD
based systems, Linux systems, Mac OS X and others. I've used countless
free software projects, in server and desktop, contributing code, bug
reports, and I'm happy to be part of this community.

I appreciate the feedback, and if there's anything else you want to
comment on, i'll be more than happy to hear about it ! Snippets of code
from my previous work in Google Summer of Code 2007 are available at

-   <http://planet.homeunix.org>

I will be available on IRC at Freenode network, with the nickname
**typ0**.

### References:

\[1\] Pidgin Instant Messenger and libpurple, <http://pidgin.im/>

\[2\] Abstract of Google Summer of Code 2007 successful Pidgin
application,
<http://code.google.com/soc/2007/gaim/appinfo.html?csaid=C682D350CA504A3C>