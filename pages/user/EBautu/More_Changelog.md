[category: Summer of Code](category:_Summer_of_Code.md) This is
the changelog for [more.brlcad.org](http://more.brlcad.org) GSoC
project. The project plan and specification is located
[here](../EBautu.md).

# April, 20 – May, 23 - Bonding period

During this period I got to know better Cliff, Sean and other BRL-CAD
comunity members and GSoC students.

I used [Drupal forums](http://drupal.org/forum) to gather some
information about what others with similar projects have done, what
modules have they used and how. It seems that most of similar projects
used CCK and views to power most of the site features, with some modules
specific to their content (audio, content, etc). Therefore, I plan to
use CCK and views, too and to suplement those with the custom modules
I'll create for handleing BRL-CAD models task.

During discussions with Sean, Cliff and Erik, some of the features were
left out, while others were promoted. Among the most import issues
pointed out were (sorted by importance, from most important to less):

-   model licensing
-   import cad geometry (at least .g files, maybe more)
-   export .g files
-   browsing & searching
-   queing operations (conversions, raytracing, etc)
-   multiple upload methods (some model files could be bigger than
    '1GB')

This period was also good for reading some more information about the
many BRL-CAD tools, since I'll have to use many of them in the second
part of the project.

# May, 25 – July, 10 - Coding period

During this period I have to do initial setup of more.brlcad.org with
Drupal and whatever existing modules I could reuse and select/adapt the
site theme of more.brlcad.ord.

## May, 23 - June, 2

I got an account on brlcad.org with mysql, SVN, SSH access and all the
tools/access rights fast and easy. I started out by installing Drupal
and some models: CCK, Views, captcha, flag, pathauto, token.

I decided to use Drupal 5 for various reasons: it's used by brlcad.org,
I'm more familiar with it (and contrib modules for it), I'm not very
fond of D6, there are more modules available for it. Not all modules I'm
using were commited/enabled from the begining; first I like to make sure
they work as advertised and that they are useful to me; for others, I
didn't know they existed and I added them later.

Also, after a long period of testing and (subjective) comparing many
themes, I have finally made up my choice about the site's theme. It's
[FireflyStream](http://drupal.org/project/fireflystreamcom)! I like it
very much because it's very light (color and code-wise) - my oppinion.
I'll probably need to change the logo (maybe one of Cliff's tires).

I also updated codebase for www.brlcad.org and its modules. During this
process, I cleaned up the Drupal modules and themes directories (by
moving non-core entries in other places) and installed new modules in
sites/all/modules (as recommended by Drupal). This makes later upgrades
easier.

With some additional configuration the new captcha module (version 3) is
able to add captcha points to the site contact form, something that Sean
and I talked about some time ago :)

Meanwhile, I got a database dump and the zipped code from the main site
and created a testing environment on my PC. This way I can test things
safer and easier and independently of whether my Internet connections is
working or not.

## June, 3 - June, 10

I tried two ways of implementing licensing: node type and CCK node
reference or taxonomy and terms. The advantage of taxonomy solution is
its lightweight and the easily ability to produce tag coulds from it.
However, it has limited features and posibilities for customization. I'm
not sure right now how far this licensing issue will go, so I'd like to
have some freedom. As thing will move on, maybe I'll come back to this
solution, but for now...

I decided to define a new content type for licenses (in addition to the
one I used for models). Then I setup models to require a single
node-referenced license. This will force users to select one of the
licences we support when submitting a model.

Cliff adviced me to start with some already existing open-source
licenses, like GPL. I think it's a good way to do it, because it's
easier to add new licences in the future that it could be to drop one
license and the reassign its models.

For reporting license problems, first I wanted to use the
[abuse](http://drupal.org/project/abuse) module. However, it's still in
beta and someone advised me to look at a more feature-rich module,
called flag.

Using the flag module I defined a new type of tagging, which will allows
users to report whenever they notice a license infringement. The
administrators can retrive a list of the marked models in order to check
the report.

*TODO: I think I could integrate this tagging with CIA notifications, so
that messages are sent when content is tagged.*

## June, 11 - June, 16

I installed and configured the pathauto, token, imagefield, filefield
and nodequeue modules. These will allow the site to use user friendly
addreses. I decided to use the following patterns for content:

-   pages: content/title-raw
-   licenses: license/title-raw
-   models: model/title-raw
-   stories: news/yyyy/mm/dd/title-raw
-   users: user/username

I'll probably need soon the token module for the custom modules I'm
working on (to create the model preview images).

The last days I've been checking out some WYSIWYG editors modules for
Drupal. There are many out there, although it seems that lately, many of
them have converged towards the [WYSIWYG
API](http://drupal.org/project/wysiwyg) module. Mainly, I focused on
testing and comparing browser compatibility and features for the
FCKeditor, TinyMCE, HTMLArea (using Xinha), widgeditor, and some others.

The most complete/complex editor was probably TinyMCE. It has many
features and plugins. However, once enabled, it seemed to be too much
for the simple model descriptions: most users will probably to very
little formatting. Also, all these features have with some weights
(bigger files and longer loading times). The same thing goes for
FCKEditor (which also presented some formatting issues) and Xinha (which
has some issues with Opera). On the hand, some other modules (like
BUEditor) are too simple and don't seem to help very much in editing
your content.

In the end, I decided that widgeditor offers the best balance between
features and lightweightness, so we'll stick with it for now.

## June, 17 - July, 6

-   June 17 - I tryed to find a module that allows FTP uploaded files to
    be included in filefields. I found filefield sources module that
    does something similar, but not exactly, it's still beta and only
    available for Drupal 6. I also found a forum post from the filefield
    author saying this feature is not suported and will never be (unless
    commissioned as a payed job). So I decided to implement it myself by
    modifing the filefield module. Meanwhile, I also started to commit
    the other modules I'll use and tomorow I'll copy the database from
    my PC to the server.
-   June 18 - I finished implementing the local file selection features.
    This means that model files can be uploaded via the web form or FTP
    (and later selected). The file selection uses AJAX (when available)
    to present a list of potential selection. I also finished uploading
    all the modules. I lost some time struggleling nodequeue because
    some files had different line endings (Unix, DOS and MacOS) and were
    rejected.
-   June 19 - I finished bringing everything on the live server. For the
    theme, I fixed some small bugs. I have created a site logo using the
    humvee from the BRL-CAD gallery and customized the maintenance page.
-   June 20 - I started working on the custom modules for integration
    with BRL-CAD.
-   June 21 - June 28 - I was away to Iasi to attend and give a talk at
    the summer school ECODAM 2009 (focused on applications of
    Evolutionary Computation in optimisation and data-mining). In the
    few spare moments I got, I refined the design of the custom modules
    for integration. They will use mged with custom scripts to perform
    actions on models.
-   June 29 - I worked on the BRL-CAD code for raytracing models.
-   June 30 - I tested (a bit unsuccessfully) various mged commands to
    retrieve metadata from models. I seems that mged outputs to data to
    stderr instead of stdout and when supplying 2 commands separated by
    ; only the last gets executed. Erik said this looks like bugs. I was
    unable to get a command to list the trees of the top objects (eval
    tree \[tops\] doesn't work). I also worked on an attempt to
    implement a multistep model submission form. This seems the only
    approach to allow users to select which objects to render.
-   July 1 - I finally realized that mged actually supports fully Tcl
    syntax. I started learning basic Tcl and writing the integration
    scripts for object hierarchy retrieval and metadata retrieval. The
    custom module will autodetect and support multiple BRL-CAD versions
    though using these scripts.
-   July 2 - I implemented a connector to PHP through Tcl scripts and
    redirects, and I started implementing scripts (metadata until now).
-   July 3 - Metadata retriving is completed (tcl scripts and Drupal
    code). For now I store title, db version, units and summary, but
    this can be extended with other information since it has the
    customizable tcl scripts.
-   July 4 - I rewrote the php-mged integration part to use
    proc_open/proc_close functions instead of exec. This allows more
    flexibility, including parameter pass between PHP and mged. I
    implemented the raytracing scripts and code. Last couple of hours I
    try without success to fix a bug in filefield module that prevents
    proper cleanup of unused files.
-   July 5 - A lot of things got done today: I fixed the bug in the
    filefield module; I implemented the queueing process (twice, first
    with nodequeue, then with flag); I added some tags for models; I
    optimized and improved the thumbnail generation process (now allows
    customized and automatically generated images) and added a thickbox
    gallery for them; I customized some aspects of the theme; I ported
    everything on mode.brlcad.org and \`\`Erik helped me by installing
    the lasted brlcad version.
-   July 6 - I fixed some bugs. I copied everything on more.brlcad.org
    and submited two models live for testing. I noticed some more bugs
    on more.brlcad.org (raytrace images are created in the wrong
    directory and title is not retrieved correctly). I fixed the later
    one.

## July 7 - 31

-   July 7 - I started looking at the other features that I have to
    implement: better browsing/search, better model theming, allow users
    to select the raytracing objects, multiple formats.
-   July 8 - Today had less time to work, but I focused on the model
    theming. Especially the teaser of the model should provide enough
    information to attract the user. This now includes the thumbnail
    image of the first (which should be more appropriate one, not just
    the top one).
-   July 10 - Yesterday and today I did some experiments with multistep
    forms in order to allow users to select which object to show in the
    images. I'm not very happy with the solution I got so far, so I'll
    have to work some more on it. The main problem is that multistep
    submissions are not very easy to implement in drupal. I foresee the
    same problem (maybe harder) will arrise when implementing the
    multiple format upload and conversion.
-   July 14 - Last two day I started to implement the object selection
    for raytracing. In order to do that, I had to reimplement the
    php-mged interface in order to support multiline outputs. I needed
    this feature in order to retrieve the list of the objects in the
    database (and their features). I'm also testing a rewrite of the
    raytracing feature because after some talks with \`\`Erik (he
    mentioned that for realy large databases, loading in mged can take a
    few minutes). If this works, metadata extraction and raytracing will
    be done by a single script, starting mged only once per database.
-   July 17 - I finished implementing the new php-mged interface which
    allows to extract model metadata and create all raytracing of a
    model with a single call to mged. This should improve performance
    for raytracing large models or doing many raytraces on a single
    model.
-   July 18 - I finished implementing object selection for rendering.
    The user can select which objects from the model file will be drawed
    before raytracing. In order to do this, I developed a new model that
    allows displaying multicolumn select lists. I also extended the
    filefield and imagefield modules to allow the use of the Node Id in
    the path. This will solve the problem of images being saved in a
    single directory.
-   July 20-21 - I started working on conversion. According to initial
    chat with Starseeker and Brlcad, the original file that the user
    submitted should still be available after conversion. Also, another
    request is to make the conversion part of the off-line queue-based
    processing system. I created a new CCK filefield for the original
    submitted file and now I'm implementing the conversion and system.
-   July 22-23 - I don't know what happened with the activity log for
    these two days. I'm pretty sure I submitted it and watched it show
    up, but now I don't see it anymore. Maybe I clicked preview instead
    of save and then I closed the browser. Basicly I worked on the
    conversion code.
-   July 24 - Wow! I worked all day, did a lot of code cleanup,
    refactoring, and in the end, I implemented the conversion from/to
    BRLCAD file. Works really nice, I'll port it on the server on
    Monday.
-   July 25 - I added automatic detection for supported file formats.
    Now, when you create a new file field named forma_file (where
    format is a supported BRLCAD format), models will be automatically
    converted to that field. I implemented a new script system and I
    added fivestar ratings. There is still work to do on the theme and
    site browsing.
-   July 27-29 - I added various browsing features (by rating,
    popularity, etc). I implemented a very light download counter for
    model files, fixed some bugs in conversion code. I had to make some
    changes to the raytracing code because mged is starting rt in
    background (which creates problems with PHP IPC functions). I put
    everything live and started testing.
-   July 30 - I got the cianotify module I developed during the
    application period and implemented more features and settings. I'll
    use it to provide feedback in irc about site activity.
-   July 31 - I finished testing the cianotify module. I refined the
    model processing code so that new raytraced images are produces only
    if necesary. This reduces the reprocessing times with 80% on models
    of small-medium complexity.

## August 3-Today

-   August 3-6 - I fixed a few bugs. I changed the licence from node to
    vocabulary because it's lighter and give more features (like
    tagcloud, models with the same licence), and changed the theming
    accordingly. I copied everything on production and setup CIA notify.
-   August 7-15 - I posted more example models on the site to check test
    it some more. I removed the readonly option from mged so that the
    model titles get displayed correctly (the problem is in the BRL-CAD
    version installed on the server, but it was fixed in CVS). I added
    service links and link back code on the model pages so that users
    can link back to us easily and votes on social sites the models they
    like. The service links are not displayed for visitors right now (I
    don't know why, but I'll fix it after GSoC final evaluation, so that
    I don't break the "pencils down" rule).
