## About Me

My name is **Neil Dhruva**. I am currently pursuing Bachelors in
Computer Science from BITS-Pilani, Goa, India.

### Interests

-   Web Development
-   App Development with Java
-   Open Source
-   Mobile App Development

### Languages Worked With

-   PHP
-   Javascript
-   Java
-   Python
-   C

### Contact

-   IRC : *Neil* / *Neil_* / *Neil__* etc.
-   E-mail:
-   Website:

## BRL-CAD Tentative Proposal

**Topic** - *Materials Database*: Create a Materials Database web site
for collecting, managing, and providing programmatic interfaces to
material properties.

**Brief project summary (&lt;500 words)**
The project deals with creating a Content Management Site to aid the
functioning of the BRL-CAD software. The CMS is meant for managing a
database of various different materials and properties of these
materials for users to share with each other and use in their projects.
The users can add new materials to this site, edit properties of
existing materials, and request generation of certain file formats like
XML that consist of different materials and corresponding properties.
The website will thus make it easier for users to share data and results
used in their projects.

**Detailed project description (&gt;500 words)**
I have a few ideas regarding the Materials Database website. The website
at present contains the following:

1.  index.html
    1.  It has 2 options: (1) generate an xml file of the current
        database (2) login as admin to admin.php
2.  admin.php
    1.  Page has a simple linear layout of all the materials that have
        been logged so far along with various properties that have been
        added to each material.
    2.  Options are provided for editing the description of each element
        which gives a text box when 'edit' is clicked.
    3.  The user can create his/her own material, add traits to it and
        edit it. The user can also make it private or public. Every
        element is associated with a user which obviously is via the
        relational backend.
    4.  Also, when a user tries to change a trait/material that will
        affect the rest, he/she is asked if sure whether to make the
        change. All this is accomplished by the GET method.
3.  generate.php
    1.  This generates the XML document and outputs it to the browser.

I feel a lot of other features can be added to the existing site:

-   The most important one being 'Search'. The main purpose of this
    website is sharing information and I believe Search is an integral
    part of helping users achieve results faster.
-   User interaction is another important feature which can be
    incorporated in terms of better profile pages with message
    facilities. Links can be provided and an individual can be notified
    in such events via mail.
-   The entire format of the site, I feel, should be changed. The front
    end requires work to make the site more user friendly and amiable.
    Better CSS and JavaScript to make the site more pleasant, yet
    simple.
-   Also, various different pages along with a navigation bar should be
    assigned for different tasks, for eg, main page with different
    materials, another page for editing the database, one more profile
    page and so on. Also, every material can be assigned a page with the
    GET method. All of this is shown in the website flow diagram\[3\].
-   POST method should be used for the edit pages.
-   Comparison of different materials based on different properties can
    be added.
-   I also think the backend will require work in order to relate tables
    better for handling more data. And this can further be used to
    publish the data in various formats like XML which has already been
    done.
-   Server side caching can be done to optimize the speed with which
    pages can be viewed.

*Technicalities*:

-   **Database**: The database will mainly store two things: user
    information and materials information. User Information mainly
    includes name, e-mail, password, and other personal profile
    features. It will also include paths of files uploaded by users.
    Materials information will include the ID, name, description and the
    properties. There will be more tables that the user and materials
    table can each be broken down into, or just for foreign key
    associations.
    However, I had another idea in mind as well. One could link all the
    user profiles back to the BRL-CAD wiki pages of the users. This will
    make it easy for integrating the materials website with the BRL-CAD
    official website. A link in the toolbox can then be provided to the
    Materials Database.
    -   **MySQL**: For the tables, I believe MyISAM would be better than
        InnoDB because there will be a lot more reads than writes. Also,
        the full-text search option will then be available which will be
        very handy for the database. This will require some work
        regarding foreign key maintenance, but I don't think there will
        be too many tables to worry about. Also, MySQL manages Query
        caching, parsing and optimization pretty well.

<!-- -->

-   **Server Files**: The files on the server will include images
    uploaded by users like profile pictures. If user profiles are going
    to be their BRL-CAD wiki pages, then this mechanism is already
    provided for in \[1\]. Apart from this, all the PHP, JavaScript,
    CSS, and Cache files will lie on the server. The XML and other
    documents generated on the fly can be made available to the user in
    two ways. Currently, XML is generated on the fly and it is output as
    an XML document to the browser directly. However, I feel there
    should be a directory dedicated to XML documents generated by
    different users. There can be an upper limit on the number of XML
    documents stored in this folder and can be replaced there after.
    Whenever a user generates an XML, it is stored in the folder and a
    link is provided for download. The links to the paths of these files
    can be stored in the database corresponding to the user ID for
    future reference.

<!-- -->

-   **Apache**: I am reading a lot about server management and
    performance optimization. One of the things we can incorporate is a
    Reverse Proxy or an HTTP accelerator. I am not sure about this
    approach because it is meant for very high traffic sites and I'm
    still reading about it.
    There are a lot of techniques involved in maximizing PHP processing
    of scripts. I'll be using output buffering with ob_start() etc.; or
    a simple output_buffering=on in .ini file to decrease errors. The
    buffered data can then be flushed to the user. Also, since we are
    using individual pages for user profiles and each material, I
    suppose flat-file caching would be a good option to cache recently
    generated HTML, especially when the materials pages are viewed
    because there will rarely be changes in these pages. I am also
    reading about the mod_rewrite facility of Apache that should be
    greatly helpful in managing cache files. Managing cache files can be
    a bit tricky, given the uncertainty about user traffic, when to
    replace certain cache files etc. Hence, I will try to incorporate
    this feature towards the end of the project.
    Also, I will be relying on .htaccess and other methods for directory
    security.

