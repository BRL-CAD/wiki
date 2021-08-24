# Development Logs

## Community Bonding Period

-   Explored various options regarding nodejs and non-node frameworks.
-   Learnt basics of development with meteor, using templating engines
    etc.
-   Also looked into alternative framework Expressjs.
-   Discussed with mentors about the choice of framework.
-   Packaged three.js for meteor.
-   Ran a simple OBJLoader example in meteor.

## Development Period

### Week 1

'''''19th May

-   Worked on Authentication Module in meteor
-   Wrote LogIn, Registeration, Forgot Password and Reset password form
    templates.

'''''20th May

-   Completed the views and helpers for the templates and Added
    validations to the forms
-   Modified the directory structure and read Hacking file again and
    made edits to my code accordingly.
-   Pushed the code to github
    <https://github.com/inderpreetsingh/OGV-meteor>. Forgot-password
    form is now able to send the mails but stuck at an error regarding
    Reset-Password template.

'''''21st May

-   Reset-Password error solved, Authentication is complete now.
-   Started looking into file upload. Tried a package called
    dropzone.js. Published my three.js package
    <https://atmospherejs.com/package/ogv-threejs>.

'''''22nd May

-   Worked on File Upload module, tried various file upload packages.
-   At last settled for packaged named formidable from npm.

'''''23rd May

-   Having done the first milestone, today I explored other frameworks
    and read more about the technologies involved. Did some work in
    expressJS.

'''''24th May

-   Uptil now, I was dealing with file uploader in a separate app, today
    I ported file uploader to OGV.
-   Now we can upload files in OGV, currently any files can be uploaded
    but will soon change that so that it only accepts .g files.

'''''Milestone Set

-   Authentication

'''''Milestones Completed

-   Authentication
-   Got three.js working with meteor
-   File uploader partially completed

''''' Things yet to do

-   Improve UI
-   Add routers

### Week 2

'''''26th May

-   The ported file uploader started facing errors, mostly regarding
    styles. I was unable to apply global bootstrap. I couldn't work much
    due to some power issues at my home.

'''''27th May

-   Today, I improved my earlier file-uploader by removing the
    dependency from formidable and directly use the 'fs' package.
-   As I have time, I am still giving Collection-FS a try, so that I
    don't miss out on anything useful.

'''''28th May

-   Read about meteor collections, started working on file manager.

'''''29th May

-   I was unable to work, due to some urgent work at home. Will make up
    for it by working more in coming time.

'''''30th May

-   Completed the new file uploader (except validations), and added it
    into main code. Looking into rendering part and routers.

'''''31st May

-   Added Basic router file.
-   Each user will now have it's own folder and uploaded files go there.
-   Added more comments in the code.
-   Implemented the file extension check, now only .obj files can be
    uploaded (will restrict that to .g files when I deal with g-obj
    conversion)
-   A bit stuck on how to pass errors from server to client via meteor.

'''''Milestones Set:

-   File Uploader

'''''Milestones Completed:

-   File Uploader

### WEEK 3

This week I have my final exam on 3rd June and 5th June, So will be busy
a bit there.

'''''4th June

-   Routers integrated, now we have different URLs for log-in, sign-up
    etc.

'''''6th June

-   Solved the problem regarding file uploader errors.
-   Worked on adding OBJLoader in OGV.

'''''7th June

-   added minimal file manager
-   added models collection, now each user has list of models in
    database
-   created the universal header as I showed in mockup
-   Unable to send verification email at sign-up.
-   added lovemeter to each model (dummy yet).

'''''8th June

-   File Manager completed
-   Styling of existing components
-   Verification email works fine
-   uploaded to <http://ogv.meteor.com/>
-   more improvements

'''''Milestone Set:

-   File Manager

