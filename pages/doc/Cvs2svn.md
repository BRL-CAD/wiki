At the end of 2007, preparations to convert BRL-CAD's CVS repository to
Subversion began. The cvs2svn tool was used to perform the conversion,
initially with version 1.5.1 but later using the latest available 2.0.1
version. The page is provided for historic reference on how the
repository was converted including the steps that were taken.

Using version 1.5.1, cvs2svn using all default options took over 7 hours
of processing before it filled up available hard disk space (only 3GB
was available at the time). More space was made available and cvs2svn
version 2.0.1 was installed, which provided a new more direct and faster
method of extracting data from the CVS repository. Using the same
default options, version 2.0.1 took just under 3 hours. The conversion
was performed by Christopher Sean Morrison (aka brlcad). The details of
this conversion process are documented in following.

# CVS repository preparations

As cvs2svn reported issues in the repository processing, some repairs to
BRL-CAD's CVS root was required. Working on a copy of the CVS root
files, this included fixing five directory subtrees that were in the
Attic:

-   html/manuals/Attic/mged4.0
-   html/Attic/release-notes
-   Attic/libitcl
-   Attic/libtcl
-   Attic/libtk

These directories seemed to expose a bug in cvs2svn's Attic processing.
Initial thoughts were that someone had manually moved directories into
the Attic, but upon further investigation it seemed more likely that
this was perhaps actually proper behavior for an old version of CVS. All
of the files in the Attic subdirs were properly marked as dead, and they
were a **hierarchy** of ,v files that were properly marked as Dead
revisions in that Attic subdir. Also, the directory "deletions" into the
Attic were performed by multiple developers (namely butler, parker, and
pjt iirc) during the late 90's, when the repository was located on an
old IRIX server with an old version of cvs (pre 1.10 but unknown).

The workaround solution used, without needing to modify cvs2svn, was to
create Attic directories throughout the hierarchy subfolders, move the
,v files into their respective Attic directory for each subfolder, and
then move the directory up one level out of the Attic. The Attic/libitcl
directory conflicted with an existing libitcl/ directory, so it was
simply purged given it would not have been beneficial to preserve that
external dependency history.

Another message reported by cvs2svn was that there was (exactly) one
commit that had non-ascii characters. Upon investigation, it was a
commit that contained an ?? in utf-8 so the --encoding option was added
to use utf-8. At that point, the options being used were:

`cvs2svn??--encoding=utf_8??--cvs-revnums??--auto-props=auto-props??--eol-from-mime-type??--mime-types=mime.types??--dumpfile=/path/to/brlcad.dumpfile??/path/to/cvs/repository`

Upon performing a full checkout of the entire newly imported Subversion
repository, the checkout failed in a branch (rel-5-1-branch) on checkout
of cup.g from html/manuals/mged/. Upon review of the CVS root files, it
was not apparent what was unique about cup.g,v other than the fact that
there also existed a Cup.g,v (both of which existed in the Attic). As
that file was entirely a triviality as a v4 binary BRL-CAD database file
used in a documentation example, both the uppercase and lowercase files
were removed.

# The executable bit

Although not a critical issue as the <svn:executable> property can
easily be set on files after they're imported into Subversion, there
were problems with files that were properly set as executable in CVS not
getting properly set in Subversion. Some scripts got the setting while
others did not, other files that CVS did not make executable upon
checkout (like C source files) were getting marked as executable. It
seemed to be a mix of problems, some caused by inconsistent permissions
set on the CVS root files and by unexpected cvs2svn behavior that is
inconsistent with the behavior of CVS.

There were indeed inconsistent permissions on the CVS root files that
needed adjusting to make sure everything that should or should not be
mode ugo+x had the appropriate bit setting. With the repository
repaired, attention was directed at the making sure the auto-props file
also has the <svn:executable> property set on corresponding files. Even
with the auto-props carefully customized to list <svn:executable> for
the files that should be executable, they still came across without the
exec bit set. In fact, it seemed the care and attention more
categorically made all scripts files, for example, not have the
executable properly set. As the executable property is not critical, the
files had the property set manually once the SVN repository went
on-line.

