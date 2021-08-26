# Project Details

------------------------------------------------------------------------

Name: [Mandeep Singh](/wiki/user/Mandeeps708.md)

IRC: Mandeep_Singh

Project: [The FreeCAD Plugin Installer](../gsoc_proposal.md)

Commits: [mandeeps708/PluginManager](logs.md#Coding_Period) @GitHub

------------------------------------------------------------------------

# Community Bonding Period

------------------------------------------------------------------------

-   Discussion about the project proposal.
-   Build FreeCAD from source on Archlinux.
-   Shifted to Ubuntu and tried building. Discussed the dependencies
    issue faced on IRC.
-   One issue was solved by creating a symlink of libfreeimage.so to
    /usr/lib from /usr/lib/x86_64-linux-gnu/ due to a bug on Ubuntu
    16.04 (Xenial).
-   Another issue I was facing was related to C++.

`   c++: internal compiler error: Killed (program cc1plus)`
`   Please submit a full bug report,`

It was due to the **make -j4** as it made the compiler run out of
memory. Never happened on Archlinux though.

-   Discussed to use **PySide** and Qt.
-   Learning PySide.

------------------------------------------------------------------------

# Coding Period

------------------------------------------------------------------------

**23 May** : Plan is to try out the existing pluginloader & addon
installer. Trying the pluginloader.

**24 May** : Had my last exam today. So couldn't do much. But read some
old conversations about the existing plugin manager on the FC forum.

**25 May** : Installed and used the pluginloader by microelly. Discussed
some general concepts like Workbenches, Plugins and Macros with the
mentor and how they are being dealt in FreeCAD. It downloads the zip's
from GitHub and unzips to the \~/.FreeCAD/Mod/ directory.

**26 May** : Installed and used the Addon installer and saw it's
working.

**27 May - 28 May** : Comparing pluginloader
(https://github.com/microelly2/freecad-pluginloader) and Addon installer
(https://github.com/FreeCAD/FreeCAD-addons\#1-using-the-installer-macro)
and listing out what we can keep or not for reuse. And getting mentor's
views.

**29 May** : Having other community member's opinions on the forum.
Discussed the plan about what can be done next. Looked at the
addon_installer code.

**30 May - 31 May** : Discussed the design with ickby and yorik. Parsing
macro code from wiki:
<https://github.com/mandeeps708/scripts/blob/master/FC_getMacro>

**1 June** : Improved code for FC_getMacro script. Ported it to use
python2 as well as python3. There is some compilation problem with
etree.pyd in lxml (shared lib) on Windows.

**2 June** : Weekly meeting + discussed and finalized some things like
code structure etc.

**3 June** : Went through some OOPS concepts and how to do them in
python.

**4 June - 5 June** : Think of some design and relations. Code structure
added to github.

**6 June** : Modified the fetch Macro Script to use BeautifulSoup (with
html.parser) instead of pyquery (lxml).

**7 June - 9 June** : Health issues. Also, got some problem with laptop.
Started learning about object oriented programming (with python).

**10 June** : Learned Inheritance in Python. Weekly meeting. Discussed
about the code structure.

**11 June** : Some experimentation with parsing from FreeCAD-addons
repo. Looking into PyGithub for GitHub API.

**12 June** : Finally get PyGithub working. Got list of files and some
more examples.

**13 June** : Fetching of only submodules using PyGithub. Got the
submodules and their related info. like submodule original URL.

**14 June** : Added more code to FetchFromGitHub class and created
instances of Plugin().

**15 June** : Mainly had the discussion today; about the work down and
what to do next.

**16 June** : Edited FreeCAD macro recipes wiki page to add a template
tag. Used sed command instead of doing manually. Basically, the template
wraps the macro links around a span having class "MacroLink".

**17 June** : Weekly meeting. Set goals. Fetched list of macros from the
FreeCAD wiki. Fetched URL, description, author of individual macro.
Code:
<https://github.com/mandeeps708/scripts/blob/master/FC_getMacro/wikimacro.py>

**18 June - 19 June** : Worked on GitHub API. Tried to find if we could
fetch repository name by using the repository URL. Talked to GitHub
officials regarding this. But it's not there. So tried regular
expressions in Python. And it's done.

**20 June - 21 June** : Fetched submodule info like author, description
etc. Also integrated Macro fetching code into the main.py file. Created
a separate getPlugins module that would be able to fetch all plugins
available. Currently, it's like hard coded with fetch classes names.
Will make it more robust.

**22 June - 23 June** : Mid-term Evaluation Period. Studied about
Exception handling in Python. Added exception handling code for basic
exceptions to both classes.

**24 June** : Mainly focussed on to find a way to register application
on GitHub to use OAuth. Found a method in PyGithub. But not sure about
its usage. Hence using Personal Access tokens as of now.

**25 June** : Initially, it took about 25 API calls to identify which of
the item is a submodule. But now it takes 1 API call to fetch basic
information and then used regular expressions to filter out the
submodules.

**26 June** : Some more exception cases to Macro class if a user didn't
correctly added a macro on the wiki. It'll get skipped.

**27 June** : Implemented getInfo() methods for both classes. The basic
information about the plugins will now be fetched through the
getPluginsList() methods. And additional things about a plugin like the
author and the description will be fetched through calling the plugin
with getInfo() method. For example: getInfo(PluginName), it will fetch
more detail about the plugin. This will be further used in the GUI to be
called when a user clicks a plugin entry.

**28 June** : Mainly discussed with the mentors about next task. And I
was suggested to get overview of the things like creating a design how
overall thing will work. And some other ideas like having a library that
could interact with all fetch classes to provide an interface to the
user to manage plugins (Wb+macros) altogether.

Bad health.

**3 July - 4 July** : Created some design about the workflow.

**5 July** : Shared the design with mentor and got the views. It lacked
some of the functionality. So added that.

**6 July** : Added a new function for getting all plugins to combine
instances of all plugins together.

**7 July** : Converted that function to a class and had an interface
(getPlugins.py[1](https://github.com/mandeeps708/PluginManager/blob/master/getPlugins.py))
for using this.

**8 July - 9 July** : Adds the interface class
[2](https://github.com/mandeeps708/PluginManager/commit/402c3aae6551df225893f15d04dc168b4696db3d)

**11 July - 12 July** : Searched about various methods through which the
interface can be improved to use getInfo() function within the interface
as it was the other class' method. Couldn't figure out much how to do
that.

**13 July** : Unable to work due to the power cut.

**14 July - 15 July** : Worked on getting the getInfo() function
working. Tried a few methods and some did not work. Finally, it worked!

**16 July** : Mainly read about threading in Python.

**17 July** : Extended the info() function to include the macro case
too. Also had a talk with the mentor. Some things need to be changed and
some improvements were suggested to make the code more generic so that
after adding another fetch class, the code should work fine.

**18 July** : Changed getInfo() functions to take plugin as an argument
instead of plugin name.

**19 July** : Removed redundant inheritance, tried adding a new x.fetch
= self. Having problems. Solving...

**20 July** : Made getInfo() of the base class to work as it does in the
derived ones. Changed the "repo.owner.name" to "repo.owner.login" as it
was not working (Related to GitHub API).

**21 July** : Made the interface more encapsulated so that fetch classes
aren't accessible through the interface. Now the code works fine. Even
with getInfo() too. Renamed a few things better.

**22 July** : Worked on adding install() method to the interface and
also getting Macro and Workbench paths to which these plugins are to be
installed.

**23 July** : Existing code improvements. Added basic installation
plugin interface. Implemented install() method for GitHub plugins. The
GitHub plugins are now being cloned with depth=1 (hence making it
faster).

**24 July** : Implemented the install() method for the Macro plugins'
installation. Also, had the weekly routine talk with the mentor.
Discussed a few existing issues related to some Macro installation like
the encoding problem, path problem etc..

**26 July** : Added some code for detecting the user-preferred Macro
installation directory or the default one and setting up one. If it
doesn't exist, it'll be created.

**27 July - 28 July** : Modified code according to the PEP8 coding
conventions and changed the creation of directories.

**29 July - 30 July** : Automatic directory creation for workbenches (if
it doesn't exist). Testing of all plugins! Better exceptions for Macro
fetching. Added code for fetching the macro with the non-English
characters (used encode function with utf8).

**31 July - 1 August** : FreeCAD Wiki now has the new CSS class for the
block of macro code if there are some other code chunks (that are not
the actual macro code). So in that case, they are parsed instead of the
original macro code because the syntax highlighting is having same CSS
classes. If there are multiple chunks are present, then we'll add a new
class "macro-code" to the actual macro code and if there is no element
with macro-code on that page, then the default method is taken (for
single code block).

**2 August** : Worked on blacklisting some macros. Some macros do not
contain any code. A few cases are there, that use some other method to
store the macro code. So skipping them as of now. Other cases are like
the macros are just a reference to the Workbenches (and info. related to
them). So make that cases simpler for the future, created a list
"blacklisted_plugins_list" that will contain the name of the macros
that are to be blacklisted.

**3 August** : Worked on implementing the isInstalled() method for both
the Wiki and Workbenches Fetch classes. What it does is that it checks
for the existing directory/file for the workbench/macro and see if it
exists. Also added a check in the install() method to see if it
isInstalled() returned False. Else it already exists.

**4 August - 5 August** : The FreeCAD wiki now have a new element i.e.
macro-version. It tells the current version of the macro. It'll help to
check if the macro is up to date or not. PluginManager.info() now
returns the plugin (with additional data). Also worked on the feature to
retrieve the contents from the Web only once. If the info. has been
fetched already, then no need to fetch it again. The method getInfo()
fetches everytime we call it (even with the same plugin, twice). Added
code to store the fetched info. in a dictionary and it's fetched when
calling with the same plugin.

**6 August - 7 August** : Added isInstalled() to the library interface.
Now the FreeCAD wiki pages have a new element "Version" defaults to 1.0.
It'll be helpful while checking for updates. Also added version to the
macro name while storing. Some code cleanup. Added uninstall() method
for macro plugins and also added the library interface for that. Further
added the same for the GitHub Workbenches. Also, read about the lambda
functions in Python.

**8 August** : Associate macro-version with the Plugin instance.

**9 August - 10 August** : Get the current version of the macro
(installed). Removed the dictionary used to store the fetched info about
plugins.

**11 August** : Better way to make PluginManager fetch the plugin info
only once.

**12 August** : Implemented the isUpToDate() method for Macro Plugins.

**13 August - 14 August** : Implemented isUpToDate() method for GitHub
Plugins too. Implemented update() plugins method for both the fetch
classes.

**15 August - 16 August** : Adds return statements to methods and update
the README for contributors.

**17 August - 20 August** : Macro version handling in update() method
working fine now. Used package "glob".

**21 August - 23 August** : Adds example usage, adds some more
documentation, README. Submitted the Final Evaluation.
