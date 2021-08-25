Here goes my **development logs** and **personal notes**

# **BONDING PERIOD**

-   Playing around with meteor framework
-   Getting to know how models are being viewed
-   Updated the production ready plan
-   Talking to Deepak, discussing about work flow
-   Finding resources that would help me develop back-end and go through
    my milestones
-   Explored three.js. Made a few alterations to the code, and saw the
    effects on the view. I am particularly
    unhappy the way the models are being viewed. Lacks clarity, color
    etc.
-   Updated production ready plan after a few words with Sean. Deploying
    the app as soon as possible
    shall be a top priority.

# **CODING PERIOD**

## **Week 1**

**May 25**

-   I think I should shift the login portion to the end (after
    deployment). Otherwise I'll have to do the settings
    twice unnecessarily.
-   I'll work on the model-viewer page this week. Need to talk to Deepak
    about the front-end, so that we are
    finished with it completely this week.

<!-- -->

-   Getting random colors on models. Confused :/. How to handle coloring
    (definite colors on models).
-   Smoother mouse rotation of camera \[DONE\] and Removed grids and
    axes \[looks more classy\]
-   Had some discussions, I'll get back to login now, from tomorrow then


**May 26**

-   made a gmail ID by the name ogv.mailer\[at\]gmail.com. I'll use this
    Email ID to configure mailgun,and
    hand over the password to the BRL-CAD team.
-   Implemented Email Verification of registered user. Forgot Password
    working fine. Changed Email templates
-   omniAuth remains. Basic issue would be to verify 3rd party login.
    Need for some searching
    (nothing impressive seen yet).
-   Maybe I know what to do.

**May27 - May 29**

-   I just went to my cousin's place for a hangout.
-   Tech-fest in college, loads of meetings.
-   Back to OGV from tomorrow

**May 30**

-   In my searching for the solution I found a repo that has implemented
    github login, and is working fine there.
    I will be taking some reference from there for sure.
-   Made a sample app and added user accounts in it. Added omniAuth
    successfully in the sample app.
-   Still confused. It's the only part left in login. I'll need to ask
    about it from someone.

**May 31**

-   Its early in the morning. And I found the bug, residing in router.js
    -_-.
-   omniAuth will be finished by tonight. I am relaxed.
-   Login system of OGV is production ready.
-   User will be removed from DB, if he does not verifies his/her email
    within x hours.

`   `**`Login`**
`   Registering and email verification working fine (done via mailgun)`
`   Forgot password mails are going as well`
`   omniAuth added: google and github (facebook after deployment)`
`   User entry from DB will be deleted if email is not verified within x hours`


Some points to take note of regarding oAuth:

`   1. Will require setup of configuration from your side`
`   2. Therefore, you won't be able to test on localhost until and unless you configure googe/facebook/github.`
`   3. I'll do the configurations after deployment`
`   4. The back-end part for omniAuth is complete. (you can ask for a video as well :D)`

## **Week 2**

**June 1**

