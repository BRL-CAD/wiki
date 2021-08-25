<center>
<h1>

\#1. WORDPRESS PLUGIN (IMPORT ALL XML/CSV)

</h1>
</center>

Import All is plugin for using to import the XML/CSV content into
wordpress as wordpress page or post. This plugin is open source and free
to use. The pros and cons of this plugin are as follows.

<h3>

Pros

</h3>

1.  Freely available but not full package if need to use cron job
    feature then you need to buy full package.
2.  Easy to install.
3.  Works with xml files.
4.  Shows the content of xml file as wordpress page or post.
5.  Shows the content of xml file into HTML.
6.  Plugin divides the all content of file into chunks according tags.
7.  Plugin works on drag and drop method which information you need then
    you just drag and drop into editor and save.
8.  This also uses the cron job.

<h3>

Cons

</h3>

1.  GUI of this plugin is not good.
2.  This plugin cannot import the all content of xml file into wordpress
    we need to drag and drop the content.
3.  This plugin does not work with Docbook tags.
4.  The representation of content is not good.
5.  No validation rules for xml content.
6.  This Plugin not markup the changes into xml file they just import
    the content into wordpress when user does any change in content
    those are not applied on imported file.
7.  This plugin works on more manual work for importing the content of
    xml file.
8.  This plugin does not support the our document structure because when
    I uploaded the content then the more of information is not imported
    into wordpress. I only able to import small part of information .
    only information which is contained in child tags.
9.  Cron job feature is not supported in free version.

<h4>

Rating: 2/5

</h4>
<center>
<h1>

\#2) MediaWiki (XML2WIKI)

</h1>
</center>
<h3>

Pros

</h3>

1.  This is very simple script which are using to convert the docbook
    tags into wiki format.
2.  This script is open source
3.  This script easily converts the xml tags into .txt file which stores
    all code for wiki.

<h3>

Cons

</h3>

1.  Does not fully support all docbook tags.

<h4>

Rating: 2/5

</h4>
<center>
<h1>

\#3) WORDPRESS (IMPORT HTML)

</h1>
</center>
<h3>

Pros

</h3>

1.  Very easy to use
2.  Easy to install
3.  open source
4.  Representation is very good
5.  Managing the docs is very good
6.  Search is good
7.  Conversion all html docs into wordpress post or pages
8.  Easy to import docs into wordpress post or pages

<h3>

Cons

</h3>

1.  Not using cron job to update regularly all docs
2.  Some time they make duplication of document.

<!-- -->

<h4>

Rating: 3.5/5

</h4>
<center>
<h1>

\#4) Mediawiki (OWN EXTENSION)

</h1>
</center>
<h3>

Pros

</h3>

1.  Representation is well according to mediawiki theme.
2.  Searching is dedicated to all docs(brlcad document) but not work
    with mediawiki pages.
3.  Editing is also performed under the mediawiki special pages using
    own editor.
4.  Import the document is under special page and show also under
    special page.
5.  Cron job work for commit the changes using shell script.
6.  Editing based on docbook xml language.
7.  Provides the authentication on xml content (editing time
    authentication like:- unclosing tags).
8.  Completes A-F options.

<h3>

`Cons`

</h3>

1.  Search works for BRL-CAD document under special pages.
2.  URL is large including special pages url (I think this can be sorted
    out).

<h4>

Rating. 4.5/5

</h4>
<center>
<h1>

\#5) Wordpress (OWN PLUGIN+HTML IMPORTER)

</h1>
</center>
<h3>

Pros

</h3>

1.  Easy to import all documents.
2.  Representation is good.
3.  Editing in the docbook format
4.  Corns job for commit and updating document time to time using shell
    script.
5.  Completes A-F in well manner
6.  Represents the document in Pages or post under wordpress
7.  User Authentication also works for user.

<h4>

Rating: 4.5/5

</h4>
<center>
<h1>

\#6) Other Tools(PANDOC)

</h1>
</center>
<h3>

Pros

</h3>

1.  Converts the document into any format
    like(HTML-&gt;DOCBOOK,DOCBOOK-&gt;HTML)

<h3>

Cons

</h3>

1.  Some html tags not converted properly
2.  Internal links not properly not converted
3.  BRL-CAD structure is not properly converted
4.  Lots of documents content is changed like(tags of document HTML to
    docbook)
5.  Book document in html converted into article not in book
6.  BRL-CAD validation system does not validate the output of converted
    document.
7.  Need own script which provide the some rules and validation on
    converted document.

<h4>

Rating: 2.5/5

</h4>
<center>
<h1>

\#7) XMLLINT

</h1>
</center>
<h3>

pros

</h3>

Using to validate the document.

<h2>

Rating:-5/5

</h2>
<center>
<h1>

\#8)TINYMCE

</h1>
</center>
<h3>

pros

</h3>

