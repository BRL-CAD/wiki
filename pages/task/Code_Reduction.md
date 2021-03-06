BRL-CAD is a large code base with more than a million lines of code
across hundreds of binaries and dozens of libraries. Improving
maintainability is an active requirement which includes identifying code
duplication and refactoring accordingly.

This project entails identifying common patterns of duplication
throughout the code (there are tools that can help automate this). Once
identified, the code can be carefully refactored into new routines,
common functionality, library code, etc.

Testing is required to make sure refactoring was correct and
functionality was not changed. Test-driven development would be helpful
here.

# References

-   run the sh/enumerate.sh script to see current line count statistics
-   <http://en.wikipedia.org/wiki/Duplicate_code>
-   <http://www.harukizaemon.com/simian/index.html>
-   <http://checkstyle.sourceforge.net/config_duplicates.html>

# Requirements

-   Ability to write regression tests
-   Ability to refactor C/C++

# Past Efforts

-   [GSOC12](../user/Ksuzee/Reports.md)

# See also

-   [Code Cleanup](../doc/Code_Cleanup.md)