UPDATE: Shortly after first posting this article, one of the cvs2svn
developers (Michael Haggerty via IRC, thanks mhagger) contacted Sean
regarding this write-up and the issues encountered with the BRL-CAD
cvs2svn conversion. He reviewed the config and input file settings and
noted that the executable bit problems were directly the result of the
auto-props file settings being used. Contrary to SVN's behavior, cvs2svn
interprets <svn:executable> as meaning ***unset** that property* instead
of setting it. So, the file needed to have something like
<svn:executable=1> instead of just <svn:executable> to ensure the
property was set. This was at least the behavior as of version 2.0.1 of
cvs2svn. It was subsequently suggested that cvs2svn not diverge from
SVN's behavior and instead allow a **!**<svn:executable> indicate the
explicit *unsetting* of properties.

# Mime types

The repository conversion went through yet another full conversion when
it was discovered that several files in the repository had been marked
as binary. While Subversion does have improved binary diff management
than CVS, it still will not show you the diff or history of a file that
is marked as binary. This was particularly detrimental in our repository
as I originally used a standard Apache mime.types file in addition to a
custom auto-props file. The Apache mime type for a .tcl file is
application/x-tcl which Subversion only understands as "binary", making
it difficult to view the history. The fix, of course, was to re-run the
conversion without the Apache mime.types file but instead be much more
more comprehensive about setting types in the auto-props file.

# Single project vs multiproject

The default behavior of cvs2svn is to import all of the CVS modules (or
projects) as a single project, putting module directories into each of
the /trunk, /branches, and /tags directory. For BRL-CAD, this results in
a hierarchy that looks like the following:

`/trunk/CVSROOT/...srcs...`
`/trunk/brlcad/...srcs...`
`/trunk/...other_cvs_modules.../...srcs...`

`/branches/ansi-branch/brlcad/...srcs...`
`/branches/windows-branch/brlcad/...srcs...`
`/branches/...other_brlcad_branches.../brlcad/...srcs...`
`/branches/...other_cvs_module_branches.../module/...srcs...`

`/tags/rel-5-2/brlcad/...srcs...`
`/tags/rel-7-0-2/brlcad/...srcs...`
`/tags/...other_brlcad_tags.../brlcad/...srcs...`
`/tags/...other_module_tags.../module/...srcs...`

Since BRL-CAD's modules really have been historically treated as
entirely separate projects, it became apparent that a different
hierarchy would be more desirable. It was not desirable to checkout the
trunk and receive all of the former CVS modules. Similarly it was not
desirable to have the extra module/project subdirectory in each of the
tag and branch directories.

Instead of restructuring the layout after the import to Subversion, the
BRL-CAD CVS repository conversion would be run through cvs2svn again as
a "multiproject" import. It became necessary to create a cvs2svn options
file where modules are individually listed. As a multiproject import,
the following hierarchy results:

`/CVSROOT/trunk/...srcs...`
`/brlcad/trunk/...srcs...`
`/...other_modules.../trunk/...srcs...`

`/brlcad/branches/ansi-branch/...srcs...`
`/brlcad/branches/windows-branch/...srcs...`
`/brlcad/branches/...other_brlcad_branches.../...srcs...`
`/...other_modules.../branches/...other_module_branches.../...srcs...`

`/brlcad/tags/rel-5-2/...srcs...`
`/brlcad/tags/rel-7-0-2/...srcs...`
`/brlcad/...other_brlcad_tags.../...srcs...`
`/...other_modules.../...other_module_tags.../...srcs...`

This parallels the CVS root files more directly and their nature as
independent projects. Upon conversion as a multiproject import, the
repository was once again validated both manually and quantitatively.
Creation of a Subversion repository from the dumpfile was verified. It
was verified that a complete log could be extracted via "svn log"
without error and that no warnings or errors existed in the cvs2svn
verbose output. Also, a complete checkout of the SVN root was performed
after upload to Sourceforge to verify no errors were evident.

It was later detected that permissions were incorrect on a limited set
of the CVS root files (a couple dozen), but the <svn:executable>
property was fixed on those files after import into SVN.

# cvs2svn Options

