# Online Geometry Viewer Project Proposal

## Personal Information

**Name:** Gauravjeet Singh

**Email Address:** gaurav.ishwerdas@gmail.com

**IRC Username:** gjeet

### Brief Background Info

I study in 3rd year B.Tech (Computer Science and Engineering) at Guru
Nanak Dev Engineering College, Ludhiana (India). I was welcomed in this
community in late 2012 via Google Code In (GCI). I was a GCI 2012
student and then acted as a GCI mentor of BRL-CAD for next two
consecutive years (2013 & 2014).

I have been interested in 3D graphics from a long time. In early 2013,
after finishing up with GCI as a student, I started looking for
opportunities to work with BRL-CAD. And I ended up taking a very small
part of BRL-CAD functionality on the web, using a simple shell script
and CGI. Here's the Github repo of that app:
<https://github.com/GreatDevelopers/wBRLCAD/tree/master/general/tableModel>

Later that same year(2013), I came to know about a GSoC project called
Online Geometry Viewer. I have been an active listener about OGV
discussions since then.

Also, I have been contributing to various Meteor projects in the past
few months. These include

-   Lord Byron: A real-time text editor that checks for grammar using
    Natural Language Processing.
-   Blocks: Application for making presentations and static websites

My experience in meteor and interest in 3D graphics makes OGV a perfect
project for me.

## Project Information

### Brief Summary

OGV has the ambition to become something of an Instagram for 3D models.
It includes features like profiles, likes, comments, followers. But the
code is a lot buggy and unstable.

**What has been done** As previously stated Online Geometry Viewer
started as a GSoC project in 2013 by a student named Harmanpreet Singh
to show BRL-CAD modeling capabilities on the web. It was initially a
vanilla PHP + three-js project. This project was continued by Inderpreet
Singh in 2014 and was converted to Meteor from vanilla PHP in order to
get a robust backend. Next year in 2015 two Students Deepak Sharma and
Shubham Chauhan continued the meteor project.

**What I will do** One of the major motives of my GSoC would be to
improve the existing code. To complete the things that are almost
complete. Also, the new features I am adding aren't completely new, they
are an extension of some existing feature of OGV. By the end of GSoC, I
want OGV to be **production ready** and available to use for a wider
majority of people.

I am mostly concentrating on the **efficiency** and **control over the
model viewer**. For now, we can only view the complete model. We have no
control over what parts of a model to show/hide. This includes giving
different color/material separately to different parts of a model
instead of the complete model. There are much more such things that I
would accomplish during my GSoC tenure. Things I will do in GSoC are
listed as following:

Things that I'll improve:

-   Search (for models, users and even parts inside model)
-   Database schema (Adding schema to the collections)
-   Increasing speed and efficiency in handling Obj files (merging
    multiple Obj files and removing duplicates)
-   Overall User Experience and User Interface
-   Removing redundancy and unused code

Things that I'll add:

-   Show/hide parts of model (also color them separately)
-   Adding push notifications for like, comment, share
-   Easy Deployment procedure
-   Adding view restrictions on uploaded models
-   Enabling users to create Groups/lists of followers

## Detailed Project Description

### Code Cleanup

-   **Github branches and PR's**: There are a lot of branches and PR's
    pending, my task would be to merge all the code and get the desired
    stable code in the master branch.

<!-- -->

-   **Current Code**: Changes in the code includes adapting to more
    appropriate variable names, removing redundant code.

For example, there exists redundant code in file
*OGV/client/views/model_viewer.js* at line no 220. The package
*ishwerdas:ogv-threejs* is not updated since it is created by Inderpreet
Singh in 2014. There are many such instances in the code that needs to
be fixed.

### Robust and secure database by using Schema

We are using MongoDB in OGV. It is a schema-less database. But however,
it is generally a good practice to define a schema that validates the
content of the collection. If we don't use schema, there comes a high
chance of adding wrong values in the database. That's the reason meteor
officially supports and recommends using schema.
<http://guide.meteor.com/collections.html#schemas> To add schema to
meteor collections, we may use package

`   aldeed:simple-schema`

For instance, we have a collection in OGV called "Ogvsettings".

`   settings.schema = new simpleSchema({ `
`gobjPath: {type: string} });`

If we apply the above schema to collection Ogvsettings, it will make
sure we get a string value in the "gobjPath" field of the collection.
Thus, **making our application more robust and secure.**

### Efficiency in handling Obj files

OGV is a bit slow for now. It can't handle big models, one of the main
reasons is the number of HTTP requests for each obj file. Thus, OGV can
be boosted by doing following things:

