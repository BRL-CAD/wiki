## Proposal draft for adding exec option to search command (WIP)

#### [Personal information](../../Bhinesley.md)

##### [Contact info](../../Bhinesley.md#Contact)

##### Alternate contact info

##### [Who I am](../../Bhinesley.md#Who_I_am)

##### [Experience](../../Bhinesley.md#Experience)

##### Interest in BRL-CAD

##### Benefit to BRL-CAD


=== Project Information ===

#### Summary

This project focuses on the addition of an exec option to the libged
*search* command. The idea is similar to the exec option of the *find*
command in Unix. Like *find*, *search* is a powerful tool for generating
a list of matches of given a search pattern. However, while the search
pattern may be specified using diverse criteria, there is currently no
option for performing operations on the results.

Suppose major changes had recently been made to a model. *search* could
be use to find all empty combinations (analog to directories in Unix):

`search -nnodes 0`

In order to remove all of the combinations returned, a user would have
to either *kill* each one manually, or write a Tcl script to iterate
over them. The former method is not feasible for a large number of
results. The latter involves multiple time consuming steps. Performing
operations on search results is a common enough problem that having
integrated support is well worth the implementation effort:

`search -nnodes 0 -exec kill {};`


Command names supplied via the exec argument must map to libged
functions, so that *search* can call them. Currently, these mappings are
done outside of libged. A major milestone in this project will be
creating these mappings inside libged, by having each command add itself
to a registry.

While MGED and Archer themselves will eventually rely upon the libged
command registry for mapping command names to functions, it is not yet
clear if this migration is within the scope of the project
(<font color=red>**TBD**</font>).

#### Description

-   code references/samples/etc.
-   measurable goals

#### Milestones

#### Timeline

#### Prior commitments

The program starts three weeks before the end of my quarter, not
including finals week. Most, if not all, of my classes are project-based
this year. This will work to my advantage. I will be able to get the
bulk of the work done ahead of schedule, minimizing the impact on the
project. If there is any lost time, I will make it up in the following
weeks, at a rate of +5 hours per week.

#### Contingencies
