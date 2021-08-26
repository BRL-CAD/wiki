[category: Summer of Code](category:_Summer_of_Code.md)

## Abstract

The more.brlcad.org website (MoRe as in Model Repository) will help
build a common repository of BRL-CAD models, which will allow BRL-CAD
users to share their models and to easily locate useful models. An
advantage of using Drupal both for the repository and the main site is
that we can integrate the two sites (use the same code base, share users
accounts, etc). The activity logs for this project are
[here](EBautu/More_Changelog.md).

## Description

This project will focus on developing a Drupal-based web application
that will allow BRL-CAD users to browse BRL-CAD model repositories,
search, download and comment on models, as well as publish their own.
This will permit users to share their models with the community, in
order for others learn from their models, to increase their productivity
and reduce modeling time. At the beginning, the application will be
hosted on the more.brlcad.org (MoRe = Model Repository), but in the end
it will also be packaged as a Drupal installation profile, allowing
other users to quickly setup their own repositories.

I plan to build the model repository website using mostly existing
Drupal modules and to develop new ones only where needed (i.e. extract
metadata from models, generate thumbnails from models, convert models).
The site will have a light design based on strict XHTML and CSS
standards. It will use clean URLs in order to increase the friendliness
towards users and search engines.

The CCK module will be used to define custom fields for each model node
and comments and fivestar voting will allow users to provide feedback on
the models they used. Each model will have its own page with information
on the model (name of the model, author, description, comments) and
links to related pages: model file downloads, similar models,
screenshots, etc. A versioning system will be setup so that version
updates of models are preserved and available to users.

Apart from model pages, the site will also feature book node pages
allowing user to share their modeling know-how with others. I hope that
with time and help from the community, some of these will evolve into
real tutorials or even books (as was the case for Drupal, Moodle, and
other open source projects).

When submitting new models, users will provide some information about
the model (name, description, tags, etc), and upload their file(s).
Users may also upload image files of the model that best showcases their
features. Administrators will be able to promote interesting images to
brlcad.org’s gallery.

Models may be uploaded in various file formats supported by BRLCAD and a
custom module that will use BRL-CAD tools to automatically create
thumbnails and to convert to other formats (as a cron job or on the fly,
depending on the server configuration).

The site will allow various searching and browsing methods: browsing by
author and by tags, searching by model name and advanced searching, tag
clouds to show largest model categories, etc.

The MoRe BRLCAD site will support automatic content translation
(english, french, german, italian, etc) and critical activities (user
registration, model submission, model commenting etc) will be protected
by CAPTCHA validation in order to prevent spam.

## Schedule

-   April, 20 – May, 23 – discus web site features with the mentor;
    collect feedback from the mentor and community (both BRLCAD and
    Drupal).
-   May, 25 – June, 7 – setup more.brlcad.org with Drupal and existing
    modules; adapt the site theme of www.brlcad.ord
-   June, 8 – July, 10 – develop custom modules for specific tasks
    (import model metadata, thumbnail generation);
-   July, 12 – August 8 – develop custom modules for specific tasks
    (automatic model conversion);
-   August, 9 – August, 15 – remove reported bugs
-   September, 3 – submit code and resource files to Google

## Completion criteria

The more.brlcad.org will allow users to search and browse for models
using various criteria, download models, and submit new models.

## Results

The more.brlcad.org website will help build a common repository of
BRL-CAD models, which will allow BRL-CAD users to share their models and
to easily locate useful models. An advantage of using Drupal both for
the repository and the main site is that we can integrate the two sites
(use the same code base, share users tables, etc).

## Conclusions (added at the end of the project)

When the "Firm pencils down" day arrived for GSoC 2009 this was the
implementation status of the requirements for our model repository
project (collected from IRC chats with starseeker, brlcad, \`\`erik, and
others, and presented in random order):

-   have a clear licensing: implemented using a taxonomy
-   HTTP upload method: implemented using a customized filefield module
    (which allows normal and Ajax uploads)
-   other non-HTTP upload methods: implemented using a customized
    filefield module; users can upload their files through FTP (or other
    methods) and then select those files in the submit model form (using
    Ajax completion)
-   possibility to report abuse (licence infringement): implemented
    using the the flag module (initially was node_queue, but was later
    replaced)
-   automatic metadata extraction: the brlcad custom module reads the
    summary, title, units, database version, objects list, and top
    objects from the models.
-   information from the model to be accesible on web (web-ready
    information capabilities): metadata extracted from the model is
    filled into CCK fields which can be further edited
-   categorize the model through the website: implemented using
    taxonomies (one for licence, one for keywords)
-   visualize the model: the imagefield module is used to store model
    raytrace renderings (automatically generated and/or uploaded by the
    user)
-   automatic raytracing: the brlcad custom module automatically
    raytraces models, convert the raytraced rendering to png and adds
    them to the imagefield CCK fields.
-   captcha points for submissions: implemented with recaptcha
-   uploaded geometry gets queued for addition, views are queued for
    rendering, etc: when submitted or edited, all models get flaged as
    "requiring BRLCAD processing". The brlcad custom module process
    these models one by one, when the cron task is triggered (or when
    started manually).
-   import cad geometry: the site accepts uploads in many formats (g,
    asc, dxf, stl, iges, euclid, etc); when processed, for each model a
    .g model file is produced.
-   export cad geometry: the site allows the conversion of the .g file
    to multiple formats (asc, dxf, stl, iges, euclid, x3d, dxf, vrml,
    etc). This is enabled automatically by creating a filefield CCK
    field named \`\`format\`\`_file in the group_files group of the
    model content type (where format can be: asc, acad, autocad, euclid,
    iges, stl, tankill, vrml, x3d)
-   browse: implemented with views, using various ordering methods
-   provide a strong feedback loop (like cia and/or e-mail notifications
    on changes): the cianotify custom module sends cia notification on
    various (customized) site events (e.g. a model is submitted, a model
    was processed by BRLCAD, a user registered, etc)
-   rating system: implemented through fivestar module
-   submission should have a cited source and the submission process
    allowing that source to be specified: there is a required CCK field
    for it.

Other things (not explicitly required, but implemented):

-   download count: implemented with a custom made very light download
    count module which works both for private and public files
-   tag clouds: implemented with taggadelic module (customized to fix
    some caching bugs)
-   brlcad processsing optimizations: A non-preemptiv processing time
    limit is implemented to prevent long task from keeping the server
    busy. Many other optimisation methods are also implemented: files
    are not converted between same format (just linked together), only
    the misssing renderings are generated, only the missing file formats
    are converted, etc.
-   support for multiple version of BRLCAD: all BRLCAD related task are
    externalized in TCL scripts (these scripts will be very similar for
    most versions, but have some special processing for a few versions).
-   customized view points and view sizes: the number, size and the view
    points of the automatic raytrace renderings can be changed in the
    site admin UI.
-   allow users to select which objects should be to render: object list
    is read from the model file and custom made CCK widget (a
    multicolumn select list) allows users to select to object to render
    (by default, the top objects are selected).

These things I did not implement:

-   a special flag to note whether it's a solid model or not: i didn't
    focused on this one (it can be done by parsing the object list:
    there's only 3 primitive types we support that aren't solid)

## See also

-   [Activities logs](EBautu/More_Changelog.md)
-   [Model Repository site](http://more.brlcad.org)
