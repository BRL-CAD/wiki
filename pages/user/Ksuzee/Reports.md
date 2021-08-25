# GSoC 2012

## 0 week

-   2/05/2012 - installing Ubuntu-12.04, XChat
-   4-5/05/2012 - downloading sources, successful building with CMake
-   8-9/05/2012 - making folder which contains the information about
    duplications in every folder of /trunk/src
-   12/05/2012 - csh script for finding duplications
-   15/05/2012 - patch r50549 for adrt/isst_tcltk.c
-   16-18/05/2012 - patches:
    -   /fb/orle-fb.c
    -   /util/picbackgnd.c
    -   /libbu/htonf.c

## 1 week

-   -   start fixing duplications, which are situated in different
        folders
    -   patch /libbu/convert.c for check
    -   patch /util/lowp.c for check
    -   patch /rt/viewarea.c for check
    -   getting familiar with Astyle

Also I continue to check folders which contain duplications in one file.

There're folders: util, vfont, tclscripts, sig, shapes, rtthem, remrt,
proc-fb, nirt, libwdb, libtermio, libsysw, librtserver. All these
directories are checked. They either have no duplications in one file
which should be reducted or reductions are put to patch tracker for
check. I'm working on directories: tab, rt. mged, libtclcad, librt

## 2 week

-   28/05
    -   correction to patches: /fb/orle-fb.c and /util/picbackgnd.c
        (testing)
    -   working at duplications in /mged/points/process.c

<!-- -->

-   29/05
    -   there's a huge duplication in rt/worker.c. I'm working on it
    -   checking some more directories (will write the result later)

<!-- -->

-   30/05
    -   checking some more directories (will write the result later)
    -   leave worker.c for discuss (ready, but not tested yet)

<!-- -->

-   31/05
    -   correction the util/lowp.c patch
    -   checking some more directories

<!-- -->

-   1/06
    -   all the directories are checked for duplications in one file

<!-- -->

-   2/06
    -   preparing the summary about duplications

tab/tabinterp.c - functions step_interpolate and linear_interpolate --
the bodies're different but part which contains "for", "while" and "if"
can be put in common static inline function.

/rt/worker.c - there're two huge parts in function "void do_pixel" in
"begin unroll"-"end unroll" and "begin non-ubrolled"-"end non-unrolled".
However, you told it problem file, so I'll wait your comment here.

/mged/cmd.c - functions "int cmd_ged_edit_wrapper" and "int
cmd_ged_simulate_wrapper". The only ddifference is value of av\[1\].
Both these functions are used in setup.c, so it's better to use static
inline function too. I suggest to make one more variable for parameter
of argv\[\]

/libtclcad/tclcadobj.c - 1) functions "HIDDEN int
to_mouse_move_arb_edge", "HIDDEN int to_mouse_move_arb_face" and
"HIDDEN int to_mouse_move_pipept". The difference's in: av\[0\] =
"move_arb_face"; - to_mouse_move_arb_face av\[0\] =
"move_arb_edge"; - to_mouse_move_arb_edge av\[0\] =
"move_pipept"; - to_mouse_move_pipept

and ret = ged_move_arb_edge(gedp, 5, (const char \*\*)av); ret =
ged_move_arb_face(gedp, 5, (const char \*\*)av); ret =
ged_move_pipept(gedp, 5, (const char \*\*)av);