<!-- -->

-   **Generating XML on the fly**: XML is generated whenever a user
    wants a list of materials along with selected properties. This is
    done by pulling the desired data from the materials database tables.
    A script already exists that accomplishes this. It is currently
    \[2\]. However, there will be a lot more materials that the user can
    choose from once the website is in frequent use. I suggest providing
    the user with a table of all materials to choose from. A small
    segment at the top of the page can indicate all the materials the
    user has already chosen to be included in the XML (JQuery can be
    used for this). This can also be accomplished by JavaScript through
    a pop-up window. Once the user chooses the materials, the XML is
    then generated by pulling the required resources from the database.

<!-- -->

-   **Authentication**: User authentication is another issue to be
    tackled. Creation of new user and the 'forget password' option can
    both be authenticated by sending a mail to the user. The mail can
    either be the generation of a new password and the user can then
    change it or it can be an authentication key. I'll use SMTP for
    sending mails and set up a queue folder for mails not sent and deal
    with the situation accordingly.
    Once the user is logged in, sessions will be used, which are in turn
    authenticated by cookies for each user. The users can then view
    their profile, recent XMLs generated by them and various materials
    added to the database by the individual user (user's contribution).

<!-- -->

-   **Error Handling**: Error handling has to be accomplished in order
    to keep track of various errors encountered by users. This can be
    done by creating a directory for error handling and using PHP
    functions like error_log() to tackle the errors generated. The
    administrator can also be notified by mail if the error is serious.

Apart from these, I have also uploaded a basic architecture diagram of
the web server process along with a a website flowchart at \[3\]. I have
also provided the basic flow of the website as I see it presently, along
with possible database tables and files on the server at \[4\]. Apart
from this, a basic mock-up of the website can be found at \[5\] and the
initial SQL schema at \[6\].

I will come up with a lot more ideas as the project moves along. I had
developed a CMS last year for a project at an Information and Library
Network in my hometown under their open source and software development
wing. It was based on allowing the employees order inventory and office
supplies via an online portal. I have uploaded a few snapshots of the
same here \[7\].

The project will be very useful for all the users of BRL-CAD and I hope
I can contribute to the same.

\[1\] - <http://brlcad.org/wiki/Special:Upload>
\[2\] - <http://mater.brlcad.org/xml/generate.php>
\[3\] - <http://brlcad.org/w/images/4/4d/Arch_diagram3.pdf>
\[4\] - <http://brlcad.org/w/images/8/89/Website_flow.pdf>
\[5\] - <http://brlcad.org/wiki/Image:Mock_up.pdf>
\[6\] - <http://brlcad.org/wiki/Image:SQL_schema.pdf>
\[7\] - <http://brlcad.org/wiki/Image:Cms_snapshots.pdf>

**Deliverables (specific, measurable goals) / Milestones**

1.  Develop basic front end, set up a database
2.  User profile pages
3.  Materials pages
4.  Search features
5.  Generating XML and other formats from database entries
6.  Improve front end
7.  Server side caching for faster page retrieval

**Describe time availability (40+ hours/week assumed)**
I have my end-semester exams from May 1 to May 15 and then the summer
break from May 16 to August 2. Hence, I will be absolutely committed to
GSoC throughout the span of 14 weeks.

**Timeline**

-   May 1 - May 15
    -   End-semester exams at college

<!-- -->

-   May 15 - May 31
    -   Go through the current code, database structure and select
        everything that can be improved upon and what all needs to be
        created.
    -   Read more about Apache server, MySQL data handling
    -   Read more about caching, IP authentication, SMTP etc.

<!-- -->

-   June 1 - June 10
    -   Prepare a basic layout of the website to work with (css)
    -   Prepare database tables (users, materials)
    -   Create user login, authentication pages and user area

<!-- -->

-   June 11 - June 30
    -   Finalize design of the Materials pages (layout)
    -   Code for the Materials pages, interaction with the database
    -   Implement the interaction between user and materials database,
        user authentication to edit the database entries and so on.

<!-- -->

-   July 1 - July 15
    -   Write code for converting MySQL entries to XML and other
        required formats (can use part of existing code for this)
    -   Code for easier front end for generating such documents and
        downloading them like check-boxes to include all the materials
        and properties required in the document

<!-- -->

-   July 16 - July 25
    -   Implement server side caching, error logging and other features
        not thought about in the initial stage.

<!-- -->

-   July 26 - August 13
    -   Improve the front end, add javascript for notifications etc.,
        improve css
    -   Write the documentation, tutorials, examples if any to make
        working with the website easier
    -   Review code, run tests

<!-- -->

-   August 13 - August 20
    -   Make all the necessary changes/additions required before final
        submission.

**Currently Reading About**
\* CakePHP(for better security, caching etc.)

-   JSON (alternate to XML)
-   Caching using PHP; APC (Alternative PHP Cache)
-   Reverse Proxy

**Why BRL-CAD?**
BRL-CAD is a great open source software and fun to work with and I want
really to contribute to this project. My PHP skills are better than C++
and hence I think I can better contribute to BRL-CAD with my web
development skills.
Sharing is important in every community and I believe BRL-CAD users can
benefit a lot from the Materials Database site.

**Why Me?**
I have been coding for the past few years now and I believe I am getting
a good hang of things, especially website development. I want to further
my knowledge while at the same time contribute to the open source
community. GSoC would be the perfect opportunity for me to accomplish
both of these.