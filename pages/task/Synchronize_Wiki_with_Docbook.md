BRL-CAD has more than a million words of documentation (thousands of
pages) in a variety of formats. We have a long-term goal to consolidate
as much as possible into the Docbook format so that it can be more
directly managed by our revision control system and integrated with the
source code. At the same time, we have a user-editable wiki that is
really easy for users and developers alike to keep up to date. The two,
however, are not immediately compatible with one another. Data is not
shared or synchronized.

The main goal of this project would be to synchronize the two so that
edits to either are reflected in the other without loss of data. One of
the main challenges is how to retain the more expressive Docbook markup
within Mediawiki so that edits via the wiki are not "dumbed down" to the
more simple Mediawiki syntax.

The initial thoughts on our end are to implement a Mediawiki extension
that understands how to translate to/from the Docbook format that
faithfully preserves all Docbook tagging. You're welcome to suggest
another approach.

A great starting point for this project are our existing command sets
for BRL-CAD and MGED (our main geometry editor). They respectively
constitute approximately 400 and 700 commands that have a page of
documentation each.

# References

-   doc/docbook

<!-- -->

-   [MGED_Commands] (MGED_Commands.md)
-   [BRL-CAD_Commands](BRL-CAD_Commands)

# Requirements

-   Basic familiarity with Docbook
-   Basic familiarity with Mediawiki editing and/or Mediawiki extensions
-   Familiarity with web development technologies
-   Basic familiarity with a revision control system (Subversion)