So these functions could call another static function which'd have all
the body and get char \* parameter for av\[0\] and functional type for
ret. 2) functions "HIDDEN int to_poly_ell_mode" and "HIDDEN int
to_poly_circ_mode". Differnce's in consts -
gdvp-&gt;gdv_view-&gt;gv_mode = TCLCAD_POLY_ELLIPSE_MODE; and
gdvp-&gt;gdv_view-&gt;gv_mode = TCLCAD_POLY_CIRCLE_MODE; so
necessary const could be got by common function (type - ged_view, if
I'm not mistaken). Also difference is in bu_vls_printf, but type
char\* can be transmit too.

/librt/primitives/nmg/nmg_rt_segs.c - functions "HIDDEN int state5"
and "HIDDEN int state6". It'd be easy to reduct, because difference's
only in ret_val (in two situations at the end of functions) which is
INT. So I'd be necessary only to transmit ret_val1 and ret_val2.

/libpc/pcParameter.cpp - methods Point::Point(VCSet & vcs, std::string
n, void \*ptr) and Vector::Vector(VCSet & vcs, std::string n, void
\*ptr): the blocks in if (ptr) {...} are the same, so this block can be
put in other function.

/liboptical/sh_camo.c - functions HIDDEN int marble_setup and HIDDEN
int camo_setup. The difference is in bu_log (just static comment) and
in memcpy.

/libbn/plot.c - functions void pd_3space and void pd_3line. I made
static inline function pd_3 which gets the same parameters as those two
functions + char l. Both functions call pd_3 with l == 'W' for
pd3_space and l == 'V' for pd_3line. Making was successful.

/fbserv/server.c - void fb_server_fb_scursor and void
fb_server_fb_cursor. Difference is: (void)pkg_plong(&rbuf\[0\],
fb_cursor(fb_server_fbp, mode, x, y)); and
(void)pkg_plong(&rbuf\[0\], fb_scursor(fb_server_fbp, mode, x, y));
So common function can get just: struct pkg_conn \*pcp, char \*buf +
functional type

/fb/pl-fb.c - int GetDCoords(coords \*coop) and int Get3DCoords(coords
\*coop). Difference is only here: if (debug) {fprintf..}. So text for
fprintf can be transmited like a char \* in common function.

## 3 week

-   4/06 - getting familiar with unit tests

<!-- -->

-   5/06 - cheking some more directories for duplications

<!-- -->

-   6/06 - CMakeFiles and Makefile

<!-- -->

-   7/06
    -   patch for src/util - files util.c and util.h.
    -   util_yuv is almost ready (something need to be checked)

<!-- -->

-   8/06
    -   working with util_yuv (ready)
    -   come back to firt patch (ready \*need to send patch)

<!-- -->

-   9/06
    -   /mged/cmd.c is refactored
    -   work with /libtclcad/tclcadobj.c. Have some problems with
        functional type
    -   /fb/pl-fb.c is refactored. Static inline function is added.
        Making and running are successful

## 4 week

-   11/06
    -   further checking for duplications in one directory, different
        files
-   12/06
    -   the same checking. Hope to finish it by today's evening
-   13/06
    -   sent all prepared patches,
    -   did some making and running of refactored functions to be sure
        in right result.
-   14/06
    -   /librt/primitives/nmg/nmg_rt_segs.c is refactored
    -   some more checking
-   15/06
    -   checking for copy-pastes in 1 dir - different files is
        completed! The count of such places -- 14, +2 are already
        patched
-   16/06
    -   getting familiar with u-f.c, d-i.c etc. Understanding how they
        work.

## 5 week

-   18/06
    -   reduction in sig/d-i.c and ../f-i.c. Patch's added
-   19-20/06
    -   reduction in libged/view_obj.c and ../vutil.c. 2 functions're
        put in util.c
    -   reduction in libdm. There're quite enough dups, so need a bit
        more time to finish
-   21/06
    -   reduction in libdm is finished
-   23/06
    -   find a bit more in libdm, add it

## 6 week

-   25/06
    -   getting familiar with g-nff, g-obj, g-xxx_facets
-   26/06
    -   reduction in src/conv for g-nff, g-obj and g-xxx_facets is done
    -   made small man pages for src/sig: f-i, d-i, u-f, i-f
-   27/06
    -   made man pages for src/sig: a-d, bw-d, d2-c, d-a, d-bw, d-u,
        f-d, u-bw, u-d
-   28-29/06
    -   check duplications in different folders. Most dups've already
        been found. Hope to finish by tomorrow evening and make a whole
        report by them
-   30/06
    -   all the duplicaions in differesnt foldres are checked. There're
        about 35 such situations. Some of them are a bit disputed and
        needed to be discussed.

## 7 week

-   02/06
    -   worked with libged/ps.c and png.c but unsuccessful. They
        couldn't be reducted
-   03-04/06
    -   looked through left TODOs. Tomorrow will finish it and reduct.

TODO: to correct existing patches a bit

-   05/06
    -   did some reduction in

/liboptical/sh_camo.c and /tclcad/tclcad_obj.c (thanks to \`\`Erik).
Will patch them in a few days because of some problems with my laptop

## 8 week

-   09-10/07
    -   added patch for /liboptical/sh_camo.c
    -   submitted my Student Midterm Evaluation
    -   checked some previous patches
    -   work on reduction in sig/umod.c and sig/imod.c. It must be the
        last reduction for 1 directiory - many files
-   14/07
    -   spent some time reading HACKING file

During the first part of GSoC program I:

1\. Found, reducted (where it was possible) and patched all the
duplications which are contained in ONE (the same) file

2\. Found, reducted (where it was possible) and patched all (except one)
the duplications which are contained in different files, but in one
directory. Usually I added 2 new files - util.c and util.h, which
contained the duplicated code. I need to add some necessary comments to
the new files.

3\. Created some small manual pages for some programs in src/sig. Will
commit them after the getting commit access.

4\. Found all the duplications which are contained in different
directories and have a full list of necessary reductions.

## 9 week

-   16/07
    -   working on headers from some previous patches
-   18/07
    -   updated patches for src/util
-   21-22/07
    -   updated patches for other duplications in 1 directiory -
        different files

## 10 week

-   26/07
    -   updated patches for src/conv
    -   added patch for src/librt/primitives/nmg/nmg_rt_segs.c
-   27/07
    -   found several editing methods for duplicate code in different
        folders
    -   trying to reduct code in different folders
-   28/07
    -   updated patch for src/fb/pl-fb.c
    -   updated patches for src/libdm
    -   closed unnecessary patch for src/libdm
    -   checking other patches
-   29/07
    -   updated two patches for src/sig
    -   updated two patches for src/utils
    -   added comments for patches on patches tracker where it was
        necessary

## 11 week

-   30/07
    -   fixed error at patch for src/libdm
    -   reducted patch for fb/pl-fb.c
    -   added some screenshots for patches
-   31/07
    -   continue working with clip.c.in libbn
-   1/08
    -   some work on previous patches
-   2-3/08
    -   clip.c.in libbn is ready. Now there're 3 functions, commmon for
        libdm and libged

## 12 week

-   6/08
    -   made one more reduction in libbn. Now there're files
        track_reg.c and track_reg.h. They have common funtions for
        libged/track.c and libwdb/reg.c
-   8/08
    -   refactoring in libicv and util. The same as previous
-   9/08
    -   refactoring in fb and libfb. Tha same as previous
-   10/08
    -   some more reductions in previous situations for good patches.
        Almost everything I supposed to do during GSoC is ready
-   12/08
    -   added 2 more prepared patches

## 13 week

-   work on cleaning and reviewing the patches