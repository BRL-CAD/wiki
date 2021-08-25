# Personal information

# About me

-   Name: Anurag Murty
-   E-mail address: anuragmurty@gmail.com
-   IRC username: anuragmurty


**I am an MTech student of Computational Science at IISc Bangalore**

# About The GSoc Project

[Brief Description of my project on the GSoC
page](http://www.google-melange.com/gsoc/project/google/gsoc2012/anuragmurty/22001)

# Development Log

First task is compilation of BRL-CAD


BRL-CAD succesfully built from source

Learning to use the Software / Explore the code


Have Completed the tutorial on BRL-CAD available on the site(Basically
mged commands and USING the software)

Raytracing Commands related to my project work


having learnt to use rt , rtweight from a USERs perspective, going
through the respective codes and understanding the modules now

Wrote a small patch for bitv.c in src/libbu.Waiting for feedback:)

Going through the gqa program as I have been asked to learn to use and
understand it too

patch for ctype.c also submitted. waiting for reviews. had some problem
with the previous patch too. Turned out that it wasnt in the unified
diff format as required.

\[ PS: Some problem with IRC. Unable to join the brlcad channel. Should
be fixed in a while hopefully.\]

<u><b>`      21st to 23rd`</b></u>` -- done understanding code for rtexample.c. discussed with mentor(d_rossberg) about how to extend rt_shootray for getting the voxels. `

parameters to be used : size of voxels,rays to be shot per voxel,
minimum volume to be considered as threshold for considering. have
started with implementation of a first , very basic program to get
voxels.(one ray per voxel for now, simple shapes also).

first patch accepted.. test_bitv.c!! second patch i submitted
test_ctype has to be modified according to hacking guidelines...

working on rt_shootray for 3 views, which will be submitted today, but
in a little while.

Written rtexample_3view.c that uses the midpoints of the faces of the
bounding rectangular parallelopiped to shoot three rays in three
perpendicular directions and gives data of the partitions
encountered(the hit code is exactly taken from rtexample.c). the same is
being submitted as a patch.

Indentation changes made to test_ctype. Also, a typo related patch was
submitted yesterday. Working on shooting a grid of rays at object to be
raytraced(towards the negative x-axis). Should be able to submit that as
a patch tonight or maybe tomorrow.

i will be going through codes for libanalyze and libged commands as
directed by brlcad. Also, I will not be available on IRC tonight(as i
will be travelling)

<b><u>30/5/2012</u></b> : Got commit access today. Lot of time spent
trying to rebuild brlcad. Some problems with MGED dependencies.
Everything deleted and rebuilt. Working fine now. Though still unable to
locate what went wrong. Presently completing the code for shooting a
grid of rays and putting it in src/conv so I can make my first commit.

<b><u>31/5/2012</u></b> made my first commit. A simple, safe g-voxel
program which did not actually get voxels. Just shot a grid of rays.

<b><u>1/6/2012</u></b> i wrote a simple voxelize program. right now, it
just prints if the voxel in the path of each ray is in or out. Right
now, the parameters are hardcoded(parameters like threshold a voxel is
to be filled to consider as in, size of voxel in each dimension ,
others). I think i also will have to consider some other method apart
from only using the bounding box as in some cases(example, a 3-D plus
sign) too many rays are shot which might be a waste of time.

<b><u>5/6/2012</u></b> have shifted the evaluation of voxel to main and
writing code for multiple rays per voxel. though multiple rays through a
voxel is buggy(minor, most probably). Will commit as soon that is done

<b><u>6/6/2012</u></b> there was problem with voxel calculations when
hitDistOut was on a voxel boundary. Also, I was computing the ending ray
data slightly wrong. this was also rectified.

multiple rays are being shot now-- through same point because i have to
ask my mentor whether those rays have to be random and how to proceed on
volume calculations after that.

I have two variables for now- ray num threshold, threshold- depending on
how the IN/OUT of a voxel has to be determined. one of these two will be
discarded.

<b><u>7/6/2012</u></b> studying gqa.c

<b><u>8/6/2012</u></b> Made lots of changes to previous code of
g-voxel.c. Also, now running "./g-voxel \[.g file\] \[region-name\]" in
bin/ of the build directory outputs a file "voxels.txt" that gives a
frame by frame representation of the desired region.

