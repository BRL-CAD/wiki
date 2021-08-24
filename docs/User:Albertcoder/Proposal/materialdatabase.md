Name: Albert

E-mail address: eralbert9191@gmail.com

IRC username: albertcoder

Phone number: 0091 902 323 2373

Brief background:

I am an undergraduate 3rd year Computer Science student at Guru Nanak
Dev Engineering College, Ludhiana. I have an interest-driven learning in
C++, Shell Scripting and MySQL. I have a strong affinity for Linux which
keeps my inquisitiveness alive for learning more about “How it works?”.
I also have passionate affection for mathematics and physics.

Project Title: Materials Database.

Brief Project Summary:

This project is all about making a web application where users can
easily store/retrieve the properties or traits of materials in a
methodical manner such that those can be retrieved effortlessly. We will
have to create a centralized repository for the storage of
material-properties and give a web interface that would provide all the
necessary features for accessing, sorting and manipulating data and
importing / exporting support for formats like CSV, XML and JSON etc. I
have scrutinized the present database schema of materials database and I
would prefer to continue with it by making it functionally more
productive and lucrative with the usage of latest web technologies.

Detailed Project Description:

Quick review of present state and codebase of project:

After carrying out the scrutiny of present working code I found the
following limitations: Non working code, no comments in the source code,
missing documentation, interface is throwing MySQL queries to the user,
desired data is not displayable, content seems to be disorganized, and
code not complying with BRL-CAD coding guidelines.

Regarding the database(back-end), I have studied the design of the
existing database carefully and tried to test its validity with sample
data and finally found out that it is well designed and thus qualifies
to be used further in my project.

Project partition:

The project can be split into:

1\. Front end(Web interface)

2\. Back end(Database)

Front end

It is the one of most important zones of the project which will make the
database too accessible and pleasant to work with. The data will be
available to the users in the tabular form and they will be empowered to
the access the data with the help of interactive interface. They would
be able to use features like searching and sorting which would fully
satisfy their need.

Searching

`   Search by name`

`   Search by trait`

Sorting(by value)

`   Ascending`

`   Descending`

The Front end would consist of the following:

The following image will make it clear by visualizing the front end:

<https://drive.google.com/file/d/0B4N8HUa1o7MUZE9tbFhHTThQZjg/edit?usp=sharing>

1\. Homepage: The homepage in general would consist of:

`   Header`

`   Sign in/ Sign up`

`   Call to action buttons: Search by name, Search by trait, View all Materials`

`   Search bar`

`   Export / Download data(in the form of CSV, JSON, XML etc.)`

`   Help`

`   Contact`

`   The following image depicts the homepage:`

<https://drive.google.com/file/d/0B4N8HUa1o7MUb2hxcmZ2dXBjVGc/edit?usp=sharing>

2\. View all Materials page: Materials would be categorized and
displayed accordingly in a user friendly way.

There would be certain categories of materials. Under these categories,
links to the materials would be provided that would enable the user to
go onto a specific material-page using JavaScript which would further
provide all the traits of that particular material.

The following image depicts the View All Materials page:

<https://drive.google.com/file/d/0B4N8HUa1o7MUbDVCdlY0SGVDZ2c/edit?usp=sharing>

Now we can see that the user can see different categories of materials.
So he can select a particular category which will be further opened in a
JavaScript Dialog showing the materials under the selected category.

The following image depicts better:

<https://drive.google.com/file/d/0B4N8HUa1o7MUTmJqZi1pU19JLUk/edit?usp=sharing>

Admin Interface:

I have thought of a way in which malicious users would be prevented from
tampering the data. For this the admin would be notified whenever any
user tries to modify the current data and it would be his wish whether
to approve the change or not. He can even block/remove that user. This
would ensure the updation, safety and preservation of data. Another
useful feature to ensure the safety of the data is that the data would
be accessible to all but only the registered users would be provided the
privilege to modify the data and if any malicious activity is tracked,
the concerned user can be deemed accountable.

Back end

I have thoroughly studied the existing database schema which is
absolutely fine so far its approach is concerned. I feel the back-end
needs to be pondered upon i.e. adding foreign keys across tables
(wherever necessary) so as to keep the data consistent and connected.
This may require discussion with senior developers and may take time, so
I decided to tackle it in community bonding period.

