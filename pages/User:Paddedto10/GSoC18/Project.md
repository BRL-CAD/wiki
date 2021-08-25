# Adding support for the -exec option in the search command

## Overview

BRL-CAD databases are like file system trees, so the tools around it
evolved in a similar fashion to UNIX tools, including a *search* command
that is somewhat analogous to *find(1)*, one key difference is that it's
missing the *-exec* option. Currently, MGED specific commands only take
"data" options, things that are present in the database, or are literal
values - like numbers or text - and as such, they are accessible to
*libged* without - the editor library. However, for *-exec* to work in
MGED *search* would have to run arbitrary Tcl commands, but the search
logic lives in *librt*, which has no access to the Tcl interpreter. The
original plan was a C-side table mapping command names to functions, but
because the Tcl namespace is dynamic, the only way to translate a name
to a command is by asking Tcl.

## Proposed solution

The solution we settled on is adding an "exec_handler" callback to
*db_search*, which will take the usual argv/argc pair, but also take a
*void\** that will also be provided in the call to *db_search*. This
will get called on each node and return a boolean value, it will receive
the parameters passed to it in the '-exec' query with the '{}' ones
replaced by the current path.

*(The '{}' syntax is not final, but since it is easy to change, it does
not need to be.)*

MGED can then provide a callback that simply runs its *argv* in the Tcl
interpreter passed to it through the void pointer.

## Detailed solution

I plan to use TDD throughout the project and I will document
added/changed functionality in Doxygen as I go. Here is my roadmap with
rough and pessimistic time estimates:

### Milestone 0

1.  Add callback type definition in the relevant header, add callback
    and userdata parameters to *db_search*.
2.  Add necessary fields to the search plan struct.
3.  Add evaluation logic for exec in plans.
    -   This is the first big one, I'll have to study how search
        evaluation works more in-depth, but it shouldn't take longer
        than a week.

### Milestone 1

1.  Write the parser for the *-exec* option.
    -   It shouldn't be too hard, just your run-of-the-mill custom
        argparse.
2.  Integrate it with the planner logic.
    -   Definitely harder, the planner looks quite weird at first, so
        I'll have to make sure I understand it completely before I go in
        and start grafting things onto it; still, it's shouldn't be
        super difficult, should be done in a week, maybe two.
3.  Modify rest of evaluation logic to more closely correspond to
    *find(1)* (such as not implicitly printing when -exec is present).
    -   By this point I will have acquainted myself with the planner and
        evaluation logic enough that this one shouldn't be hard.

### Milestone 2

1.  Write the exec_callback that will call Tcl functions on MGED's
    side.
    -   Biggest difficulty here is understanding how Tcl works on the C
        side, how to push results, call functions, pass parameters, that
        kind of thing, so this could take a while, 2 weeks maybe.
2.  Hook up the two sides.
    -   should be easy by this time, I estimate 1-3 days.

### Milestone 3 (extra?)

1.  Add support for '+' form.
    -   I left this for last, so the ';' form can be released to end
        users sooner and because its necessity is not yet clear. The
        biggest difficulty here is aggregating multiple paths into a
        single call and deciding where that call should take place. I
        suspect this one to take 2 weeks.