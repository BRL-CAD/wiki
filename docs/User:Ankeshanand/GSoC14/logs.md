# Development Logs

## Project Details

|                             |                                               |
|-----------------------------|-----------------------------------------------|
| **Project Name**            | Benchmark Performance Database                |
| **Project Sudent**          | Ankesh Anand                                  |
| **IRC(nick)**               | ankesh11                                      |
| **Github**                  | [ankeshanand](https://github.com/ankeshanand) |
| **Website**                 | <http://www.ankeshanand.com/>                 |
| **Google-Melange username** | ankeshanand1994                               |
| **Phone Number**            | +91 8348522098                                |
|                             |                                               |

## Introduction

This page will contain weekly targets and Updates about the work done.

### Community Bonding Period

***(23rd April to 18th May)***

-   Got familiar with the modules and database schema from previous
    repository.

<!-- -->

-   Had a discussion with H.S. Rai(Project Mentor) about the
    infrastructure to be used. We settled on Django as a web framework
    for the project.

<!-- -->

-   Learnt Django by reading through books and building a couple of
    small applications with it.

<!-- -->

-   Set up the development repository on
    [Github](https://github.com/ankeshanand/benchmark).

<!-- -->

-   Discussed about the deployment options on BRL-CAD servers. It
    already has Python and MySQL support, and since we manage it
    ourselves, it would be easy install new packages on it.

<!-- -->

-   Fixed a few bugs to get the database and parser portions fully
    working. The benchmark logs can now be parsed and indexed into the
    database from the command line.

<!-- -->

-   Built a Django app with jquery to support file uploads that let's
    users(Link to the code is
    [here](https://github.com/ankeshanand/benchmark/tree/master/fileupload)):
    -   Upload Benchmark logs
    -   Does validation checks
    -   allows the admin to view a list of files.

### Development Phase

#### Week 1 (19th-25th May)

-   **19th May(Monday):** Started working on the plots app. Integrated
    the legacy database from previous repo with the models in the plots
    app.

<!-- -->

-   **20th May(Tuesday):**' Continued the work with plots app,
    integrated both the databases(fileupload and benchmark) to a single
    database. Read the Django documentation on views and templates to
    refresh and understand a few details. Updated url mappings, and a
    simple admin interface for plots app.

<!-- -->

-   **21st May(Wednesday):** I went through the tutorials on Highcharts
    and emulated a few examples. Created simple bar and line charts to
    understand the concept of series, axes and how the data is loaded
    via AJAX.

<!-- -->

-   **22nd May (Thursday):** I decided to JSON as the data source for
    plots. This would require me to pass JSOn objects from view to
    templates. I went through the json module of python, particularly
    *json.dumps* and *json.encode* functions which will help in parsing
    JSON. I also thought about the types of plots I could generate from
    our app.

<!-- -->

-   **23rd May (Friday):** Brainstormed over the visualizations I should
    work on, referred to suryajith's work on this and had a look at
    Openbenchmarking.org. After a discussion on the mailing list, we
    were able to arrive at a preliminary set of plots I should work on.
    Fixed a bug in the database connection file. Also got in touch with
    Sean regarding a server account.

<!-- -->

-   **24th May(Saturday):** Half day of work. I created some charts
    using AJAX and a JSON file with initial data with the Highcharts
    library, had a few hiccups along the way. Next step is to refine
    these prototypes and integrate with the Django application.

#### Week 2 (26th May-1st June)

-   **26th May(Monday):** Did a comparison of various charting
    frameworks as Rai Sir had asked for. Also mentioned the reasons of
    choosing the HighCharts library. Further experimentation with
    HighCharts,I am able to load the series and chart options
    dynamically now. The url configurations have been modified to
    provide appropriate mapping for the charts and their data. Threw a
    couple of stub views which now I have to worked on. Cleaned up the
    fileupload app which was a mess of useless JS files.

<!-- -->

-   **27th May(Tuesday):**

:\* Forked the repository to BRL-CAD's Github organisation, subsequent
development will take place there. The new home for the repository is:
<https://github.com/BRL-CAD/benchmark>

:\* Wrote the Django template file for charts. This contains the chart
config and the JS script to make AJAX calls for JSON data.
(https://github.com/BRL-CAD/benchmark/blob/master/plots/templates/chart.html)

:\* Started work on **plots/data.py**: The script which will return the
aggregated data from database in the form of a dictionary. Wrote the
aggregation codes for Avg VGR vs Processor Graphs, other plots should
follow this structure.
(https://github.com/BRL-CAD/benchmark/blob/master/plots/data.py)

:\* Wrote the rawdata view in **plots/views.py** that dumps JSON string
after invoking the appropriate data aggregation function from data.py

-   **28th May(Wednesday):** Resolved a bug which prevented sending AJAX
    requests for the raw data in form of a JSON string in Django. Added
    support for two more plots, Average VGR Rating vs Number of Cores
    and Average VGR Rating vs OS Type. Made the chart template dynamic
    so that we don't have to change it depending on the plot. Added doc
    strings to views and data files.

<!-- -->

-   **29th May(Thursday):** Added support for 4 more plots: Logarithmic
    VGR Rating vs Processor Family, Logarithmic VGR Rating vs OS Type,
    Logarithmic VGR Rating vs Number of Cores ,Running Time vs Processor
    Family. Spent some time resolving a bug in Django ORM.

<!-- -->

-   **30th May(Friday):** Another plot supported now, the Absolute Rays
    per sec against Reference Images plot is up. Also added the options
    to export chart in form of a PDF, or an image. This is how one of
    the plot looks like:


<http://i.imgur.com/NKp1qyz.png>

-   **31st May(Saturday):** Had to hold off work on HighCharts due to
    licensing issue. Spent some time figuring out the details of
    alternative libraries. People on the list have asked me to do a
    spreadsheet comparing different libraries, and I got started on
    that.

<!-- -->

-   **1st June(Sunday):** Did a comparison of various charting libraries
    to arrive at an alternative to HighCharts. After several
    considerations, I think Flot is the best way to go. The detailed
    document is here:
    <https://github.com/BRL-CAD/benchmark/wiki/Selection-of-an-appropriate-Javascript-Charting-Library>.
    Experimented with Flot configurations to better understand the
    Library

#### Week 3

-   **2nd June(Monday):** Created prototypes with Flot to get a better
    understanding of the API references. Read through Flot's
    documentation, and was able to emulate earlier plots with plastic
    data. Also got flot charts to works via AJAX data.

<!-- -->

-   **3rd June(Tuesday):** Ported all the plots from HighCharts to Flot.
    The template and data modules were modified accordingly. Here is a
    sample chart in Flot: <http://i.imgur.com/KFQrLdp.png>

<!-- -->

-   **4th June (Wednesday):** Resolved a few bugs in data module,
    changed the format of JSON data to better integrate with Flot, made
    the code a bit more modular so that it is flexible across all the
    plots.

<!-- -->

-   **5th June (Thursday):** Drew mockups of the plots page, and started
    working on the index page in the plots app.

<!-- -->

-   **6th June (Friday):** Made an initial prototype of the plots page.
    The different charts are loaded via AJAX, so there are on page
    transitions. Updated URL patterns, added custom styles in the
    process. This is a screenshot of the initial version, for a higher
    resolution, see [here](http://i.imgur.com/eEA99Hm.png)


![](Wireframe-plots-index.png)

-   **7th June (Saturday):** Fixed bugs in the front-end, added support
    for a new plot (Average VGR vs Number of Processors)

<!-- -->

-   **8th June (Sunday):** Took the day off.

#### Week 4

-   **9th June (Monday):** Read a few articles on the science behind
    data-visulaizations and how to achieve better and meaningful
    results. Also started working on multi-series plots and refereed to
    the documentation accordingly.

<!-- -->

-   **10th June (Tuesday):** Worked on integrating both the plots and
    upload applications. Also ensured that they are decoupled so that
    the code remains independent and modular, besides this is also a
    recommended Django design principle. Related UI fixes and
    configuration changes were carried out in the process.

<!-- -->

-   **11th June (Wednesday):** Added efficiency plots(Average VGR Rating
    against CPU MHz and no. of cores). Studied open benchmark suites and
    looked at openbenchmarking.org to get a better understanding of the
    end-usage aspects of a benchmarking tool. Also, requested Sean to
    provide logs which will assist in testing.

<!-- -->

-   **12th June (Thursday):** Completed the integration of the front-end
    interfaces of plots and the upload app. Also ensured the line charts
    and their labels are automatically scaled when the data is not
    discrete. I still await the benchmark logs from Sean, but I will
    move forward next to creating scripts that check for new benchmark
    logs.

<!-- -->

-   **13th June (Friday):** Leveraged the earlier script written by
    Surjyajith to process files from the queue. Made relevant changes to
    get it working. The scripts needs to be run periodically, we can use
    crontab for that. I enquired on the IRC channel and Erik confirmed
    that crontab is installed on the servers.

<!-- -->

-   **15th June (Sunday):** Added the multi-series plot Performance of
    Processor Families against Reference Images. Along with that added
    two plots in the Running Time Section. Fixed some issues with line
    chart, and added comments to the index page. With this, I think the
    initial roaster of plots is complete, however I still need to find a
    way to work with Logarithmic axis for Log charts and think about
    Distribution charts.

#### Week 5

-   **16th June (Monday):** Caught a minor flu so couldn't accomplish
    much work today. Had a relook on the documentation and tried to
    brain-storm further aspects of the project. Tried reaching Sean
    again unsuccessfully, I need further perspectives on the project I
    think, will draft a detailed mail on the list if IRC discussions are
    not possible

<!-- -->

-   **17th June (Tuesday):** Tried to figured out the problems with
    logarithmic axis in Flot, it turns out logarithmic axis are not
    supported out of the box and we need to provide ticks manually.
    Thought of solutions to serve the performance data to developers,
    and took notes from OpenBenchmarking.org in this aspect. This week
    is reserved for documentation and testing, so I asked on the list if
    I should continue the documentation now. Also posted some issues and
    questions I had.

<!-- -->

-   **18th June (Wednesday):** Had a great IRC discussion with Sean
    about several aspects of the project. We discussed the possible
    views of the application, and the importance of displaying immediate
    results to the user, alongside comparisons with the database.
    Regarding this I look into the speedtest portal to get an idea of
    the UI aspects. I will hold off on docs now as advised.

<!-- -->

-   **19th June (Thursday) and 20th June(Friday):**


Couldn't update the logs yesterday due to sudden internet outage. I have
worked on making the website consistent with the BRL-CAD color scheme. I
posted a screenshot on IRC.

Apart from this I worked on making the immediate results view of the
uploaded logs. I explored how to resolve the issue of conflicting file
names. Discovered that Python has a uuid library which produces unique
strings, which can be appended to the filename to get a unique name. To
generate unique URLs, I can use the hash of this filename and serve the
results on that URL to the user.

-   **21st June(Saturday):** Started creating the module for showing
    individual results. Prepared mock-ups of the design after having a
    look at a few dashboard sites and other relevant links. Also, fixed
    a few issues in the new color-scheme.

#### Week 6

-   **23rd June (Monday):** Continued the work on results module. Create
    the starting models and views. Since the models used by this module
    and the polls module would be same, I looked for ways to share them,
    and found an answer from the Django community. I worked on UI as
    well and started implementing my mock-up.

<!-- -->

-   **24th June (Tuesday):** Studied various dashboards to derive inputs
    from them, continued to work on the frontend of the results page,
    implemented demo scripts for hashing the file-name and then
    generating a unique URL as well. For now the unique URL length is
    rather too long, I will study further to see how I can compress it.

<!-- -->

-   **25th June (Wednesday):** Did a bit of code-cleanup and some UI
    fixes. Also started on the blog for midterm evaluations, a
    half-draft is done and plan to complete the rest by tomorrow.


**Midterm Report:**
<http://www.ankeshanand.com/posts/gsoc-midterm-status-quo/>

-   **26th June (Thursday):** Finished writing off the blog today and
    studied about writing Python setup scripts from here:
    <https://docs.python.org/2/distutils/setupscript.html>

<!-- -->

-   **27th June (Friday):** Read about working with Virtual Environments
    in Python. Deployed the application at: <http://202.164.53.122:3000>

<!-- -->

-   **28th June (Saturday):** Worked on a sample application using
    django social-auth for managing user accounts and integrating logins
    from OAuth providers. Tried to resolve a file upload bug
    un-successfully even after logging stdout and stderr as there were
    no error messages logged. Will try to resume it tomorrow.

#### Week 7

-   **30th June (Monday):**

:\* Ensured unique filenames for all uploaded logs using Python UUID4.

:\* Modified models to make sure all are accessed by Django ORM.

:\* Added show_result view to immediately parse the log and it's
information is inserted into the database. The data for the file is then
extracted using Django ORM and returned as a dictionary to the result
template.

-   **1st July (Tuesday):** Completed the template markup, linked the
    view to the template. The front-end now shows all the information
    extracted from the file immediately uploaded. Next step is to
    trigger AJAX request from the fileupload app to the results page.

<!-- -->

-   **2nd July (Wednesday):** Was sick due to a minor fever and
    headaches. Took medication and hope to compensate in the upcoming
    days.

<!-- -->

-   **3rd July (Thursday):** Completed the Results view I was working
    on. Here's a screenshot, for a larger version, click
    [here](http://i.imgur.com/HN3fc97.png). Next up, I have to integrate
    this with the file-upload app, so that results are shown
    automatically on file-uploads.


![](ResultsInterface.png)

-   **4th July (Friday):** Encountered a bug while integrating the
    fileupload and results module. The database changes were not
    reflected in Django ORM due to query caching. Tried flushing the
    transaction, but it didn't work, will look more into this.

<!-- -->

-   **6th July (Sunday):** Integrated the results module with
    fileupload. Now, upon uploading benchmark logs, users are shown the
    Benchmark Result immediately. Resolved the bug I was facing earlier
    my doing a configuration change in MySQL. Also, ensured database
    connections are closed after parsing the file, which was not the
    case earlier. Tried deploying the new code to the remote machine,
    but couldn't login through ssh, maybe the system was shut down.

#### Week 8

-   **7th July (Monday):** Couldn't get much work done due to a faulty
    internet connection.

<!-- -->

-   **8th July (Tuesday):** Deployed the application on the server.
    Resolved a bug related to CSRF tokens which caused file-uploads to
    stop midway. Discussed further project plans with Sean on IRC.

<!-- -->

-   **9th July (Wednesday):** Explored the feature of uploading files
    via a web POST API. I found a library django-tastypie that solves
    the issue of easily creating APIs. Went through it's documentation
    and tutorials to understand it better.

<!-- -->

-   **10th July (Thursday):** Worked on an example of POST API with
    django-tastypie. Was able to do fileuploads with an API key on the
    example. Also looked at Geekbench Benchmarks to get an understanding
    of different benchmark systems.

<!-- -->

-   **11th July (Friday):** Went through the documentation on Django
    Forms in detail. The comparisons page would require filtering from
    the database, and hence Django Forms would be useful there.

#### Week 9

-   **14th July (Monday) to 16th July(Wednesday):** My institute opened
    from Tuesday, so I had to pack my luggage and travel from my home to
    my institute on Monday. It took a day to complete the registration
    and fee payment there, and another day to fix logistics as I had to
    shift to a new accommodation.

<!-- -->

-   **17th July (Thursday):** Back to work resuming the code for the
    Comparisons module. Wrote it's further backend logic based on Django
    Forms ORM which would help to communicate with the database based on
    different filters. I will set up the demo back tomorrow and continue
    further work on the module.

<!-- -->

-   **18th July(Friday):** Completed the backend logic of the
    Comparisons view. After selecting the options, a POST request is now
    sent which returns the appropriate filtered data. The user is shown
    his VGR Rating and the Average VGR Rating among the filtered logs.
    Next up, I have to present the data in a better manner, and include
    a graph for comparison.

#### Week 10

-   **21nd July (Monday):** Almost done with the comparisons module,
    have added the filters and completed backend querying code. Here's a
    screenshot, for a larger version, click
    [here](http://i.imgur.com/BxIbmTN.png).


![](ComparisonsInterface.png)

-   **22rd July (Tuesday):** Added a Date filter to the comparisons
    view. It lets filter down logs submitted this week, this month, this
    year or at all times. Added More-Info modal dialogs which give
    detailed information of the ratings in the result and comparison
    view.

<!-- -->

-   **23th July (Wednesday):** Completed minor changes in the
    Comparisons module and started working on the POST API for file
    uploads. I am using django-tastypie which facilitates easy
    development of apis for django projects. Will host the project on
    BRLCAD's server once this module is done, which would be 2-3 days
    probably.

<!-- -->

-   **24th July (Thursday):** Continued work on the Web API for file
    uploads. Was able to send get requests via the API but POST requests
    were unsuccessful. Also, fixed a few minor bugs and redeployed the
    demo.

<!-- -->

-   **26th July (Saturday):** Worked on deploying the app to production.
    Read lots of documentation and articles on this to understand every
    bits and pieces. Set up Post Receive hooks in the remote repository
    so that it is synced with Git. Created a makefile for easy
    installation of dependencies and carry out other deployment related
    tasks. Will contact admins from the IRC channel tomorrow to set up
    the apache mod_wsgi configurations and get everything running.

<!-- -->

-   **27th July (Sunday):** Did a bunch of changes to get the production
    and development environment in proper setup and running. New
    installation instructions are now in place. Today's commits can be
    accessed here:
    <https://github.com/BRL-CAD/benchmark/commits/master>.

#### Week 11

-   **29th July (Tuesday):** Completed the Web API for file uploads.
    Now, files can be uploaded from the command line via a POST request
    such as:


*curl -F "slug=test" -F "file=@run-10644-benchmark.log"
<http://localhost:8200/upload/api/v1/picture/>*

-   **30th July (Wednesday):** In some cases the files uploaded via the
    Web api were being partially uploaded. Added a deserializer method
    to take care about of that. Also refractored the api code.

<!-- -->

-   **31st July (Thursday):** Refactored some of the code, and did some
    mockups of Live feed for the benchmark home page.

<!-- -->

-   **1st August (Friday):** Looked into automatic uploading of logs
    from the benchmark script. I am able to make file uploads from the
    script, but need to find a way to make it fault tolerant. I tried a
    few suggestions mentioned on SO but they were not completely solving
    the issue. Will dig into this further.

<!-- -->

-   **3rd August (Sunday):** Checking off things from the TODO. Made the
    social media sharing icons work. Fixed some of the broken links in
    the navbar. Started working on the home page and file archiving, had
    a few doubts regarding them, so sent a mail to the mailing list.

#### Week 12

-   **4th August (Monday):** Started work on the homepage created a few
    mockups and continued code-refactoring. Awaiting response from the
    mailing list about my questions.

<!-- -->

-   **5th August (Tuesday):** Found the solution to the file archiving
    issue. The recommended way is to organize files in yy/mm/dd
    directories so that they are searchable by date and less number of
    files in a directory would also significantly improve performance.
    Started implementing the home page mockup, refactored some code in
    the results page.

<!-- -->

-   **6th August (Wednesday):** After experimenting with different
    designs, settled down on the landing page. I have implemented the
    mockup, below is a screenshot.


<img src="BenchmarkHome.png" title="fig:BenchmarkHome.png" width="700" alt="BenchmarkHome.png" />

-   **7th August (Thursday):** Pushed the site to deployment after
    enabling the site in apache, it is now live again at
    <http://202.164.53.122/benchmark/>. Tested the site across multiple
    platforms, resolved most of the UI fixes. There is a top margin
    issue that's left to be resolved. Will work on the file archiving
    issue tomorrow.

<!-- -->

-   **8th August (Friday):** Implemented file-archiving, the files are
    now segmented across separate directories for each month. This
    ensures they are easily searchable and also significantly improves
    the speed of the app.

#### Week 13

-   **11th August (Monday):** Wrote the structure for application feed.
    The feed would list out all the recently uploaded log files with
    links to results page for each. I have to plug in the ORM statements
    to make it working.

<!-- -->

-   **12th August (Tuesday):** Modified the production setup to use
    virtualenvs as this was causing the other projects to come down.
    This included a different make configuration and changes to the WSGI
    file. The setup was also moved from /var/www to
    /home/benchmark/deployment. The aliases were configured accordingly

<!-- -->

-   **13th August (Wednesday):** Wrote a view that lists out the most
    recently uploaded logs by listening to the database for newly
    uploaded logs. This can be merged with the homepage later.

<!-- -->

-   **14th August (Thursday):** Worked on the script to extract logs
    submitted via email. Leveraging some part of the work that was done
    by Suryajith. The IMAP library has limited support now but the
    script works, tried to port this into the new library by GMail.

<!-- -->

-   **15th August (Friday):** Completed the port of the script to
    extract email logs. Improved parser scripts to remove hardcoded
    variables, and use project settings instead.

<!-- -->

-   **16th August (Saturday):** Improved inline documentation in the
    results and fileupload module. Resolved the issue of navbar
    responsiveness on iPad. Few other UI tweaks along the way.

<!-- -->

-   **18th August (Monday):** My lab had a visit from Prof. Khosla, the
    Chancellor of UCSD. I was busy preparing a presentation regarding
    the same and then giving a talk on the current ongoing research in
    the lab.

<!-- -->

-   **19th August (Tuesday):** Wrapped up everything and submitted the
    final evaluation. The whole experience was great and I can
    definitely say GSoC was one of the best things I have ever done.
    Thanks to Prof. Rai and Sean for being so helpful along the way.
