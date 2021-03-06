Below is a list of potential development activities remaining for the
geometry service. No single task should take more than a month of effort
to implement.

# GSoC 2016 Task List

**github branch structure (proposed)**
developer branch - <name>_dev
release branch (brlcad) - release
master branch (mentor) - master

Product release at the end of midterm and final term (official)
Merge student branch at every product release
{\| ! Task status \|- \| style="background:\#FFC7CA;"\| Not Done \|- \|
style="background:\#FAF8C5;"\| In Progress \|}

|                    |                          |                                                                             |          |
|--------------------|--------------------------|-----------------------------------------------------------------------------|----------|
|                    | Tag                      | Short Description                                                           | Priority |
| Community Bonding  | Pub-Sub                  | Learn in-depth about publication and subscription, on which meteor is based |          |
|                    | Add color                | brlcad code and API to add color parameters from g to obj file              |          |
| Initial            | Code Integration         | Merge and clean code from GSOC15-merged to master, remove branches          | P0       |
|                    | Deployment               | Deploy initally the update master branch. Do not make it public             | P0       |
|                    | Refactor Database        | Only where needed                                                           | P0       |
| Social Integration | Like, Share, Comment     | UI/UX Improvement                                                           | P0       |
|                    | Following users          | Primarily UX related issues                                                 | P0       |
|                    | Dashboard                | UI improvement and database query issues                                    | P0       |
|                    | Notifications            | User must get notified of things                                            | P1       |
| Model Lifecycle    | Publish Control          | User can keep data private or publish it publically                         | P0       |
| View Models        | Large files\*            | Laptop freezes, unable to finish the conversion                             | P0       |
|                    | UI/UX                    | Improve user experience at view model page                                  | P0       |
|                    | Thumbnails\*             | Thumbnail generation from the model view itself (phantomJS)                 | P1       |
|                    | Manage views             | Look for other technologies or improve existing (datGUI)                    | P1       |
|                    | Enable color\*           | Enable upload of models with color parameters                               | P0       |
| Admin Panel        | User Tables              | All data and navigation                                                     | P2       |
|                    | Push Notifications       | The ability to notify users via mail, or web-app notification               | P1       |
|                    | Blog or news page        | News and blog updates by brlcad admin                                       | P2       |
| User               | Temporary User           | Upload and view your Models without sign-in                                 | P1       |
| Security           | Publication/Subscription | Check safe publication-subscription workflow                                | P2       |


\* High priority hard level problems to look at.

\# P0 tasks - 10

\# P1 tasks - 5

\# P2 tasks - 3

# New Features


**User Dashboard**

<!-- -->



Currently, OGV is lacking an important feature of user dashboard. At
present user cannot see his previously uploaded files. We need to design
the workspace for user where he can add, delete and share files among
developers, recent activity etc. Just like Google drive or cloud service
he should be able to create folders, categorize files according to
project(s) and much more.

<span style="color:red">**update**</span>- User can see his previously
uploaded files, and even the files uploaded by the user he follows.
There are some UI/UX issues but the backend development is complete.

<!-- -->


Inspiration:

-   <https://360.autodesk.com/> (Create your account)
-   <http://www.youtube.com/watch?v=aXklwQ8OFY8>


**Model Sharing and embedding**

<!-- -->



Share option of OGV can be extended such that user could embed his
models on their websites, blogs and social websites as discussed in
recent mails.

<span style="color:red">**update**</span>- iframes are available and is
functional at the backend level, but is buggy. The navbar, notification
div, datGUI div and other icons also come in the iframe. This needs to
be fixed. Only the div that consists of the model needs to get embedded.

<!-- -->


**Comments on model**

<!-- -->



A feature to enable users to comment on their own and shared models.
This would help a lot in collaborating viewing, and after some time,
collaborative editing. Even we can add chat for easy experience.

<span style="color:red">**update**</span>- Likes and comments have been
added to the models in online geometry viewer

<!-- -->


**BRL-CAD viewer: Mobile App**

<!-- -->



For ideas for BRL-CAD viewer mobile app:
<http://www.youtube.com/watch?v=Cy7kENzHzao#t=35>

<span style="color:red">**update**</span>- Meteor as a framework is
mobile-friendly, therefore it is easy to reproduce it to mobile devices.
There is a need to check for responsiveness in recently created/changed
pages (newsfeed, profile page, model viewer page etc.)

<!-- -->


**Options to change colours of model**

<!-- -->



Currently a model got a random default color when loaded in ThreeJS and
user has not control to change it. There should some color options for
user to play with.

<!-- -->



Reference::

-   <http://workshop.chromeexperiments.com/examples/gui/#1--Basic-Usage>
-   <http://davidwalsh.name/dat-gui>



<span style="color:red">**update**</span>- datGUI has been integrated
with OGV with options like ambient, emissive, wireframe, opacity,
transparent, shininess and a few others. This can be expanded to add
colors to specific layers of the uploaded model, which becomes a hard
problem - low priority problem. There is a need to add the colors from
the parent g file to the converted obj file.

<!-- -->


**Login through Google, Facebook, Twitter**

<!-- -->



Enabling users to login with their already existing accounts on above
sites.

<span style="color:red">**update**</span>- Done

<!-- -->


**Realistic models**

<!-- -->



