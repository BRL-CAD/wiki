## Preface of Study

------------------------------------------------------------------------

### Pre-November 8, 2012

##### Summary of events


After finishing up the summer SEAP high school internship working on
BRL-CAD, I wanted to continue working with BRL-CAD. After finishing up
my Calculus 3 course (getting an A!!), the arrangements were made for my
Independent Study. My hard drive has been on the fritz ever since this
summer. I bought a new hard drive around Halloween and loaded up fedora
17 64-bit, and downloaded all necessary packages to build BRL-CAD and
compile code. I completed the array write to file program, with limited
problems.

##### Goals Accomplished

-   Finished up calc 3 course with an A
-   Downloaded the BRL-CAD package
-   Completed the array write to file C program.

------------------------------------------------------------------------

### November 8, 2012


Created the wiki page. Worked on reading array from file, have an issue
with the program not reading the file correctly. Attempted first build
of package from svn, had an issue when running "make" command, fixed it.

### November 9, 2012


Finished the reading array from file, after fixing an error with memory
allocation and pointers. Started looking into patch making for open
source projects.

### November 13, 2012


Started working on patch for moving comments from source to header
files. Built BRLCAD in BRLCAD src directory accidentally, re-downloaded
and rebuilt source.

### November 14, 2012


Continued to move comments for the patch. A little bit of confusion on
what to do, mainly do I keep the comments in the .c file or just cut
them out?

### November 15, 2012


The majority of the patch was done today.

### November 16, 2012


Wisdom teeth removed.

### November 19, 2012


Out for the day to recover from Wisdom teeth surgery

### November 20, 2012


Completed moving comments for BRL-CAD patch.

### November 21, 2012


Got caught up in holiday home cleaning and home baking

### November 21 - 25, 2012


Thanksgiving break. Attempted to find a list of bugs for Mozilla on my
free-time.

### November 26, 2012


Mozilla Built very slowly. Finally found a list of quick bug fixes for
Mozilla. Started work on the bug fix.

### November 27, 2012


Short period, Continued work on patch for Mozilla, getting some help
from contributers over at Mozilla.

### November 28, 2012


Short period, Finished patch for BRL-CAD, sent in when I arrived at a
good network connection (home). Patch ID on SourceForge: 3590871

### November 29 - 30, 2012


Worked on the Mozilla patch, finally been given assigned to status.

<https://bugzilla.mozilla.org/show_bug.cgi?id=815921>

I have been over complicating how to solve the problem, which has been
giving me many delays. A contributor pointed me in the right direction
with another similar bug. Will finish up the first version of patch
tomorrow.

### December 1-2, 2012


Finished up the big bulk of the work for the Mozzila patch.

### December 3, 2012


Built Mozzila with first version of patch (took a good amount of time).
Corrected for dependencies and references to the edited files.

### December 4, 2012


Another contributor uploaded a patch before I could get my patch up.

#### The Patches: A look back


Slow to finish patches; lost the assignment of both patches because of
this. Patches require quick turn around from assignment to upload. Also
includes quick understanding of concepts and the goal of the patch.

------------------------------------------------------------------------

## PDB-G

### Reading pdb files

------------------------------------------------------------------------

### December 5, 2012


Wrote up the pdb-g.c file. Placed it in proc-db/, Made patch, built
successfully, and submitted to Mentor.

### December 6, 2012


Edited patch, added some of the args. Looked up a few things on command
line args.

### December 7, 2012


Edited patch, started adding the command line argument management into
the code.

### December 8-10, 2012


Added check for validation of files both pdb and g. Built successfully,
created patch. Bad network connection at school, sent along at home.
Created new wiki page for summary of project and schedule.
(http://brlcad.org/wiki/User:Jacksixb/Proposal)

Also finished applying to Cornell, will hear from 3 of my colleges this
Friday (knock on wood)

### December 13-14, 2012


Edited pdb-g.c file for stylistic changes based on the standards
outlined in the HACKING file. Started work on the next edit. GOT INTO
University of ILLINOIS! (number 3 on my list) tomorrow I learn of MIT!

### December 17, 2012


Ran template.sh to add header/footer to the C file. Got deferred to
regular decision at MIT, will be hearing the final decision mid-march
sometime.

### HAPPY NEW YEAR!

### January 7, 2012


Getting back from the holidays. pdb-g was added to the trunk. Sent along
the patch for reading the TITLEs of pdb files. This source:
<http://www.wwpdb.org/documentation/format32/sect2.html> assisted a lot
in doing it.

### January 9, 2012


Found a few inconsistent things within patch \#4. Specifically calling
malloc and strcmp instead of calling bu_malloc and bu_strcmp.

### January 28, 2012


Finished up finals last week. Started the mid-year report/start of final
report.