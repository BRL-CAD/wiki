# Compiling BRL-CAD

This page contains simplified steps for building ***quickly***.

## Install Dev Tools

*If you downloaded the virtual machine disk image, skip this step.*

BRL-CAD uses the CMake build system and may be built with most
compilers, so first step is to [download and install
CMake](http://www.cmake.org/cmake/resources/software.html). If needed,
compiling from their source distribution is actually very easy.

-   Debian/Ubuntu:
        aptitude install build-essential make cmake

<!-- -->

-   Fedora:
        yum install clang++ make cmake

<!-- -->

-   CentOS:
        yum install python3-pip devtoolset-9 ; pip3 install cmake ; scl enable devtoolset-9 bash

## Install Dependencies

*If you downloaded the virtual machine disk image, skip this step.*

If you're on a Mac or Windows, you're good to go. For Linux, BSD, and
other package-managed systems, you'll want to install a few things.

-   Debian/Ubuntu:
    -   aptitude install sed byacc flex xsltproc

    -   aptitude install libncursesw5-dev libfontconfig-dev

    -   aptitude install xserver-xorg-dev

    -   aptitude install libx11-dev libxi-dev

<!-- -->

-   Fedora:
        yum install libx11-devel

## Download BRL-CAD

*If you downloaded the virtual machine disk image, run this to make sure
you have the latest sources:*

    svn up brlcad-svn-trunk

For everyone else, we recommend obtaining the latest sources from our
repository:

    svn checkout svn://svn.code.sf.net/p/brlcad/code/brlcad/trunk brlcad-svn-trunk

If you run into trouble, snapshot release sources may also be obtained
from
[Sourceforge](https://sourceforge.net/projects/brlcad/files/BRL-CAD%20Source/).

## Configure your Build

Next, set up a build directory and configure your compilation:

    cd brlcad-svn-trunk
    mkdir build
    cd build
    cmake .. -DBRLCAD_ENABLE_STRICT=NO -DBRLCAD_BUNDLED_LIBS=ON -DCMAKE_BUILD_TYPE=Release

By default, our build enforces code standards that will halt on trivial
issues, so we recommend turning off that strict behavior for your first
compile. By default, it will also search your system for dependencies,
but this can be complicated so we tell the build to use our bundled
versions. When you graduate to doing development, you'll want to change
the build type to -DCMAKE_BUILD_TYPE=Debug instead of Release.

On a Raspberry Pi running Raspbian 10 also the option
-DBRLCAD_ENABLE_COMPILER_WARNINGS=NO is needed for the build to
complete.

BRL-CAD source files contain an
[INSTALL](http://brlcad.svn.sourceforge.net/viewvc/brlcad/brlcad/trunk/INSTALL)
file with more detailed instructions if you want to customize the build.

## Compile

You're good to go, now it's time to compile:

    make

Compilation can take anywhere from a couple minutes to an hour depending
on your hardware. If you had a quad-core CPU, you might run '"make -j4"
to request compiling in parallel.

If the build fails, re-run make while capturing all output to a log:
make &gt; build.log 2&gt;&1 Please report any build failures.

## Run!

You don't have to install to run BRL-CAD. You can just run the binaries
you just finished compiling. They are in the brlcad/.build/bin
directory. There are 400+ tools in BRL-CAD. Here's a couple to get
started:

    bin/benchmark run
    bin/mged
    bin/archer

The first command will evaluate your system performance. If you made a
Release build, please submit your benchmark results to benchmark at
brlcad dot org.

The second command runs the main graphical interface. Be sure to check
out the extensive [Documentation](Documentation.md) and
[Main_Page](Main_page.md) for tutorials.

The third runs our newer graphical interface that is under development.

## What now?

Help make BRL-CAD better! There are many ways you can contribute to open
source and you don't need to be an experienced programmer. We do need
software developers, but we also need artists, writers, designers, and
managers.

See [Deuces](../task/Deuces.md) for really easy ways to get started!
