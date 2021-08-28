# How to create, edit or apply a patch

## Prerequisites

To handle and apply patches, BRL-CAD uses
[Subversion](http://en.wikipedia.org/wiki/Apache_Subversion).

`You will need to install Subversion (Often abbreviated as svn).`

If you're on a Debian/Ubuntu system you can get it by running:

    sudo apt-get install subversion

You can obtain the latest version of BRL-CAD by running:

    svn checkout https://svn.code.sf.net/p/brlcad/code/brlcad/trunk brlcad

If you are in the folder where the "brlcad" folder is and you run that
command, svn will only download updated/modified files.

## How to create a patch

In order to submit a patch it is important to have the latest version of
BRL-CAD from a Subversion repository checkout. Any changes you make to
files can be automatically captured in a standard file format called a
***patch*** file using 'svn' commands. Running this command will tell
you what files you have modified, added, or removed:

    svn status

If you added any new files, they will show up as lines starting with
'?'. To include new files in the patch, run:

    svn add myfile.txt

If you have removed any files, they will show up as lines starting with
'!'. You can include that change in your patch by running:

    svn remove myfile.txt

After you have added and/or removed files, the next most important step
is to generate a patch file (aka a diff file). Redirecting 'svn diff'
output will create this file automatically:

    svn diff > mychanges.patch

The last step is to read the patch file you created to make sure it 1)
includes all of the changes you intended and 2) does not include any
changes you did not intend. A patch file is a simple text format, so you
can review it using any text editor or file viewing tools (e.g., 'more
mychanges.patch'). Read it to make sure it contains what was intended
and only what was intended.

## How to Submit a patch

To submit a patch to the BRL-CAD tracker you must first create a
[sourceforge account](http://sourceforge.net/). Of course, if you have
one already, you don't need to create another.

Now, you can submit your patch on the [BRL-CAD
tracker](http://sourceforge.net/tracker/?group_id=105292&atid=640804) by
clicking "Create Ticket".

You should use the description field to explain what you did there and,
if necessary, what isn't working.

Be sure to check out the extensive
[Documentation](Documentation.md) and
[Main_Page](Main_page.md) for tutorials and
[Deuces](../task/Deuces.md) for ways to get involved!
