Compiling against any of BRL-CAD's 20+ libraries is generally quite
straight forward. Say you have a simple C++ source file named `test.cpp`
using LIBBU, BRL-CAD's basic utility library:

<code>

    #include "bu.h"
    #include <iostream>

    int
    main(int ac, char *av[]) {
        bu_setprogname(av[0]);
        std::cout << "Program name is " << bu_getprogname() << std::endl;
        return 0;
    }

</code>

Building software involves compiling source code, linking objects, and
running our application. No matter what compiler or operating system you
use, there are options for all three of those:

-   To *compile*, you need to specify paths to headers (so the \#include
    lines work).
    -   For gcc/clang, this is usually -I options.
-   To *link*, you need to specify paths and libraries to link (so it
    can find functions).
    -   For gcc/clang, this is usually -L options and -l options.
-   To *run*, you need to specify run paths to libraries (so it can use
    functions).
    -   For gcc/clang, this is usually an -rpath linker option.

So say we put that `test.cpp` file in \~/brlcad and have BRL-CAD
compiled at \~/brlcad/.build but not installed. (You don't need to
install to use any library -- you just need to know where to find
headers and libs!) After changing directory to \~/brlcad, we can
compile, link, and run our little test program:

<code>

    c++ -c -Iinclude -I.build/include test.cpp
    c++ test.o -L.build/lib -Wl,-rpath -Wl,.build/lib -lbu
    ./a.out

</code>

Woot! If you didn't confuse l with 1, put the wrong path, or mix
something else up, you should see:

<code>

`Program name is a.out`

</code>

And that's essentially all there is to it! We can even simplify the
entire process into one compile+link command if we are careful enough to
make sure include flags come *before* source files and linker flags come
*after* the source files in the right order:

<code>

`c++ -Iinclude -I.build/include `**`test.cpp`**` -L.build/lib -Wl,-rpath -Wl,.build/lib -lbu`

</code>

From there, we set up to use any function in LIBBU. If we want to link
against another library like LIBRT or LIBGED, we already have the right
paths so we'd simply add -lrt or -lged respectively to the link line. To
find functions, we can browse around the headers and subdirs in the
include directory as nearly every public function is documented in
detail there with comments, often with code snippet examples too.

If we already installed BRL-CAD into /opt/brlcad and want to use all
headers and all the core libraries, the process remains the same.
Specify paths to headers, source file(s), paths to libs, and then the
libs need:

<code>

`c++ -I/opt/brlcad/include -I/opt/brlcad/include/brlcad -I/opt/brlcad/include/openNURBS `**`test.cpp`**` -L/opt/brlcad/lib -Wl,-rpath -Wl,/opt/brlcad/lib -lged -lrt -lbn -lbu`

</code>

Happy coding!