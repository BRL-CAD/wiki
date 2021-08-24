__FORCETOC__

------------------------------------------------------------------------

# Wed, July 1, 2015: ***Week 6 (of 14)***

-   [commit
    \#1](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/d29dbe2491598d5b0f4a44e7c3e1cd9d82d29d80?diff=split):
    filling out vertex info with structures to avoid errors with
    incomplete data structures
-   getting crash in nmg_mvu on line 365: BU_LIST_APPEND(...); need
    to investigate.
-   use case for above: 'make modelname nmg', then 'nmg cmface modelname
    coords'
-   rechecked patch <https://sourceforge.net/p/brlcad/patches/387/>
-   verified by compiling with STRICT enabled. posted build.log to
    sourceforge.
-   problems with compilation apparently not associated with changes.
    builds fine with STRICT disabled.

# Thurs, July 2, 2015

-   Appointment with retinal specialist from 9:30am to Noon PST.
-   Not be able to work today due to pupil dilation.

# Fri, July 3, 2015

-   [Midterm
    summary](http://brlcad.org/wiki/User:Bhollister/MidtermSummary2015)
    located at link
-   still investigating nmg_mvu issue for ged_nmg_cmface subcommand:
    -   likely that the vertexuse is being improperly treated for loop
        creation.
    -   should there be a vertexuse present in the model for the new
        loop (prior to nmg_mvu call from nmg_cmface)??

# Sat, July 4, 2015

-   n/a

# Sun, July 5, 2015

-   n/a

# Mon, July 6, 2015: ***Start of Week 7 (of 14)***

-   [commit
    \#1](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/b72d2551ee08b6cb05f5880c6725698ae5f51883?diff=split)
    fixed issue with missing bu_list in vertex struct
    -   while commit \#1 provides a "working" call to nmg_cface with
        three verts, the face is not visible in the render window??
    -   ged_nmg_cface appears to make the proper calls...
    -   once problem is found with rendered model, need to extend for n
        verts (should be trivial)
-   [commit
    \#2](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/c51818d023cbe118042483eed2058439a7dda7a5?diff=split)
    attempt to fix issue with ged_nmg_cmface crash in
    nmg_info/nmg_findeu(); in loop

# Tues, July 7, 2015

-   received good direction from brlcad in irc
    -   reviewed
        <http://www.google-melange.com/gci/task/view/google/gci2014/5546966268248064>
    -   reviewed <http://brlcad.org/wiki/NMG>
    -   previously unaware that nmg models could be created with
        ged_put
-   todo: need to plan high-level subcommands after cmface working
-   todo: check winding order in cmface, as <http://brlcad.org/wiki/NMG>
    mentions potential crashing with incorrect winding order

non-brlcad time expenditures...

-   spent some time applying for positions

# Wed, July 8, 2015

-   investigated put / get database commands.
    -   should illuminate sequence of calls needed by subcommands for
        nmg api calls
    -   posted related questions in irc
-   todo: use info from above to fix mged calls implemented in
    libged/ged_nmg_cmface.c
-   [commit
    \#1](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/5fc1f3c370d706f840b4f659124936a4512a5b0b):
    null commit to synchronize to github from nonlocal repos

non-brlcad time expenditures...

-   oil changed for car; 3 hour wait!
-   wrote essay, etc. for instructor position application

# Thurs, July 9, 2015

-   investigated get / put nmg object creation...
    -   need to follow the code from this sequence of calls using 'put'
        CLI:
        -   ged_put()
        -   rt_nmg_make()
        -   rt_nmg_adjust()
    -   above sequence of calls creates an nmg object and adds verts /
        faces
-   todo: revamp \*ged_cmface\* using preceding process.
-   note: apparently using nmgmodel.c was not the best example of
    manifold nmg object creation!
-   todo: once ged_cmface() properly impl and submitted as patch, can
    move on the spec for high-level subcommand list; perhaps vert / face
    removal subcommand CLI routines are the easy to start with??

non-brlcad time expenditures...

-   VDA 2016 template and reformat of paper for submission
-   10 job applications submitted

# Fri, July 10, 2015

-   [commit
    \#1](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/74902ee6b8c2737b625e81ae26c9193ff8ebbf92?diff=split)
    using method from rt_nmg_adjust. still some issues with calls to
    nmg_cmface. soon to be resolved.
-   appears that vert structs are not being filled out correctly and
    thus crash in cmface; need to test with known "working" args

non-brlcad time expenditures...

-   applications
-   car in garage again for brake pads
-   car will be in garage again next week for air bag recall (ford
    mustang)

# Sat, July 11, 2015

n/a

# Sun, July 12, 2015

n/a

# Mon, July 13, 2015: ***Start of Week 8 (of 14)***

-   [commit
    \#1](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/6043568f31aa1d140132cdb6ee751ebf5577e419?diff=split)
    cmface now working. using rt_nmg_adjust as model for impl.
-   [commit
    \#2](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/9146049d71ced81163f33eb312f87b23b552fa01?diff=split)
    added variable number of verts for CLI.
-   [commit
    \#3](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/90400f946981422c6a7b8dcffc5a3053726cec83?diff=split)
    check for minimum number of verts for manifold face
-   cmface [patch 390](https://sourceforge.net/p/brlcad/patches/390/)
    submitted

# Tues, July 14, 2015

-   mm (make nmg object model) subcommand [patch
    391](https://sourceforge.net/p/brlcad/patches/391/) submitted
-   updated [patch 390](https://sourceforge.net/p/brlcad/patches/390/)
    with build fix and code cleanup
-   [commit
    \#1](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/3457b81b9cab57c9bc07d4681c991b73b93b6926?diff=split)
    cleaned up loop var. removed unused fastf_t declaration
-   found potential build problems when BRLCAD_ENABLE_STRICT=YES.
    noted in patch 390 reply (opennurbs lib)
-   todo:
    -   impl face kill routine as subcommand
    -   design remaining subcommands (will be higher-level than internal
        nmg api)
    -   post usage instructions for simple box creation use case using
        subcommand 'cmface'
    -   will need to determine which routines that have been submitted
        in [patch 387](https://sourceforge.net/p/brlcad/patches/387/)
        that need to be removed

# Wed, July 15, 2015

-   re-tested with 'strict' build options - works!
-   updated schedule to include new designs
-   created [MGED_CMD_nmg](http://brlcad.org/wiki/MGED_CMD_nmg) design
    doc
-   proposed new subcommands:


**sface**


Selects a face by highlighting it. Subsequent commands for manipulation
or removal act on the selected face. By repeating this call, the
currently selected face is advanced to the next face in the NMG object
of the first encountered shell and region. *If an (optional) point is
specified, the subcommand finds the closest face to the point and
selects that face instead.*

**deselect**


Deselects all prior selected parts of the nmg object.

**kface**


Removes the geometry and faceuse of the currently selected face.

-   todo: need to get mentor(s) advice and okay before implementing
    proposed new subcommands
-   todo: submit patch to remove calls to low-level api that are not
    needed
-   todo: update top-level command 'nmg' to reflect help / changes

# Thurs, July 16, 2015

-   investigated ways to draw geometry different colors
    -   traced ged_draw, etc.
    -   this will be needed in order to highlight selected face via
        'sface' subcommand
-   updated 'nmg' command design page

non-brlcad expenditures...

-   applied for more positions
-   answered questions from interviewer (email)

# Fri, July 17, 2015

-   read / posted a response to mailing list about command design
-   investigated design options (see my response)
-   investigated implications of various implementations (see my
    response)
-   todo: polish declarative syntax for 'creation' subcommands per
    Sean's suggestions
-   added 'nmg' to [mged cmds](MGED_Commands.md)

non-brlcad expenditures...

-   researched university locations for jobs
-   found out that I have jury duty in early august - need to postpone
    if possible

# Sat, July 18, 2015

n/a

# Sun, July 19, 2015

n/a

# Mon, July 20, 2015: ***Start of Week 9 (of 14)***

-   updated [proposed
    subcommands](http://brlcad.org/wiki/MGED_CMD_nmg#Proposed_subcommands)
    -   need to find way of marking model parts
    -   need to allow users to select desired model parts through model
        labels in subcommand (see previous link for design ideas)
-   investigated color setting with mged
    -   only found info on
        [comb_color](http://brlcad.org/wiki/MGED_CMD_comb_color) which
        doesn't appear relevant
    -   need to find simple way to set real-time geometry window colors
        (down to an opengl state function possibly?? and trace that back
        up to the higher-level call)
    -   libged/draw.c, _ged_drawtrees() sets the wireframe
        color...*need to leverage this functionality for labelling /
        marking geometry!*

non-brlcad expenditures...

-   interview scheduled for 10 AM PST (Skype)

# Tues, July 21, 2015

-   since arbs have vertex labelling
    -   may want to rethink (at least) the *kill V* subcommand
    -   vertex numbering **already** works with nmg, but there are some
        scaling issues
    -   i.e. vertex labels are not located right on vertices but too far
        from them
-   new create / kill subcommands should be:
    -   consistent with modal behavior of mged command line
    -   i.e. only in "edit" mode do we use create / kill nmg model parts
-   todo: need to investigate further libged/edit.c
-   *if* we choose color faces / verts diff colors:
    -   code proposal: check if in "edit" mode, then:
        -   either add new function and call it, i.e. something like
            'ged_draw_guts_edit_mode()'
        -   or add to already large ged_draw_guts() with conditional
            logic
        -   there is only a single *struct _ged_client_data* used for
            entire model
        -   potentially needs to be revamped, since we need it to change
            per model *part*
        -   warning: could be extensive and therefore may have to use
            *existing* labelling system
-   found this at the end of /include/ged.h. should be useful.

<!-- -->

    /***************************************
     * Conceptual Documentation for LIBGED *
     ***************************************
     *
     * Below are developer notes for a data structure layout that this
     * library is being migrated towards.  This is not necessarily the
     * current status of the library, but rather a high-level concept for
     * how the data might be organized down the road for the core data
     * structures available for application and extension management.
     *
     * struct ged {
     *   dbip
     *   views * >-----.
     *   result()      |
     * }               |
     *                 |
     * struct view { <-'
     *   geometry * >------.
     *   update()          |
     * }                   |
     *                     |
     * struct geometry { <-'
     *   display lists
     *   directory *
     *   update()
     * }
     *
     */

non-brlcad expenditures...

-   had another interview 10 AM PST (Skype) - second one this week
-   have a third for this week scheduled @ 10 AM PST tomorrow

# Wed, July 22, 2015

-   researching how vertices are labelled in 'SOLID EDIT' mode
    -   traced: ged_view_update(struct bview \*gvp) from
        libged/vutil.c
    -   traced: f_sed(ClientData clientData, Tcl_Interp \*interp, int
        argc, const char \*argv\[\]) from mged/chgview.c
    -   traced: stateChange(int UNUSED(oldstate), int newstate) from
        mged/buttons.c
    -   usage of [sed](http://brlcad.org/wiki/MGED_CMD_sed) command and
        [facedef](http://brlcad.org/wiki/MGED_CMD_facedef) command
        (relevant to nmg subcommands for updating nmg geometry)
-   found label vert functionality:
    -   /\* Usage: labelvert solid(s) \*/ **f_labelvert**(ClientData
        UNUSED(clientData), Tcl_Interp \*interp, int argc, const char
        \*argv\[\])
    -   from **mged/overlay.c**
    -   further calls:
        -   librt/vlist.c, rt_label_vlist_verts() --&gt;
            libbn/font.c, bn_vlist_3string()
-   todo: can labelling work for faces / regions / shells without
    resorting to color change??
    -   color change may involve substantial rework of state setting
    -   not to mention other problems for color labelling (visually
        impaired users, ambiguity in color differences, etc.)??

non-brlcad expenditures...

-   had phone interview @ 10AM PST

# Thurs, July 23, 2015

-   [commit
    \#1](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/63932fe80449968587145fba79371b7bc024701f?diff=split)
    removed files associated with CLI stubs for internal nmg api
-   [commit
    \#2](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/27ece977173f135cb69bd4383c72e5ebff98a532?diff=split)
    added ged_nmg_kill_v and associated src files
-   [commit
    \#3](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/5edfea7e407163255eb74d02570d74e255541e31)
    fixed parameter ordering for cmface and mm subcommand - for
    consistency with new syntax
-   [commit
    \#4](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/07c51b26a2f7688fdb0bdb6d3c6f0c6251bff396)
    trying to get vertex labelling to work for subcommand kill V.
    work-in-progress. currently not building during link phase.

# Fri, July 24, 2015

-   investigated mged command 'permute' as it relates to altering
    vertices in object
-   investigated mged GUI 'primitive' editor under 'Edit' menu.
    -   editor shows vertices (number labels) and allows their coords to
        be altered by increment / decrement
    -   potentially useful for cmd line functions with proposed similar
        functionality
    -   insight into the linkage between vertex \# and vertex data
        structure (how)

non-brlcad time expenditures...

-   job application
-   car air bag recall (in shop)

# Sat, July 25, 2015

n/a

# Sun, July 26, 2015

n/a

# Mon, July 27, 2015: ***Start of Week 10 (of 14)***

-   [kill V](http://brlcad.org/wiki/MGED_CMD_nmg#Proposed_subcommands)
    design updated
    -   determined that the best way to select a vertex is to use
        [labelvert](http://brlcad.org/wiki/MGED_CMD_labelvert) on object
        to select vertex by coords
    -   user then issues selected coord for [kill
        V](http://brlcad.org/wiki/MGED_CMD_nmg#Proposed_subcommands)
-   [commit
    \#1](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/c714dcd21a909d7fdd6dfa8116c7db9a858287e9)
    revamped ged_nmg_kill_v. now requiring user to first use
    'labelvert' mged command to label vertices in object. todo: work out
    way to visit all vertices (i.e., or vertexuses) to find matching
    coords issued to be killed.

# Tues, July 28, 2015

-   [commit
    \#1](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/3285aab44203e3c14c6e2b9ef3b49751caef3c4a)
    now traversing each edgeuse to find vertexuses that reference a
    vertex structure with location specified on cli. todo: fix problem
    with edgeuse check failure. this could be due to invalid model and
    not problem with routine.
-   todo: check above commit with *known* valid nmg object

non-brlcad expenditures...

-   skype interview @ 11-12 PM Pacific time

# Wed, July 29, 2015

-   [commit
    \#1](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/11db05355983400727cd37f2384747a0298eeb0f)
    added nmg_m_struct_count as prototypical traversal algo for
    finding removing specified vertices @ cli.
-   [commit
    \#2](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/9679d23c0061b310151a86063120da7cb378f9d5)
    cleaned up struct counting algorithm and added nmg_kvu where
    vertices are found. appears to work, but model is not currently
    being updated...
-   if calling wdb_put_internal() at end of ged_nmg_kill_v(),
    getting a NULL vertexuse ERROR.
    -   however, this is what nmg_kvu() performs on the nmg object
        structure
-   [commit
    \#3](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/1841e1bd0ce3f2f0c84c151dce64b2d06685f8ef)
    added call to wdb_put_internal, however this produces ERROR due to
    NULL vertexuse after calls to nmg_kvu()

# Thurs, July 30, 2015

-   *kill V* now works! (see commit \#2)
-   [commit
    \#1](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/8b18eb753bf38aaa1c43f0ebd275a4e545dec158)
    added the proper nmg_k\* calls to removed faceuses, loopuses, or
    edgeuses that results from removal of selected vertex.
-   [commit
    \#2](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/52cbebc1efcd673ec8b203df6af9caf3b25941d6)
    remove_vertex() was missing some needed calls to remove lu's and
    eu's they're added now. cleaned up error message as well. cmd leaves
    it to the user to refresh vertex labelling in overlay.
-   [commit
    \#3](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/79c07597af1600a595e57447929542d360559b19)
    removed unused vars
-   todo: need to update usage for nmg command for new *kill V*
    subcommand
-   todo: tomorrow will submit two patches
    -   \#1 cleanup for nmg_\* files not needed
    -   \#2 *kill V* subcommad patch
-   spent time trying to make sure build works with applied patch to
    current trunk
    -   didn't quite work which is why two patches are scheduled for
        tomorrow
    -   separating patches into the two above to help avoid build error:
        *../../lib/libged.so.20.0.1: undefined reference to
        \`brlcad_interp'*

# Fri, July 31, 2015

-   submitted [patch 395](https://sourceforge.net/p/brlcad/patches/395/)
    -   originally planned to have two separate patches, but addition of
        new source file / removal of stubs both were reflected in
        changes to libged/nmg.c
    -   patch contains the following:
        -   addition of 'kill V' subcommand
        -   see
            <http://brlcad.org/wiki/MGED_CMD_nmg#Proposed_subcommands>
            for 'kill V' usage
        -   removed source file stubs for low-level nmg api subcommands
        -   reversed order of subcommand and nmg object name syntax (per
            request)
-   [commit
    \#1](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/10237773391b9baf2a51125818f51027f8a7de57)
    updated github branch with libged files from svn head; renamed
    nmg_kill.c to nmg_kill_v.c; added help for kill V
