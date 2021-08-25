# Online Geometry Viewer Proposal

**Name:** Deepak Kumar Sharma

**Email Address:** deeky.sharma@gmail.com

**IRC Username:** ih8sum3r

### Background Information

Final year B.Tech student of Information Technology at Guru Nanak Dev
Engineering College, Ludhiana, India. Google Code-In 2014 mentor with
BRL-CAD.

## Project Description

### Brief Summary

With the desire of glimpsing BRL-CAD’s native file format (.g format) on
the browser, OGV was commenced in 2013. JavaScript and Three.js are its
other main ingredients. In the year 2014, some extensive development was
performed when the unified project was reworked in JavaScript's full
stack framework that is termed as “Meteor”. With its use, it is
developed into cleaner, extra functional and also it has increased more
opportunities for improvements. In GSoC 2013, Harmanpreet Singh gave
kick start to this project in php and In GSoC 2014, Inderpreet Singh
worked on it. It’s an online 3D geometry viewer that runs on WebGL using
three.js. Older version of OGV uses vanilla PHP on server side whereas
JQuery and Bootstrap on the front-end. This proposal is aimed at
continuing the project by adding essential features and fixing bugs thus
improving the overall project to achieve the ultimate goal of making OGV
a production ready web application.

### Improvements in OGV

There are lot many things on which work needs to be done in order to
improve OGV functionality.

-   **Multiple Error / Success Notifications**

Notifications are important to your users because they let them know the
status of their jobs. OGV has a notification module, but it’s not
working properly. For an <example:->

When the user tries to submit data with an empty input field, an error
message is shown. If the same is repeated again, newer notification
along with the previous ones is displayed and the notifications would
keep on popping up whenever the user clicks on the submit button. I have
solved this error and submitted as patch but there are other problems
too. Whenever the image with exceeding limit is uploaded, a red bar
without any error message is shown. One may not learn the reason of
failure.

I am proposing to re-factor the notifications module so that these
errors can be identified and removed. Notifications.js a file that hosts
all the code for notification, needs close inspection and refactoring.
For example this error can be removed by passing the correct parament of
msg to the notification.

Following logic can be used:-

If (notification.seen) {

`   delay(5000);`

`   notification.delete();`

} else {

`   notification.show();`

}

-   **oAuth Module**

Nowadays, creating new account for different application seems a
difficult task to every user. Most of us try to use oAuth login like
with Google, Facebook, Yahoo account as it’s easy, effective and
efficient way to create/logging an account. So oAuth acts as one of the
most important feature of every application, but OGV lags this crucial
feature. Previous year, the idea to implement oAuth was taken into
account but no steps were taken to implement it. This time I would
consider it as one of the primary features to be implemented in OGV. For
oAuth I’m going to use oauth1 package.

Available functions listed below initiate the login process with an
external service (eg: Facebook, Google, etc), using OAuth.

Meteor.loginWithFacebook Meteor.loginWithGithub Meteor.loginWithGoogle
Meteor.loginWithTwitter

-   **Undertaking it to the current meteor**

Instantly meteor is active in the venerable form and conceding that
there can be a fighting chance if it is switched over to the latest
version, it will give birth to complications or it can be discontinued.
Nevertheless, I will lift it to the current version and take flight.
Currently. OGV in running on meteor version-1.0.0. My target is to shift
it to latest release of meteor and clean bugs, errors, make changes in
code etc. which may appear during version upgrade.

### Enhancement

-   **Production Ready**

Online geometry viewer is not yet production ready lot of work need to
done on it to make it production ready web application. So production
ready is one of the primary goal for this GSoC. One of the problems is
that it’s not deployed on BRL-CAD servers, for that I propose meteor up
package to bundle and deploy. After that there are things like debug
outputs in JS console and two accounts are registered by default, whose
passwords are written directly in the code. Such things are security
risks and need to be removed before deploying. Currently we do it
manually by going to specific files and removing details. I will add a
web interface from where we can directly shift between production and
development snapshots.

-   **Different modes such as wireframe in model viewer**

Wireframe model visualizes real-world 3D object in skeletal form. It
represents the underlying design structure of a 3D model. If wireframe
models are available, one may easily obtain the visualization of final
result.

Wireframe models are popular due to their efficiency. They can be used
for preview purpose. Rendering a complex model or an animation sequence
could become very much time consuming if all objects are to be rendered.

Three.js can serve us to create a wireframe. This can be done by setting
the wireframe property to true when instantiating a material.

-   **Support for Other CAD Formats**

Every CAD software package have their own and number of file formats
available. OGV supports to .g and .obj formats which needs to extended
further.

Availability of the different file formats is the necessity for
export/import module and it too defines interoperability of the
software. The main focus would be to widen its scope by providing the
support for the other CAD file formats that are commonly used like
g-stl, g-dxf, g-step etc.

This can be accomplished by using BRL-CAD’s inbuilt converter and
creating Javascript converter scripts for each of the new supported file
formats. There’s a conversion script in cfs-uplaoder.js for g-obj
conversion. I propose to make it generic. Like it will have variables
which can be changed depending upon type of input file.

filetype = InputFile.extension ; output = g; converter = filetype-g;

these variables can then be changed. when we get the .g file, to convert
it to obj file. Conversion from g to obj already exists in our codebase.
So nothing to worry about that.

-   **Online Converter Module**