'''''Work Done:

-   File Manager
-   UI
-   Routing

### Week 4

9th June

-   Solved some deployment problems with ogv.meteor.com
-   Forgot Password form stopped working, so corrected it.
-   Added preloader

11th June

-   Tried to deploy on my own server (facing problems)
-   moved from meteor-router to iron-router

12th June

-   Corrected some iron-router problems
-   Struggling to get OBJLoader working with meteor

13th June

-   Tried a lot to get files from private folder to load, but failed.
-   Put a mail in meteor mailing list about it.

14th June

-   Added model Viewer, and got it working with OBJLoader. Now we can
    see the 3d OBJ models rendered in OGV.

15th June

-   Improved the way model Viewer looks.

### Week 5

'''''16th June

-   Improved the menu bar (small fix)

'''''17th June

-   Today I was back to hacking file, and added more comments
    documentation and cleaned my code.
-   Added keyboard controls to the model viewer

'''''18th June

-   Keyboard controls were not behaving correctly, improved them.
-   Added canvas render support so that it can work even where webgl is
    not working
-   Started searching about running system commands with meteor

'''''19th June

-   Tested the whole app again, and removed few bugs

'''''20th June

-   Started working on g-obj conversion
-   Re-installed latest brl-cad
-   Added lovemeter to models (similar to '+1' or 'like')

'''''21st June

-   Added Minimal g-obj conversion function.

### Week 6

'''''23rd June, 24th June

-   Tried Deployment first on the college server, and then on personal
    digital ocean droplet. I was able to deploy on digital ocean droplet
    but still faced some issues with uploader, so then deployed using
    meteor development server where it worked but with glitches. Will
    work on these issues soon.

'''''25th June

-   Faced problems with previous file uploader, started using
    collectionFS.

''' 26th June

-   New file uploader is almost ready, and I wrote a blog post for my
    mid term evaluation at <http://ishwerdas.com/journal/gsoc-mid-term/>

'''''27th June

-   Was unable to work because of some urgent work at home.

'''''28th June

-   Completed working on collectionFS.
-   Worked on file extension check.

### Week 7

30th June, 1 July, 2 July, 3rd July Did not work much.

'''''4th July

-   Extension check completed
-   Working on better way to show errors

'''''5th July

-   Tried to understand g-obj conversion
-   Started writing a separate server method for converting file

'''''6th July

-   Need to store files in a separate directory after g-obj conversion.
    Able to store them, but trying to figure out a way to get a public
    url of them to view.

### Week 8

'''''7th July

-   Can store files in a separate directory, but could not find a way to
    get it's public URL. Till now, I have been working on converting all
    uploaded g-files at once, also tried to get it working for file
    whenever it's uploaded.

'''''8th July

-   Changed the logic of storing .obj files and the .g file in different
    directory, instead will add a meta information on each obj file that
    will contain info about which database it belongs.
-   Stuck on an error while getting path of the uploaded .g file, won't
    be able to convert until I get the path.

'''''9th July

-   Instead of converting files on upload, I will instead now convert
    files while viewing. This solved the error I was previously facing
    in converting files. Now g-obj conversion is working.

'''''10th July

-   Tried to get the converted files in CollectionFS but could not find
    a way to do it.

'''''12th July

-   I got a solution in meteor mailing list, which is about using
    transformWrite handler and creating a new FS.File object for each
    OBJ file. I have been able to get transformWrite handler working but
    facing some problems with creating new FS.File object.

'''''13th July

-   Whenever I created new FS.File object, I got this weird error about
    meteor fibers. So I learnt more about how "non-blocking" code works
    and what are meteor fibers but still I could not make it work.
-   I posted my problem as issue on CollectionFS github. There, I got
    another logic to work on. Now instead of transform write I was to
    work on "stored" listener.
    <https://github.com/CollectionFS/Meteor-CollectionFS/issues/362>

### WEEK 9

'''''14th July

-   Worked on stored listener, but could not get it to work.
-   Asked again on CollectionFS issues, could not get the new "stored"
    logic to work but was able to solve the error I got in transform
    write handler.

'''''15th July

-   Added multiple obj loader to the model_viewer.
-   Tested new obj loader with various heavy .g files.

'''''16th July

-   Improved the conversion, and removed some bugs.
-   Tweaked model_viewer to show some big files.
-   Tested with various large .g files.

