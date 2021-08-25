__FORCETOC__

------------------------------------------------------------------------

# Sat, August 1, 2015

n/a

# Sun, August 2, 2015

n/a

# Mon, August 3, 2015 ***Week 11 (of 14)***

-   Summoned for jury service: Spent entire day at court house in Santa
    Cruz.
-   Dismissed from jury duty but was called to jury box.

# Tues, August 4, 2015

-   investigating ways of labelling faces for CLI specification
    -   looked at:
        -   [E](MGED_CMD_E_upper.md)
        -   [e](MGED_CMD_e_lower.md)
        -   [ev](MGED_CMD_ev.md)
        -   [B](MGED_CMD_B.md)
    -   none label objects with symbols (only color change, etc. and NOT
        faces)
    -   *ev* provides some direction
-   todo: may have to implement something like *f_labelvert* (in
    mged/overlay.c) but for face index labelling
    -   OR have users specify verts for face selection (probably not
        preferable)
-   updated design docs reflecting recent integrated patches

non-brlcad expenditures...

-   spent time in phone conversation negotiating / considering a job
    offer

# Wed, August 5, 2015

-   implementing new mged cmd called *labelface* need for kill F
-   [commit
    \#1](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/cdbe653c24e26fea050289d6f6d9fa220931927f)
    added placeholder for lableface mged cmd
-   [commit
    \#2](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/db9a7aa52d7d3fc8c8448b99aba2ab9fc7b3aa83)
    traversing model to collect a list of faces to label. work in
    progress...

# Thurs, August 6, 2015

-   *labelface* impl
    -   working to get list of faceuses from nmg model
    -   working to get center coord of face polygons
        -   this will allow labels to be displayed at center of faces

non-brlcad expenditures...

-   spend much of the day deciding between two employment offers
-   chose post-doctoral research over lecturer position

# Fri, August 7, 2015

-   [commit
    \#1](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/35e5931d443219253c223f60e1bcf15a51192723)
    verified that faceuses are properly gathered in get_face_list.
    todo: use bu_list instead of array placeholder for faceuse list.
-   todo: need to find how to calculate barycenter for face verts (there
    must be a utility function in brlcad)
-   instead: *very easy as a simple average of coords of face verts*
    -   where face labels will be placed using *bn_vlist_3string()* in
        *rt_label_vlist_faces()*

# Sat, August 8, 2015

n/a

# Sun, August 9, 2015

n/a

# Mon, August 10, 2015 ***Week 12 (of 14)***

-   [commit
    \#1](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/b230dec94cb5358f0337d8c7f5a2f5b588bc3180)
    able to label faceuses at min pt of their bounding box. faceuse
    index used for label. todo: need to plot label at center of face.
    also need to find way to show both front / back facing faceuses.
    right now they are overdrawn. placeholder array causes seg fault
    when dereferencing empty faceuses in array.
-   [commit
    \#2](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/9efa36cfadd3e3cc8522f0489c6b4bfcbd3f6224)
    using struct face as replacement to struct faceuse
-   todo: use center of face for face index placement
-   since there are two facesuses per face, best to use index of face
    for label
-   see:

<!-- -->


    /**
     * Note: there will always be exactly two faceuse's using a face.  To
     * find them, go up fu_p for one, then across fumate_p to other.
     */
    struct face {
        struct bu_list l;       /**< @brief faces in face_g's f_hd list */
        struct faceuse *fu_p;   /**< @brief Ptr up to one use of this face */
        union {
        uint32_t *magic_p;
        struct face_g_plane *plane_p;
        struct face_g_snurb *snurb_p;
        } g;            /**< @brief geometry */
        int flip;           /**< @brief !0 ==> flip normal of fg */
        /* These might be better stored in a face_a (not faceuse_a!) */
        /* These are not stored on disk */
        point_t min_pt;     /**< @brief minimums of bounding box */
        point_t max_pt;     /**< @brief maximums of bounding box */
        long index;         /**< @brief struct # in this model */
    };

# Tues, August 11, 2015

-   [commit
    \#1](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/49f6daaddfd8b6630832c48c7de0f730aa136175)
    now taking avg of min and max bounding extents. works great for
    label placement.
-   [commit
    \#2](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/aa0082b0e10a15d256b59ad944bf9313154a7947)
    rt_label_vlist_faces caught in infinite loop. face list element
    had forw / back points to itself. todo: fix.

# Wed, August 12, 2015

-   added [labelface](http://brlcad.org/wiki/MGED_CMD_labelface)
    documentation
-   added patch [403](https://sourceforge.net/p/brlcad/patches/403/) for
    *labelface* cmd
-   [commit
    \#1](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/2a9d3a7077547a6fe72b138ffe3d70467ddcae31)
    fixed problem with adding same face struct to bu_list - which
    caused self-referential node (forw/back pointers pointing to node
    itself) in list
-   [commit
    \#2](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/2f2d1ce261a5798390937ac8d334d5bf00b84fd8)
    added help lookup for 'lableface'
-   [commit
    \#3](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/5d69a16a456b2fbd607a9e9193b86aca4c8ffb15)
    removed accidental redundant error checking
-   **todo: implement 'kill F' next, using the indices provided in
    display by [labelface](http://brlcad.org/wiki/MGED_CMD_labelface)**

# Thurs, August 13, 2015

-   submitted patch [404](https://sourceforge.net/p/brlcad/patches/404/)
    for 'kill F'
-   [commit
    \#1](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/144539694228226172afa30c573a08688e4a369c)
    added boiler-plate for ged_nmg_kill_f cmd
-   [commit
    \#2](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/1dc5b185b818bdaa88015a53c6001852aa0cd38f)
    using nmg_kfu(). loops / edges still present after faceuse / face
    removal. todo: either verify that face is removed by testing with
    solid face rendering, or remove loops / edges along with face...
-   Documentation updated:
    <http://brlcad.org/wiki/MGED_CMD_nmg#Subcommands>
-   todo: impl 'make V' as proposed

# Fri, August 14, 2015

-   [commit
    \#1](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/bf83734208abbc9f4d25a748580d1d908428b32f)
    boiler-plate for move V mged cmd
-   [commit
    \#2](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/777e9e006d454f851bd7f770c35807a093f32679)
    move V cmd implementation. More or less a variation on kill V.
-   [commit
    \#3](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/7476b5b7f4e95c6c2ef73c1dc3c0567f5565391e)
    added check for cmd argument length. should not exceed two coords.
-   submitted patch [405](https://sourceforge.net/p/brlcad/patches/405/)
    for move V nmg subcommand
-   updated docs
    -   [nmg](MGED_CMD_nmg.md)
    -   [labelvert](MGED_CMD_labelvert.md) for proposed -i
        (index) option
        -   this will allow for CLI specification with make F
-   updated [project
    schedule](Bhollister/Proposal#Project_Schedule.md) to
    reflect remaining work for next week, i.e. make F, make V, labelvert
    -i

# Sat, August 15, 2015

n/a

# Sun, August 16, 2015

n/a

# Mon, August 17, 2015 ***Week 13 (of 14)***

-   [commit
    \#1](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/0e1b539601a3167dcce14d98601612815502ae66)
    beginning of vertex index labelvert -i option.
-   crashing in bn_vlist_3string with MAT_DELTAS_VEC(
    xlate_to_origin, origin );
-   todo: fix above issue

# Tues, August 18, 2015

-   [commit
    \#1](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/b7d06366f26525d4d28cbc674cf1579dd90b1c25)
    labelvert -i option working. however, code uses new struct vtxlabel
    to avoid potential lists already used by nmg datastructure (struct
    vertex). also, there is no freeing of label list. todo: either use
    struct vertex instead if there is no list in nmg structure using
    struct vertex, or free list appropriately after usage.
-   [commit
    \#2](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/05790259d2ecd8347c287494dba8895fb335755e)
    struct vertex does not have a l bu_list. do not want to alter nmg
    types. thus, now freeing struct vtxlabel list after use.
-   todo: will cleanup above commits (if needed) and submit as patch
    tomorrow

# Wed, August 19, 2015

-   posted patch: [412](https://sourceforge.net/p/brlcad/patches/412/)
-   posted patch: [409](https://sourceforge.net/p/brlcad/patches/409/)
-   [commit
    \#1](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/c54ea02a09eb78003e5d1dc43b0e4aadb3fafcf7)
    now freeing heap memory for vertex label list
-   [commit
    \#3](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/2f9576729eb60133ba1ebcfddacc3dba6e0fb7a4)
    using bu_malloc and bu_free now.
-   make V subcommand:
    -   [commit
        \#2](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/931eb783599ff956b69ca594d2912e72376e373b)
        boiler-plate for make V cmd
    -   [commit
        \#4](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/59760062ff10d5cca5df14af2693ac6a49a7502f)
        getting casting error with return variable from nmg_mvvu()

# Thurs, August 20, 2015

-   [commit
    \#1](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/ed9acc12b1ee48f486ab1eb2d8261ede791e87ae)
    apparently we don't want to create a new loopuse for each new
    isolated vertex. can only add one vertex per shell. so, todo: use
    nmg_msv, for each new vertex + shell.
-   [commit
    \#2](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/a424344f653a9ef0ca4f50f36d7db6137d4f3ffa)
    working and cleaned up ged_nmg_kill_v. now adding a new shell
    when needed for a new vertex coord.
-   [commit
    \#3](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/248c05b10d46c007cb208d2517afe79745f2e871)
    added info about move V subcommand.
-   patch hasn't build properly with merge of latest changes
    (nmg_make_v.c) to trunk...working on it. todo: submit patch
    tomorrow??
    -   build dies @ 97 percent for linking ../../../../bin/step-g?
    -   [commit
        \#4](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/801d4143aa4cf6935163ef8b22a178aa46b4f9dc)
        simplified code to not add into existing shell. this was causing
        an undef linking error due to header issues with nmg_mvvu().
-   'make V' nmg subcommand patch submitted, see...
    -   patch [414](https://sourceforge.net/p/brlcad/patches/414/) Adds
        new vertices specified by their coords. Each vertex is added to
        a new shell in the NMG object.
-   todo: will see if I can get 'make F' working and submitted by COB
    tomorrow...
-   todo: minor updates to mged nmg docs as well.
-   todo: fix up -i option patch

# Fri, August 21, 2015 ***FIRM PENCILS DOWN***

-   [commit
    \#1](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/688c64e1d20b8bbd0d24ee727fcd241a47b8a151)
    moved vtxlabel struct def to rt/vlist.h
-   [commit
    \#2](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/d058369dc0ec7815364df314bb7d2e2d17b099be)
    boiler-plate for ged_nmg_make_F subcommand
-   [commit
    \#3](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/ff9ea3190265b3aafdf6c16b57ae10a03ad67be3)
    added find verts function stub with nmg traversal
-   [commit
    \#4](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/4a6bea01bef8d6b84d58111d2547a6c85935f10e)
    make F working for three vertices specified by labelvert -i index
    labels
-   [commit
    \#5](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/fdd8abb11d46c31d3294a7aaff02a72bfeadf3ec)
    first take on variabel command line with F
-   [commit
    \#6](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/12bb0c06cfa8b8dc28aa25fcfbee6e4329b552db)
    appears to work for multiple F
-   todo: will submit patch for move F over weekend after more
    testing...

# Sat, August 22, 2015

-   [commit
    \#1](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015/commit/c2e49d80e0776ea6da4358a345a04f56e0088b90)
    processing mulitple faces on command line for 'make F' subcommand
-   submitted patch [415](https://sourceforge.net/p/brlcad/patches/415/)
    for 'make F' subcommand
-   finished final evaluation on google-melange
-   updated [mged nmg subcommands](http://brlcad.org/wiki/MGED_CMD_nmg)
    documentation

# Sun, August 23, 2015

n/a

# Mon, August 24, 2015 ***Week 14 (of 14)***

n/a

# Tues, August 25, 2015

n/a

# Wed, August 26, 2015

n/a

# Thurs, August 27, 2015

n/a

# Fri, August 28, 2015 ***FINAL EVALS DUE***

n/a
