## Migrating from Sourceforge to Github

BRL-CAD is migrating from Sourceforge to Github. This page is intended
to identify and track steps taken so there is awareness and confidence.

## Migration V&V steps

-   <s>Convert and upload repository candidate</s>
-   <s>Verify GitHub presentation</s>
    -   <s>Verify commit count is &gt;= SVN commit count</s>
    -   <s>Ensure at least 75% of committers are represented</s>
    -   <s>Ensure at least 95% of commits are represented by
        committers</s>
    -   <s>Ensure commit metadata presents meaningfully</s>
    -   <s>Manually test file history tracing on 10+ files in different
        directories</s>
        -   CANNOT SEE FULL HISTORY -- KNOWN GITHUB ISSUE BUT NOT GIT
            ISSUE
        -   support e-mailed
    -   <s>Manually identify and compare a UTF file's presentation
        (e.g., AUTHORS)</s>
    -   <s>Manually identify and compare a UTF commit message's
        presentation</a></s>
    -   <s>Verify repo cloning</s>
-   Verify repository contents (accounting for and documenting all
    discrepancies)
    -   <s>Verify SVN commits are all present or otherwise accounted
        for</s>
    -   <s>Verify SVN commit metadata are all present or otherwise
        accounted for</s>
    -   <s>Iterate all SVN committers, compare against GitHub commit
        count</s>
    -   <s>Iterate all SVN committers, compare against GIT commit
        count</s>
    -   <s>Iterate all SVN commits, ensure they can be found in GIT</s>
    -   <s>Iterate all SVN commits, compare GIT checkout with SVN</s>
    -   <s>Manually inspect 10+ files in different directories</s>
    -   <s>Manually identify and compare a UTF file checkout (e.g.,
        AUTHORS)</s>
    -   <s>Manually identify and compare a UTF commit message</s>
    -   <s>Verify GIT repo cleanup (garbage collect, orphans) doesn't
        change repo</s>
-   Migrate SourceForge project data
    -   Migrate SourceForge tracker data for bugs/support/requests to
        issues
    -   Back up SourceForge mailing lists into searchable archived form
    -   Migrate / Encode SourceForge Metadata (project categorization,
        screenshots)
    -   Migrate SourceForge patches (process TBD)
-   Update Docs
    -   Update HACKING text and refs
    -   Update README, doc/README\*, & INSTALL text and refs
    -   Search/update repo SVN/subversion/Sourceforge/sf.net references
    -   Search/update website SVN/subversion/Sourceforge/sf.net
        references
-   Update infrastructure
    -   Update self-hosted Jenkins
    -   Configure GitHub repo to make branches and tags immutable
    -   Populate GitHub with releases
    -   Disable SourceForge trackers
    -   Disable SourceForge mailing lists
    -   Mirror GitHub project to Sourceforge
    -   Migrate Zulip to Gitter
-   Update Website
    -   Point Download section to GitHub
-   Announce
    -   IRC+Gitter
    -   Facebook+Twitter
    -   News mailing list

## Known Discrepancies

-   Some SVN commits are represented as multiple GIT commits
    -   Implies the GIT commit counts may be higher
-   SVN metadata (i.e., props) commits are not represented in GIT
    -   Implies the GIT commit count may be lower
-   Some SVN metadata is stored in the GIT log
    -   Strip trailing \\n\\n(svn:.\*\\n)+ lines to compare commit
        messages
-   "Initial revision" commits have their commit replaced
    -   Their svn revision numbers are missing from Git metadata
    -   Their commit messages appear to be replaced
-   no-diff commits result in no commit in git
    -   for example 66607 merged from branch, no-op changes to
        include/bu/defines.h

## Remaining Items to Consider

=