Deliverables:

List of material properties in the form of an amicable interface with
well linked database at back-end.

Normal user profile.

Admin interface.

`   Search features (search by name, search by trait)`

`   Importing/Exporting data in CSV, XML, JSON etc. formats from database.`

Development schedule:

Community Bonding Period

Interact with the developers on IRC / mailing list regarding the
integration of this application with BRL-CAD wiki in the form of
Mediawiki extension which is one of the most aspired features.

`       Discuss about the categorization of materials.`

`       Discuss other queries and problems faced.`

`       Discuss the extensible areas and make room for new ideas with the help of fruitful discussions.`

WEEK 1 (19th May to 25th May)

`   Finalize the module and fragments so as how to proceed.`

`   Traverse the current code and database structure and make out what areas need to be worked upon.`

`   Tuning the current database.`

WEEK 2 (26th May to 2nd June)

`   Work on Login Page. Sign in / Sign up process will have a peculiar feature that the users who sign up on material website would be automatically directed to the BRL-CAD wiki website for sign up and bring back to the materials website after the sign up.`

WEEK 3 (3rd June to 9th June)

`   Normal User page will be designed. It would have the a dashboard on which user can see the number of edits previously made in the database, pending approval requests made to the Admin for the change made in the database and so on.`

WEEK 4 (10th June to 16th June)

`   Admin page will be designed. This would be almost similar to the Normal User page but the dashboard would contain features like approve edit requests, number of previous edits, user details and so on.`

WEEK 5 (17th June to 23rd June)

`   Work on Homepage: Homepage would consist of header, body and footer. Header would contain the options like sign in / sign up, help and so on. Body would contain options like search by name / search by trait and view all. And footer would contain options like About, Contact and so on.`

`   Work on Search page: Search by name, Search by trait, View all Materials`

WEEK 6 and WEEK 7 (24th June to 7th July)

`   Work on View All page. Here all the materials would be listed with their full details.`

`   Work on Sorting / Searching.`

MID TERM EVALUATION

WEEK 8 (8th July to 14th July)

`   Work on Operation or Data Manipulation pages. Like how to add, modify, delete a material, a table etc.`

WEEK 9 and WEEK 10 (15th July to 28th July)

`   Work on Suggestion pages. Suggestion pages would intimidate the Admin about the edits made by users in the database and it would be his choice to save or discard them.`

WEEK 11 (29th July to 4th Aug)

`   Testing and Enhancement period.`

WEEK 12 (5th Aug to 11th Aug)

`   Debugging`

WEEK 13 (12th Aug to 18th Aug)

`   Documentation.`

`   Make all the necessary changes required before final submission.`

Time availability:

I will be available for 40 hours/week however this is flexible and
subject to the requirement of the project.

Future Prospects:

1\. Synchronization of materials data with other resources wherever
possible.

2\. STEPCode integration (need more knowledge about the subject and it
will be gathered).

3\. Integration of periodic table, may be a sort of interactive widget
(only if it is felt relevant). It would be able to display the
properties of elements once the user clicks on the symbol / name of
element on the interactive periodic table(I personally feel this can be
of substantial help to the users to see the traits of elements in
periodic table).

Why BRL-CAD?

As I loved the very concept of open source development from the moment I
learned about it, it would be a matter of honour for me to be a part of
such a magnificent crew. Also I have a firm belief that I will excel
tremendously in my area of interest and nurture my skills by working
assiduously. BRL-CAD being an epitome of its field lured me to work with
it and learn manifold new things.

Why me?

Being highly diligent and ardent for my work I would love to contribute
to the open source development since it is like a holy grail to me. I
had been into coding environment from quite a time and I wish to apply
my whole coding-momentum to a point. I have joined the \#brlcad channel
on IRC a few days ago and I feel good to interact there and I have
already got some precious suggestions. This is the real boon for the
young saplings in the garden of programming to grow under the shade of
the sublime mentors. I am so much self-obliged and excited to work with
proficient developers across the globe and be a part of the legacy.