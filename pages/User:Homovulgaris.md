__NOTOC__

## Dawn Thomas

-   Enrolled in PostGraduate Program at Indian Institute of Management,
    Bangalore.
-   Bachelors in Architecture at Indian Institute of Technology,
    Kharagpur.

## GSoC 2009 Log

### 2009.06.20

-   code added to cc command to add an empty rt_constraint object to
    the database

### 2009.06.18

-   cc (create constraint) framework added

### 2009.06.17

-   lscon command framework added to libged

### till 2009.06.17

-   Expression grammar defined

## GSoc 2009 Proposal Draft

### Abstract

Continuing with the libpc work from last gsoc, the proposal is for
providing the following functionalities in mged/libged for the end-user

1.  creation/modification of constraint objects
2.  a solve command for solving a set of constraints / all the
    constraints in the loaded .g file
3.  options for selection from a range of solutions if possible

for achieving the same, the work falls under the following heads

1.  An inclusive definition of constraint grammar on the basis of the
    existing Math grammar which can be easily extened later.
2.  Integration with libged - framework for calls into librt and libpc
    for solution, storage and updation.
3.  Writing a robust modular constraint solver
4.  Testing of the framework throughout

### Proposal

The status of libpc project as of now is as follows.

1.  Abstraction Framework - Objects implemented : Parameters, Variables
    and Constraints, Constraint Network
2.  Solution System - Generic solver testing all possible variable
    assignment combinations, Graph specific solver using boost graph
    library
3.  Math Virtual Machine (work in progress) - expected to be complete
    with around 400 to 500 lines of code change at max.
4.  Basic constraint I/O in librt - will need changes till constraint
    grammar is finalized

Project definition for the approximately 480 coding hours of gsoc ( May
23rd to August 10th) is as follows.

**1. Constraint grammar (\~90 hours)**

This would be dependent on the underlying Math grammar system. Testing
out the grammar system would include correct parsing of expressions
implying the constraints into the constraint objects. For instance ( "
tangential(ell1, sph1)" being parsed into the correct constraint objects
containing evaluating functions in terms of the variables)

**2. Integration with libged/librt (\~230 hours)**

The purpose is to create adequate commands for the creation and
modification of constraint objects and their "solving". libged would
interface with the user and the already existing code and its
modification will provide database I/O. This work can be done along with
the development of the constraint grammar work mentioned above since
both are in a way interdepedent.

**3. Solution system (\~75 hours)**

Undoubtedly the most important aspect of the constraint system. Two
approaches can be taken for modularity of the solver from other parts of
libpc. One way would be to use a server-client model possibly using
inter-process communication or a simple file based transfer of data
between the two. Alternatively it could be a part of the libpc library
itself requiring a particular format of the constraint satisfaction
problem. This could be passed on to the solver as string data or as a
data structure. Of the various approaches towards solving geometrical
constraints, I am slightly in favour of graph-constructive methods over
the others (see \#1) But eventually I think something like a Locus
Intersection method (\#4) which is a hybrid between the computational
and search approaches would be ideal. One of the reasons I feel that the
solver should be completely independent of the constraint satisfaction
problem definition or representation is the fact that it is a field
rapidly undergoing changes in terms of new approaches. The priority of
course is for the creation of a basic overall framework that is user
accessible rather than an extremely fine tuned solver. Depending on the
rapidity with which libged progresses, more time can be alloted for this
job over the other heads mentioned.

**4. Test Use-cases for the entire framework (\~90 hours)**

This involves using the libpc framework for doing the rt_prep checks
for each of the geometry primitives as well as the testing of the entire
framework spread throughout the development process. This work can be
pursued independent of the work on the solution system , using the
existing generic solver. Also in terms of implementation this would be a
good start to finalize the common type of constraints grammar wise (
parallelism, perpendicularity etc.) The estimate for testing is
approximately at the rate of 1 day of work per week.

### Schedule and Status

**Pre GSoC**

-   Math VM/ Grammar completion
-   Documentation Overhaul
-   Do further groundwork on Solver
-   Finalize expected commands, argument set and output

**May 23 - July 6 (\~ 6 weeks)**

-   libged commands
    -   create constraint (ongoing)
    -   edit constraint
    -   display constraint (ongoing)
-   Finalizing Constraint grammar
-   Test of the creation and display

**July 6 - August 10 (\~ 5 weeks)**

-   libged commands
    -   solve
    -   select solution
-   Complete Solver work
-   Test the solve/ select solution use-cases
-   Further overall testing \*\*
-   librt rt_prep checks transition to libpc\*\*

`** if ahead of schedule at mid-term analysis`

**Post GSoC**

-   Add further commands to the ui
-   Improve solver(s)
-   Increase the number of "available/hard-coded" constraint types
-   Improve the solution display / selection system ?

### Other Notes

-   Some tinkering is also needed to make the existing code more
    modular.
-   There is also a "small" memory leak in the solver which needs to be
    taken care of.
-   In the long run, I am sure that the rigor of the solver would be the
    major factor in terms of usability as well as performance. Even
    though I have been toying around with some generic constraint
    solvers as well as geometric ones, I haven't found one which could
    be easily integrated into brl-cad. The ideal approach would be to
    make the solver an independent module. This would not only support
    using multiple solvers by using the same "protocol or format", but
    also simplify the process of progress in terms of solver
    optimizations.

### References

[1](http://www.cs.purdue.edu/research/technical_reports/1993/TR%2093-054.pdf)
A geometric Constraint Solver, W Bouma, I Fudos, C Hoffmann, J Cai, R
Paige - Computer Aided Design, 1995

[2](http://portal.acm.org/citation.cfm?id=502348.502362) A Modular
Geometric Constraint Solver for User Interface Applications, Hiroshi
Hosobe , ACM symposium on User interface software and technology, 2001

[3](http://eprints.kfupm.edu.sa/65700/) Solving geometric constraint
systems, GA Kramer, BB Qh - 1992\]

[4](http://dx.doi.org/) Solving spatial basic geometric constraint
configurations with locus intersection, XS Gao, CM Hoffmann, WQ Yang -
Computer-Aided Design, 2004 - Elsevier
<doi:10.1016/S0010-4485(03)00056-3>