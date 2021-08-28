If you want to work on **computer-aided design (CAD), geometry, or
graphics** documentation, you've come to the right place! Please check
out our project ideas below. They are roughly in order or priority and
difficulty. Here are some links to help you get started with a proposal:

1.  [Get BRL-CAD source code](../doc/Compiling.md)
2.  [Read our existing docs](../doc/Documentation.md)
3.  [Get additional doc perspective](../doc/Main_page.md)
4.  [Read our contributor guide](http://brlcad.org/HACKING_BRL-CAD.pdf)

We will consider GSoD proposals for **all** skill levels ranging from
simple to crazy hard and everything in between. [Introduce yourself via
chat](https://brlcad.zulipchat.com) (preferred) or [via
e-mail](mailto:devs@brlcad.org), and we'll help you plan a project right
for you.

Remember that project descriptions are just *rough ideas*. You must
expand with [considerably more
detail](../Summer_of_Code/Application_Guidelines.md). Set goals
that fit your experience and interest.

# Migrate doc infrastructure

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
<td><p>BRL-CAD has extensive documentation infrastructure using Docbook XML whereby we "compile" them into HTML, PDF, and other formats. This approach helps ensure docs remain up-to-date, without syntax/structure errors, and allows the documentation to be composed and reused in different ways (e.g., an tutorial on some topic might get embedded as an appendix in one document or a chapter to another). That said, the underlying format is tedious to write and hard for contributors. We'd like to migrate to a newer system like <a href="https://antora.org">Antora</a> or <a href="https://docusaurus.io">Docusaurus</a> or <a href="https://www.mkdocs.org">MkDocs</a>, converting everything over while still retaining build system integration. References:</p>
<ul>
<li>see doc/docbook in a source checkout</li>
<li><a href="http://brlcad.org/HACKING_BRL-CAD.pdf">http://brlcad.org/HACKING_BRL-CAD.pdf</a></li>
<li><a href="https://docbook.org">https://docbook.org</a></li>
<li><a href="https://antora.org">https://antora.org</a></li>
</ul></td>
<td style="text-align: center;"><p>Docbook XML, AsciiDoc, Markdown, Antora</p></td>
<td style="text-align: center;"><p>Medium</p></td>
<td style="text-align: center;"><p>morrison, rossberg, yapp</p></td>
</tr>
</tbody>
</table>

# Organize all existing user docs

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
<td><p>Tame the beast. BRL-CAD has more than a million words of documentation spread across hundreds of documents. Some are huge, some are small. There are books, articles, presentations, manual pages, diagrams, reference cards, and more in a variety of formats and locations. The goal of this task to to conduct a complete audit of all existing documentation, catalog them, make recommendations and/or facilitate with merging overlapping documentation, and present all available documentation in a new web index. References:</p>
<ul>
<li>see doc/ hierarchy in a Subversion checkout</li>
<li><a href="http://brlcad.org/wiki/Documentation">http://brlcad.org/wiki/Documentation</a></li>
<li><a href="http://brlcad.org/wiki/Main_Page">http://brlcad.org/wiki/Main_Page</a></li>
<li><a href="http://brlcad.org/HACKING_BRL-CAD.pdf">http://brlcad.org/HACKING_BRL-CAD.pdf</a></li>
</ul></td>
<td style="text-align: center;"><p>Mediawiki, Docbook XML, Subversion</p></td>
<td style="text-align: center;"><p>Easy</p></td>
<td style="text-align: center;"><p>yapp, morrison, rossberg</p></td>
</tr>
</tbody>
</table>

# Write a "BRL-CAD Primitives" manual

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
<td><p>BRL-CAD has approximately 2 dozen primitives. New users learning how to model with BRL-CAD for the first time end up utilizing an appendix in our existing MGED Tutorial Series, which is a brief guide to some of the supported primitives. For this project, we'd like all primitives to be documented with rendered visuals where appropriate, explanation of all parameters, and depiction of the variety possible with each primitive. References:</p>
<ul>
<li>see src/librt/primitives in a source checkout</li>
<li><a href="http://brlcad.org/gallery/picture.php?/5/category/1">http://brlcad.org/gallery/picture.php?/5/category/1</a></li>
<li><a href="https://brlcad.org/w/images/c/cf/Introduction_to_MGED.pdf">https://brlcad.org/w/images/c/cf/Introduction_to_MGED.pdf</a></li>
<li><a href="http://brlcad.org/tmp/primitives/">http://brlcad.org/tmp/primitives/</a></li>
</ul></td>
<td style="text-align: center;"><p>Docbook XML, Subversion, basic reading of C/C++</p></td>
<td style="text-align: center;"><p>Hard</p></td>
<td style="text-align: center;"><p>morrison, rossberg</p></td>
</tr>
</tbody>
</table>

# Organize and publish developer docs

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
<td><p>BRL-CAD uses <a href="http://www.doxygen.nl">Doxygen</a> for API documentation. It's a simple way for developers to document API by merely adding /** comments like this */ to their code, typically before a function. The primary goal of this project is to make sure all of the public API has a Doxygen comment, has parameters tagged appropriately, grouped accordingly, and that all groupings are documented as well. The secondary goal is to then publish the output from Doxygen to our website in HTML and PDF forms so that reference documentation is available to everyone. References:</p>
<ul>
<li>see misc/doxygen in a source checkout</li>
<li><a href="http://brlcad.org/HACKING_BRL-CAD.pdf">http://brlcad.org/HACKING_BRL-CAD.pdf</a></li>
<li><a href="http://www.doxygen.nl">http://www.doxygen.nl</a></li>
</ul></td>
<td style="text-align: center;"><p>Doxygen, Subversion, C/C++ code comments</p></td>
<td style="text-align: center;"><p>Medium</p></td>
<td style="text-align: center;"><p>yapp, morrison, rossberg</p></td>
</tr>
</tbody>
</table>

# Convert unmanaged to managed

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
<td><p>BRL-CAD has several books, presentations, and other documentation written in familiar publishing tools like Microsoft Word, Microsoft Powerpoint, Adobe InDesign, LaTeX, Apple Pages, and more. They are "unmanaged" in the sense that they are not easily kept in sync, unlike the majority of BRL-CAD's docs that are compiled alongside code and easily updated with a text editor (i.e., "managed"). The main reason they are unmanaged is because they have specific layout and formatting. For this project, the goal is to figure out how to manage them so that they're in an editable markup format like AsciiDoc **and** any custom formatting is preserved (e.g., through the use of stylesheets). References:</p>
<ul>
<li><a href="https://github.com/Ardemius/asciidoctor-presentation">https://github.com/Ardemius/asciidoctor-presentation</a></li>
<li><a href="https://asciidoctor.org/docs/asciidoctor-revealjs/#convert-asciidoc-into-slides">https://asciidoctor.org/docs/asciidoctor-revealjs/#convert-asciidoc-into-slides</a></li>
<li><a href="http://rhythmus.be/md2indd/">http://rhythmus.be/md2indd/</a></li>
<li><a href="https://pandoc.org">https://pandoc.org</a></li>
</ul></td>
<td style="text-align: center;"><p>AsciiDoc, Pandoc, Markdown, Docbook XML</p></td>
<td style="text-align: center;"><p>Hard</p></td>
<td style="text-align: center;"><p>yapp, morrison, rossberg</p></td>
</tr>
</tbody>
</table>