-   Lazy
-   Learning three.js online editing model techniques and found [**this
    great
    resource**](http://threejs.org/docs/scenes/material-browser.html#MeshPhongMaterial).
    Want to make something like this for the viewer.
    Loads of studying.

**June 2**

-   Updated proposal both on melange and brlcad-wiki. Was somewhat
    pending (now fully complete).
-   Added buttons to change view to wireframe, and to add grid/axes to
    renderer. backend part only. Button GUI is temporary.

**June 3**

-   Asked for help regarding model viewing, especially colors in object
    model.
-   Might take some time to respond.
-   **Implemented feedback system** via formspree.io. Unable to add
    notification for feedback completion.

**June 4**

-   Mainly tech fest work
-   Added link to edit model in the my-models page
-   tried adding the delete button for a model. I think code is right,
    why is it not working is the issue. confused :/

**June 5**

-   Studying code base, g-obj conversion and other technical stuff
-   Read. Read. Read. The resources provided by Inder and other
    resources as well.
-   Implemented deleting model. Unable to delete thumbnail associated
    with it.

**June 6**

-   Completed delete model. Thumbnail not getting deleted.
-   Need to understand thumbnail-model architecture.
-   More searching about g-obj and mged for capturing color attributes.

**June 7**

-   Implemented delete, update info for OGV models. Some finishing
    required in edit-form required.
-   No reply on mailing list regarding colors in models.
-   Decided to drop the idea of having a separate modal for editing
    information. User will land up on the description page
    and change things there itself.
-   Routing changed. Now user won't be able to tamper or see the edit
    description page of other user's models.
    (let's say by copy pasting the URL). Code is safe from hackers :D
    :D.

**WEEK SUMMARY**

`* user's can change view to wire-frame mode.`
`* user's can add axes/grids to model for better idea of directions.`
`  ^ Both need some back-end finishing.`
`* user's can provide feedback about the website to a developer, by filling up a form whose details will be forwarded to developer's email.`
`* user's can now delete their uploaded models (also the thumbnails associated with it)`
`* user's can update information about their uploaded models i.e. name, description and thumbnail.`
`* user's cannot see/tamper with information of other user's models. Earlier if you had access to someone's model's description form's link, `
`  that user could create problems (not actually change) in the information of that particular model. `
`  New routing set takes care of this, and if the model does not belongs to the logged in user, he is redirected to the upload page, `
`  even if he pastes the link to the description form of other's model.`

## **Week 3**

**June 8 - 9**

-   Sorted things about feedback front-end.
-   Working on adding dat.GUI features in model_viewer. Not working due
    to some reason.
-   dat.GUI works now fine in the meteor app. Adding functions related
    to OBJMaterial. Model Viewer almost complete.

**June 10**

-   Completed adding functions in dat.GUI. Might need to add more, but
    it has what a basic viewer needs.
-   Functions consisting of wireframe, wireframe+model, set
    transparency, opacity, ambient color, shininess etc.
-   Unable to customize background color through dat.GUI.

**June 11**

-   Nothing much. unwell
-   Tried categorizing models into categories.
-   Worked fine when one model has only one category, but that should
    not be it. A model can have more than one category.
-   There can be 2 ways of going through the problem. Either make a new
    collection, or make a field named
    "category" in the model document itself, among which the latter
    looks more promising and efficient.

**June 12 - June 13**

-   Unwell
-   Slept a lot
-   Some GUI for model_meta form for category checkboxes.

**June 14**

-   Added a field for category in modelFiles.
-   "categories" is a field in model Files which is an array that stores
    categories in which the model belongs to.
-   The categories that go in the model files is chosen by the user in
    the model_meta form.
-   There are 12 pre-defined categories (check-boxes). The user selects
    the category to which the model belongs to (can be more than one).
-   Merged with edit-info. Need to work on certain validations (another
    2 hour job).

## **Week 4**

**June 15 - 16**

-   Tech festival work. Related to organizing events
-   Finished with edit info implementation. Everything works fine now in
    case of updating
    model details: name, description, thumbnail and category.

**June 17 - June 18**

-   Nothing much.
-   Looked for ways to tag models. Added and tries using a bootstrap
    package for the same. Might need some work.
-   Waiting to get the previous work merged in the GSOC'15 branch of
    BRLCAD (both back-end and front-end).
-   Searched about followers/following architecture in mongodb. Got a
    pretty good idea
    [**here**](http://stackoverflow.com/questions/4042917/twitter-like-app-using-mongodb).
    For this to work, every user should have a profile page as well.

**June 19 -June 20**

-   Made working profile pages, with routes for users. Basic Info about
    any user can be seen on the profile page.
-   Profile pages accessible at /profile/:_id
-   Will surely take time to complete. Should be complete by midterm
    evaluation.

**June 21**

-   Stayed at home

## **Week 5**

**June 22**

-   Stayed at home

**June 23**

-   Stayed at home

**June 24**

-   Stayed at home
-   Added a follow button to profile pages (won't show if you are
    visiting your profile). Does nothing yet.
-   Made a few changes to the previous profile page work.

**June 25**

-   Added routes to profile page on model feed. Linking with profile
    pages of user.
-   Appending id to follower/following array in user document
    successful. Working Following button.
-   Feed will show models of users who are being followed by the current
    user.
-   Working un-Follow button added.
-   Trying to handle visibility of both buttons under different
    circumstances.

**June 26 (midterm evaluation starts)**

-   Visibility still problematic.
-   number of people following shown on profile.
-   Improved front-end of profile page (unresponsive, relative
    positioning).
-   error message on the model of not being converted added in
    model_meta.js
-   Need to handle visibility and update follower list (only following
    list working).

**June 27**

-   Continuing with error message of conversion and follower.following
    part.
-   More Front-end work to profile pages. Not much of a work.
-   Proper Indenting and commenting of code.
-   Fixing Issues in previous work.

**June 28**

-   Visibility of buttons handled
    -   UNFOLLOW button visible on those user profiles who are being
        followed.
    -   FOLLOW button visible on those user profiles who are not being
        followed.
    -   no button on user's own profile.
    -   FOLLOW button changed to UNFOLLOW button after clicking and vice
        versa
-   Tried updating follower array of other user. Unable to do so till
    now.

## **Week 6**

**June 29**

-   Nothing much just standard bug fixing here and there.

**June 30**

-   Newsfeed (homepage) viewing:
    -   User's see their own models
    -   User's see the models of the people whom they follow
    -   User's see the models who have likes greater than a specific
        number. popular models.
-   added the field countLovers to the Lovers collection to keep account
    of number of likes.
-   All above items on the homepage will be sorted reversed
    chronologically (the model uploaded last, will be shown first).
-   Removed smooth mouse movements from model_viewer (earlier added by
    me). Were very messy and difficult to handle.
-   Added profile button on model_viewer/renderer which leads to the
    owner of the model.
-   Added follower array updating functionality (update other user's
    parameters) but needs to be more secure.

**July 1**

-   Added buttons on filemanager page. Added a temporary delete button
    as well.
-   On user initialization/creation of the user, He will be following
    two users by default, the admin user and himself.
-   Dire need to make user update method secure. Trying to do so.

**July 2**

-   Display google+ user profile picture if user logged in from google.
    unable to view on usr settings page.
-   limit character length in about section in forms. Show number of
    characters left as well.
-   updated the displaying of number of followers.
-   feedback button and page, accessible from anywhere at all times.

**July 3 (midterm evaluation ends)** **[Midterm Summary](Midterm_Summary.md)**

**July 4**

-   Came across html2canvas which can be used to take screenshot and
    save that as thumbnail for the model.
-   made feedback thanks page, user will be lead to the page after
    successful feedback form submission.

**July 5**

-   Added a sidebar on newsfeed page that will show. Template ready.
    -   current user info
    -   suggested users to follow
    -   suggested models to view
-   Sidebar now showing current user info that includes, profile pic,
    name, \# followers, \# people following and \# models.
-   Solved the problem of repeatedly saving profile picture of same
    user.
-   Added a field by the name "countModels" in profile section of user,
    that gets updated as per insertion/deletion of model.
-   Sidebar now shows users suggestions who can be followed. Showing
    -   Users excluding the ones who are already being followed
    -   excluding himself.
    -   Users having highest number of models first.
-   Newsfeed shall remain empty unless no user is being followed
    whatsoever.

## **Week 7**

**July 6**

-   Added a field by the name "viewsCount" keeping track of number of
    views of model.
-   The newsfeed now shows popular models, sorted on the basis of number
    of views.

**July 7**

-   Initial trials to incorporate wmater command in the viewer.

**July 8 - July 11**

-   Stayed at home.

**July 12**

-   Searched about "load more" feature for pages (newsfeed, profile page
    and my-models page). Pagination in meteor
    **[here](https://github.com/alethes/meteor-pages)**.
-   Need to test the meteor-pages package in the app.
-   No success in wmater command.
-   'Load more' functionality is working with **[meteor paginated
    subscription](https://github.com/tmeasday/meteor-paginated-subscription)**
    package. But needs a lot of work.

## **Week 8**

**July 13**

-   Deleted/disabled the suggested models feature. Issue in meteor
    subscription/publication functionality due to which, the load more
    feature
    does not seem to support different kinds of publication for the same
    collection. Need of a different "explore models" page.
    But first finishing of existing bugs is required.
-   Explore Page, for searching/exploring models:
    -   Search bar (only by name)
    -   Sort by: number of views, number of likes, time of upload (radio
        buttons)
    -   Search in: Categories (check boxes).
    -   Approximate time to be taken for completion 7-10 days.
    -   Problem to be faced: Publishing data differently from same
        collection on single page. (keeping the load more functionality
        intact)

**July 14**

-   Set up a new explore page.
-   Looked into different methods in which models can be viewed.
-   Need to set the load more functionality aside.
-   Successfully displaying models with different sorting properties,
    but without user input.

**July 15**

-   Tried to work with load more functionality and displaying different
    views of the same collection.
-   Just trying to work on the load more functionality

**July 16**

-   Tested meteor packages for adding search-bar and search models by
    name option to Explore page.
-   Successful implementation of search-box (searching models through
    name) using search-source package.
-   User can search through search box by model name and user name.

**July 17**

-   Searching models and users through search boxes complete. with front
    end.
-   Started working on filter wise searching/displaying of models.
-   Filters: Category, Upload time-range, Sort
-   Taking input through drop-down menu, appending selected input to
    text field, and displaying selected filters.
-   Undo button for removing last added filter.

**July 18 - July 21**

-   Out of station for hackIndia (national level hackathon).

## **Week 9**

**July 22**

-   Stayed at home

**July 23**

-   Tried working with wmater command to get color of models. Confused
    about its use.

**July 24**

-   Working on the explore page to search models according to category.
-   Facing difficulties in previous implementations.
-   Made a form for submission of filters.

**July 25**

-   exploring wmater and get_comb

**July 27**

-   Got PR merged on GSOC branches.
-   Stop adding further features, work on bug-free OGV.

**July 30**

-   Started the bug fixing routine. fork now up to date with the
    GSOC15-merged branch.

**July 31**

-   Bugs due to merging fixed. Ambiguous front-end problems and deleted
    routes problem has been solved

**August 1**

-   unwanted file deletion
-   generalized feedback frontend and a few other issues.

**August 2**

-   Eliminated a different explore page and combined it with newsfeed
    page.

**August 3**

-   College reopens. Classes start.
-   Google+ profile pictures are successfully being viewed (except on
    newsfeed page)

**August 4**

-   Profile page and newsfeed front end fixes mostly including alignment
    and positioning.

**After 5 August**

-   Fixing bugs about backend and front end part
-   There were many small isuues
-   Trying to work on deployment part, on ubuntu server, but coud not
    complete sue to some reasons.
-   Talked to deepak (had better progress in working with deployment),
    came back to fixing bugs etc.
-   Send my update branch PR.
-   Plenty of merge-conflicts come up. Working with project partner
    Deepak to resolve issues and make GSOC15-merged branch clean
-   Prepared a list of enhancements to OGV and how to bring them into
    it.

<!-- -->

-   College fest work.
-   Preparing for internships (competitive programming).
-   Starting of college projects (3 course projects to come and 1
    project under a professor ongoing).

**8 OUT OF 10 PROPOSED MILESTONES COMPLETED [see link](OGV_production_ready_plan.md)**
