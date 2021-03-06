BRL-CAD and Doxygen

Doxygen (http://www.stack.nl/\~dimitri/doxygen/) is a tool for
generating documentation from source code comments in C and C++ sources,
which works automatically so long as certain formatting conventions are
respected. In order to generate diagrams, users should also install the
Graphviz (http://www.graphviz.org/) graph visualization software.

Once the necessary tools are installed on your computer, BRL-CAD's CMake
build will detect them and enable compilation targets to generate HTML
output:

make dox - this is the toplevel Doxygen target, and the preferred way to
generate the documentation. It works on all the libraries
simultaneously, which makes for the best quality documentation but may
also take longer to generate output.

To view the output generated from this command, open it in firefox or
some other web browser:

firefox doc/doxygen_output/html/index.html

make dox-&lt;lib\*\*&gt; - per library doxygen targets that build
documentation only for a single library (libbu, librt, etc.)

The per-library outputs will be in their own directories:

firefox doc/doxygen_libbu/html/index.html

## Editing Doxygen

For examples of how to format Doxygen comments in source code, study the
libbu headers - these are the most mature of BRL-CAD's libraries when it
comes to doxygen formatting.

The hierarchical structure of the comments is not controlled by comments
in the headers themselves, but in special purpose files located in
BRL-CAD's misc/doxygen directory. Each library has a lib\*\*.dox file
within which it's hierarchy is defined. libbu.dox is a good example of a
mature file of this type - as of this writing (early 2015) most of the
libraries do not have a mature hierarchy defined.

To properly organize the documentation for a library, the first step is
to populate its lib\*\*.dox file. Once that file is ready, appropriate
markup is added to the header contents to properly categorize content.