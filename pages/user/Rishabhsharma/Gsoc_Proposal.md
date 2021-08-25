# Personal Information

**Name** - Rishabh Sharma

**E-mail address** - rishabh.bits038@gmail.com

## Background Information

I am a third year computer science undergraduate student from Birla
Institute of Technology and Science, Pilani (India). I’m a passionate
web developer and an equally enthusiastic 3D Animator.

I’ve a fair bit of experience with programming 3D graphics in OpenGL ,
as well as implementing it for the web ( Web-GL using three.js ). I was
involved in programming the first 3D website of any college festival in
India for Apogee, the annual technical festival of BITS Pilani
(http://bits-apogee.org/2014/). I’ve also done a lot of modelling and
animation in Autodesk Maya, something that required that required
dealing with a lot of file formats for different kinds of models, meshes
, nurbs etc.

As a part of academic, study and personal projects in my college, I have
implemented node.js replacing prior implementations of databases in PHP
and Django. I’ve also implemented Django at many different scales for
the websites of my college festivals. Some of these were simple, nothing
more than a couple of models, with a few views. Some were complex , with
individual dashboards and profiles for about 4000 users , each having
features like Google/Facebook connectivity , Easy upload of user info ,
photos , videos and pdf’s , automatic emailing for updates , and
tracking the history of user actions.

# Project Information

## Project Title

Server-side implementation of Online Geometry Viewer using Node.js and
improving the client side interface for better user experience.

## Brief project summary

OGV is an online viewer for BRL-CAD’s geometry files which enables the
user to view files without having BRL-CAD installed. OGV currently uses
PHP on the server side. Since, OGV needs a more powerful, scalable and
robust backend, I propose to replace the existing backend in PHP with
node.js. In my opinion, a framework like express.js will be perfect for
a web application like OGV, simply due to the massive community support
behind it, and easy and logical bug testing. To complement express.js,
MongoDB, can be efficiently utilized to handle databases, due to the
JSON style dynamic schemas provided , that offer simplicity and power.

These is also a HUGE scope of improvement in the current version of OGV.
I've discussed my views and ideas on providing an interface for better
user experience of OGV as a web application.

## Detailed project description

### Tools to be used

**Express.js as the framework**

There are many options available for frameworks with node.js. However,
for the proposed OGV web application, express.js is the perfect tool. It
has a massive community backing it up, hence support and bug testing is
easier. Also, it provides a lot of HTTP utility methods and connect
middlewares, that help a lot in creating robust , scalable and
interactive web applications.

**MongoDB as the database**

I propose using MongoDB as the primary database for the viewer. MongoDB
is the leading no-sql database that allows schemas to change quickly as
applications evolve, providing the user all the functionality of a
traditional database. MongoDB is built for scalibility, performance and
high availability, scaling from single server deployments to large,
complex multi-site architectures, something that will greatly help the
viewer.

**LuMongo for real time search**

LuMongo is a real time distributed search system. LuMongo is the perfect
open source system for implementing the proposed Universal Search
feature ( user and model search) . It provides flexibility and powerful
search, and complements the scalability that MongoDB provides. It
intelligently leverages Mongodb, and provides faster real time search ,
as compared to the sluggish “query” search of Mongodb.

**Three.js for the client side**

Following the current implementation of OGV in three.js, I’ll be using
the library to add a lot more functionality to the client side. Features
like model editing ( lighting and texturing) , viewcube and the proposed
four screen view can be implemented using the Light and Camera classes.
I’ll also be fixing a few bugs in the Zoom feature. This aims at
improving the user experience of the viewer.

### Server Side

The current backend of OGV is written in PHP. We need a more powerful,
scalable and robust framework at the server side to handle the proposed
functionalities and features. I propose replacing the existing PHP
backend with a more robust and more importantly, scalable backend ,
using node.js.

#### Why node.js ?

Javascript on the server is Node’s biggest advantage. It is a lot easier
for the developer to write and understand the code without switching
languages for the front and the back end. It also makes it easier for a
developer to work on both the client and server side. Node is fast. It
being asynchronous, has less database I/O delays. Also, the javascript
interpreter V8 is very fast which makes javascript much faster on the
web.

### Proposed Features

**Facebook/Google Connect**

The user would be provided an option of logging into the OGV through his
Google or Facebook account. There would also be options to share the
models on social networking sites like Google plus and Facebook. We
could also integrate OGV with the Facebook Application API, and develop
a Facebook application for the same (optional). I've submitted a patch
for Facebook login to OGV in PHP(
<http://sourceforge.net/p/brlcad/patches/260/> ).

**Creating a User Dashboard**

As discussed in the mailing list, a user dashboard needs to be created
wherein a user can see the history of models viewed, bookmark models of
his choice and save his work for further use. The dashboard will allow
the user to edit his profile and update his location, educational
qualifications, work experience and contact details and the user will
have an option to share this information with other users or keep it
private.

**Privacy Settings**

The application will allow users to decide the privacy settings for
their profiles, and the models that they upload. These settings can be
varied for individual models as well. These settings will be enforced on
every registered user viewing his profile. There will also be an option
of deciding the “Public Privacy Settings”, that will be enforced on
unregistered users.

**Universal Search**

The application will feature a Universal Search, that will allow the
user to search for other useher users and models. It will be implemented
using LuMongo, a real-time search system , for MongoDB.

**Stats**

The application will also feature a Stats page on the dashboard. It will
provide detailed statistics such as views/downloads per day, per week.
It will also provide a graphical display of the statistics, and will
have a feature of sorting the stats from an initial and final date.

**Follow Feature**

This feature will allow the users to Follow their favourite users, and
even models. The application will provides feeds and updates of the
users followed. The user will also be provided with email updates.

**Option to store, share, download, rate, comment and like models**

•The users would be provided an option to upload their work on the cloud
and a database of all such objects would be maintained from where the
users can download and upload their models.

•There would be an option to search the models and the output of each
query could be filtered on various parameters including name, rating,
download and latest.

•Each user would be provided an option to share his work with his
friends/colleagues much like documents are shared on Google drive and
Dropbox.

**Tag Feature**

The user will be able to tag their work for easier browsing by other
users. This would also improve the search feature of the website.

**Timeline feature**

A user can create a timeline and edit it to track the progress of his
project.

**Compatibility with other file formats**

The application will be compatible with other common file formats
including .max, .3ds, .3dm, .mb. The user can upload and convert any of
these to .obj and store it on his dashboard.

### Client Side/Front End

I’ve worked on the very first 3D website of any college festival in
India ( <http://bits-apogee.org/2014/> ) . It involved implementing
camera animation , lighting , model import , texturing and dynamic
editing of model attributes ( such as texture changing ) . I’ve proposed
similar features to be implemented in the client side of the application
, which would improve the user experience immensely.

**Zoom feature**

The current navigation of the model on the browser needs to improve. I
will fix the bugs and smoothen the zoom in /zoom out function.

**Implement a View Cube**

A view cube will be implemented on the top right to change the screen
view as per user’s requirements. The implementation is fairly
straightforward, and it’s rotation will be linked to the universal
rotation function of the current viewer.

**Four View Screen**

The feature would split the screen into four quadrants showing the top,
front, side and perspective views. The changes made in one quadrant
would be reflected in all the other quadrants. The Camera class of
three.js can be utilized to render views from the top, front , side and
perspective angles.

**Basic Model Editing**

Basic options to edit the model including material, lighting and camera
settings would be given to the user. We will use the Lights and Texture
classes provided by three.js for applying a custom texture and Lights to
the scene.

**Snapshot Feature**

The user can take a snapshot of his current screen view, save it on his
computer or upload/share it on popular social networking sites like
Facebook, Twitter, Instagram.

# Deliverables

-   Server side implementation using node.js, replacing the current PHP
    backend for the application.
-   Implementing the aforementioned features at the server side and
    setting up a robust backend for the application.
-   Implementing the proposed features in the client side to improve the
    user experience drastically.
-   Documenting the application.

# Proposed Timeline

-   **April 21 to May 19 ( 4 Weeks , Community Bonding Period)**
    -   Discuss the project outline and proposed implementation with the
        community.
    -   Work on a deployment strategy and setting up the development
        environment.
    -   Start rewriting the existing PHP code in node.js.
    -   Get to know more about the community requirements and
        constraints.

<!-- -->

-   **May 20 to June 3 ( 2 Weeks )**
    -   Implement a basic user dashboard with a login feature.
    -   Implement the user profile and create databases to store user
        information like Name, Contact info etc.
    -   Add a updates feed to the home screen.
    -   Implement the Timeline feature that captures user action
        history.

<!-- -->

-   **June 4 to June 19 ( 2 Weeks )**
    -   Implementing core functionalities like upload, and download of
        models.
    -   Implementing tagging of models to facilitate better search.
    -   Creating databases for storing the models and indexing them.

<!-- -->

-   **June 20 to July 4 ( 2 Weeks )**
    -   Setting up LuMongo to implement searching of users and models.
        Study it’s performance and enhance it wherever possible.
    -   Implementing Stats for profiles. Also, implementing a graphical
        display for stats.

<!-- -->

-   **July 5 - July 12 ( 1 Weeks )**
    -   Work on implementation of the central database where the users
        can download the models, upload them, rate and comment on the
        existing ones.

<!-- -->

-   **July 13 to July 20 ( 1 Weeks)**
    -   Implementing Facebook and Google login for the dashboard.
    -   Adding the follow feature to the application
    -   Finishing the dashboard and testing for bugs.

<!-- -->

-   **July 21 to August 3 ( 2 Weeks)**
    -   Implementing the viewcube utility for the client end of the
        application.
    -   Implementing the four view feature using three.js
    -   Adding basic model editing ( textures and lighting) to the
        application.
    -   Fixing bugs in the current implementation of the viewer.
    -   Implementing the snapshot feature.

<!-- -->

-   **August 4 to August 18 ( 2 Weeks)**
    -   Finishing off a stable version of the application.
    -   Documenting the progress and the code.
    -   Community feedback and Bug Testing.

# Time availability

During the phase of this project, I’ll be having summer vacations and
will be available for almost the entire day. I’m confident that I’ll be
able to devote 40-50 Hours a week for my project.

Preferable timings:

Time Zone: UTC +5:30 (Indian Standard Time)

Timings: 8:00 A.M. to 2:00 A.M.

# Why BRL-CAD?

I chose BRL-CAD because it best suits my interests. Developing intuitive
and flexible real time web applications has always been my passion. That
coupled with my enthusiasm for 3D Programming and Modelling, I believe
is the reason for my interest in spending my summers pushing code for
the OGV. BRL-CAD being one of the largest open source organizations with
over 30 years of development history, provides a platform for budding
programmers like me to bring their innovative ideas to life.

# Why me?

I’m currently pursuing my undergraduate studies in Computer Science from
the Birla Institute of Technology and Science, Pilani. I was among the
top 15 people joining the college for undergraduate programs. That aside
, I’ve had a keen interest in 3D programming as well as web application
development , and I’ve pursued that interest with passion since the last
3 years.

Here are a few points illustrating my proficiency with web development
and 3D programming.

-   I am the Coordinator of the Department of Visual Media in BITS
    Pilani. The Department is a group of talented, hard working and
    motivated people working in the fields of development, animation and
    design for the festivals of BITS Pilani. My work primarily involved
    developing and managing the server side for all the websites, and
    web application development to suit the different needs of the
    festivals. I was also involved in 3D Modelling and Animation, and
    have been involved in providing assets and animation for the
    promotional videos for the fests.
-   I was involved in the development of a Django backend for 4000 users
    that had features like - Profiles for users , Google/Facebook
    connectivity , Uploading photos , videos and pdf’s , automatic
    emailing of updates , history tracking and more.
-   I was involved in the development of a 3D website for BITS Apogee
    2014, the annual technical festival of India . It involved using
    three.js for importing and editing 3D Assets. It featured dynamic
    model and camera animation.

URL - <http://bits-apogee.org/2014/>

-   I’ve been involved implementing Node.js for various study, academic
    and personal projects. I’m also currently replacing my Django
    implementation of the backend for our festival websites with Node. I
    have a fair bit of experience with different frameworks and
    databases for the web - like Express.js, Mongodb , Socket.io etc.