CAD industry is filled with variety of file formats. There is STL, DXF,
DWG, G, OBJ and what not. BRL-CAD has state of the art conversion
support. A module, a special part can thus be made to convert one file
format to another. BRL-CAD has lot of converters, so if we are accepting
more cad formats, and doing conversions so it also makes sense to not
only import from various formats but also export to various file
formats.

-   **Embedding Model**

As listed in todo list, embed model feature is not yet implemented in
OGV. Embed feature help our models to post on social media, blogs,
forums or any website.

Advantage of sharing model is that just like we share, videos, images on
internet similarly in that way now we can share models too with the
addition of this feature.

For embedding models we need to generate an iframe as it’s generated
when we share youtube videos.

-   **Optimize obj conversion**

Currently we are saving obj files twice, once when they are converted
and once when they are transferred via collections. This leads to
wastage of space and duplication of files. I propose to delete those
unused obj files as new files are created. There are following ways in
which this can be done

`   * delete instantly, when new files are added to collection`
`   * delete regularly, at the end of day (or other such perioidic time)`

I will use nodejs file api for deletions. We already use some functions
of it in our current conversion.

-   **Loader indication**

Whenever the entity loads, some kind of notification must be given. For
successful loading, notification should be provided with the simple
confirmation message, or if, the entity has already loaded user must be
given indication with help of message. In case, if any exception occurs
along with the error message user must be guided to step forward.

This makes the Application itself more intuitive and user friendly. A
notification will help user how move forward. If its uploaded
successfully, user may continue viewing/editing otherwise if an error
occurs he might look towards solving the error itself.

For this I’ll use tympanus Creative loading effect or SVG Loader.
Example :-

$(function() {

`  $("#container").progressbar({ value: 50 });         `
`  $("#container").progressbar();`

});

-   **Camera position**

Presently, the position of camera is fixed and the entity size is
sometimes too small or too big. As a consequence, user have to find it
by zoom -in/ zoom -out in either case.

The entity should always be in the focus of camera as soon as entity is
drawn. Either there must be an option to scale or the position of the
camera should be adjustable accordingly.

The approach followed to sort out this would involve the calculation and
comparison of bounding box and window width, as a result camera would be
resized.

if (window.width &lt; boundingbox.width ) {

`   camera.reposition();`

}

-   **Allow to change colors**

Sometimes the materials used in the model are of different types, may be
steel, iron, brass, plastic, glass or such, Differentiating these could
be easier with support of colours moreover the models themselves might
be made of different coloured attributes for example a jeep might have a
yellow body, black tires, grey rims, orange indicators this could also
be differentiated with the help of colors support.

Data will be passed to JavaScript functions like vertex shader, fragment
shader which will be turned into pixels displayed in the WebGL canvas on
the screen.

### Milestones

-   **Week 1 (25th May)** : Upgrade to new meteor version. Solve issues,
    bugs for new version.

<!-- -->

-   **Week 2 (2nd June)** : Add oAuth module to login with google,
    facebook and github.

<!-- -->

-   **Week 3 (9th June)** : Loader indication while uploading models.

<!-- -->

-   **Week 4 (16th June)** : Improvise obj conversion

<!-- -->

-   **Week 5 - 6 (30th June)** : Add wireframe mode in model viewer.
    Test and document code before mid term evaluation.

Mid-Term Evaluation

-   **Week 7 (7th July)** : Automatic Camera reposition.

<!-- -->

-   **Week 8 (14th July)** : Allow to change colors.

<!-- -->

-   **Week 9 (21st July)** : Support for Other CAD Formats.

<!-- -->

-   **Week 10 - 11 (4th August)** : Test the working, check for bugs and
    code cleaning.

<!-- -->

-   **Week 12 (11th Aug)** : Deploy on production server.

<!-- -->

-   **Week 13 - 14 (18th Aug)** : Start documentation (using LaTeX or
    any other tool) including developers documentation, user’s
    documentation.

Final Evaluation

### Time Availability

I will be available 40 - 50 hours / week, if needed can spend more. No
restriction of time.

### Why BRL-CAD?

OGV being a lightweight geometric viewing software is very effective for
visualizing BRL-CAD files on browser. The software has full potential to
accumulate much more in the sphere of geometric figures and visuals.
With some proper investment in it’s development, it could definitely
exceed many expectations and become a Swiss knife for geometry viewers.

### Why me?

Graphics, combined with programming, is my passion. Together, they work
as a stimulus for my thought processes and I’m really excited to work on
a project entirely related to graphics. What really motivates me to do
my best is the idea about contributing to an open source project that
people may use around the globe.

I’ve been using 2D and 3D graphics softwares for quite a while and as a
user, I have the basic idea about what people look for, when they use
such softwares. I have also been through various sites which serve the
same like OGV eg: Sketchfab, Grabcad and I am really positive that this
project will definitely help me build a better outlook as a developer
and will certainly enhance my ability to better understand the
necessities that people may expect from Online Geometry Viewer and
provide solutions for the same.

I will definitely be a part of OGV development even after this project
is finished because I believe that delivering the product is not the end
stage yet, maintenance of the same is crucial after developing a
software, for its ultimate success. So I will continue to enhance and
extend its capabilities.

### References

-   [Meteor.com](http://docs.meteor.com/)
-   [Meteor Packages](https://atmospherejs.com/)
-   [ThreeJS](http://threejs.org/)