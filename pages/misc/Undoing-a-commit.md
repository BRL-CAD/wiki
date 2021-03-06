# Undoing an svn commit

Sometimes one may inadvertently commit a change that was not intended or
need to revert a change made by someone else because it breaks
functionality. For example:

`$ svn ci test_vls.c`
`Sending        test_vls.c`
`Transmitting file data .`
`Committed revision 9999.`

We want to "uncommit" the change. If we don't want to lose the changes
we just committed, no worries. We can copy those file(s) to an
unversioned directory **before** we do the merge steps below or extract
those changes at any point in the future with the "svn diff" command.
Stash the changed file(s) if desired.

Do the merge (note the dot):

`$ svn svn merge -r9999:9998 `**`.`**
`U  test_vls.c`

That just "merged" the commits from revision 9999 to 9998, which
effectively "undoes" 9999. Check that your trunk checkout has changed
back to the state before the bad commit:

`$ svn diff`
`...`

Save the diffs if desired.

Commit the change (**caution**: this will undo local changes that were
originally committed!):

`$ svn commit -m "Reverting r9999 because ..."`
`Sending        test_vls.c`
`Transmitting file data .`
`Committed revision 10000.`