Exporting material, color, lightening and other information from .g file
and use it to give realistic look to models in ThreeJS.

<span style="color:red">**update**</span>- This has been done using
ThreeJS and datGUI.

<!-- -->


**Cross section view**

<!-- -->



A feature to allow CAD users to see the cross section of the model.

<span style="color:red">**update**</span>- cross section view has not
been implemented and how it needs to be done is yet to be decided.

# Enhancements


**Use of framework**

<!-- -->



As the issue was raised in recent mails, OGV needs framework for more
robust infrastructure. Frameworks provide inbuilt facilities such as
authentication module, validations, testing etc., also they save
significant time and efforts. Laravel and node.js were proposed during
discussions but you can propose another one if you feel it is more
suitable for this project.

<span style="color:red">**update**</span>- OGV has been developed using
the Meteor Framework.

<!-- -->


**Security of application**

<!-- -->



OGV is using simple sign-in signup module but it is not much secure and
lack robustness which need a fix. It is using swift mailer library for
email sending. If we adopt some framework for this project, it can be
easily done.

<span style="color:red">**update**</span>- Handled by the use of Meteor
framework.

<!-- -->


**Add prefix to obj files**

<!-- -->



All obj files of different .g files are stored in same directory and
conflicts may occur when if two OBJs from different .g files have same
name. It can be fixed by editing code so that each time when obj
created, a prefix of its database is added to its name.

<span style="color:red">**update**</span>- All the object files are
identified by a unique ID in the mongo Database.

<!-- -->


**Loader indication**

<!-- -->



While entity loads, some indication / status about "loading" should
appear. ???If entity loaded successfully, a confirmation message should be
given to user and if entity already loaded, a user friendly message
should be displayed otherwise if error occurred appropriate message
should be given with instruction to take further steps.

<span style="color:red">**update**</span>- A loader is required to
indicate that the object is being converted. Until the object is fully
converted, the user must not proceed further. Confirmation messages have
been added. Minimal changes needed in the alert messages.

<!-- -->


**OBJ search**

<!-- -->



Before drawing an entity, a search should be made in 'obj' directory of
corresponding user to check whether the required obj file is already
made. If file found, it should be loaded, otherwise new should be
generated.

<span style="color:red">**update**</span>- One can search uploaded
object files from the entire object database. This has been implemented.
Additionally, search for users (by username) was also been added.

<!-- -->


**Set focus**

<!-- -->



At present position of camera is fixed and sometimes size of entity is
too small or too big. In either case, user have to find it by zoom-in /
zoom-out. As soon as the entity is drawn, it should always in the focus
of the camera. Either the position of camera should be adjustable
according to size of entity or there must be option of scaling.

<span style="color:red">**update**</span>- Has been completed more or
less. The model viewer page needs a considerable amount of changes in
UI/UX.

<!-- -->


**Configuration form**

<!-- -->



A global configuration file is made to set different variables. User can
change value of variables in that configuration file rather than editing
individual files. Now this file should be written through a web form.

<span style="color:red">**update**</span>- A configuration form for
models was implemented.

<!-- -->


**GUI**

<!-- -->



OGV needs better GUI. Simple and clean rich of features. Use of buttons,
icons, menus, radio buttons, drop down lists to make it easier for users
to find the functions they want. Principles of GUI design must be
considered during planing and implementing phase. Look at following
services for ideas:

<span style="color:red">**update**</span>- This is one of the most
important areas of focus for Online Geometry Viewer. The work regarding
this is incomplete at many levels. One must also need to check the
overall user experience at all levels (login, uploading, viewing, social
collaboration etc.).

|                          |                                  |
|--------------------------|----------------------------------|
| AutoCAD 360 Beta:        | <http://app.autocad360.com>      |
| GrabCAD:                 | <http://www.grabcad.com/library> |
| Revizto:                 | <http://www.revizto.com>         |
| Sunglass.io:             | <http://www.sunglass.io>         |
| TeamPlatform:            | <http://www.teamplatform.com>    |
| TftLabs' Json3d Gallery: | <http://json3d.tftlabs.com>      |
| TinkerCAD:               | <http://www.tinkercad.com>       |

# Bugs

-   Data from upload_file.php is transferred to model_display.php
    through URL by GET method of PHP. When the length of GET method is
    exceeded by a certain limit, OGV stops. It happens mostly in the
    case of large models. We need a reliable method for transfer of data
    to resolve this serious issue.


<span style="color:red">**update**</span>- This is also a primary area
of focus at the present moment. There are quite a decent number of
features that have gone in OGV, but needs bug-fixes. Bug-fixes is a more
important issue as compared to introducing enhancements.

# Research work

-   More smoothness of model.
-   Representation type. Changing ploygons to something more reliable
    and robust.
-   Making 2D drawings and annotations in OGV. We can use 3D model data
    to produce 2D drawings. However, for this we may need to use third
    party library. For example,
    [Two.js](http://jonobr1.github.io/two.js/)
-   Performing analysis in OGV with ThreeJS.
-   Continue...

# Future plans

-   Writing an API to use BRL-CAD's existing code in OGV.
-   Support for other CAD formats.
-   Continue...

If you're interested in getting involved, please join the [brlcad-devel
mailing list](../Mailing_Lists.md) and introduce yourself.
