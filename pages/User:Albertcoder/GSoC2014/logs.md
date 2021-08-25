# Development Logs

## Community Bonding Period

-   Couldn't do much GSoC-oriented in this period owing to the clash of
    my end-semester exams with this period, still I tried to study those
    subjects with uttermost care whose concepts could be used in my GSoC
    project like Relational Database Management Systems, Web
    Technologies(including PHP, JavaScript, XML and so on), Software
    Engineering etc. during this period. I am sure I utilised this
    period doing so.

## Development Period

### Week 1

'''''21st May(Wednesday)

Installed MediaWiki. Faced some problems doing that, encountered a few
warnings, removed them.

Studied about MediaWiki extensions. Failed to make a simple extension
due to some problem in the tutorial. Still studying about
extension-making.

'''''22nd May(Thursday)

Followed the extension-tutorial at mediawiki.org for other sample
extensions. Extension making process still in progress.

Installed a couple of extensions and tested them on my system like
"Awesome" extension and "CategoryGallery" extension.

'''''23rd May(Friday)

Being mainly a C/C++ developer, had to explore some concepts of PHP. So
studied some PHP tutorials in detail.

Also studied/studying HTML forms in MediaWiki which are used in
extension-making.

'''''24th May(Saturday)

Writing my log just a couple of minutes past 12:00 AM. Apologies for not
been able to write right in time.

Today I made a form which can take input from the user using the special
page functionality.

Also studied the present database in detail and will ask about some
queries on the IRC.

'''''25th May(Sunday)

The form which I created yesterday, needed validations but I struggled
to accomplish it. Hope I will get over it by tomorrow.

Studied about Data Entry and connecting/storing that data into the
database.

### Week 2

'''''26th May(Monday)

Tried to apply validations but still not done with that.

Read previous logs and mails which I couldn't read due to my final
exams.

'''''27th May(Tuesday)

Browsed various Materials Database websites, observed how these stored
data, in which format. Also observed various features like advanced
search, import/export and sorting.

'''''28th(Wednesday) and 29th May(Thursday)

