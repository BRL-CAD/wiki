# Midterm Summary: Command-line Editing NMG Data-structures in BRL-CAD (GSoC 2015)

Initially started mapping all nmg_\* routines of the internal API to
the CLI. This raised issues of passing parts of the model as a
parameter, which currently is not possible. There is also some ambiguity
as to the usefulness of shells and regions in the NMG data structure.

Much of the work to date has been exploratory. Preliminary
implementations will be iterated over. Daily commits are hosted
[here](https://github.com/behollis/brlcad-svn-rev65072-gsoc2015).

A top-level CLI command is available for use since r65522. This revision
allows for each subcommand's parameters to be specified by the
corresponding ged routine. Generic usage: $ nmg subcommand model-name
parameters-list