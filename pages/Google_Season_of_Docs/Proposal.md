# Migrate BRL-CAD's Documentation Infrastructure

Our organization focus for the 2021 Season of Docs entails migrating our
doc infrastructure from Docbook XML. Alternative
\[Google_Season_of_Docs/Project_Ideas\|project ideas\] may also be
considered, but please discuss it with our dev team. Please come [chat
with us](https://brlcad.zulipchat.com). You may also direct any
questions or comments to devs@brlcad.org

## About BRL-CAD

BRL-CAD is a powerful cross-platform solid modeling system for 3D
computer-aided design and graphic visualization. Currently standing at
more than a million lines of code and hundreds of staff-years
investment, BRL-CAD has nearly 40 years development history (since 1979)
and is in production use by more than 2000 organizations around the
world. BRL-CAD is represented, used, and developed by a collective of
industry, academia, and government participants from all over the world.

In all, BRL-CAD has *more than a **million** words* of documentation
across hundreds of manual pages, dozens of tutorials, hundreds of wiki
pages, dozens of technical papers, and other resources. There are
literally thousands of features created over decades of development.
BRL-CAD's set of current manuals, guides, tutorials, and other
documentation [are listed](../doc/Documentation.md) on our [website
wiki](../doc/Main_page.md) and included in our
[repository](https://github.com/BRL-CAD/brlcad/)\].

## About Our Doc Infrastructure

<table>
<thead>
<tr class="header">
<th></th>
<th style="text-align: center;"><p>Technologies</p></th>
<th style="text-align: center;"><p>Difficulty</p></th>
<th style="text-align: center;"><p>Contacts</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>BRL-CAD has extensive documentation infrastructure using Docbook XML whereby we "compile" them into HTML, PDF, and other formats. This approach helps ensure docs remain up-to-date, without syntax/structure errors, and allows the documentation to be composed and reused in different ways (e.g., an tutorial on some topic might get embedded as an appendix in one document or a chapter to another). That said, the underlying format is tedious to write and hard for contributors. We'd like to migrate to a newer system like <a href="https://antora.org">Antora</a> or <a href="https://docusaurus.io">Docusaurus</a> or <a href="https://www.mkdocs.org">MkDocs</a>, converting everything over while still retaining build system integration.</p>
<p>References:</p>
<ul>
<li>see doc/docbook in a source checkout</li>
<li><a href="http://brlcad.org/HACKING_BRL-CAD.pdf">http://brlcad.org/HACKING_BRL-CAD.pdf</a></li>
<li><a href="https://docbook.org">https://docbook.org</a></li>
<li><a href="https://antora.org">https://antora.org</a></li>
</ul></td>
<td style="text-align: center;"><p>Docbook XML, AsciiDoc, Markdown, Antora</p></td>
<td style="text-align: center;"><p>Medium</p></td>
<td style="text-align: center;"><p>morrison, rossberg, yapp, Sahib</p></td>
</tr>
</tbody>
</table>

# Scope of the Migration Project

This project attempts to modernize our infrastructure migrating existing
documentation from Docbook XML to AsciiDoc in Antora. For this project,
we anticipate and are planning to prefer Antora due to previous
evaluation, but are open to discussion and
\[Google_Season_of_Docs/Project_Ideas\|alternate project
proposals\]. Come talk with us interactively at
<https://brlcad.zulipchat.com>

## What is in scope?

The minimum scope of the project is migrating our existing Docbook XML
docs in our [repository](https://github.com/BRL-CAD/brlcad/). This
includes:

-   Successfully completing onboarding outlined in our contributor guide
-   Developing a migration plan for mapping Docbook XML structures to
    AsciiDoc
-   Setting up a preliminary custom output style for BRL-CAD in Antora
-   Mocking up a manual conversion of our About document
-   Representing translations in Antora for all docs already converted
    to other languages
-   Coordinating with others on partially automated conversion from
    Docbook to AsciiDoc
-   Coordinating with others on feedback and issues identified
-   Documenting the essential steps required to migrate a document
-   Setting up an instance of Antora on brlcad.org
-   Configuring Antora and/or Github for online editing by anonymous
    contributors
-   Working with dev team to establish required Github and/or CMake
    logic that deploys docs to Antora
-   Working with dev team to coordinate deployment of Antora to
    brlcad.org
-   Migrating all of our Docbook XML documents in doc/docbook to
    Asciidoc in a separate repository
-   Maintaining a public log of and writing up a summary of project
    outcome

## What is not in scope?

There are extensive docs not in Docbook XML format in our repository, on
the [website wiki](../doc/Main_page.md), [in other
formats](../doc/Documentation.md), and in other files that are
desirable and may also be migrated (e.g., for testing purposes), but
they are secondary priority and need not be considered in scope.

Also not in scope is technical administration, maintenance, and
installation of Antora itself on our production server. This will be
handled by the dev team. The technical writer will need to be capable of
setting up Antora locally for development and testing purposes.

The technical writer can expect responsive interaction (typically within
a few hours) from several mentors that will be on hand to provide
technical assistance, discussion, testing, and technical support.

We estimate that this project will take 3 months to complete. We have
three mentors willing to directly help with this effort and that have
committed to supporting the project.

# Measuring Project Success

As this project centers around migrating documentation, measuring
success is a simple function of percent documentation converted to
AsciiDoc and deployed to Antora. At present, there are 505 .xml
documents in doc/docbook of the repository that require conversion.

We would consider the project successful if at least 90% of the existing
Docbook files are fully converted to AsciiDoc, imported to Antora, and
deployed online.

We would also consider the project successful if, within a year, it
results in external pull requests to a migrated AsciiDoc documents and
renewed documentation.

# Project Budget

We we anticipate the project requiring 3-4 months of near full-time
effort. As such, our budget is set at $9060 total with $7560 (84%)
allocated to the technical writer and $1500 allocated to 3 community
volunteers ($500 each):

|                                                      Budget Item                                                       | Amount | Running Total |       Notes/Justification        |
|:----------------------------------------------------------------------------------------------------------------------:|:------:|:-------------:|:--------------------------------:|
| Technical writer doc infrastructure setup, demo, doc migration from Docbook, online editing, and continuous publishing | $7560  |     $7560     |                                  |
|                                                   Volunteer stipends                                                   |  $500  |     $9060     | 3 volunteer stipends x $500 each |
|                                                         TOTAL                                                          |        |   **$9060**   |                                  |

# Additional Information about BRL-CAD

## Previous experience with technical writers or documentation

BRL-CAD has an extensive development legacy that spans three decades.
[BRL-CAD's bibliography](https://brlcad.org/BRL-CAD_Bibliography.pdf)
speaks for itself as to the extensive nature of our community's
experience with documentation and technical writers. BRL-CAD maintains
hundreds of existing documents, tutorials, guides, quick references,
diagrams, presentations, books, and more that help teach fundamentals to
advanced CAD topics and everything in between.

For many years in the early 2000's, one of BRL-CAD's leading sponsors
employed a technical writer to work full time on BRL-CAD documentation.
This resulted in daily interaction over many years and gave our
community an appreciation for the value technical writers bring to the
table. Since that time, we have continued to engaged technical writers,
write technical documentation ourselves, consult with technical writers
on our docs, and engage documentation contributors.

## Previous participation in the Season of Docs, GSoC, GCI, Google DocCamp

BRL-CAD was fortunate to participate in the inaugural 2019 Season of
Docs. We had a wonderful experience working with Sahibpreet Kaur to
create a concise Intro to BRL-CAD. This document was instrumental in the
creation of updated modeler training that has been utilized in four
separate in-person and online training classes for BRL-CAD.

BRL-CAD also participated in the 2020 Season of Docs, however our tech
writer withdrew from the program after unsuccessful prioritization of
time and effort. Over many weeks, we tried various strategies to remedy
participation including discussions, probation, and consultation with
other orgs and GSoD staff, however the project was ultimately cancelled
once the participant withdrew.

Since 2012, BRL-CAD participated 6 times in Google Code-In (GCI). The
GCI program was an exceptionally good fit for our code and community,
and was generally revered as one of our favorite Open Source activities
to date until the program was discontinued in 2020. By rough estimation,
we engaged over 1000 students, acquired at least 5 core contributors
that remained involved with the project after 12 months, and received
contributions that equated to more than 10 staff years of full time
effort! We loved GCI and were sad to see it go.

In 2013, BRL-CAD was selected to participate in [Google Doc
Camp](../Google_Doc_Camp.md) where our team of developers and
technical writers wrote a Contributor's Guide. That guide continues to
be used today for onboarding of new contributors, showcasing features,
and showcasing the potential effectiveness of a development
offsite/retreat/camp.

Having participated nearly every year since 2008, BRL-CAD is one of the
oldest organizations in the Google Summer of Code. We have mentored
hundreds of students have had exceptional outcomes. GSoC revolutionized
our community practices, organized our outreach activities, helped
coordinate development prioritization, helped grow our open source
community, and have inspired development successes for more than a
decade.