'''''18th July

-   More testing, laptop hangs at big files.
-   Worked a bit on drag and drop uploader

'''''19th July

-   Added server side converting progress

'''''20th July

-   Corrected and update the repository.

### Week 10

'''''21st July

-   Added drag and drop functionality to the uploader.
-   Working on user dashboard
-   Improved File manager to show only files that have been converted

'''''22nd July

-   Added User roles to the authentication for having admin and normal
    users.
-   Made one default admin user and one default normal user.

'''''23rd July

-   Added User Dashboard and admin templates
-   Added config.js, a file that store configuration variables

'''''24th July

-   Sign up form stopped working, solved that problem.
-   Added log-in/log-out buttons in the header
-   Started working on concept of models feed, a list of uploaded models
    with description and option to like, comment and share. Kind of like
    timeline on facebook.

'''''25th July

-   Worked on design of model feed.

'''''26th July

-   Wrote model feed template and views.
-   Working on model feed, a bug was introduced in file manager, which I
    solved.

'''''27th July

-   Improved dashboard template with extra fields.

### Week 11

'''''28th July

-   Started working on comments section, designed it, wrote it's
    template and views and hence added it's collection.

'''''29th July

-   Comments section completed.
-   Improved some dirty code.

'''''30th July

-   Started working on 'love' button (analogous to like on facebook)
-   Wrote templates, views and made love button working.
-   Removed a bug from model viewer. Actually model viewer stopped
    working when we refreshed it. Dig into the problem and solved it.

'''''31st July

-   Improved menu bar, added buttons for file manager, dashboard etc.
-   Worked on generating embed code for model.

'''''1st August

-   Took a break today, din't work much. Did add some icons to model
    viewer though.

'''''2nd August

-   I deployed OGV at <http://104.131.212.220/>
-   Improved routing, preloader a number of small fixes and
    improvements.

'''''3rd August

-   Added images to file manager
-   Improved model thumbnail image view template
-   Improved model viewer
-   Set 70% as acceptable conversion rate.

### Week 12

'''''4th August

-   Took a break for a day.

'''''5th August

-   Worked on user dashboard, now users can change their name and write
    a brief description about themselves (will be used in profile
    pages).
-   Working on adding profile picture, a bit stuck on how to store
    profile picture in database, so that I can easily grab a url and if
    there's no pic uplaoded yet a default pic can be seen.

'''''6th August

-   Able to add profile picture to user through user settings, also
    added them in model feed.
-   Improved the styles of comments and lovemeter
-   Worked on admin settings, added collections and fixtures for it,
    changed the code to get settings from database (earlier they were
    hard coded).

'''''7th August

-   Improved the structure of database regarding profile picture and
    model's owner. Actually earlier I used to add full user object to
    model's owner field but that became problem when user object was
    updated through some other way (for ex:- changing profile pic)
-   Now user can change admin settings from the website.

'''''8th August Had to go out of town, so could not work.

'''''9th August

-   Improved and added a new Error/Notification mechanism.

'''''10th August

-   Read about deployment procedure (on various platforms) and also
    re-read about coding standards and documentation.
-   Gave a seminar to college juniors about OGV and BRL-CAD. They got
    really excited to be working in OGV.

### Week 13

'''''11th August

-   Added embed code generator
-   Made the icons in model viewer working
-   Started working on documentation

'''''12th August

-   I am stuck on how to show comments on model_viewer page , the
    technical part is done, I am able to retrieve comments but I am
    stuck on the UI part, like where to gracefully put them so that it
    plays well with the model viewer.
-   Enabled extension and file type check on profile pic uploads and
    thumbnail image uploads.

'''''13th August

-   Completed the comments part.
-   Started wrapping up the code.

''''' 14th August

-   Started working on developer documentation and improving the code.

''''' 15th August

-   Worked on User documentation and Developer documentation, read
    Hacking file again.

''''' 16th August

-   Improved security of some models.
-   Completed Developer documentation and wrapped up the code. Latest
    and complete code is on github now.
-   Started working on pagination (to improve page load time).