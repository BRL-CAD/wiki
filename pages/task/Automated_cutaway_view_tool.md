Recent research has outlines automatic methods for generating "cutaway
views" of geometry - select removal of outer components of geometry that
allow visualizations access to inner components. See
<http://grail.cs.washington.edu/projects/cutaways/>

For BRL-CAD, this visualization might be achieved by inserting selected
subtractions into a boolean hierarchy tree to expose inner components. A
student proposal on this topic should outline how they would approach
issues like identifying the shape to use for removal and identifying
where in the tree to add the subtractions. This should also be done
without changing the original geometry, so the tool would need to work
on a duplicate of the boolean tree (without duplicating the underlying
primitives as well.)

Requirements:

-   Familiarity with C

Difficulty: low to medium