## Reorganize NMG Data Structure

The functionality of struct **model** and **nmgregion** are top two
level of old nmg structure. One **model** can include multiple
**nmgregion**, and one **nmgregion** can include multiple **shell**. We
can have a brief view at following class definition.

    struct model
    {
        uint32_t magic;
        struct bu_list r_hd;    /**< @brief list of regions */
        char *manifolds;            /**< @brief structure 1-3manifold table */
        long index;         /**< @brief struct # in this model */
        long maxindex;      /**< @brief # of structs so far */
    };

    struct nmgregion {
        struct bu_list l;       /**< @brief regions, in model's r_hd list */
        struct model *m_p;      /**< @brief owning model */
        struct nmgregion_a *ra_p;   /**< @brief attributes */
        struct bu_list s_hd;    /**< @brief list of shells in region */
        long index;         /**< @brief struct # in this model */
    };

In general, it's a classical representation for NMG structure. But they
are redundant in BRL-CAD. There have been similar concepts here called
**combination** which can hold several primitives as a whole. So some
reorganization is necessary that these two structs (**model** and
**nmgregion**) are replaced by the BRL-CAD inner **combination** to fit
new NMG philosophy.

To achieve this target, we should move some important members from
**model** and **nmgregion** to new **shell** to keep existing function,
then take the new **shell** as the top level of new NMG structure.
Details as following:

-   **char \*manifolds**: Describe the meaning of a NMG structure.
-   **long maxindex**: Record the element(nmg structure of various
    levels) count of a NMG structure. It is important in MAKE and
    IMPORT/EXPORT part such as deciding how big memory should be
    allocated.

Then, let's check the definition of old **shell**:

    struct shell {
        struct bu_list l;       /**< @brief shells, in region's s_hd list */
        struct nmgregion *r_p;  /**< @brief owning region */
        struct shell_a *sa_p;   /**< @brief attribs */
        struct bu_list fu_hd;   /**< @brief list of face uses in shell */
        struct bu_list lu_hd;   /**< @brief wire loopuses (edge groups) */
        struct bu_list eu_hd;   /**< @brief wire list (shell has wires) */
        struct vertexuse *vu_p; /**< @brief internal ptr to single vertexuse */
        long index;         /**< @brief struct # in this model */
    };

Obviously, some members should be changed to achieve new NMG philosophy:

-   **struct nmgregion \*r_p**: Can be removed since there is no
    **nmgregion** concept any more.
-   **struct bu_list l**: We don't need this backward point which
    points to **shell** 'superior level structure. But a new member
    **uint32_t magic** is still necessary.

Following is the new **shell** definition after reorganization.

    struct shell {
        uint32_t magic;
        struct shell_a *sa_p;   /**< @brief attribs */
        struct bu_list fu_hd;   /**< @brief list of face uses in shell */
        struct bu_list lu_hd;   /**< @brief wire loopuses (edge groups) */
        struct bu_list eu_hd;   /**< @brief wire list (shell has wires) */
        struct vertexuse *vu_p; /**< @brief internal ptr to single vertexuse */
        char *manifolds;        /**< @brief structure 1-3manifold table */
        long index;         /**< @brief struct # in this model */
        long maxindex;      /**< @brief # of structs so far */
    };

## Fit New NMG Data Structure

Changing the NMG data structure is just first step. Due to these change,
thousands of compiling errors are coming. I spent most of my time in
these weeks to fix and test them properly.

It worth mentioning that 28 functions in raytrace.h are removed which
may simplify the future work because they are no longer useful. The
detailed list is as following:

-   struct model \***nmg_mmr**(void);
-   struct nmgregion \***nmg_mrsv**(struct model \*m);
-   int **nmg_kr**(struct nmgregion \*r);
-   void **nmg_km**(struct model \*m);
-   void **nmg_region_a**(struct nmgregion \*r, const struct bn_tol
    \*tol);
-   struct model \***nmg_find_model**(const uint32_t \*magic_p);
-   struct vertex \***nmg_find_pt_in_model**(const struct model \*m,
    point_t pt, struct bn_tol \*tol);
-   void **nmg_pr_m**(const struct model \*m);
-   void **nmg_pr_r**(const struct nmgregion \*r, \*h);
-   int **nmg_find_outer_and_void_shells**(struct nmgregion \*r,
    bu_ptbl \*\*\*shells, struct bn_tol \*tol);
-   fastf_t **nmg_region_area**(const struct nmgregion \*r);
-   fastf_t **nmg_model_area**(const struct model \*m);
-   struct model \***nmg_mk_model_from_region**(struct nmgregion
    \*r, reindex);
-   int **nmg_mv_shell_to_region**(struct shell \*s, nmgregion \*r);
-   char \***nmg_manifolds**(struct model \*m);
-   void **nmg_r_to_vlist**(struct bu_list \*vhead, struct nmgregion
    \*r, int poly_markers);
-   void **nmg_m_to_vlist**(struct bu_list \*vhead, struct model
    \*m, int poly_markers);
-   void **nmg_pl_r**(FILE \*fp, const struct nmgregion \*r);
-   void **nmg_pl_m**(FILE \*fp, const struct model \*m);
-   void **nmg_vlblock_r**(struct bn_vlblock \*vbp, const struct
    nmgregion \*r, int fancy);
-   void **nmg_vlblock_m**(struct bn_vlblock \*vbp, const struct
    model \*m, int fancy);
-   void **nmg_vshell**(const struct bu_list \*hp, const struct
    nmgregion \*r);
-   void **nmg_vregion**(const struct bu_list \*hp, const struct model
    \*m);
-   void **nmg_vmodel**(const struct model \*m);
-   int **nmg_ck_closed_region**(const struct nmgregion \*r, const
    struct bn_tol \*tol);
-   void **nmg_r_radial_check**(const struct nmgregion \*r, const
    struct bn_tol \*tol);
-   void **nmg_visit_region**(struct nmgregion \*r, const struct
    nmg_visit_handlers \*htab, genptr_t state);
-   void **nmg_visit_model**(struct model \*model, const struct
    nmg_visit_handlers \*htab, genptr_t state);

After that, there is no shortcut but to check the compiling errors one
by one. Read the codes, understand the context and fix them to fit new
nmg structure. It's a bit tedious but helpful for getting familiar with
this part of BRL-CAD further more. There are some main kinds of
situation:

-   Change a function of **model/nmgregion** version to a **shell**
    version.
-   Extend existing function to support new members of **shell**.
-   Remove the traversal of **model/nmgregion**. Fortunately, some
    function assume only one **shell** in the **model**.

## Conclusion

At first, I'd like to extend my heartfelt gratitude to my mentor, Daniel
and other developers in BRL-CAD community. I was so excited to learn
plenty of knowledge and skills which cannot be gained in other places.

I am sorry that my progress falls a little bit behind compared with my
initial proposal because some mistake make me go into a wrong way
especially when I fix the functionality about Import/export modules. It
takes me some time to figure out what happens exactly to MGED when user
use 'facetize -n' command and to find out the most proper solution. In
next weeks, I will speed up to catch up with the schedule and try my
best to finish the project as what I promised.

As for the code statistics, the result from statSVN shows 303 places in
my branch have been changed. The count of code lines been changed is
3608.