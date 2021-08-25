**Name:** Mandeep Singh

**IRC Nick:** Mandeep_Singh

**Blog:** **<https://mandeep7.wordpress.com>**

**GitHub Profile:** **<https://github.com/mandeeps708>**

**Brief Background Information**

I am a final year B.Tech. student of Computer Science and Engineering at
Guru Nanak Dev Engineering College, Ludhiana, India.

I have always been passionate about programming. My work on various open
source projects is briefed below:

-   *PyDrain-* A project for automating drawing creation in DXF using
    > dxfwrite library and calculating area of enclosed entities.

-   *Civil Octave-* This project is used for the Analysis of Dynamics of
    > Structures.

-   *Booking System:* A Django based web-application for booking seminar
    > halls.

-   I have experience of Image Processing using MATLAB.

-   Apart from this, I also have my profound interest in Web development
    > and Shell Scripting. I did several mini projects for fun and
    > learning.

For more details about my work, you may refer my GitHub account:

[*<https://github.com/mandeeps708>*](https://github.com/mandeeps708)

My knowledge of various open source technologies expands over

-   Python

-   Shell scripting

-   Web Technologies (HTML, CSS, JS)

-   Frameworks: Django, meteor.js, Bootstrap

-   CGI (Common Gateway Interface)

-   Databases: MySQL and MongoDB

-   LaTeX, Doxygen

-   Git, IRC and basic development workflow etc.

# Project Information

# Project Title: The FreeCAD Plugin Installer

# Brief Project Summary

My main idea is to implement a plugin manager for FreeCAD that will be
used to install/remove/update plugins and other unofficial workbenches
or modules and macros. Besides, this project will make the life of the
FreeCAD developers, workbench authors as well as the end-user easier.

# Detailed Project Description

**Current Scenario**

There are many plugins available for FreeCAD and developers are creating
more. So the task for getting pull requests, managing and merging them
becomes a tedious task. Quite similar is in the case of macros. And it
also makes the code base of FreeCAD a bit more or like bloatware to be
delivered to the end-user. Efforts have been done by the FreeCAD
developers to separate the installation of plugins from the FreeCAD
software itself.

One has to do manual work for getting plugins installed on their system
to be able to use them. So this project considers the issue and tends to
implement an universal plugin manager that will manage the plugins and
it will include the following:

1.  List all the plugins installed

2.  Remove the installed plugins

3.  Add new plugins locally/remotely

4.  Plugin Compatibility Test

5.  Update the plugins (basically git pull)

6.  Enable/Disable the plugin

7.  Adding Git support

8.  Implementing Plugin details (identifier)

9.  Package and dependencies resolver

As FreeCAD is having many workbenches/macros fully coded in Python so
they can be imported, without any necessity of compilation. As the
plugins authors have to go through the painful (and somewhat lengthy)
process of Pull Request on GitHub to get their code reviewed and
accepted. This project focuses on making the same process rather easier
to get the plugins working at the user’s end, so that user can integrate
designs modules into their projects as a plug-in with ease. So the main
idea is to present a simple, intuitive and interactive user interface.

The problem with the existing system is that it’s currently using manual
technique to get everything done i.e. it uses git submodules that have
to be fetched manually every time a workbench/macro code is updated.
Rather, it has to be automated.

**Project Goals**

1.  ***Better User Interface:*** The main objective of the project is to
    > helping the FreeCAD users to manage their plugins with simple user
    > interface to make the overall user experience better. This product
    > that will be delivered to the end user will include the UI such
    > that he could manage the plugins with a few simple clicks.

> **'Implementation Process**'

1.  A menu item or a sub-item will be added to launch the plugin
    > installer.

2.  Then it will proceed to a new window (tabular based) which will show
    > the plugins currently installed.

3.  It can have a checkbox beside each plugin to select/deselect it.

4.  There will be buttons like Enable/Disable, Remove (Uninstall) and
    > Update etc. for plugins. After selecting a particular set of
    > plugins, user will be able to click on a particular option
    > (button) as specified above.

Here is a prototype for the same:

![](img/image01.png)

1.  ***Getting list of installed workbenches and stored macros:*** To
    > get the list of installed workbenches and created macros, we will
    > first look for the specific plugin directory which will be
    > different for different operating systems. As FreeCAD is a
    > cross-platform application, we may use something like environment
    > variables or as suggested by the mentors. After getting listed all
    > the available plugins, the plugin installer will show the details
    > of the plugin like description, purpose of the plugin and some
    > other information.

2.  ***Adding/Removing workbenches and macros:*** After getting the list
    > of installed plugins, the user will be able to add new plugins
    > according to his requirements. It will allow the user to provide a
    > link to the Git hosted repository and install that directly. On
    > the back-end, it will clone the repository and place it in the
    > appropriate directory. If it’s planned to use a particular
    > repository for hosting the plugins, then what we can have is to
    > scan (fetch) for that repository and list down the plugins for the
    > user to choose from and install from the installer itself. For
    > this to be implemented, we can request the repository and can get
    > the json response of the available plugins on the repository and
    > which later on can be filtered with the installed plugins.

3.  ***Plugin Compatibility Test:*** The plugin authors can be suggested
    > to create a particular file i.e. a “plugin detail file”. This file
    > would contain a specific version of requirements e.g. Python
    > version needed, version of FreeCAD needed. Even if some dependency
    > is missed in the plugin detail file, the plugin installer will be
    > able to detect the plugin and perform some tests already laid down
    > to check compatibility. For example, this test may include a
    > module that will check for the Python version. One approach could
    > be that the tester module can try executing the plugin sub-module
    > and get to know if it’s compatible or not. If it’s found to be
    > incompatible, then it should revert the installation or in simpler
    > words delete the particular plugin directory.

The structure of the plugin directory may go like this. Suppose there is
a main plugin directory i.e. */usr/lib/freecad/Mod/Plugins/* and it
contains two plugins “Plugin1” and “Plugin2”. Then each plugin will have
some sub-directories (like images) or files (python modules). The tree
structure will look like following:

> Plugins directory (/usr/lib/freecad/Mod/Plugins)
>
> \|
>
> \| - Plugin 1
>
> \| \| - File1
>
> \| \| - File2
>
> \| \| - File3
>
> \| \| - File 4
>
> \| \| - Plugin detail file
>
> \|
>
> \| - Plugin 2
>
> \| \| - Directory
>
> \| \| - File1
>
> \| \| - File2
>
> \| \| - File 3
>
> \| \| - Plugin detail file

Then the idea is to have a “Plugin detail file” that will reside in the
plugin directory itself and will contain the following information:

-   Author Information

-   Plugin details like what the plugin is all about (description).

-   Path settings (like which file to load)

-   Dependencies details (like required Python and FreeCAD version) etc.

So this is the file that will be looked for by the plugin installer.

1.  ***Updates:*** The user can set his preferences for the duration to
    > check for updates for the already installed modules. As already
    > described, the plugin installer will try connecting to the remote
    > repository from where the plugins are to be fetched and check if
    > it contains some updated code. If some update (git fetch) is
    > detected, then the user may simply click on update and it will
    > simply do the git pull.

2.  ***Adding Git support:*** As discussed above, adding and updating
    > plugins will be achieved using Git hosted repositories. So it will
    > be essential to add Git support to make all those happen. On Linux
    > and Mac, it’ll be pretty easier to set up git via some shell
    > script. And for Windows, we can set up “git for Windows”
    > ([*<https://git-for-windows.github.io>*](https://git-for-windows.github.io/))
    > with the standalone (or portable) installer and then create a
    > batch (.bat) file for setting it up. As “git for Windows” includes
    > a program named “Git BASH” that includes bash shell and later
    > configuration can be done in it.

3.  ***FreeCAD dependency tracking:*** It’s good to be considered that
    > some plugins depends on other plugins to be able to work
    > correctly. As already discussed above, the plugin author will have
    > a “Plugin detail file” in the plugin directory. That file will
    > include the list of dependencies that needs to be resolved first.
    > We can incorporate something like *pypi* or a plugin manager like
    > *bower* such that plugin’s dependencies can be manageable.

# Milestones

**Community Bonding Period**

-   Having interaction on Mailing list and IRC.

-   Get to know the code of FreeCAD and try solving some existing issues
    > to get better understanding of the code.

-   Seeing the scope where we can reuse the existing code in an
    > efficient manner

**23 May - 31 May**

-   Understand the existing implementation of the plugin loader and
    > Macro installer and reuse whatever is possible.

**1 June - 7 June**

-   Write prototype (Qt window with basic widgets like buttons and
    > scroll) code to list all the plugins installed.

-   Discuss the implementation with Organisation and getting reviews.

**8 June - 14 June**

-   Integrating “Plugin detail list” with UI to implement “list all
    > plugins” feature.

    -   Get data from “Plugin detail list” and show in the UI window the
        > information like Author detail, plugin purpose and description
        > etc.

**15 June - 20 June**

-   Setup Git and its integration with FreeCAD.

    -   Making scripts for Linux and Mac (auto-detection of OS).
    -   Making batch file for downloading, installing on Windows and use
        Git Bash to set up.

-   Add new plugins remotely using Git remote repository link.

-   Setup UI to show the fetched available plugins from GitHub (or any
    > remote Git hosted) repository.

**21 June - 28 June**

-   After getting the plugins listed on the UI, implementing the remove
    > (Uninstall) plugins feature.

-   Testing and fixing found bugs

-   Documenting the code using Doxygen or any other recommended tool

-   Mid-term evaluation.

**29 June - 7 July**

-   Implementing keyboard shortcuts for launching Plugin installer.

<!-- -->

-   Document the code.

-   Adding Macros support

**8 July - 14 July**

-   Plugin compatibility test

**15 July - 21 July**

-   Working on feature Enabling/Disabling the plugin.

-   Prototype code for Update the plugins (basically git pull).

**22 July - 28 July**

-   FreeCAD dependency tracking

    -   Integrating with plugin detail file

    -   Adding support for plugin manager

**29 July - 7 August**

-   Brush Up the UI of plugin installer.

-   Discuss about the security concerns if we get some extra extra time.

**8 August-15 August**

-   More testing and cleaning.

-   Writing user documentation for the project.

-   Time to make up for missed milestone (if any).

**16 August - 24 August**

-   Cleaning and Testing code.

-   Final Evaluation

# Time Availability

I will be available 40 hours / week, if needed can spend more. No
restriction of time.

# Why FreeCAD?

I have always been fascinated by operating of CAD softwares. This
project got my interest. It will provide me a great opportunity to work
on a realistic project in collaboration with great experienced
developers.

# Why you?

I found myself fit for this project according to my skill set and
interest. I am very passionate to explore and learn new things. I
understood well the workflow of this project. I want to work for FreeCAD
organisation to gain more experience and enhance my knowledge about CAD.
I will also be actively contributing and maintaining the code even after
GSoC.
