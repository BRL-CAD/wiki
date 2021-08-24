# Online Geometry Viewer Project Proposal

## Personal Information

**Name:** Inderpreet Singh

**Email Address:** indrplus@gmail.com , singhs.ishwer@gmail.com

**IRC Username:** Ishwerdas

### Background Information

I study in 4th year B.Tech (Computer Science and Engineering) at Guru
Nanak Dev Engineering College, Ludhiana (India). I was introduced to
this community about a year ago and have tried to help with whatever I
could. I can write in C++, PHP, Python, Javascript.

## Project Information

### Project Vision

When we built our initial HTML web pages in 90s we din't have an <img>
tag. Just a few years back Video was a foreign element added via third
party plugins. Today images,videos and audio all have become first class
citizens of the web. HTML 5 has introduced many new members to the
family. Canvas, WebGL and SVG being few of them. These technologies
allow us to manipulate and access 2d and 3d graphics right in the
browser. Today we have incredible power in our hands when it comes to
handling graphics on web. Even with technologies like WebGL, 3D graphics
have not yet become a part of our daily web experience. I believe in OGV
as one of those platforms that will make sharing 3D models on the web as
normal as sharing videos on youtube or images on flickr.

### Brief Summary

Online Geometry Viewer started as a GSoC 2013 project by Harmanpreet
Singh. It's an online 3D geometry viewer that works on WebGL using
three.js. It uses vanilla PHP on server side whereas jQuery and
Bootstrap on the front-end. To give it a robust foundation, the
community discussed about changing it's backend to something more
powerful. I took an active part in that discussion and the community
ended up with choosing node.js as a replacement for the current PHP
based backend. After looking at various frameworks I decided to go for
[meteor](https://www.meteor.com/). Reason for this choice is that meteor
has a comparatively larger community which means more support, bugs are
removed quickly and more code to learn from. So first step would be
porting the current app to node js after that we can improve on previous
features and add new features. I have prepared a list of improvements
and features that I will add to OGV this summer.

**Things that I will Improve on: -**

-   The way data is handled about models. (Currently GET method is used)
-   The way errors are given. (Many of the errors are not given at all)
-   The way Authentication is done (Will be handled by meteor now)
-   Installation and Configuration
-   User Experience and User Interface

**The features that I will add: -**

-   Dashboard (admin and non-admin)
-   Sharing & Embedding Feature
-   Image alternatives for 3D Models (Requested by Mediawiki)
-   More Geometry conversions.

## Detailed Project Description

As it's clear from the previous section the project is divided into
three parts

-   Porting OGV to nodejs (meteor)
-   Improving the old and removing the bugs
-   Adding New features

### Porting OGV to node.js

We have made a choice to move to node.js. Then there's a choice to be
made among various kinds of frameworks, and then various frameworks in
each kind. We decided to go with Full Stack frameworks like derby or
meteor. I decided to choose meteor over others because it has a larger
community i.e used and tested by more people as compared to others like
derbyjs.

So My first task would be to replace each module of OGV to meteor. I
have written about the details for each module in the sections below.
Third party libraries in meteor can be added by writing packages for
them. So one of the important tasks will be to either write a package or
use existing package of three.js

### Improvements in OGV

After we have a sound foundation with node.js, now we can concentrate on
improving the existing OGV features.

#### Models Data Handling

Currently in upload_file.php, a list of names of obj files is sent to
model_display.php using GET method. We can send a very limited amount
of data through Get method. Larger models fail to get loaded because of
this limit. It's just an array of file names so I will use HTML5 local
storage to store this array locally on the client and fetch it again
from there.

This will remove the bug and also add all the speed and benefits that
come by storing data locally. Few older browsers do not support local
storage so for them we can use a polyfill such as [amplify
amplify.js](http://amplifyjs.com/api/store/). Fortunately meteor has a
package called [amplify](http://docs.meteor.com/#amplify), that does
exactly the same thing.

#### Errors

No matter how much we hate errors, they are very important to the user.
They tell something is wrong and they contain information about solving
itself. Can they be any nicer?

Currently at some places errors are not given to user at all and at
other places errors are not that explanatory. For example there is no
error given if the user account folder is deleted, neither a remedy is
taken to create the user folder again. Just the models are not displayed
in model_display.php without any error or any indication of something
that has gone very wrong behind the walls.

Then there's a case with configuration errors, if say mged path is wrong
then there's a small error in the sidebar of the model_display.php.
Which is not clear and also gives no cue to user about how to solve that
error.

For other errors like mysql credentials, I believe bootstrap's alert
class needs to be used, so that it looks like an error. It's half of a
UX problem and half of the functionality problem. For configuration
errors, I have submitted a patch to the official github repository.

#### Auth Module

As also stated in To do list of OGV, current Auth system is not that
secure and lacks robustness. Meteor has it's own robust authentication
system. Secondly, current auth system does not have user roles but we
need at-least two kinds of users, admin and non-admin. Admin user must
be able to edit configuration files, add remove accounts etc, whereas
non-admin can not do such tasks. Following features of meteor are going
to help me with this

-   [connection.allow](http://docs.meteor.com/#allow) for providing user
    roles.
-   [Accounts API](http://docs.meteor.com/#accounts_api) for handling
    accounts.
-   [Secure Remote Password
    Control](http://en.wikipedia.org/wiki/Secure_Remote_Password_protocol)
    Support.
-   [oAuth](http://docs.meteor.com/#meteor_loginwithexternalservice) for
    **logging in with various services such as facebook, twitter etc**.
-   The Accounts UI provided by meteor for user interface

And this all comes as one package with meteor.

#### Installation and Configuration

There's a scope of improvement in current OGV Installation, and also as
we grow we need in place some standard Installation mechanism so that
any user without any prior knowledge to any programming can Install it
easily. I am inspired from Wordpress' 5 minute installation or Anchor
CMS's 2 minute install to bring in OGV it's own easy install. I have
worked on the configuration part and submitted a patch regarding it.

#### User Experience and User Interface

I am passionate about creating good interfaces. More than eye-candiness
I care for the experience that user gets. To make things easy for the
user. Then the second part of User Interface design is about prompting
users to take actions. To make sign up buttons that no one can ignore
but click. I will use bootstrap as underlying framework which I will
edit to customize it specifically for OGV.

-   I tend to make a very clean and minimal Interface, where the whole
    focus is on the content. I have chosen flat icons, and a
    **mobile-first** interface.

![](img/Ogv_viewer.png)

-   The front page will provide users an option to Sign In/ Sign Up and
    also showcase the ability of OGV. The text abive Form is an embedded
    model from OGV. We can use any 3D model here. It showcase what OGV
    can do, not just by writing but doing it. It gives user a chance to
    play with a model, even before he signs up. I believe that will lead
    to more people signing up.

![](img/OGV_Sign_in.png)

-   When we hover on the above model, it will highlight the various
    options that user can perform without even logging in. Comments
    cannot be added but read without signing in.

![](img/Ogv_sign_in_hovered.png)

-   Sign up page is same as that of sign in page.

![](img/Ogv_sign_up_hovered.png)

-   This is how upload page may look, using dropzonejs a drag and drop
    interface for uploading files can be created.

![](img/Ogv_uploader.png)

-   I will use [Hakim.se's](http://lab.hakim.se/ladda/) in-button
    progress bar for uploading. The button itself turns into a progress
    bar showing percentage of file uploaded.

![](img/Ogv_uploading_btn.png)

-   File manager shows all the files that the user has uploaded at one
    place. Clicking on these files take the user to full screen viewer.

![](img/Ogv_file_manager.png)

These are just the early rough mockups and not the exact design so it's
not pixel perfect. I try to make pixel perfect designs using grids and
various design prinicples. I have also not made a mock-up for each and
every page as that would require more thought to be put into and more
feedback from community. I have a good knowledge about

-   Color Theory
-   Typography
-   Emotions in Design
-   Transitional Design
-   Responsive Design

OGV's design will follow all these principles + look great.

### New Features to be added

#### Dashboard

Currently we just have a upload button on the name of dashboard. I
propose to add a full fledged dashboard where we can see all the models
that we have previously uploaded. These dashboards will have options
depending upon what kind of user you are. Admin user will have more
options like Editing configuration files, adding/removing accounts etc.
The rough list of what a dashboard will contain is as follows.

-   A File manager, showing all your uploaded models.
-   A button to upload your models.
-   Option to edit your profile.
-   View your profile (will contain feed of models you shared)
-   Edit Configuration file / app settings. (Admin Only)
-   Edit, Add or Remove Accounts (Admin Only)

#### File Manager

File uploading is a little tricky part with meteor. Firstly, meteor does
not have any ready-made built-in solution as such for file management
(way it has for authentication). I have looked across some packages for
meteor js that can be tried, tested and customized to feed our needs.

-   [Dropzonejs](https://atmosphere.meteor.com/package/Dropzonejs)
-   [CollectionFS](https://github.com/CollectionFS/Meteor-CollectionFS)

#### Sharing and Embedding

Social element in OGV is I guess the most exciting part of OGV. The
ability to like other's models and share them among users. To share them
on social network websites and have an embed code that can be used on
any website. I would like to add following Social Features in OGV:-

-   Like
-   Share
    -   Share on Profile
    -   Share with unique URL
-   Embed code

Likes and shares can be stored in database for each model. A unique URL
is already being generated for each model, we just need to provide a way
to share it. Embed code can be generated from this unique URL.

#### Image Alternative

When I talked about Online Geometry Viewer on mediawiki mailing list
they were kind enough to share their views and the features they would
like for the extension. One of those features was to have an image
alternative for each model. We can use earlier described File Manager
packages to either make user upload an image or another approach can be,
if once loaded on any client we can use .toDataURL() method of canvas to
get image from canvas or a combination of both.

## Milestones

-   Community Bonding Period
    -   Get more user requirements
    -   Start initial movement from PHP to meteor.
    -   Lots of healthy discussions about choices to be made.

<!-- -->

-   **WEEK 1 (19th May)**

Work on Authentication Module with Nodejs (meteor)

-   **WEEK 2 (26th May)**

Port File Uploading to Nodejs (meteor)

-   **WEEK 3 (2nd June)**

Write a File manager so that users can see old files and view them.

-   **WEEK 4 (9th June)**

Start working on model display part with three.js aka work on using
three.js along with meteor.

-   **WEEK 5 (16th June)**

Continue working on display part, Handling models data, Saving data for
later view.

-   **WEEK 6 (23rd June)**

Make Viewer ready by making app call mged commands and geometry
conversion commands on the server.

MID TERM EVALUATION

-   **WEEK 7 (30 June)**

Make Dashboard for users and admins

-   **WEEK 8 (7th July)**

Allow users to embed models in their websites.

-   **WEEK 9 (14th July)**

Allow share and like on models

-   **WEEK 10 (21st July)**

Revisit Dashboard to show user's Shares and Likes

-   **WEEK 11 (28th July)**

Automate Installation and Configuration of the app.

-   **WEEK 12 (4th Aug)**

Test the working , check bugs, Clean the code.

-   **WEEK 13 (11th Aug)**

More testing, Check errors in Documentation.

-   **WEEK 14 (18 Aug)**

FINAL EVALUATION

## My Preparation

-   I have been collecting user requirements for long. I also approached
    mediawiki community to ask their views.
-   I have read and understood the code of current OGV. I have also
    pointed out some bugs and limitations. (In this proposal itself)
-   I have submitted few small patches to the repository and will submit
    more to show that I have read and understood the code.
-   I have explored the framework of my choice, figured out what modules
    of meteor I'll need and use. (shared them above)
-   I also try to communicate as much as possible in the community on
    mailing lists and IRC.

## Why BRL-CAD?

I have been in this community for a year. I have always been encouraged
here to share Ideas without hesitation and other community members have
helped me even If I ask or do something stupid. I love the openness one
gets in this community and I have lots of friends here.

## Why Me?

-   I am open to Ideas, I don't stick with tools but tasks.
-   I have read and understood the OGV code and given patches and
    bringing more of them.
-   I have tried communicating as much as I can in mailing lists and
    IRC.
-   I have and will try to help others as much as I could.
-   I have planned to work on OGV even after GSoC.

## References

-   [nodejs frameworks](http://nodeframework.com/)
-   [meteor.com](http://docs.meteor.com/)
-   [Production Ready Meteor
    Apps](https://www.meteor.com/blog/2013/11/21/meteor-devshop-9-tech-talks-production-ready-meteor-apps-understanding-the-event-loop-async-and-fibers)
