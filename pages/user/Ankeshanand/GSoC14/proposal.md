# Personal Information

------------------------------------------------------------------------

|                   |                                            |
|-------------------|--------------------------------------------|
| **Name**          | Ankesh Anand                               |
| **Email Address** | <ankeshanand1994@gmail.com>                |
| **Webpage**       | [ankeshanand.com](http://ankeshanand.com/) |
| **IRC(nick)**     | ankesh11                                   |
| **Phone Number**  | +91 8348522098                             |
| **Time Zone**     | UTC +0530                                  |

### Brief Background

I am Ankesh Anand, a 3rd year Mathematics and Computer Science undergrad
at the Indian Institute of Technology, Kharagpur. I am a huge
open-source enthusiast who believes in the zen of Javascript and uses
Vim and Ubuntu at his workstation. I like building full stack
web-applications and programming in PHP, Python, Javascript, C and C++.
I have worked previously in diverse environments ranging from a privacy
start-up where I worked on anonymized analytics to a research group
focused on analyzing Citation Networks. I am also the lead developer of
the Autonomous Underwater Vehicle Group at my institute which designs
submarines for international competitions.

# Project Information

------------------------------------------------------------------------

### Project Title

Benchmark Performance Database

### Abstract

BRL-CAD Benchmark Suite has been used over the years to analyse and
compare a system's performance based on certain parameters. The goal of
this project is to deploy a database and visualization website that
provides multiple mechanisms to add new benchmark logs into the database
and provide various forms of visualizations for the aggregate data.

### Detailed Project Description

#### A Diagrammatic Overview


Benchmark Runs produce a log-file which contains the results of the
ray-tracing program on a bunch of sample databases, along with a linear
performance metric, system state information and system CPU information.
These log-files then need to be uploaded to a server via multiple
mechanisms such as Email(Mail server), FTP, scp and an http API.There a
parser reads the information from the log-file and subsequently stores
it into a database. The database schema is ideally designed to index all
the information in the log-file. The front-end pulls the aggregate data
from the database and displays it in forms of various plots and tables.
There is also a file upload mechanism via the web front-end as well as a
search functionality which enables searches filtered to parameters such
as machine descriptions, versions, results etc.

<!-- -->


![](/wiki/user/img/Benchmark_overview_v3.jpg)

#### The current status of the Project


There was an earlier GSoC project\[1\] which did a nice job of building
a robust parser and capturing all the relevant information into the
database. I plan to leverage the parser and database modules. The
front-end is buily using the Python Bottle Framework and it Google
Charts Library which is not robust for data-visualizations. I feel I
could be more productive if I start my implementation of front-end from
scratch, the details of which are highlighted in further sections.

#### Mechanisms for Upload

-   **Emails**


The current de-facto standard to submit the benchmark results is to send
an email to benchmark@brlcad.org. Any approach to build a benchmark
performance database must cater and support parsing of emails to
retrieve the attached logs. Keeping this in mind, I have decided to use
the php-mime-mail-parser\[1\] library, which is a wrapper around PHP's
Mail Parser extension to parse and extract attachments from the mails.
It's fast and has an easy implementation:

`   // require mime parser library`
`   require_once('MimeMailParser.class.php');`
`   // instantiate the mime parser`
`   $Parser = new MimeMailParser();`
`   // set the email text for parsing`
`   $Parser->setText($text);`
`   // get attachments`
`   $attachments = $Parser->getAttachments();`

-   **Drag-n-Drop Files**


The front-end will provide a convenient interface to upload log-files
with a drag-n-drop support. An uploader script based on **HTTP POST**
will handle the implementation details, and the drag and drop feature
can be realized using the DropzoneJS\[2\] library. This also means the
file can be sent with a command line tool such as **curl**.

-   **FTP**


The files can also be uploaded to the server via a FTP client. A
cron-job keeps checking for new files on the server at a regular
frequency(say 5mins), and then subsequently sends them for parsing.

#### Data-Visualizations

-   **MVC Architecture**


To attain flexibility for the application, I plan to use the MVC pattern
for the visualization framework. It would help in separation of
responsibility across different components. The model would be the
database itself, the contollers bring the code that aggregate and filter
the data based on input and the views would the graphs and tables
presented on the browser. I am an admirer of the Laravel PHP framework
and plan to use it for this project.

-   **Visualization Library**


I went through a couple of tools to decide what could be best for the
project, and in my opinion d3.js is probably the best library out there
for creating dynamic and interactive data-visualizations in the browser.
In contrast to many other libraries, D3 allows great control over the
final visual result. It's very versatile and gives us wide options in
terms of graphical visualizations. I have played around with d3.js in my
past projects, so that should come in handy.

-   **Types of Analytics**


*(This probably needs some discussion with the community. I have
highlighted some of the primitive ideas.)*

-   Average Performance of Different Architectures against Reference
    Images (A Grouped Bar Chart)
-   A comparison of different architectures with respect to VGR Metric.
-   Historical Progress in Performance across different Processor
    Families.
-   Performance against Number of CPUs.

-   **Categorization**


A number of categorizations are possible for the final analytics. Some
examples include categorization by the Processor Family, categorization
by the type of machine(Desktop, workstation, servers) etc.

#### Search Functionality


One of the goals of the project is to let the users perform wide range
of queries on the data. The storage in the database enables the content
to be searched via parameters such as processor family, number of CPUs,
and other machine descriptions. The results could be presented in a
tabular form.

### Deliverables

-   Implement mechanisms to add new performance data into the database.
-   Multiple forms of visualizations for the aggregate data.
-   A search functionality to enable users to perform queries over the
    data.
-   Integrate the parser and database modules from the previous GSoc
    project.
-   Detailed Documentation for the project.
-   A deploy-able Database and Visualization website for the BRL-CAD
    Benchmark Suite.

### My Preparations for the Project

-   Cloned and built the BRL-CAD source code on my system.
-   Contacted the previous GSoC candiadate on this project and exchanged
    ideas about the current state of the project and possible
    extensions.
-   I ran the benchmark on a couple of systems, and went through the
    documentation to make sense of the results, how the benchmark suite
    works, and how a comparison between different machines is done.
-   Went through the repository of the work done in the previous GSoc
    project and made notes about each module. I also read the concerning
    dev-logs and reports.
-   Introduced myself on the mailing list and took part in IRC
    discussions about the project.

### Development Schedule

#### Phase I : Analysis and Design Period

-   **(April 22 - May 16)**
    -   Get familiar with all the parser and database modules in
        Suryajith's repository.
    -   Make a short rough bio about each and how they work.
    -   Prepare mock-ups and rough implementations of each functionality
        .
    -   Discuss with the community about several aspects of the project
        including the Types of Analytics we want in the final
        implementation, details about upload mechanism and a discussion
        of broad implementation details.
    -   Learn details of the Laravel MVC framework.


**At the end of this phase : A robust plan to proceed for the
development of the Benchmark Database Website.**

#### Phase II : Developmental Phase (May 18 - July 31)

-   **SPRINT 1 : (May 18 - June 22)**


**\[Feature to be implemented : The visualization framework\]**

-   Week 1 : *(Planning sub-period)* Clearly define the Models, Views
    and Controllers of the visualization architecture.
-   Week 2 : Prototype the various forms of graphs and tables to be used
    in the final implementation.
-   Week 3 : Write codes for the controller modules which pull the data
    from the database and aggregate them.
-   Week 4 : Add options to the front-end to switch between various of
    visualizations and parameters and integrate the modules for models,
    views and controllers so that they seamlessly work.
-   Week 5 : *(Testing sub-period)* Testing, Ensuring compatibility
    across different browsers, documentation, Mid Term Reports.

-   **SPRINT 2: (June 23 - July 12)**


'''\[Feature to be implemented : Search Functionality, Various
Mechanisms to upload Benchmark logs\]

-   Week 1 : Implement the search functionality for performing queries
    on the data and the HHTP POST api for file-uploads via the
    front-end.
-   Week 2 : Implement the Email-Parser and write scripts for the
    cron-jobs to check for new files on the server.
-   Week 3 : Document progress, and testing of the FTP, Email and HTTP
    POST upload mechanisms.

-   **SPRINT 3: (July 14 - July 31)**


**\[Integration of the Parser and Database Modules**\]

-   Week 1 : Test the parser and database modules for any minor bugs and
    fix them. Write scripts to automate parsing of new files on the
    server, and dumping the information into the database.
-   Week 2 : Document the progress, More tests, ensure everything is
    seamless integrated uptil-now.

#### Phase III : Final Wrap-Up and Cleaning (August 2 - August 20)

:\* Week 1 : Code Cleaning, Cross-Browser Testing of all functionality.

:\* Week 2 : Code Reviews, Final structure to the Documentation.

:\* Week 3 : Final submission to Melange, Buffer Period.

### Time Availability

-   I understand GSoC is equivalent to a full time project, and I will
    ensure I dedicate appropriate time and commitment to the project.
    The motivations of working on a pushing a meaningful project to
    deployment are huge.
-   I can devote an average of 40-50 hrs. per week to the project. It
    will vary from 6-8 hours on the weekdays and 3-4 hours on the
    weekend.
-   I have no prior known commitments and the majority of the timeline
    coincides with my summer vacations. If any commitments arise, I can
    devote extra hours on the weekend to keep the project on track.

### Why BRL-CAD?

I was looking for a meaningful open-source project to contribute to in a
long-term perspective when I stumbled upon BRL-CAD which had exciting
several web-oriented modules in initial stages and this seemed like a
perfect fitting. The community was another affirmer as it helped me
along getting acquainted with the project via meaningful discussions on
the IRC and the mailing list.

### Why me?

I have an inquisitiveness to learn things and I feel my skills are a
right match for this project. My enthusiasm for open-source and my
interests in building web applications are the motivating factors behind
this project. I look forward to being an active contributor to BRL-CAD
in the future.

### References

\[1\] <https://bitbucket.org/suryajith/benchmark/src>

\[2\] <https://code.google.com/p/php-mime-mail-parser/>

\[3\] <http://www.dropzonejs.com/>

\[4\] <http://laravel.com/>

\[5\] <http://d3js.org/>

\[6\] <http://users.soe.ucsc.edu/~elm/Papers/cmg00.pdf>