1.  Open Source
2.  Compatible with html and xml
3.  Provide the GUI Mode and Source code mode
4.  If user make any mistake and xmllint gave the error then user use
    the source code mode and edit the code and remove the error form xml
    code

<center>
<h1>

FINAL RESULT ACCORDING TO ME

</h1>
</center>

Now I am considering some pros and cons of all options. So now i am
going to evaluate the all options according to all A-F options.

<h2>

How source files in repo are handled:-

</h2>
<h4>

Options:-

</h4>
<center>
<h3>

\#1(wordpress import all)

</h3>
</center>

This option does not work with original repo; after importing the
content moves to database.

<center>
<h3>

\#2(html2wiki)

</h3>
</center>

Does not work with repo.

<center>
<h3>

\#3(html import)

</h3>
</center>

Works with repo but only imports the content into wordpress and save
into database. Any updates not applied on repo document.

<center>
<h3>

\#4(own mediawiki extension)

</h3>
</center>

Work with repo, document content show as special page in mediawiki. Show
the all category repo name-wise.

<center>
<h3>

\#5(own wordpress plugin+html import)

</h3>
</center>

Work with repo, Import the content into wordpress using HTML 2 import
plugin. After changes do by any user and accept by admin then content
updated in repo as well as website using own plugin.

<center>
<h3>

\#6(pandoc)

</h3>
</center>

`Pandoc does not work with repo.`

<h2>

How content is uploaded to the website? How content is presented to a
website visitor?

</h2>
<h4>

Options:-

</h4>
<center>
<h3>

1.  1(import all)
    </h3>

</center>

This option waits for manually uploading all the xml pages into
wordpress.

<center>
<h3>

\#2(html2wiki)

</h3>
</center>

This option does not work with that, that only work to convert the html
to wiki syntax.

<center>
<h3>

\#3(html import)

</h3>
</center>

This option supports this work it directly imports the all content into
wordpress and convert into wordpress page or posts.

<center>
<h3>

\#4(own mediawiki extension)

</h3>
</center>

This option also support this. Import all document into mediawiki and
show as mediawiki special pages.

<center>
<h3>

\#5(own wordpress plugin+html import)

</h3>
</center>

This option also supports this. directly imports the content as pages.

<center>
<h3>

\#6(pandoc)

</h3>
</center>

This not support this option.

<h2>

How a website visitor edits that content?

</h2>
<h4>

Options:-

</h4>
<center>
<h3>

\#1(import all)

</h3>
</center>

This supports editing in html format but does not convert into docbook.

<center>
<h3>

\#2(html2wiki)

</h3>
</center>

This provide the editing under mediawiki in html format then through
this script convert this content into wiki content but does not follow
the all tags of docbook.

<center>
<h3>

\#3(html import)

</h3>
</center>

This option provides the help to edit the content of uploaded content
into html format and changes only applied on wordpress not on original
document

<center>
<h3>

\#4(own mediawiki extension)

</h3>
</center>

This option also helping to edit the document. If user want to edit the
document then original document is open in editing mode in docbook xml
format. And user made the changes then commit are gone on main repo
after reviewing the commit and accepting this commit than changes
applied on main document as well as on website content.

<center>
<h3>

\#5(own plugin + html import)

</h3>
</center>

This option also helping to edit the document. If user want to edit the
document then original document is open in editing mode in docbook xml
format. And user made the changes then commit are gone on main repo
after reviewing the commit and accepting this commit then changes
applied on main document as well as on website content.

<center>
<h3>

\#6(pandoc)

</h3>
</center>

Convert the document into html format and make the changes then convert
into docbook format. BRL-CAD system not support the output of pandoc
converted document so be need to use own script with pandoc.

<h2>

How edited content gets staged for review? How edited content is
reviewed?

</h2>
<h4>

Options:-

</h4>
<center>
<h3>

\#1(import all)

</h3>
</center>

Not support this function(docbook files of BRL-CAD). But you can review
only html changes.

<center>
<h3>

\#2(html2wiki)

</h3>
</center>

Not support this function(docbook files of BRL-CAD). But you can review
as wiki content.

<center>
<h3>

\#3(html import)

</h3>
</center>

Not support this function(docbook files of BRL-CAD). But can review only
html changes.

<center>
<h3>

\#4(own mediawiki extension)

</h3>
</center>

Using online editor for editing the xml file content. Using commit or
patch system. automatic check the changes using xmllint online, if error
found then commit not gone else commit gone. creating Shell script.

<center>
<h3>

\#5(own wordpress plugin + html import)

</h3>
</center>

Using online editor for editing the xml file content. Using commit or
patch system. automatic check the changes using xmllint online, if error
found then commit not gone else commit gone. creating Shell script.

<center>
<h3>

\#6(pandoc)

</h3>
</center>

Need Manually review all changes.