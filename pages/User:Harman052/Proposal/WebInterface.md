# GSoC 2013 Project Proposal: Web Interface of BRL-CAD

## Personal Information

**Name:** Harmanpreet Singh

**Email Address:** harman052@gmail.com

**IRC Username:** harmanpreet

**Brief Background Information:**

Final year B.Tech student of Computer Science and Engineering at Guru
Nanak Dev

Engineering College, Ludhiana, India.

Google Code-In 2012 mentor with BRL-CAD.

**Phone number:** +91 998 877 1252

## Brief Summary

This project aims at making a web interface of BRL-CAD, means shifting
all features and functionality of desktop software to browser. Although,
the scope of this project is much wider, but for current GSoC project,
we are implementing it as a basic concept, enabling the user to access
BRL-CAD from anywhere through the web, perform basic operations and
finally obtain the output in desired way (.g, .raytraced image) itself
on the browser. This way, we are extending BRL-CAD’s capability to
mobile users hence helping to reach more users, without any need for
download and installation. Hence, this web interface of BRL-CAD is
adding another dimension in the improvement for its ease of use.

## Why this project?

BRL-CAD is a desktop application. Everything from desktop is ultimately
shifting to the web. Cloud computing is example. It is very popular and
has high demand among business houses and normal user nowadays. Main
reasons behind this are ease of access and readily available services
for 24x7. With the advancement of web and web based applications, it has
become a preferred way to do things. For example, Google's almost every
service is web based with ease of collaboration and sharing with no
overheads involved on the part of user.

There are numerous excellent examples that prove the power of today's
web and craze among people doing such things. Here are some mind blowing
examples: <http://threejs.org/>. By looking at current trend, this craze
will increase in coming future and browser will dominate over desktop.

Moving in the same direction I am proposing the project of web interface
of BRL-CAD that will deliver a more reliable, user friendly experience
with very basic, yet important feature of platform independent being
readily accessible for 24 hours.

## Detailed Summary

### Overview

This project has two ends: Front end and Back end. User will make model
on the browser (front end) and his inputs will be written as BRL-CAD
commands in a shell script. When model completes, on submission, the
shell script will be executed and processed by BRL-CAD at back end and
return desired file (.g, .pix, .png) to the user back on browser. This
is the basic flow of the project. There are certain challenges involved
in both these ends.

### Detailed Approach

Various tools and technologies to be used to accomplish this project
while resolving the following challenges are being discussed further in
the proposal.

Challenges involved in front end are: Providing option on browser to
make primitives. Positioning. Applying boolean operations on primitives
to make complex models.

Above points are the basic tasks needed to be carried out by user while
working on BRL-CAD.

Challenges involved in back end are: Processing user inputs. Returning
desired file (end product) to user.

### Front End Approach

Let's discuss the front end part. For providing options on browser to
make primitives, this should be graphical and easy to work with.
However, it would be excellent if we make it as drag 'n' drop feature
and enabling the user to see such primitives as 3D where he can rotate
and move it, but for starting point we can make it as click 'n' click
feature having four standard views (top, left, right, bottom (and may be
isometric also)). These four different views will be captured in four
different display windows.

**Wireframe Replacement** Here user will not see any wireframe as in
BRL-CAD's graphics window. When user will come to web page, he/she will
see options to make primitive and four display windows that will be
empty at that time. When user click on any option to make primitive, he
will see 2D projections of four different views of primitive or object
in four display windows.

In other words, this projection will be just an area filled with some
default colour say grey, representing the object. Thus, when user
creates a primitive he / she will see 2D views of 3D object.

On clicking any primitive option, the user will be asked to enter input
values specific for that primitive. This input can be taken in variety
of ways, such as, on clicking, a dialog box will ask for values, or just
input boxes appear. The later seems to be more reliable and user
friendly.

For this GSoC project, we will consider only one or two basic
primitives. Other primitives can be added in the same way as these basic
ones would be added.

**Resizing:** In case, the user need to resize the object / primitive,
it can be done either by again asking for new values or a slider option
can be provided. Slider option will be more easier to use. When slider
moves, changes in each view will be visible in the display windows
simultaneously. When user satisfies with size, he click on SAVE button
to save changes.

All explained above can be implemented using webGL or HTML5 canvas. I am
sure it is capable to do much more than this. To be more specific we can
use threejs.org and scenejs.org libraries to accomplish above tasks.

**Performing Boolean Operations:** Second challenge is to perform
boolean operations on primitives to make complex models. For this we
need two primitives and need to consider their respective position. For
better user experience we will make it graphical i.e. user will be able
to place objects at any given position with mouse within the display
windows. The four standard views will help the user to place objects
accurately. Again this can be accomplish using power of open source
javascript libraries like kineticjs, threejs, scenejs etc.

