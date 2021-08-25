# Primitives Details

There are 19 (to be precise) primitives which needs to be added.

I list below the dependencies of those primitives.

-   The following primitives depend upon the fundamental data types or
    the data structures which have been taken care by already
    implemented ctypes adapters.
    -   ARS
    -   CLINE
    -   GRIP
    -   PG
    -   Superell
    -   HRT
    -   BINUNIF
    -   HALF
    -   Metaball

<!-- -->

-   The following primitives use few data_structures wherein I am not
    sure about the implementation and those will be sorted at the time
    of implementation based upon discussions and already implemented
    examples. These include
    -   BOT
        -   Bot_list
    -   DSP
        -   bu_mapped_file
        -   rt_db_internal
        -   bu_vls
    -   EBM
        -   bu_mapped_file
        -   bu_vls
    -   HF
        -   bu_mapped_file
    -   NURB
        -   BREP
    -   Submodal
        -   bu_vls
        -   db_i
    -   PNTS
        -   rt_pnt_type
    -   Annotation
        -   rt_sketch_internal :: Done already in the implementation.
        -   bu_vls
    -   CONSTRAINTS
        -   bu_vls
    -   BREP
        -   ON_BREP

<!-- -->

-   Following are the structures which have dependencies in the
    primitives.
    -   bu_vls :: Stands for variable length string.
    -   bu_mapped_file : To Be Discussed and Found
    -   rt_db_internal : To Be Discussed and Found
    -   ON_brep To Be Discussed and Found
    -   db_i :: TO Be Discussed and Found