To perform the conversion, the following options file was used:

    import re

    from cvs2svn_lib.boolean import *
    from cvs2svn_lib import config
    from cvs2svn_lib.common import UTF8Encoder
    from cvs2svn_lib.log import Log
    from cvs2svn_lib.project import Project
    from cvs2svn_lib.output_option import DumpfileOutputOption
    from cvs2svn_lib.output_option import ExistingRepositoryOutputOption
    from cvs2svn_lib.output_option import NewRepositoryOutputOption
    from cvs2svn_lib.revision_reader import RCSRevisionReader
    from cvs2svn_lib.revision_reader import CVSRevisionReader
    from cvs2svn_lib.checkout_internal import InternalRevisionReader
    from cvs2svn_lib.symbol_strategy import AllBranchRule
    from cvs2svn_lib.symbol_strategy import AllTagRule
    from cvs2svn_lib.symbol_strategy import BranchIfCommitsRule
    from cvs2svn_lib.symbol_strategy import ExcludeRegexpStrategyRule
    from cvs2svn_lib.symbol_strategy import ForceBranchRegexpStrategyRule
    from cvs2svn_lib.symbol_strategy import ForceTagRegexpStrategyRule
    from cvs2svn_lib.symbol_strategy import HeuristicStrategyRule
    from cvs2svn_lib.symbol_strategy import RuleBasedSymbolStrategy
    from cvs2svn_lib.symbol_strategy import UnambiguousUsageRule
    from cvs2svn_lib.symbol_transform import RegexpSymbolTransform
    from cvs2svn_lib.property_setters import AutoPropsPropertySetter
    from cvs2svn_lib.property_setters import CVSBinaryFileDefaultMimeTypeSetter
    from cvs2svn_lib.property_setters import CVSBinaryFileEOLStyleSetter
    from cvs2svn_lib.property_setters import CVSRevisionNumberSetter
    from cvs2svn_lib.property_setters import DefaultEOLStyleSetter
    from cvs2svn_lib.property_setters import EOLStyleFromMimeTypeSetter
    from cvs2svn_lib.property_setters import ExecutablePropertySetter
    from cvs2svn_lib.property_setters import KeywordsPropertySetter
    from cvs2svn_lib.property_setters import MimeMapper
    from cvs2svn_lib.property_setters import SVNBinaryFileKeywordsPropertySetter

    Log().log_level = Log.VERBOSE

    ctx.output_option = DumpfileOutputOption(
        dumpfile_path=r'/path/to/brlcad.dumpfile',
        )

    ctx.dry_run = False
    ctx.revision_reader = InternalRevisionReader(compress=True)
    ctx.svnadmin_executable = r'svnadmin'
    ctx.sort_executable = r'sort'
    ctx.trunk_only = False

    ctx.prune = True

    ctx.utf8_encoder = UTF8Encoder(
        [
            'ascii',
            'utf8',
            ],
        )

    ctx.filename_utf8_encoder = UTF8Encoder(
        [
            'ascii',
            ],
        )

    ctx.symbol_strategy = RuleBasedSymbolStrategy()
    ctx.symbol_strategy.add_rule(UnambiguousUsageRule())

    ctx.username = None

    ctx.svn_property_setters.extend([
        AutoPropsPropertySetter(
            r'/path/to/auto-props',
            ignore_case=True,
            ),

        CVSBinaryFileEOLStyleSetter(),
        CVSBinaryFileDefaultMimeTypeSetter(),

        EOLStyleFromMimeTypeSetter(),

        DefaultEOLStyleSetter(None),

        SVNBinaryFileKeywordsPropertySetter(),
        KeywordsPropertySetter(config.SVN_KEYWORDS_VALUE),
        ExecutablePropertySetter(),

        CVSRevisionNumberSetter(),

        ])

    ctx.tmpdir = r'cvs2svn-tmp'
    ctx.cross_project_commits = True
    ctx.cross_branch_commits = True
    ctx.retain_conflicting_attic_files = False

    run_options.profiling = False

    ctx.add_project(
        Project(
            r'/path/to/brlcad/CVSROOT',
            'CVSROOT/trunk',
            'CVSROOT/branches',
            'CVSROOT/tags',
            )
        )
    ctx.add_project(
        Project(
            r'/path/to/brlcad/brlcad',
            'brlcad/trunk',
            'brlcad/branches',
            'brlcad/tags'
            )
        )
    ctx.add_project(
        Project(
            r'/path/to/brlcad/jbrlcad',
            'jbrlcad/trunk',
            'jbrlcad/branches',
            'jbrlcad/tags'
            )
        )
    ctx.add_project(
        Project(
            r'/path/to/brlcad/rt^3',
            'rt^3/trunk',
            'rt^3/branches',
            'rt^3/tags'
            )
        )
    ctx.add_project(
        Project(
            r'/path/to/brlcad/rtcmp',
            'rtcmp/trunk',
            'rtcmp/branches',
            'rtcmp/tags'
            )
        )
    ctx.add_project(
        Project(
            r'/path/to/brlcad/web',
            'web/trunk',
            'web/branches',
            'web/tags'
            )
        )

