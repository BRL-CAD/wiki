BRL-CAD is a large code base with more than 1,000,000 lines of code.
That means there are guaranteed to be bugs so fixing them is always a
priority. Our current BUGS file, included in every distribution, lists
more than 100 bugs. Our BUG tracker on Sourceforge lists more.

Your project proposal should identify several specific bugs that you
intend to fix along with contingency plans for a) bugs that you are
unable to fix and b) identifying additional bugs if you fix all of your
initial bugs quickly.

You're welcome to include testing procedures and infrastructure set up
(such as automated builds) if it will help you fix bugs faster.

In any event, each bug fix should have a test in one of the established
test harnesses (or a similar one) if you have not established a new one.

# References

-   BUGS
    -   included in every binary and source distribution
-   <https://sourceforge.net/tracker/?group_id=105292&atid=640802>
-   $BRLCAD_SRC/src/libbu/tests
-   $BRLCAD_SRC/src/libbn/tests
-   $BRLCAD_SRC/src/librt/tests
-   $BRLCAD_SRC/src/libanalyze/tests
-   $BRLCAD_SRC/src/fb/tests
-   $BRLCAD_SRC/src/libcv/tests
-   $BRLCAD_SRC/regress

# Requirements

-   Proficiency with debugging methods
    -   printf does not count!
-   Familiarity with a debugger