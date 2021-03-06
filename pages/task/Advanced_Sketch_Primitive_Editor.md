BRL-CAD supports many primitives, including a 2D sketch primitive, but
we do not presently provide the means to specify values that are
undetermined or otherwise dependent calculations. So we don't have a way
to constrain (for example) a line segment to remain at a fixed angle
relative to another line segment during editing.

This task would focus on implementing basic support for this feature in
the context of BRL-CAD's sketch primitive. Options include:

-   Integrate existing BSD licensed 2D constraint solving functionality
    from exising projects:
    -   <https://code.google.com/p/psketcher/>
    -   <https://code.google.com/p/sketchsolve/>

In particular, psketcher offers some Qt visualizations of sketch editing
- a good "first step" would be to make a "Qt sketch editor" for
BRL-CAD's sketch objects. This is likely to require refactoring
psketcher and/or sketchsolve, but they do provide a starting point.

-   Once a solving framework is in place and working with BRL-CAD sketch
    objects, test out the Gecode constraint solver by defining the 2D
    constraints from the above solvers in the Gecode framework - see how
    its solving speed compares to the dedicated 2D solutions, and how
    straightforward it is to use Gecode to solve such problems.
    -   <http://www.gecode.org/>
    -   <http://www.gecode.org/doc-latest/reference/classCartesianHeart.html>

This task is related to the more general parametric constraint tasks,
but it is more narrowly scoped and more focused on immediately user
visible features.

# References

-   <https://code.google.com/p/psketcher/>
-   <https://code.google.com/p/sketchsolve/>
-   <http://www.gecode.org/>
-   <http://www.gecode.org/doc-latest/reference/classCartesianHeart.html>
-   src/librt/primitives/sketch
    -   contains sources pertaining to BRL-CAD's 2D sketch primitive

Requirements:

-   Familiarity with C/C++