Had issues with my health. :(

'''''30 May(Friday)

Talked on \#mediawiki IRC about the version of mediawiki to be used.
Although had a fruitful discussion yet, got puzzled. So talked on
\#brlcad IRC and finally got the solution(maths22 would update the older
version of BRL-CAD wiki).

Installed mediawiki 1.22.7 and started working on it.

'''''31 May(Saturday) and 1st June(Sunday)

As per my milestone sign in/sign up process is also done as my extension
will use the login-module of BRLCAD-wiki.

Making my previous extension work in latest version 1.22.7. Not working.
:(

Studied BRL-CAD supports which formats for import/export.

Tested a model by applying material on it in BRL-CAD and trying to
understand the STEP format.

'''''2 June(Monday)

I have made a simple extension which will work in BRL-CAD 1.22.7. I will
upload it on my college server tomorrow. I have some parts missing, I
will complete it by tomorrow.

Followed some mediawiki tutorials which would help in database insertion
through form. I will display this all tomorrow.

### Week 3

'''''3rd June(Tuesday)

I have submitted my first simple extension on the mailing list. I have
understood the basic structure of mediawiki extension. I am just too
close to end up making an extension which can take the data from the
user and store in the database.

'''''4th June(Wednesday)

Today I felt I needed a break from mediawiki stuff as my brain felt
suffocated so I did a lot of analysis of various CAD softwares. Created
various figures in BRL-CAD, FreeCAD, OpenSCAD and LibreCAD using
difference, union and intersection functions.

Applied materials to BRL-CAD model. Learnt how to use various commands
in like rt. Also had a glimpse of LUA script. And now I have resumed
learning advanced object oriented PHP for mediawiki.

'''''5th June(Thursday)

Made an HTML form which can take the inputs from the users. I am also
almost done with the database connectivity work. In no time I will show
the status on the mailing list.

Also went through the advanced concepts of object oriented PHP. Like how
mediawiki works with classes and objects and arrays inside arrays inside
arrays. I am having a bit of problem here but will overcome this soon.

'''''6th June(Friday) and 7th June(Saturday)

Successfully made the extension which can store the materials and their
properties in the database. Had some problems in displaying the data and
implementing search feature. It will be done too.

Uploaded on the mailing list.

'''''8th June(Sunday)

Today I went on exploring the structure and working of a bit
sophisticated mediawiki extensions. Got some valuable
responses/suggestions on my extension in the mailing list from my
mentor.

Showed the data stored by making a mysql user and letting everyone view
his stored data by logging in phpmyadmin using that user.

Did critical study of the current database for further improvements. IP
address of the user who edited some data may be recorded.

'''''9th June(Monday)

Implemented the feature with the help of which a user can see the
properties that are stored.

Implemented the search feature(search material by name).

Pushed all my work to my github account.

### Week 4

'''''10th June(Tuesday)

Today I studied about how to embed the code of separate php
app(basically database of previous years' work) into the extension that
I have made. It is not possible directly so I was stuck.

I asked for the solution / guidance for this on \#mediawiki IRC which is
pending. Also I have asked a doubt about the database in the brlcad
mailing list.

'''''11th June(Wednesday)

Today I tried to embed the code of previous years' work into my
extension. Well, I was unsuccessful in doing. I got some help on the
\#mediawiki but that was not specific. Got to learn many a new thing in
the present database after critical study.

Installed a couple of more similar extensions to do reverse engineering
and learn more.

'''''12th June(Thursday)

Although I might have done quite with the extension and GUI part, the
database still posed me some problems. Like I was stuck at what is the
difference between materialID and table_materialID in table "traits".
Also I feel there is not much normalization which lead me think again on
the database design.

Studied various resources similar to Materials Database like matweb.com,
matdat.com and so on. Got to know various features of the website and
the how of categorization of materials.

Also exported file in JSON, CSV etc. formats from current database using
phpmyadmin and used it in CAD softwares.

'''''13th June(Friday)

I had a few problems with the current database so I eliminated those
problems by making some enhancements in it. It was not connected using
primary and foreign keys. Also I have created a few more tables which
are needed.

Also I have classified the materials and their properties in the
database itself.

Also made a note of a few more features like units converter etc. in the
GUI.

'''''14th June(Saturday)

Connected the database-tables with primary and foreign keys. But still
encountering a problem. There are separate tables for each trait so JOIN
has to be applied accross each table. So if we need to see 20 traits of
a material, 20 JOINS. Trying to get over this problem.

Explored the deep use of SQL IN operator, JOINS, loop programming.
Talked with Yaron on \#mediawiki and got to learn how a query can be
inserted in mediawiki.

'''''16th June(Monday)

Tried to implement the MediaWiki extension as such with the current
database but had some problems with some attributes. Proposed some
modifications in the database which would help in better filtering and
searching. Mockup of the database mailed to the mailing list with some
modifications.

### Week 5

'''''17th June(Tuesday)

Had a very long and hard chat on \#mediawiki IRC. They suggested to use
SemanticMediaWiki for the data storage through forms.

Installed SemanticMediaWiki and Created a simple template for storing
data.

'''''18th June(Wednesday)

Made some templates
<http://202.164.53.122/~albertcoder/mediawiki-1.22.6/index.php/Template:Material>
and studied SMW(semantic mediawiki) stuff.

Studied database in MediaWiki. Had problems regarding applying JOINS
across more than two tables and getting their value on the page.
Resolved to some extent.

'''''19th June(Thursday)

Resolved the problem of applying the JOINS in MediaWiki on tables and
display the fetched data too in tabular form.

Created an extension to test the working,
<http://202.164.53.122/~albertcoder/mediawiki-1.22.6/index.php/Special:Joins>
.

Committed all my pending work on github.

'''''20th June(Friday)

Made the extension work with the enhanced database design. Had several
problems in inserting the data into the database because of separate
table for each trait but encountered them.

Added support to add new material and properties in new database.

Got some quick suggestions from \#mediawiki IRC during hurdles like
getting userID of currently logged in user.

'''''21st June(Saturday)

Brought about a number of changes in the working of the extension.
Removed check-boxes to select traits to maintain user-ease, used radio
buttons, drop-down and required features of HTML.

Pushed my latest extension(with proper database) into my github account.

'''''22nd June(Sunday)

Made certain enhancements like user cannot add a material again which is
already there in the database, dropdown for Material Privacy set as
public by default.

Accomplished the task of showing the values of all the traits for all
materials by applying joins on multiple tables and using for loops. The
code works fine in another extension right now.

Code updated and pushed to github.

'''''23rd June(Monday)

Accomplished the task of showing material names and values of traits in
the same extension. Added the feature such that no material can be added
again and again in the database.

Added units' table in the database to make it easy for the user to enter
the values of traits only in float rather than entering units alongwith.

### Week 6

'''''24th June(Tuesday)

Displayed all the required columns like material name, value and
timestamp but felt stuck at one point. Made two separate extensions, one
for adding material properties and other for viewing those properties.
Tried to ask for the solution on IRC \#mediawiki to merge these two
extensions but still to get response after they asked for the my code.

'''''25th June(Wednesday)

Got the solution to merge any number of extensions through URLs. Talked
about this on MediaWiki mailing list. They suggested using Semantic
MediaWiki. Explored the MediaWiki administration.

'''''26th June(Thursday)

Finally found the way to load any number of classes into the .php file
and also creating any number of special pages.

After a good discussion on \#mediawiki IRC, got the equivalent of using
hooks to create table in database.

Committed all my work to github and deployed the latest code on my
college server too.

'''''27th June(Friday)

User made eligible to add trait only after logging in.

Each time a user adds a new trait, a new table is created at the
back-end for that trait.

The variable in for loop which showed all the properties of materials
changed from static to dynamic.

Added hyperlinks to navigate from one page to another.

Updated the blogpost in the BRL-CAD mailing list:

<http://coderalbert.wordpress.com/2014/06/26/mediawiki-extension/>

'''''28th June(Saturday)

I was out on pilgrimage to [Golden
Temple](http://en.wikipedia.org/wiki/Harmandir_Sahib) . I will
compensate all my work by working on Sunday.

'''''29th June(Sunday) and 30th June(Monday)

Did some progress in advanced search of material by name.

Tried to link the whole database using foreign key references but there
exists some problem in the innoDB database style.

Explored the libraries used for import/export.

Wrote a few lines of code for adding new material type etc. by making
new classes in the main file.

### Week 7

'''''1st July(Tuesday)

Applied validations in the forms wherever necessary.

Combated with the problem of applying foreign keys using innoDB storage
engine.

'''''2nd July(Wednesday)

Studied the formatting of wiki page at user level including how to make
hyperlinks and headings, bold etc.

Studied/studying this handbook <http://goo.gl/iMsx4R> of MediaWiki
Administrators Handbook.

'''''3rd July(Thursday)

Added constraints for all the trait-tables using foreign keys.

Stuck at the problem of making this process automated like when a user
adds a new trait i.e. new table, it should automatically get linked
using foreign keys.

'''''4th July(Friday)

Struggled a lot to add foreign key constraint in dynamically created
tables in extension in an automated way. Talking on the \#mysql IRC I
got this ANSWER "forget about adding those automatically." They
seriously questioned the credibility of database design. Totally
refreshed all my concepts with respect to real world projects,
requirements and performance. (Need to head towards a wayout soon)

Learnt to add menus through MediaWiki:Sidebar and also went through the
various namespaces in MediaWiki.

'''''5th July(Saturday)

Finally added foreign key constraints in dynamically created tables
despite the words of \#mediawiki developers, "forget about adding those
automatically.". They might have said this in some other sense but
finally I got what I needed. :-)

Resolved the problem of data inconsistency occurring due to
miss-matching ids of values across all tables.

'''''6th July(Sunday)

Added search facility such that user can search material and its
properties by name.

'''''7th July(Monday)

Installed and learnt how to use the extension AdminLinks.

Traversed the whole code for following the coding standards.

### Week 8

'''''8th July(Tuesday)

Added foreign key constraints to all the tables that were pending.

Added one more table \`trait_units\` to specify the units of each
trait.

Adding this extra table kind of disturbed the work flow because now a
new trait cannot be added without its units. For this I have to now add
a separate text field/dropdown which will ask for the units of the trait
and also change the INSERT and SELECT queries at the backend but doing
this, encountered a few problems.

'''''9th July(Wednesday)

Finally resolved all the errors that occurred due to the addition of new
table \`trait_units\`.

Added dropdown for Units when adding a new trait. Amended all the
queries in the backend for proper insertion of data.

Updated _SERVER variable wherever it was necessary.

'''''10th July(Thursday)

Added ON CASCADE DELETE. Whenever any value is deleted from master
table, correspponding values in foreign keyed tables are also deleted.

Added userID to trait_table too, so that it can be tracked who added
that particular trait.

'''''11th July(Friday)

Added a new Special page in the extension wherefrom a user can delete a
trait. Only the traits added by a particular user can be deleted by
him/her.

'''''12th July(Saturday)

Added a new Special Page in the extension wherefrom a user can delete a
material from his added list of materials.

Added another Special page which has links to all the call to action
buttons like add material, delete trait etc.

'''''14th July(Monday)

Added Special Page for view all materials.

Tried to implement search by trait, almost done.

Tested the extension by installing on various other systems locally and
remotely.

### Week 9

'''''15th July(Tuesday)

Studied about the import/export libraries to be used for the extension.

Search by trait implemented. Now a user can either search for values of
traits either by material name or by trait name.

'''''16th July(Wednesday)

Explored MediaWiki **Editing rules, editing conventions, and
formatting**. Were very extensive topics, took more time than expected.

Tried to manipulate MediaWiki as a normal user rather than an
administrator with the help of the following and many more links:

<http://www.mediawiki.org/wiki/Help:Formatting>

<http://www.mediawiki.org/wiki/Help:Links> .

Also studied how to format **lists, images, tables etc.** on wiki pages.

'''''17th July(Thursday)

Made a separate **Special Pages** for search TRAIT by name and search
MATERIAL by name.

Used functions like **ucwords(), header() and str_ireplace()** to make
improvements like automating Initials of words in capital letters, page
refreshing, replacing '_' in names with space for displaying(like
boiling_point).

Stuck at **passing an array** of table-names in MW-Joins query in place
of a single table name to do selective search.

'''''18th July(Friday)

Added **menu bars** on the top to **navigate** through the extension.
Replaced old ugly links' Special Page with the new menu bar.

Added almost all the **units** of main traits(30 at present, will be
more) in the **drop-down** menu to prevent users from inputting wrong
values of traits.

'''''19th July(Saturday)

Whole day struggled with user rights management in MW. There was a good
user-manual to explain how permissions can be given to various groups
but it did not have anything to say about reverse i.e. having to give
permissions to multiple groups for accessing a single Special Page.

Asked on IRC about the solution they suggested two ways either to create
a new right which can be granted to multiple groups or give the right as
a second argument while calling the parent constructor in Special Page
class.

Improved the menu bar on the top of each Special Page. Thinking to add
images/icons in sometime after achieving all the basic functionality.

'''''21st July(Monday)

Applied **validations** across all the text-fields mainly of traits,
like only **decimal/integer** values can be added for traits like
boiling point etc.

**Cleaned** the code edited a few things like repositioning the forms at
proper place in the code to make it more readable.

### Week 10

'''''22nd July(Tuesday)

Data **updations** done. Values of traits can be updated by specifying
the trait name, material name and its value.

Set the **order** of traits(alphabetically) in which they are displayed
on add material page.

Added a new field **status** in all the tables for specifying whether or
not a particular value is approved by the **admin** or not.

'''''23rd July(Wednesday)

Made a few changes in the database data types to retain the
**precision** of values.

'''''24th July(Thursday)

**Searching improved** further by adding dropdown for search both
material and trait lest a user commits mistake in spellings while
searching.

Encountered some problem in implementing the **status flag** to be
administered by the admin.

'''''25th July(Friday)

Worked on **export feature**, almost done. Used **json_encode()** to
export the data by storing it in an array. Now working on passing
multiple attributes in **multidimensional array**.

**Status flag** still in pipeline.

'''''26th July(Saturday)

Could not do much **GSoC** oriented today, as I was engaged in attending
inevitable **seminars** in my college related to other technologies.

'''''28th July(Monday)

**Progress**: Been able to write the data from the backend(tables) in
**.json** file. I passed an array to json_encode(), whose result I
wrote in a file. The contents written in the file are absolutely what
they should be.

**Problem**: When I try to prompt the user to download the same file,
some futile/useless data seems to get appended at the end of the file.

Did some manipulations with the **LocalSettings.php** like changing the
logo, skin, enabling the image uploads and so on.

### Week 11

'''''29th July(Tuesday)

For exporting the data in json, found and implemented another
**solution** to store the material names and the values of different
traits in two **separate arrays.**

Used **array_combine()** to make an **associative array** of material
name and value as **key : value** pair.

'''''30th July(Wednesday)

Made json export work but there are some glitches like the file in which
the json material is written is perfect but the exported file from web
interface contains some needless data appended at the end.

'''''31th July(Thursday)

Removed the problem of **futile data** getting appended in **.json
file**.

Added a **new file** which has the code to **export** the data in JSON
format.

Added **option** to select any trait which is to be exported by storing
it in **variables.**

'''''1st August(Friday)

**Status flag** nearly accomplished which was in pipeline. **Updations**
that can be only done by **Sysop and bureaucrat** are just left.

**Status visible** in view all materials page.

**Export**(call to action button) added in the menu bar.

**Search bar** hidden from the **main login page** where is wasn't
required.

'''''2nd August(Saturday)

Couldn't work today because of engagements like depositing college fees
and shifting to new hostel. Also there was power supply's problem so I
could not keep my laptop charged.

'''''4th August(Monday)

Learned how to embed **JavaScript** in MediaWiki. Used in the
**navigation bar** on the top of each page.

### Week 12

'''''5th August(Tuesday)

**Status** now visible in **Search by Trait** and **Search by Material**
too. All the **approved** material properties are denoted by "1" and the
**pending** by "0". The privilege(for bureaucrat and sysop) to approve
still pending.

'''''6th August(Wednesday)

Facing a bit of challenge to set the privilege for approval. Because
unlike **Wiki** pages, **Special** pages cannot be edited.

'''''7th August(Thursday)

Done with the **approval part.** Now the values can be approved from the
**Special Page itself**.

'''''8th August(Friday) and 9th August(Saturday)

Visited a funeral ceremony.

Couldn't work, I also had to visit my doctor regarding respiratory
problem.

'''''11th August(Monday)

Made the navigation bar more interactive using **javascript.** Also
renamed a few variable for better **readability**.

### Week 13

'''''12th August(Tuesday)

Found a minor glitch in export. The **indices** of the **two arrays**
don't match and making the json more readable by replacing the "value"
attribute with trait name.

'''''13th August(Wednesday)

Perfectly done with the **json export** now grappling with **CSV
format.**

'''''14th August(Thursday)

Export in **CSV done**, using PHP **header** function and **array**
manipulation.

**Status** which was approved by the admin is **now visible** on the
**front-end** too.

'''''15th August(Friday)

**Exporting** data in **XML** format now possible. Now grappling with
data import.

'''''16th August(Saturday)

Added **update** , **import** call to action buttons.

Done with **import** of data in **JSON.**

'''''17th August(Sunday)

Set the permissions such that only **sysop** and **bureaucrat** can
delete **materials** and **traits.**

'''''18th August(Monday)

As today is the last day of GSoC, I have given my level best to add
everything possible to the code before final evaluation.

I have added support for importing the data by **selecting** the trait
name which earlier was **static.**

I have updated the **update page** which now allows to update all the
values of a particular material **in one go**, which wasn't possible
earlier.

I have also added the facility to the user to **add** only **selective**
traits at a time in case he does not know all the values at present.

Apart from **normal users**, a separate **call to action button** is
added for **admins** to delete materials and traits and approve the
values added by users.

And finally **removed** the **unnecessary** data **exported** from XML
like mat_id, timestamp etc.