Operations like 'Resize', 'Reposition', and 'Boolean Operations' will
have pair of 'EDIT' and 'SAVE' buttons. For example, if a user need to
resize a primitive, first he selects desired primitive, then clicks on
'EDIT' button, input fields specific to that primitive will appear to
accept new values or a slider appears to adjust size. When size finally
adjusted, user click on SAVE button to save changes.

Similar is the case of Repositioning and boolean operations.

To implement boolean operations, a function corresponding to each
operation (union(), subtraction(), intersection()) will be written in
programming. First let's discuss the boolean operations in BRL-CAD.

Union (u): Joins the shapes. Subtract (-): Remove volume of one shape
from another. Intersect (+): Keeps only overlapping parts of objects.

Union can combine any number of primitives, so our corresponding union
function will accept names of any number of primitives. One of the ways
to implement this is using variadic functions that accept number of
total arguments and arguments itself.

Subtraction and intersection are performed only on two primitives hence
their corresponding functions will accept names of two selected
primitives as arguments.

Now the question "How user will perform boolean operations?" is answered
in following steps:

1\. Select an operation from list of boolean operations. Selecting the
operation will enable the primitive selection mode.

2\. Since the user entered the primitive selection mode, type of
operation selected determines how many objects the user can select. If
selected operation is Union, then he / she can select as many objects as
possible and if intersection or subtraction is selected, only two
objects will be allowed to be selected. In case of subtraction, order of
primitive selection will have importance because primitive selected at
second number will be completely removed from assembly.

3\. Selection of primitives in step 2 will extract their names and will
be passed as arguments to corresponding function. This function will use
these arguments to write corresponding command in file.

### Back End Approach

BRL-CAD will be used as backend CAD engine that forms the foundation of
whole project. When user will be satisfied with the model, he click on
one of the options for example 'DOWNLOAD DATABASE FILE', 'DOWNLOAD RAW
IMAGE FILE', 'DOWNLOAD PNG FILE' to obtain results in desired form i.e.
database file (.g), raw image file format (.pix) or Portable Network
Graphics format (.png) respectively.

Remember, all inputs in the form of MGED commands are being written in
the shell script that forms the connection between frontend and backend
(also showed in figure under 'Overview' section). Recall the SGI cube
script: <http://brlcad.org/wiki/SGI_Cube> that take advantage of
scripting of MGED. Same is the case of our script.

When user choose any of the option mentioned above (further commands for
generating images will be added if option chosen for pix or png) will
trigger the script and generate model in BRL-CAD.

Hence, except MGED GUI interface, we are using complete infrastructure
of BRL-CAD through scripting.

After model generation, the desired file will be available on browser
for download.

Tools intended to be used:

Following are the links to open source javaScript 3D libraries that can
be used to implement front end of the project. <http://threejs.org/>
<http://scenejs.org/> <http://kineticjs.com/> <http://paperjs.org/>

## Milestones:

17 June - 24 June: 8 days Explore threejs and scenejs and other tools.
Try with examples and making small applications in them.

25 June - 4 July: 10 days Implement options to make primitives such as
sph and rpp, and display windows.

5 July - 11 July: 1 week Option of resizing the primitives / objects.

12 July - 19 July: 8 days Positioning of objects.

20 July - 24 July: 5 days Add option of union, subtraction and
intersection.

24 July - 25 July: 2 days Back up days, for any backlogs or any pending
tasks.

26 July - 29 July: 4 days Final go through, and preparation for mid term
evaluation.

3 August – 7 August: 5 days Option of downloading the output files.

8 August - 17 August: 15 days Fixing bugs, testing.

18 August - Start documentation (using LaTeX or any other tool
recommended) including developers documentation, user’s documentation.

Future scope of project: As mentioned in the beginning, this project has
much wider scope and will definitely expand in the near future there are
various ideas that can be implemented in the future, so I decided to
list them down here:

3D model display and editing. Connectivity with material database if
there is any possibility. Different user accounts. Model Sharing.

## Time Availability:

I will be available 40 hours / week, if needed can spend more. No
restriction of time.

## Why BRL-CAD?

BRL-CAD is software of my interest. I started interacting on BRL-CAD
developers’ mailing list from last year, where I found many helpful
friends and learned a lot, now I want to contribute my part. I want to
be involved in the development work during and after GSoC.

## Why me?

I am intensely excited to work this year in GSoC with BRL-CAD. Excited
to interact and work with BRL-CAD developers on such real world project.
I have been mentor in Google Code-In 2012 and enjoyed a lot while
contributing and mentoring to GCI students and now I wish to continue
working with this community through GSoC this year.