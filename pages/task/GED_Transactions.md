Transactions are discrete events that change data from one state to
another. In BRL-CAD, geometry editing transactions refer to operations
that change geometry or metadata from one state to another - say, for
example, renaming a region from region1.r to region2.r.

Our new geometry editing library libged is not currently based on
transactions, but simply acts on the data. This means that after an
action is applied, there is not convenient way to remember what was done
or how to reverse it.

This project would introduce into libged a paradigm of functions
generating transactions, which are then applied. So instead of a
translate command simply applying a matrix operation that moves a sphere
10mm in the -x direction directly, the command would return a
transaction that is then applied to the sphere. The advantage of this is
that the transaction paradigm allows for both transactions and reverse
transactions to be generated, allowing for a powerful undo capability.
Take the sphere example. If an application is maintaining an ability to
undo operations, it can note that a transaction event has been applied
to sphere and store the inverse of that transaction in its undo log.
Then, an undo operation simply applies the transaction at the top of the
undo stack (in the case of the sphere, the inverse transaction would be
moving 10mm in the +x direction) and restores the previous state without
having to store the entire state of the sphere prior to and after
editing. Admittedly when editing a single sphere this is not a large
problem, but in more complex cases the savings quickly become
significant.

A student proposal should outline an API for transaction generation and
application, and a proposal on how to integrate it into libged gradually
(libged is large and such a conversion shouldn't be an all-or-nothing
proposition) For some libged transactions the inverse transaction may
not be obvious, and the API details and design for implementation also
need careful consideration. A student proposing this topic should
discuss it on IRC or email with BRL-CAD developers (preferably IRC).

# References

-   src/libged
-   src/mged
-   include/ged.h

# Requirements

-   Familiarity with C