-   IMPORTANT: We need to set up protections for the historical branches
    in Github:
    <https://docs.github.com/en/github/administering-a-repository/managing-a-branch-protection-rule> -
    without this, we can lose history if anyone accidentally deletes old
    branches whose commits are not referenced by any undeleted branches.
    (Unfortunately Github doesn't yet support protecting tags
    (https://github.community/t/feature-request-protected-tags) but
    if/when that feature is added we will also want to use it.)

<!-- -->

-   Sourceforge also stores user reported issues, patches, and other
    secondary data we would like to migrate. This migration has been
    less thoroughly explored, but it appears
    <https://github.com/n-soda/gosf2github> may be a good starting
    point.

<!-- -->

-   We need to investigate available hooks in git for enforcing
    standards, procedures, etc for pull requests and commits.

<!-- -->

-   Email is currently hosted on sourceforge - need to decide what to do
    about migrating it (or not...). CMake recently switched to
    discourse - <https://discourse.cmake.org/>

## OLDER CONTENT

=

## Version Control History

<s>The most difficult and important of the conversion steps is the
migration of BRL-CAD's version control based source code history from
Subversion to Git. The process as it is finalizing (documented in detail
in the BRL-CAD repository itself in the misc/repoconv sub-directory)
will take a number of weeks to run, and will proceed roughly as follows:

-   Finalize the email addresses and names used to map Subversion
    accounts to Github accounts. (Once the final conversion begins,
    these user identities are "locked in" to the git history and cannot
    easily be changed - they must be fully ready before the process
    begins.)
-   Perform the initial Subversion -&gt; Git process as outlined in
    misc/repoconv. (Est. 2-3 weeks to complete, once begun.)
-   Lock the Sourceforge Subversion repository into read-only mode.
-   Run a final update to pick up any commits made during the initial
    conversion process.
-   Run the svn-fast-export process to generate the secondary git
    repositories for projects (geomcore, rt^3, etc.) other than the
    primary BRL-CAD repo in the Subversion repository on
    sourceforge.net/p/brlcad. (This process is much faster than the main
    conversion, and shouldn't take more than a few hours.)
-   Upload all of the repositories to the github BRL-CAD project.
    -   See the NOTES file in misc/repoconv for more details on this
        process.
    -   Once "live", we can no longer alter the git history without
        potential impact to other developers - a git history rewrite
        (which any change will require) is guaranteed (unlike SVN) to be
        user visible and disruptive.
-   Test checkout from the new repositories on github.
-   Announce the change on the email list and update the website links.
-   Ensure any testing infrastructure is updated to connect to the new
    git repository rather than the (now static) SVN repository.</s>

<s>For completeness, the plan is to create a Git repository that
preserves the CVS and SVN repository contents in their final states. The
original CVS history proved important when doing the Git conversion, and
should another attempt be made someday to migrate BRL-CAD's history to a
new VCS it may well prove useful to have the original early data
available, as opposed to the (inevitably) lossy Git conversion of that
data. (A quick test indicates such a repository would be about 1.7G in
size.) For best behavior the repo should probably have a .gitattributes
file identifying all file types as binary files.</s>

## In-Repository Updates

<s>Once the primary VCS migration is complete, there are a number of
features and instruction files in BRL-CAD itself that will need to be
updated to reflect the new location and tools. In particular:</s>

-   <s>README, INSTALL and HACKING - some of the HACKING procedures may
    need to be updated to reflect github's workflow.</s>
-   <s>The distcheck repository check target has some awareness of
    subversion in its verification steps. Preliminary work has been done
    to shift this logic to use Git - that work must be finalized and
    tested.</s>
-   <s>Once the VCS conversion is complete, remove the misc/repoconv
    directory - it will no longer be needed and the information it
    encodes will be preserved in the VCS history itself.</s>

<s>We'll want to put together some usage notes on how to work with
Git+BRL-CAD. Following history past renames is a problem (See
<https://marc.info/?l=git&m=123333586414420> and
<https://marc.info/?l=git&m=123333626615117>) and ideally we'd like devs
to move files first and commit the move before making any changes to
allow us to follow local file history more easily. Git philosophically
does not track per-file history, which is unfortunate given BRL-CAD's
historical practices - there are often situations where following a
file's individual history is the most efficient way to understand why a
subset of the code base is the way it is today. We have dealt with this
in the conversion by automatically inserting preliminary move commits to
allow git log --follow to work with maximal efficiency, but there isn't
a practical way to enforce this once we start using git itself - there's
no option to explicitly track file moves and without it it is up to
individual developers to remember to rename, commit, and then edit. This
is especially hard since renames without file editing often break the
build, and the reflex is to fix the build before committing...</s>

## User Workflow Updates

<s>Over the years a number of convenience setups have been worked out
for Subversion, such as the mime type defaults. Once we convert to git,
we want to establish similar defaults and standards in Git. This will be
ongoing, but already known:</s>

-   <s>UPDATE - after discussion, good reasons not to do this, skipping.
    Add a .gitattributes file to the repository to establish default
    behavior for various file types - a prototype is at
    misc/repoconv/gitattributes.</s>
-   <s>Utilize github workflows to set up cross platform CI using
    github's infrastructure. Some preliminary testing has been done in
    throw-away repositories, and once a working setup has been
    identified we will enable it in the main repository.</s>
-   <s>Set up a recommended user git config that will establish some
    semi-standard convenience aliases - in particular, for working with
    the historical information encoded in the git notes.</s>