## Community Bounding Period

**Get the commit access**

Submit two patches for nmg part of BRL-CAD. URLs as following.

-   [Unit test for
    nmg_mk](https://sourceforge.net/p/brlcad/patches/272/)

<!-- -->

-   [Unit test for
    nmg_copy](https://sourceforge.net/p/brlcad/patches/273/)

**Read the relavant Codes**

Read and be familiar with nmg-related codes in BRL-CAD.

**Acquired knowledge**

-   Keep code style consistent is important for Open Source Community.

<!-- -->

-   Comments greatly helps others to understand the function of routines
    and structs. Codes should be changed before fully tracking the call
    order of routines and totally understanding the comments of them.

<!-- -->

-   That's a really good ideas to submit one or two patch to know the
    coding convention of the community. As a chinese saying goes,
    sharpening your axe will not delay your job of cutting wood.

## Work Perod

### Week 1

**Monday, May 19**

Read TODO, HACKING, COPYING and other files again. Be ready for formal
coding job.

**Tuesday, May 20**

Find and read some pages about the details in using SVN and CMake.

**Wednesday, May 21**

Get the commit access for BRL-CAD successfully. What a day to celebrate!
Now, I begin my work on a branch for NMG reorganization. Remove model
and nmgregion struct, Then ready to fix all compilation errors.

**Thursday, May 22**

Rewrite nmg struct to fit BRL-CAD better. Remove model and nmgregion
struct, Then change shell struct as following.

-   remove member: l (bu_list);
-   remove member: r_p (nmgregion pointer);
-   add member: magic (uint32_t);
-   add member: manifolds (char pointer);
-   add member: maxindex (long);

**Friday, May 23**

Fix the rest compilation errors due to fit the new nmg structure.

**Acquired knowledge**

-   Committing without breaking the build is always the best choice. Try
    to use comment to achieve this point and record such codes in TODO
    file for fixing later.

### Week 2

**Monday, May 26**

Continue to cleanup the codes.

**Tuesday, May 27**

Until this afternoon, I finished most of the removing job. But I find
some places cannot simply replaced the model/nmgregion with shell. e.g.
the routine nmg_merge_shells used in nmg_booltree_evaluate(...) and
nmg_boolean(...).

**Wednesday, May 28**

I discuss my concern with Daniel. He suggest me to use
nmg_comb_internal to deal with such situation. And the whole job will
be done if NMG part runs good after I do all replacement.

**Thursday, May 29**

I study carefully about the the function about nmg_comb_internal and
related codes. e.g mk_lfcomb(), mk_addmember(), and so on.

**Friday, May 30**

Many places should be changed again because I missed the
nmg_comb_internal. I review the codes in NMG parts one by one.

### Week 3

**Monday, June 2**

Fix all compile errors in librt. There is no 'model' and 'nmgregion'
existing in this lib basically.

**Tuesday, June 3**

Fix rest compile errors in libged and mged. Now mged can run but the
result of facetize still remains wrong which will be fixed later.

**Wednesday, June 4**

Read the file 'Introduce to MGED' again, make clearer about the region
usage in BRL-CAD.

**Thursday, June 5**

Consult Daniel about how to deal with the rt_comb_internal level of
nmg operation. There are two sample for reference:

-   src/libged/voxelize.c \[mk_addmember\]
-   src/libged/comb.c \[_ged_combadd2\]

I study the codes but still confused about parts of them. I will take
more time being back to understand it later.

**Friday, June 6**

Organize the declaration and implementation about nmg in librt. Then,
Check the comments for nmg files. It must be invalid that most of them
are located in \*.c file, not in \*.h file.

**Saturday, June 7**

I assign working shell from facetize_tree to working instance directly.
Now the facetize routine can deal with single shell.I test rcc and sph,
and it works good but still need improving.

**Acquired knowledge**

-   Interface description should be located in \*.h, while
    implementation documentation can live in \*.c. As for this kind of
    question, libbu is a golden example.

### Week 4

**Monday, June 9**

Check the functionality of rt_comb_export5/rt_comb_import5 in comb.c
and rt_nmg_export5/rt_nmg_import5 in nmg.c,

-   The rountines in nmg.c can deal with single shell, but not
    combination tree.
-   The rountines in comb.c can deal with combination tree, but not nmg
    structure.

To fit new-nmg structure, I need combine these two functionality.

**Tuesday, June 10**

Spend some time to understand the export/import principal in BRL-CAD. In
old nmg, the model::maxindex is used to count nmg element, e.g. face,
edge, vertex. But in new nmg, to deal with the binary tree structure, I
write a new routine 'nmg_tree_maxindex_count' to count the sum of all
shells.

**Wednesday, June 11**

Daniel send a test report about facetize functionality. I repeat the
process of the test, then see the same result. It seems ASCII (text)
representation for nmg is a good way to test relevant routines.

**Thursday, June 12**

I try to change nmg import/export routines to fit new nmg structure.
Make the following change.

-   rt_db_internal::idb_ptr points to an instance of
    rt_comb_internal.
-   rt_comb_internal::tree points to an binary tree by using tree.
-   In each leaf node of the binary tree, tree::tr_op should be
    OP_NMG_TESS, tree::tr_d.td_s points to a shell.
-   In each non-leaf node of the binary tree, tree::tr_op should be
    OP_UNION.

**Friday, June 13**

I devise another thought to make the change of nmg import/export. Write
two adapter functions before nmg export/import, thus I needn't change
existing codes in nmg.c, just add two function. But the model and
nmgregion struct to be retained in rt_nmg_export5/rt_nmg_import5.

It seems a bad idea and be rejected.

### Week 5

**Monday, June 16**

Rewrite nmg_clone_shell routine in nmg_copy.c to fit new nmg
structure. Then correct the bugs in unit test for it.

**Tuesday, June 17**

Rewrite tea_nmg unit test to fit new nmg structure. But It's difficult
to check the result since the reorganizaion for nmg export/import hasn't
been finished.

**Wednesday, June 18**

change some tesselation routines for primitives to fit new nmg
structure. revert export/import to be avaliable to single shell.

**Thursday, June 19**

I test the tesselation result of following test case in trunk version:

-   hollowed a big sphere with a smaller sphere.
-   two sphere in certain distance.

All result just has single nmgmodel and nmgregion tested by function
'nmg_pr_struct_counts'.

Discuss with Daniel and Sean about the reorganization strategy. I make
sure the tesselation result is always single shell which seems simpler
than expected.

Some research should be done to make sure ANYTHING actually does create
- an nmg model with multiple nmgregion with one or more shells per
nmgregion. - an nmg model with a single nmgregion with more than one
shell.

**Friday, June 20**

I check the codes of tesselation for 43 primitives according to
yesterday's discuss, each just create single region and single shell.
The common style is just like:

-   \*r = nmg_mrsv(m);
-   s = BU_LIST_FIRST(shell, &(\*r)-&gt;s_hd);

Following routines need to be fixed at first:

-   nmg_isect_eu_fu
-   nmg_isect_fu_jra
-   nmg_isect_two_face3p
-   nmg_isect_two_generic_faces
-   nmg_crackshells

### Week 6

**Monday, June 23**

My laptop's screen is broken because of my careless hit. The mendery
promise it can be fixed today.

**Tuesday, June 24**

I need a Linux OS to fix errors which are skipped by Visual Studio. I
have less experience in working on Linux (I am sorry for this point), so
some time is spent to learn skills from webpage and ask for others.

**Wednesday, June 25**

Oracle VM Virtual Box and Linux Ubuntu are installed on my machine. Then
move the nmgreorg branch to it, and use g++ to test. At first, I MAKE
the makefile under the root dictionary, some compiling errors irrelevant
to nmg appear. Then I find it's useful to just MAKE mged's
makefile.(Sorry for my being unfamiliar with Linux again).

Fix these errors skipped by Visual Studio before. Most of them are
'variable isn't be used'.

**Thursday, June 26**

Spend this day in writing a midterm-evaluation report. Count the all the
nmg functions removed and changed. Use statSVN to estimate the amount of
code.

**Friday, June 27**

I'm trying to fit coding environment on Linux. Being familiar with the
command line of CMAKE, SVN, and so on. It seems not best but enough for
me to coding by gedit. VIM or EMACS seems a better choice, but I need
some more time to configure and learn.

**Sunday, June 29**

Debug on the Linux environment. It's surprised for me to find there are
so many errors complained by g++ which are all skipped by Visual Studio.
Two kinds of situations are most common:

-   Variable is set but not used. Direct solution is to remove these
    variable declaration. But if the variable is an input parameter and
    I don't change the function declaration now, UNUSED(..) keyword can
    be used to avoid such error.

<!-- -->

-   G++ will check all functions no matter it is referenced in this
    running. But Visual Studio wouldn't do that.

All errors are fixed, and MGED in my branch can run well on Linux now.

### [Midterm](Midterm.md)

### Week 7

**Monday, June 30**

Though MGED runs without errors on Linux, the display window disappears.
It always prompt 'attach (nu\|txt)\[nu\]' on the console.

There are two ways suggested by mentor to solve this solution:

-   check the missing package according to the CMAKE information.
-   use virtual machine image.

But I read INSTALL file again and find a useful shell ./sh/mak_deb.sh
to check the missing package on the machine. Finally it works.

**Tuesday, July 1**

Obviously, my branch nmgreorg is not synchronous with the trunk. Some
compile errors appear but fixed in trunk,

eg: .\\src\\other\\stepcode\\src\\express\\parse_data.h.

So, I try to make them both synchronous by using 'svn merge', and fix
the conflicts after the operation.

**Wednesday, July 2**

After the merge operation, new compile errors related to removed NMG
structure appear. Then fix them mainly located at .src/conv/.

**Thursday, July 3**

Continue the fix work and solve all compile errors finally. I'd like to
commit these change but fails with unknown reasons.

**Friday, July 4**

It's weird to find that I cannot commit changes on Linux today. I try
several methods to solve the problem.

-   check the web connection on Linux. It's OK.
-   check the update command acted on trunk on Linux. It's OK.
-   check the commit access on Windows. It's OK.
-   check the commit access acted on nmgreorg on Linux. It fails.

I check the detailed URL of nmgreorg, relocate
'<http://svn.code.sf.net/>...' to
'<http://svn.code.sourceforge.net/>...'. Then, it works.

### Week 8

**Monday, July 7**

Although MERGE operation and make nmgreorg branch be able to compiled on
Linux, the new nmg structure still cannot deal with multiple shells.
There are two kinds of situation: separated shells and overlap shells.
two situation cause runtime errors in two different places.

By research, Adding a calling of 'nmg_s_reindex' directly after moving
faces/edges of second shell into the first one can promote the first
problem.

**Tuesday, July 8**

It seems more complicated to fix the second problem. By consulting
Daniel, some functions should be changed because calling of them in
'nmg_classify_shared_edges_verts' makes no sense after NMG
reorganization. e.g.:

-   nmg_find_s_of_lu
-   nmg_find_s_of_eu
-   nmg_find_s_of_vu

The shells to merge don't belong to one model any more, and they are two
independent shells without any connection.

**Wednesday, July 9**

I remove the calling of 'nmg_find_s_of_eu' and
'nmg_find_s_of_vu' in routine 'nmg_classify_shared_edges_verts',
use another kind of judgement method with lower performance to achieve
the same function.

But such change causes a new unexpected running error that some edgeuse
point to bad address.

**Thursday, July 10**

I hope to fix the new error found yesterday, but has no progress today.

**Friday, July 11**

I track the calling order of the whole facetize routine, then find the
nmg structure is incomplete after tesselation operation. To avoid
introducing the problem by myself, I update the latest version of trunk
and do this series of test, then get the same result.

So, I am almost sure the incomplete structure hides in codes before and
haven't been discovered because no usage or check done on it. I will try
to find the fundamental reason for it at the weekend.

### Week 9

**Monday, July 14**

Another kind of method is used to compare two edge's equality. check one
edgeuse's point of them and the mate edgeuse is enough to judge. Such
improvement can skip the iteration error and make codes passed to next
step.

**Tuesday, July 15**

Some minor errors are fixed, but it's no use to promote the bad pointer
error. A bad address always be visited when ray-intersect faces.

**Wednesday, July 16**

By carefully check, nmg_classify_shared_edges_verts() is superfluous
because it mainly deal with shared elements. But now there must be no
shared elements between two shells to be executed BOOL OPERATION. So
remove it simply.

**Thursday, July 17**

According to the debug result, the root of errors are about maxindex.
When I use following codes to test, the result confirms to 'index + 1 ==
sA-&gt;maxindex'. That's right.

-   nmg_s_reindex(sA, 0);
-   int index = nmg_find_max_index(sA);

But if I reindex sB after reindex sA, the result is wrong.

-   nmg_s_reindex(sA, 0);
-   nmg_s_reindex(sB, sA-&gt;maxindex);
-   int index = nmg_find_max_index(sA);

It's not difficult to make sure sA and sB have some shared structure
which should be avoid after NMG reorganization work because they are
completely respectively independent now.

Finally, such wrong situation make following routines read wrong
address.

**Friday, July 18**

Succeed to facetize a combination of default sph and rcc. Use a
workaround to simulation former index domain to make sure the process of
nmg_bool, then refresh it at the end.

Then, compare carefully the bool-relavant files between branch and
trunk. Add some missing functions. According to Daniel's suggestion,
more test is required especially import/export. The codes should be
merged into trunk and moved into a new lib NMGLIB if tests are all no
problem.

### Week 10

**Monday, July 21**

Merge updates from trunk to nmgreorg. Though some reversion fails
several times due to net problem, succeeds finally.

**Tuesday, July 22**

Facetize some existing model to test the convert functions after
reorganization. Simple structure and combination are all OK, but fails
when facetizing toyjeep.g.

Then I try to facetize toyjeep.g in trunk and it fails either. According
to this situation, I am sure there are some bugs in trunk originally.

**Wednesday, July 23**

Dealing with import/export takes precedence over fixing minor bugs.

Read codes related to NMG import/export. Then change some places in
import funtion that it will skip model/nmgregion information when
reading a \*.g file made by trunk.

So IMPORT is OK, the next step is to deal with EXPORT.

**Thursday, July 24**

I read the suggestion sent by Daniel a month before and do more research
in EXPORT. I think a simulate old-model/nmgregion/nmgregion_a should be
put into file space before saving new-shell. To keep maxindex property
of new-shell consistent, calling of nmg_s_reindex() is nessesary to
force the allocation function reserve extra space for these three
structure.

**Friday, July 25**

Discussing some more implementing details which makes the solution
clearer. I am trying to finish this in this weekend.

### Week 11

**Monday, July 28**

I have finished the work about export of new NMG and have tested it. Now
it's no problem to read a \*.g file from trunk by nmgreorg and vice
versa. The storage format keep consistent no matter created by nmgreog
or trunk.

-   When import, new NMG skip redundant model/nmgregion information.
-   When export, new NMG add simulating model/nmgregion information and
    make sure the new shell is in one nmgregion as well as the nmgregion
    is located in a model.

**Tuesday, July 29**

Do much more tests about import/export functionality. It seems no
problem, but there are still some bugs in BOOL OPERATION even if some
test cases can pass. I guess the root of problem is the shared structure
mentioned before.

**Wednesday, July 30**

Track the routine:

-   nmg_isect_two_generic_faces(fu1, fu2, tol);
-   nmg_isect_two_face3p(&bs, fu1, fu2);
-   nmg_isect_fu_jra(is, fu1, fu2, &eu1_list, &eu2_list);
-   nmg_isect_eu_fu(is, &verts2, eu, fu2);
-   new_vu = nmg_make_dualvu(v, fu, &is-&gt;tol);

Before calling nmg_make_dualvu, the belonging shell of v and fu are
different. But after calling it, it's strange that the two structure
share the same shell structure.

**Thursday, July 31**

With further research, nmg_mlv in nmg_mk.c is called. It seems two
shell (sA and sB ready to bool operation) have shared structure since
here. I guess the correct method is copy a vertex to put in the other
shell.

**Friday, August 1**

Make some try to disconnect the relationship between two shell when
calling nmg_make_dualvu, but not works. These will cause other errors
in the next steps.

### Week 12

**Monday, August 4**

I skip some codes in BOOL OPERATION to make program 'can' facetize the
shifter in toyjeep.g. But it just cut off the main process and not reach
the critical parts.

**Tuesday, August 5**

Compared all files before and after change, I notice the
nmg_shell_fuse(sA, tol) and nmg_shell_fuse(sB, tol) before calling
nmg_crackshells(sA, sB, tol). The function nmg_shell_fuse remove the
repeat elements vertex/edge/edge_g in sA and sB respectively. But in
trunk, it's nmg_model_fuse, which acts on the whole model. It means
the same elements between sA and sB can also be removed. But in branch
nmgreorg, they are not.

To restore the original function, I should write another version of

-   nmg_vertex_fuse
-   nmg_break_e_on_v
-   nmg_face_fuse
-   nmg_edge_fuse
-   nmg_edge_g_fuse

I believe for this reason (sA and sB still have same element such as
vertex), it cause the zero-length edge appearance when calling
nmg_crackshells. The change is large, I decide to do the movement work
(move some files to a new-created nmglib) at first after discuss with
mentor.

**Wednesday, August 6**

Start the movement work and finish some basic parts.

-   move all nmg_XXX except a few e.g. nmg.c (becasue it includes
    import/export functionalities) into libnmg.
-   move bspline dictionary into libnmg.
-   leave all db relevant files in librt.
-   leave all tree relevant files in librt.
-   leave basic shapes definition (e.g. rcc sph arb8....) in librt.

**Thursday, August 7**

Define the NMG_EXPORT just like the RT_EXPORT to make rtlib and nmglib
import/export functions correctly when reading include files. But some
functions reference each other which makes harder to separate them.

**Friday, August 8**

The movement method done in Wednesday is wrong because they lose the
history. With Sean's lesson, I revert codes to r62036. Then use the
right way (svn mv) to do the movement and redo the following operations.

**Saturday, August 9**

Fix some compile errors and link errors to make it able to run in Visual
Studio, but fail in GCC for its more strict compilier. It wouldn't be a
thorny problem if I find how to separate nmg.h and raytrace.h perfectly.

### Week 13

**Monday, August 11**

Create a new variable nmg_debug to replace RTG.NMG_debug. This
separation means it's unnecessary to move other unrelated struct 's
definition into nmg.h. Then change all RTG.NMG_debug's reference to
nmg_debug. libbu is a good example for this problem.

**Tuesday, August 12**

Create a new variable rtg_vlfree to replace the same member in RTG for
the same reason and target as yesterday's change. It's helpful to break
some redundant connection between librt and libnmg.

**Wednesday, August 13**

The ideal is only nmg_xxx.c files in libnmg without others. now there
are plenty of nurb_xxx.c files stay here, and nmg files depend on them.
So I plan to move them into a new lib named libnurb after some
investigation.

**Thursday, August 14**

I move nurb_xxx.c files into libnurb, and change correlative header
files, CMake files and so on.

**Friday, August 15**

The task to split librt into three smaller lib: librt, libnmg and
libnurb is basically finished and be able to compiled on Linux. Notably,
there is cyclic dependency among them which maybe a kind of bad smell.

For example, functions in nmg_class.c depends on nmg_rt_isect.c, but
nmg_rt_isect.c depends on the struct xray and ray_data defined in
raytrace.h. I hope neither put nmg_class.c back into librt, nor put so
many obvious ray-trace struct in libnmg. So that's it.

I'd like to find better solution to solve it at the weekend.