-   **Removing duplicates**: When a .g file is converted into obj, each
    converted obj is copied to another location. Thus, there exists a
    duplicate file for each obj file. Thus occupying unnecessary storage
    to the server. Obj files are created at
    *OGV/.meteor/local/cfs/files/modelFiles* during conversion, which
    aren't required while viewing the model. Thus, they occupy extra
    space. I will write the code that removes these files after a
    certain amount of time automatically so that there is no wastage of
    server space.
-   **Merging all OBJ files into one**: On model rendering page,
    multiple requests are made(\~300 for complex objects) thus slowing
    down OGV. Therefore merging obj files will reduce HTTP requests by a
    big number.

![](/wiki/user/img/_details.png)

-   **Group/Ungroup merged Obj file**: User should get an option to
    group/ungroup the merged obj file. As I will load only one obj file
    for the sake of speed but I don't want the user to lose control over
    the model. Therefore, the user will ungroup to load each part of
    model separately. More on this is explained in below section Control
    over the model.

### Control over the model

-   **Show/hide parts of model**: While working on a 3D model, the user
    always finds a need to look into a specific part of a model instead
    of the complete model. Because of this, I am adding an option to
    show/hide parts of a model. Once the model is ungrouped, we can
    show/hide any part of a model. **Also we can change the names of the
    objects, by double clicking on the obj name in list.** Instead of
    obj file names we can define our own names for each part of object.
    These names will then be seen when hovered with mouse over the part
    of model

![](/wiki/user/img/_show_hide.png)

-   **Coloring parts of model**: Once the model is ungrouped, we get a
    set of different parts that can be colored in a separate color or a
    material texture.

<figure>
![](/wiki/user/img/_colored_parts.png)


-   **Searching parts of Model**: Complex models have a large number of
    parts, so it isn't feasible to go through the list manually to find
    a specific part in order to perform an operation on it. Thus there
    comes the need of searching the part of the model.

<!-- -->

-   **Searching users and models**: OGV already has this search. But it
    isn't much functional. We can't go to the desired model from the
    search results. Also, the existing search uses simple string
    comparison instead of any search algorithm. I would like to use
    phonetic search and auto-complete search algorithm for an enhanced
    search experience. Following meteor package can help us achieve
    autocorrect, phonetic search experience.

`  art1sec8:fuse`

<figure>
![](/wiki/user/img/_empty_search.png)
</figure>


![](/wiki/user/img/_search_ga.png)
</figure>

-   **Advanced Search**: With this we can search for models using
    certain filters. Filters include filter by the owner of the model,

![](/wiki/user/img/_advanced_search.png)
</figure>

### Notifications

-   **Better notification UI**: The current notification style cover the
    entire top bar, and hides the menu, thus the user can not go
    mixture of meteor sAlert notifications and simple javascript Alert.
    all the alerts to meteor sAlert. Sometimes when we follow another
    user, we get two sAlerts. This inconsistent behaviour of
    notifications needs to be fixed.
-   **Adding notification panel**: A separate panel that will record all
    the notifications and can show the history whenever a user needs.
-   **Push notifications**: Every time a user likes/comments/shares your
    uploaded model, you will get a push notification in the notification
    panel and also in the mail. Notification in the mail is
    configurable. You can switch it off if you don't want it.

<figure>
![](/wiki/user/img/_notifications.png)
</figure>

### Customized Access to models

-   Private models: Only user itself can see the privately uploaded
    models. These doesn't appear in the news feed.
-   Groups/lists: Allowing the user to classify the followers into
    groups or lists. And then share the model only with the chosen
-   Only followers: Only users who follow can see the uploaded model

### UI/UX improvements in model

-   **Progress bar for uploading**: When user uploads a model, the
    progress bar will come as shown in figure below. CollectionFS comes
    with a template for progress bar

`  {{> FS.UploadProgressBar}}`

<figure>
![](/wiki/user/img/_uploading.png)
</figure>

-   **Progress bar for conversion**: In current OGV code, the conversion
    percentage is already being calculated in file
    *OGV/server/cfs_uploader.js (variable name: ConvertPercentage).* I
    am going to use that percentage variable with a javascript function,
    that animates the button.

<figure>
![](/wiki/user/img/_conversion.png)

    image file to be used as a thumbnail of the model. Automatic
    thumbnail generation will snapshot the rendered view of a model, and
    use that image as a thumbnail.

The suggested technology for this is phantomJs. But I was successful in
creating a screenshot with simple javascript from the console. Also
doing it this way seems a right approach to me.

`   window.open( renderer.domElement.toDataURL( 'image/png' ), 'screenshot' );`


-   **Improvements in social elements**: Social elements like love and
    comment needs some UI refreshment. Also, another social element of
    sharing someone else's model on your profile is going to be a part
    of this task.

