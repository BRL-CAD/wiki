Online Geometry Viewer Update

# Personal Info

Name: Oleksandr Dubenko

Email: odybenko@gmail.com

IRC: sniok

Phone: +48577173100

# Brief Summary

This project aims to improve Online Geometry Viewer in different ways:
UI update, code quality and improved model importing.

# Detailed summary

User Interface Developing and applying new style Remake feed view Add
simple model view Remake upload view Improve advanced model view Code
structure Use meteor’s recommended code structure Configure ESLint Add
comments (JSDoc) Model importing Import .obj with colors Add support for
.obj upload

## User Interface

### Developing and applying new style

Develop and user new consistent style. OGV’s UI have a lot of room for
improvements. I want to  i mprove and remake some parts of user
interface to create the best user experience.

### Remake feed view

Current profile and feed view should be improved. Most of it needs to be
remade. Improve simple view for displaying user feed. Simple profile
card on the left, actual feed in the middle, and recommended users on
the right (not shown). This view will be same for profile.

![](/wiki/user/img/Feed.jpg)

### Add simple model view

Currently you can’t quickly preview model, download and leave comment.
Proposed view provides simple interactive preview of the model,
information about model and comments.
![](/wiki/user/img/Normal_view.jpg)

### Remake upload view

Currently after selecting the file from computer it shows simultaneously
progress bar and editing view for model info which may be confusing.
Separating all steps of model upload and showing current step at the top
will improve user experience. Remake upload process into three steps:
Upload -&gt; File processing -&gt; Editing and saving. Generate model
preview at this step.

![](/wiki/user/img/Upload.jpg)

</figure>

![](/wiki/user/img/Save.jpg)

### Improve advanced model view

view, download, social buttons and color settings view. In this view
files only ) and change scene settings.

Proposed model view

<figure>
![](/wiki/user/img/Advanced_view.jpg)


### Use meteor’s recommended code structure

Meteor's recommended structure. It still needs work. Final goal is
modules.

### Configure ESLint

ESLint was added but a lot of rules was turned off.  Some work required
here.

### Add comments (JSDoc)

Also code lacks a lot of comments. I plan to comment as much as possible
using JSDoc standard. And if it makes sense to auto generate
documentation using JSDoc.

## Model importing

### Import .obj with colors

Use patched g-obj converter ( patch link) and import .g files with
colors using generated .mtl file.

### Add support for .obj upload

Add support for uploading .obj ( and .mtl ) files.

# Short bio

I'm studying Computer Science, I've been participating in last year's
Summer of Code as a student and Google Code-In as a mentor. I've been
tinkering with OGV and have experience in JavaScript and Web Development
and I think I have skills to complete this project.

# Milestones

Bonding period Discuss project and make more design sketches 1 - 6 weeks
Create new style Update and create all planned views Add .obj and .g
color importing 7 - 9 weeks Code structure ESLint 10 - 11 weeks Fix bugs
Add comments 12 weeks Clean up, test

# Time availability

I have my finals week begin 22.06.2017 until 05.07.2017 that could limit
my availability. After finals I’ll be available 40+ hours per week.

# Patch

This is my work on OGV since last summer.
[github](https://github.com/sniok/OGV-meteor/tree/eslint)