# Automatic properties

UPDATE: As noted above regarding the <svn:executable> property settings,
the auto-props file shown below was found to be not what we wanted with
respect to how cvs2svn handles property settings that don't list a
value. As of version 2.0.1, cvs2svn treats valueless auto-props property
settings as an indicator that cvs2svn should explicitly **unset** the
property instead of setting it. As this behavior may be changed in
future versions, consult the cvs2svn documentation.

Regardless, the following auto-props file that was ultimately used for
the BRL-CAD conversion is as follows:

    [auto-props]
    *.[0-9] = svn:mime-type=text/plain;svn:eol-style=native
    *.a = svn:mime-type=application/octet-stream
    *.ac = svn:eol-style=native;svn:mime-type=text/plain
    *.ai = svn:mime-type=application/illustrator
    *.am = svn:eol-style=native;svn:mime-type=text/plain
    *.asc = svn:eol-style=native;svn:mime-type=text/plain
    *.avi = svn:mime-type=video/x-msvideo
    *.awk = svn:eol-style=native;svn:mime-type=text/plain
    *.bat = svn:eol-style=CRLF;svn:mime-type=text/plain;svn:executable
    *.bmp = svn:mime-type=image/bmp
    *.c = svn:eol-style=native;svn:mime-type=text/plain
    *.cc = svn:eol-style=native;svn:mime-type=text/plain
    *.chm = svn:mime-type=application/octet-stream
    *.com = svn:eol-style=native;svn:mime-type=text/plain
    *.cpp = svn:eol-style=native;svn:mime-type=text/plain
    *.cs = svn:eol-style=native;svn:mime-type=text/plain
    *.css = svn:mime-type=text/css;svn:eol-style=native
    *.csv = svn:eol-style=native;svn:mime-type=text/plain
    *.cur = svn:mime-type=application/octet-stream
    *.cxx = svn:eol-style=native;svn:mime-type=text/plain
    *.decls = svn:eol-style=native;svn:mime-type=text/plain
    *.def = svn:eol-style=native;svn:mime-type=text/plain
    *.doc = svn:mime-type=text/plain
    *.dsp = svn:eol-style=CRLF;svn:mime-type=text/plain
    *.dsw = svn:eol-style=CRLF;svn:mime-type=text/plain
    *.dylib = svn:mime-type=application/octet-stream
    *.enc = svn:eol-style=native;svn:mime-type=text/plain
    *.eps = svn:mime-type=application/postscript
    *.f = svn:eol-style=native;svn:mime-type=text/plain
    *.g = svn:mime-type=application/octet-stream
    *.gif = svn:mime-type=image/gif
    *.gpgkey = svn:mime-type=application/gpg-keys
    *.gtar = svn:mime-type=application/x-gtar
    *.gz = svn:mime-type=application/x-gtar
    *.h = svn:eol-style=native;svn:mime-type=text/plain
    *.hpp = svn:eol-style=native;svn:mime-type=text/plain
    *.hqx = svn:mime-type=application/mac-binhex40
    *.htm = svn:mime-type=text/html;svn:eol-style=native
    *.html = svn:mime-type=text/html;svn:eol-style=native
    *.hxx = svn:eol-style=native;svn:mime-type=text/plain
    *.ico = svn:mime-type=image/x-icon
    *.igs = svn:mime-type=model/iges
    *.in = svn:eol-style=native;svn:mime-type=text/plain
    *.itcl = svn:eol-style=native;svn:mime-type=text/plain
    *.itk = svn:eol-style=native;svn:mime-type=text/plain
    *.jar = svn:mime-type=application/java-archive
    *.java = svn:eol-style=native;svn:mime-type=text/plain
    *.jpeg = svn:mime-type=image/jpeg
    *.jpg = svn:mime-type=image/jpeg
    *.l = svn:eol-style=native;svn:mime-type=text/plain
    *.log = svn:eol-style=native;svn:mime-type=text/plain
    *.m4 = svn:eol-style=native;svn:mime-type=text/plain
    *.man* = svn:mime-type=text/plain;svn:eol-style=native
    *.mov = svn:mime-type=video/quicktime
    *.mp3 = svn:mime-type=audio/mpeg
    *.mpg = svn:mime-type=video/mpeg
    *.ms = svn:eol-style=native;svn:mime-type=text/plain
    *.msg = svn:eol-style=native;svn:mime-type=text/plain
    *.n = svn:eol-style=native;svn:mime-type=text/plain
    *.nsi = svn:mime-type=text/plain;svn:eol-style=native
    *.pbxproj = svn:mime-type=text/plain;svn:eol-style=native
    *.pdf = svn:mime-type=application/pdf
    *.php = svn:mime-type=text/plain;svn:eol-style=native
    *.pix = svn:mime-type=image/x-rgb
    *.pl = svn:eol-style=native;svn:executable;svn:mime-type=text/plain
    *.perl = svn:eol-style=native;svn:executable;svn:mime-type=text/plain
    *.plist = svn:mime-type=text/plain
    *.png = svn:mime-type=image/png
    *.ppm = svn:mime-type=image/x-portable-pixmap
    *.ppt = svn:mime-type=application/vnd.ms-powerpoint
    *.ps = svn:mime-type=application/postscript
    *.psd = svn:mime-type=application/photoshop
    *.py = svn:eol-style=native;svn:executable;svn:mime-type=text/plain
    *.qpg = svn:mime-type=text/xml;svn:eol-style=native
    *.r = svn:eol-style=native;svn:mime-type=text/plain
    *.rc = svn:eol-style=CRLF;svn:mime-type=text/plain
    *.res = svn:eol-style=native;svn:mime-type=text/plain
    *.rgb = svn:mime-type=image/x-rgb
    *.rt = svn:eol-style=native;svn:executable;svn:mime-type=text/x-sh
    *.rtf = svn:mime-type=text/rtf
    *.s = svn:eol-style=native;svn:mime-type=text/plain
    *.sh = svn:eol-style=native;svn:executable;svn:mime-type=text/x-sh
    *.sln = svn:eol-style=CRLF
    *.smil = svn:mime-type=application/smil
    *.so = svn:mime-type=application/octet-stream
    *.spec = svn:eol-style=native;svn:mime-type=text/plain
    *.svg  = svn:mime-type=image/svg+xml
    *.svgz = svn:mime-type=image/svg+xml
    *.swf = svn:mime-type=application/x-shockwave-flash
    *.tcl = svn:eol-style=native;svn:mime-type=text/plain
    *.tk = svn:eol-style=native;svn:mime-type=text/plain
    *.terms = svn:eol-style=native;svn:mime-type=text/plain
    *.test = svn:eol-style=native;svn:mime-type=text/plain
    *.tex = svn:mime-type=text/x-tex
    *.tgz = svn:mime-type=application/x-gtar
    *.tif = svn:mime-type=image/tiff
    *.tiff = svn:mime-type=image/tiff
    *.tr = svn:eol-style=native;svn:mime-type=text/plain
    *.txt = svn:mime-type=text/plain;svn:eol-style=native
    *.vbs = svn:eol-style=native;svn:mime-type=text/plain;svn:executable
    *.vcf = svn:mime-type=text/x-vcard
    *.vcproj = svn:eol-style=CRLF;svn:mime-type=text/plain
    *.xbm = svn:mime-type=image/x-xbitmap
    *.xls = svn:mime-type=application/vnd.ms-excel
    *.xml = svn:mime-type=text/xml;svn:eol-style=native
    *.y = svn:mime-type=text/plain;svn:eol-style=native
    *.zip = svn:mime-type=application/zip
    .cvsignore = svn:mime-type=text/plain;svn:eol-style=native
    AUTHORS* = svn:eol-style=native;svn:mime-type=text/plain
    BUGS* = svn:eol-style=native;svn:mime-type=text/plain
    COPYING* = svn:eol-style=native;svn:mime-type=text/plain
    ChangeLog* = svn:eol-style=native;svn:mime-type=text/plain
    HACKING* = svn:eol-style=native;svn:mime-type=text/plain
    INSTALL* = svn:eol-style=native;svn:mime-type=text/plain
    Makefile* = svn:eol-style=native;svn:mime-type=text/plain
    NEWS* = svn:eol-style=native;svn:mime-type=text/plain
    README* = svn:eol-style=native;svn:mime-type=text/plain
    TODO* = svn:eol-style=native;svn:mime-type=text/plain
    ### catch-all for files starting and ending in all caps with optional (e.g. READ.ME)
    [A-Z._][A-Z._]*[A-Z._] = svn:eol-style=native;svn:mime-type=text/plain