<b><u>12/6/2012</u></b> g-voxel.c modified so it allows multiple rays
per voxel. for input raysPerVoxel what I do is shoot a uniform
raysPerVoxel\*raysPerVoxel rays, so probably this variable name is a
misnomer. again the output is voxels.txt which gives the output text
file frame by frame.

<b><u>14/6/2012</u></b> same as last time, floats replaced by fastf_t.
some unnecessary statements variables and statements removed(mistakes
pointed out by d_rossberg).. a major error was allocating space for ALL
voxels. so now as soon as a raytrace is done, the results are printed
out to file voxels.txt. thus at any point space for only numVoxels\[0\]
is assigned, major savings.

I need to change the structure for rayInfo so it includes region names
also. this means using pp-&gt;pt_regionp-&gt;reg_name from struct
partition but i am presently getting bugs in the result. so working on
this so that I canc hange the output format so it lists data region
wise.

<b><u>18/6/2012 -20/6/2012</u></b> structure for rayInfo modified.
rayInfo is structure for storing info each time a raytrace is called. It
contains a linked list of regions inside each voxel. voxels.txt now has
data in the format:

1/0 (coordinates of voxel) (region-name) (fill fraction)

where 1/0 tell you if the voxel is in or not(according to threshold).

also to store names in a local variable of main(), i have used
bu_vls_strgrab function.

<b><u>21/6/2012</u></b> corrected a bug i found while doing some tests
on g-voxel.c with some .g file inputs

<b><u>26/6/2012</u></b> first step towards moving the voxelize work into
a library. made a function that is called from main in g-voxel.c and
takes in as input userparameters for a voxelize and outputs a file with
the necessary voxel information. used a structure for input parameters
and additional inputs might be added later. TODO: implement a callback
function for writing result into the file.

<b><u>28/6/2012</u></b> implemented callback function for printing
results of g-voxel.c. moving it to libanalyze is next todo. slight
problem being faced : i am unable to commit using svn commit. svn:
Commit failed (details follow): svn: OPTIONS of
'<https://brlcad.svn.sourceforge.net/svnroot/brlcad/brlcad/trunk/src/conv>':
Could not create SSL connection through proxy server: Could not
authenticate to proxy server: rejected Digest challenge
(https://brlcad.svn.sourceforge.net) trying to fix for a long time now

<b><u>29/6/2012</u></b> callback committed, some more modifications

<b><u>2/7/2012</u></b> library- libanalyze changed for accommodating
voxelize functions, in voxels.c in libanalyze , all the functions are
defined. also, g-voxel.c modified and uses functions from libanalyze

<b><u>2/7/2012</u></b> modified call back and parameters to voxelize
<b><u>4/7/2012 and 5/7/2012</u></b> comparison against threshold not
made in voxelize now. sent as callBackData sent as input to callback
function and decision. same changes made to g-voxel etc also

<b><u>8/7/2012</u></b> went through ged-facetize which is going to be
template for ged_voxelize.

<b><u>11,12/7/2012</u></b> wrote a voxelize.c program for libged. This
has function ged_voxelize(struct ged\*, int argc, char \*argv\[\]).
However, There is segementation fault when I run the program.

<b>------------------------------------------------------------------------------

<b><u> POST-MIDTERM EVALUATION WORK

`note: this has been updated very late,towards the end of the GSoC duration`

</u>

`segmentation fault from the program voxelize.c was removed`

the location of rt_prep_parallel was changed from callinf function to
voxelize

15 july changed a very roundabout way to bu_vls_strcpy

16th july -analyze.h unused functions for voxelize removed

`  callback functions removed from analyze.h and included here`
`  rt_prep function added into voxelize function of voxels.c, callback removed`

19-july ged.h changed to have ged_voxelize function static callback
functions were added to voxelize.c and g-voxel.c

MGED hook to voxelize created help.tcl scripts changed to enable
autocomplete tclcad_obl.c scripts changed to enable autocomplete
callback function called create boxes made to actually make the voxels
for a given input primitive/collection some code cleanup was done in
g-voxel.c create_boxes function is called evrywhere instead of
printFunction like intial case.

till now, all the parameters of a voxelize were hard coded, now (with
Daniel's help), it takes command line arguments plus all the voxels are
in a user-specified region.

code cleanup, specially for respecting alphabetical ordering. voxel
sizes multiplied by local2base, since the user provides the numbers in
his own choice of units.