## Project plan of Open Geometry Viewer(OGV) under GSoC 2021

#### <u> No error shown if upload fails </u>

**GitHub Description:** If due to any reason, the upload of the model
fails, there's no error indicating the same.

**Proposed Solution:** Apply the toast notification in the
cfs_uploader.js file from where the models are being uploaded. Also,
make sure there is no other place that is linked with this issue.

#### <u> Email Server Error </u>

**GitHub Description:** Don’t allow the creation of a user account until
the admin has set an email server. A better way is to create a set of
settings called required settings and signup/login; nothing should even
begin before these requirements are met.

**Proposed Solution:** As mentioned in the issue, I’ll go for the
required settings and stop anything from happening before those required
settings are done.

#### <u> Upload Progress </u>

**GitHub Description:** Show an upload progress bar when uploading a
model.

**Proposed Solution:** I will get code help from the PR that is already
there by someone. If I think there is a need to implement it again on my
own, I’ll do it.

Reference: Link to the solution PR

#### <u> Code linting </u>

**GitHub Description:** This is a two-step process Lint all of the
existing code (JS and CSS) Make sure no non-standard code is added again
using Husky

**Proposed Solution:** Lint all the files using a linting config
example: Airbnb. Installing configuration through the VS code extension
eslint. Using Husky, check all the code and add that to pre-commit to
make sure that the code is following linting config. There are no
standard spaces in the file, also it does not follow JavaScript ES6.
Linting will help to keep the code in sync with the latest technology.

#### <u> Remove the CFS dependency </u>

**GitHub Description:** Collection FS has been depreciated(and recently,
the depreciation label was removed). It would be better to move away
from Collection FS, and use npm packages directly to upload models. (Can
s3 be used?)

**Proposed Solution:** Get some more details about the task and change
the package Collection FS and use the Slingshot package to upload it to
s3.

#### <u> CSS code improvement \[Code Quality\] </u>

**GitHub Description:** All of the current CSS code is in one file.
Divide it into multiple files and improve the code quality. Discuss
possible porting to SCSS.

**Proposed Solution:** Breakdown CSS into small files related to the
specific components. Remove the unwanted CSS and keep the CSS files
cleaner. Port all the CSS to SCSS, which will help the CSS to shrink and
create some reusable mixins/ variables to keep the code shorter.

#### <u> Write Tests </u>

**GitHub Description:** One of the major things required to get the code
quality of OGV up is by writing tests for it. As recommended in meteor’s
official guide, we would like to use ‘mocha’ and ‘chai’

**Proposed Solution:** I’ll write the tests to do unit testing for
components using Mocha and Chai for BDD/TDD assertions. Mocha is fun to
use. I also have a little bit of experience with Mocha.

Reference: <https://guide.meteor.com/testing.html>

#### <u> OGV Mediawiki Plugin </u>

**GitHub Description:** Idea is to create a mediawiki plugin, that asks
wiki admin to enter the OGV server details and allows users to Search
for a public model from OGV server Upload modal to OGV (depends on issue
\#59 ) Embed into mediawiki page. Allow mediawiki plugin to be used
without server (OBJ uploads)

**Proposed Solution:** Get some more detail about the task and learn the
new things that are required for the fulfillment of this task. Create a
JS function that will allow the user to search for the public model.
Users will be able to upload OVG publicly after the Mediawiki oAuth is
implemented. It will make the application easy to understand by
mentioning which model is uploaded by whom.

#### <u> Mediawiki oAuth </u>

**GitHub Description:** Currently, users need to have separate accounts
on BRL-CAD site(mediawiki) and OGV. We would like to be able to add
login with mediawiki to OGV

**Proposed Solution:** Mediawiki provides an extension to provide OAuth
to the user. There is a tutorial depicting how to integrate an OAuth
extension to users. It is easy to do if we get the extension installed
on time.

Reference: <https://www.mediawiki.org/wiki/Extension:OAuth>

#### <u> Edit link is not working </u>

**GitHub Description:** The edit link currently goes to the 404 page.

**Proposed Solution:** Debug the code in the mode_editor.js file and
see why the issue occurred and solve that. Add the try-catch and show
error for certain events that are causing an error.

#### <u> Bring Custom Coloring back </u>

**GitHub Description:** OGV used to have a custom coloring panel which
was removed when we chose to add colors directly from the .g file.
However, as we also allow the upload of single obj files, it's worth
allowing the users to change colors of different parts according to
their choice.

**Proposed Solution:** Take a look at the old code where it was first
introduced. Make the feature of adding color directly from the .g file
optional, and provide support for adding custom color.

#### <u> Auto position depending upon object’s width/height </u>

**GitHub Description:** Idea is to get the visible width/height of the
obj file/files in the scene and make sure they are in the center and
zoomed enough. **Proposed Solution:** Get the coordinates of the model
image. Set offset space on sides according to the size. After having the
coordinates zoom the object accordingly on the screen. There is a pen on
codepen that gives the exact idea to set the object width/height
according to the size link to the pen Reference: find the coordinates of
image in js

#### <u> Add Responsiveness to the application (Bonus task) </u>

Proposed Idea: The application is not responsive to different screen
sizes. Today, making the application responsive is the basic requirement
especially when it’s a web application. From my prior experience, a
non-responsive website or web application always has difficulty keeping
the user from having a good experience and limits the user to a desktop
machine. It ends the sense of having portable web applications. I’ll
make the application responsive using the media queries with custom CSS
or look for a CSS grid library to make it responsive.

#### <u> Improve the directory structure and component files structure (Bonus task) </u>

Proposed idea: Currently, the directory structure for the components is
messed up. All the components are in the same directory which downgrades
the code quality. I’ll improve the directory structure of the components
and put related components to a subdirectory and segregate the
components. This improvement will prove itself a very useful one while
scaling up the application in the future.

## Timeline

### Coding Period (7 June - 15 July)

-   Start with the ‘No error shown if upload fails’ bug. This will take
    around 1-2 days to fix this issue.
-   Continue with the ‘Email server error’ bug. This will take around
    4-5 days to fix.
-   Then go for ‘Upload Progress’ enhancement. This will take around 1-2
    days.
-   Furthermore, go with ‘Code linting’. The expected time of completion
    for this will be 3-5 days
-   Will go ahead toward the ‘Remove the CFS dependency’ major issue.
    This will take a bit longer, ETA will be 6-10 days.
-   Then go for ‘CSS code improvements \[Code quality\]’ enhancement.
    This will take around 2-3 days
-   Will move further to ‘Write tests’ enhancement. This will take
    around 4-6 days.
-   For the remaining 1-2 days, I’ll go for a shorter issue ‘Edit link
    is not working’
-   Bug fixing and documentation improvement

### Coding Period (16 July - 16 August)

-   First do the task ‘OGV Mediawiki Plugin’. This will take 7-10 days.
-   Further, go for ‘Mediawiki oAuth’. This will take around 4-6 days.
-   Then move with ‘Bring custom coloring back’ enhancement. This will
    take around 1-3 days.
-   Then go for ‘Auto position depending upon object’s width/height’
    enhancement. This will take around 1-3 days.
-   Then add a few additional things like ‘Responsiveness to the
    application’ and do the enhancement ’improve the directory structure
    for components’.
-   Pending bug fixing and documentation improvement.