<!-- -->

-   **Improved embedded view**: Right now the embedded view is
    cluttered, I have already fixed this with PR:
    <https://github.com/BRL-CAD/OGV-meteor/pull/34> But now it only
    shows the model, and social elements like count of total love and
    comment are hidden. The improved view will show the social elements
    on mouse hover in embedded view.

### Admin Panel

-   **Getting rid of hard coded superuser**: Now when we install OGV, a
    super user *admin@example.com* is already in a database. The
    username and password of this user are written into the code itself.
    *(in file OGV/server/accounts.js)* Instead of this hard coded user,
    a more righteous approach would be to enable the admin to create a
    super user when a fresh install of OGV is done. The way we do during
    a Wordpress installation.

<!-- -->

-   **Improved Admin panel**: Currently in OGV, the admin panel contain
    settings like SMTP URL, mged path, g-obj path. There aren't any
    settings related to other users and OGV. A super user should have
    settings to
    -   Enable/Disable private model uploads
    -   Enable/Disable user registrations
    -   View statistics of total model uploads by each user

<!-- -->

-   Enabling guest users to upload the model without signing up.

### Deployment

-   Deploying on a freeBSD system
-   Establishing a mechanism that automatically updates the code on
    server when a new commit is pushed in master branch (gruntjs)
-   During the course of GSoC, every friday would be a deployment
    Friday(not of the master branch, but of the gsoc branch, so that it
    can be regularly tested by other members of the community).

## Milestones

-   Community Bonding Period
    -   Discuss on blaze to react conversions
    -   Making Repository ready for deployment

<!-- -->

-   **WEEK 1 (23rd May)**

Code Cleanup (Removing redundant/unused code) (23rd - 29th May)

-   **WEEK 2 (30th May)**

Deployment (Deploying master branch on freeBSD and also making scripts
for automatic deployment)

-   **WEEK 3 (6th June)**

Robust database using aldeed:schema

-   **WEEK 4 (13th June)**
    -   Improving notifications
    -   Push notifications
    -   notifications panel
    -   adding share functionality

<!-- -->

-   **WEEK 5 (20th June)**
    -   Improving user and model search using art1sec8:fuse
    -   Improving UI for social elements

<!-- -->

-   **WEEK 6 (27th June)**
    -   Thumbnail Generation
    -   Code cleanup for mid term evaluation

MID-TERM EVALUATION

-   **WEEK 7 (4th July)**
    -   Merging Obj files using threejs geometry and objExporter
    -   Removing duplicate obj files.

<!-- -->

-   **WEEK 8 (11th July)**
    -   Search inside models
    -   show/hide parts

<!-- -->

-   **WEEK 9 (18th July)**
    -   Giving different color/material(image) to different parts
    -   Progress bars (upload and conversion)

<!-- -->

-   **WEEK 10 (25th July)**
    -   Creating groups/lists of followers
    -   Restricting access to model viewing (public/private models)

<!-- -->

-   **WEEK 11 (1st August)**
    -   admin panel

<!-- -->

-   **WEEK 12 (8th Aug)**
    -   Minor UI/UX improvements

<!-- -->

-   **WEEK 13 (15th Aug)**
    -   Code Cleanup
    -   Testing
    -   Final Deployment

FINAL EVALUATION

## My Preparation

-   I have been studying about the meteor, specifically for OGV.
-   I have also gained some experience mged commands and using BRL-CAD.
-   I have read and understand how g to obj converts.
-   I have already sent a PRs regarding embedded view of models and
    other things in OGV.
-   I have spent great deal of time in reading the roadmaps and inner
    workings of meteor, so that we code with future in our mind.

## Why BRL-CAD?

-   I have been a part of this community for about 4 years now.
-   I feel like home at this community
-   When it came to GSoC I really didn't have to choose, I knew I would
    go with BRL-CAD.

## Why Me?

-   I have a rich community experience with BRL-CAD.
-   I have sufficient meteor experience. I have been contributing to a
    number of meteor projects.
-   I am following OGV, from its first iteration in 2013 till now.
-   I have been a participant of GCI 2012 and mentor in GCI 2013, 2014.
    And I tried to be helpful where I can like in BRL-CAD website.
-   I have interested in bringing BRL-CAD to web since 2013. Link to
    repository:
    <https://github.com/GreatDevelopers/wBRLCAD/tree/master/general/tableModel>

## References

-   <http://guide.meteor.com/collections.html#schemas>
-   <https://www.discovermeteor.com/blog/blaze-react-meteor/>
-   Fuse js: <http://kiro.me/projects/fuse.html>
-   Grunt js: <http://gruntjs.com/>