UPDATE: The auto-props shown above is shown for historic purposes only.
If you're looking for an up-to-date auto-props file to work with, you
may want to try using [this
one](http://brlcad.org/~sean/subversion.config) from Sean instead.

# Results and statistics

The final cvs2svn processing was performed on:

`FreeBSD??bz.bzflag.bz??5.2.1-RELEASE??FreeBSD??5.2.1-RELEASE??#0:??Mon??Feb??23??20:45:55??GMT??2004??????????root@wv1u.btc.adaptec.com:/usr/obj/usr/src/sys/GENERIC????i386`
`Intel(R)??Celeron(R)??CPU??2.40GHz??w/??1GB??mem`

The conversion resulted in a 2.8GB dumpfile and provided the following
summary statistics:

`cvs2svn??Statistics:`
`------------------`
`Total??CVS??Files:??????????????????????????20127`
`Total??CVS??Revisions:????????????????147514`
`Total??CVS??Branches:????????????????????73233`
`Total??CVS??Tags:??????????????????????????281841`
`Total??Unique??Tags:????????????????????????????80`
`Total??Unique??Branches:????????????????????32`
`CVS??Repos??Size??in??KB:??????????????516588`
`Total??SVN??Commits:??????????????????????29886`
`First??Revision??Date:????????Thu??Dec??15??19:06:47??1983`
`Last??Revision??Date:??????????Mon??Dec??31??15:25:14??2007`
`------------------`
`Timings??(seconds):`
`------------------`
`1647??????pass1????????CollectRevsPass`
`??????0??????pass2????????CollateSymbolsPass`
`??483??????pass3????????FilterSymbolsPass`
`??????1??????pass4????????SortRevisionSummaryPass`
`??????2??????pass5????????SortSymbolSummaryPass`
`??459??????pass6????????InitializeChangesetsPass`
`??342??????pass7????????BreakRevisionChangesetCyclesPass`
`??568??????pass8????????RevisionTopologicalSortPass`
`??155??????pass9????????BreakSymbolChangesetCyclesPass`
`??341??????pass10??????BreakAllChangesetCyclesPass`
`??376??????pass11??????TopologicalSortPass`
`??330??????pass12??????CreateRevsPass`
`????15??????pass13??????SortSymbolsPass`
`????14??????pass14??????IndexSymbolsPass`
`3112??????pass15??????OutputPass`
`7844??????total????`
`(initial??pass??with??mime.types??was??9573??total)`

The result is a contiguous history of BRL-CAD development that has gone
from RCS to CVS and now to SVN preserving more than 25 years of revision
history. The conversion was completed on January 10th, 2008.

[category:Historical
documentation](category:Historical_documentation.md)
