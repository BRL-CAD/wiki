Here I provide a small tutorial do make OSL running while it is not
included in BRL-CAD source code.

# Installing

## Installing OSL Dependencies

### OIIO

#### Get the latest OIIO source code

`cd /home/dude/dev`

`mkdir oiio`

`cd oiio`

`git clone https://github.com/OpenImageIO/oiio.git .`

Note: Change `/home/dude/dev/` by the desired install place.

#### Install (locally)

`make`

Note1: Some dependecies are required such as Ilmbase, OpenEXR, libpng
(please, edit this entry with any additional package you had to install)

Note2: Make sure your libpng version is 1.4 (for BRL-CAD compatibility)

### OSL

#### Get the latest OSL source code

`cd /home/dude/dev`

`mkdir osl`

`cd osl`

`git clone https://github.com/imageworks/OpenShadingLanguage.git .`

#### Set OIIO path

`export OPENIMAGEIOHOME=/home/dude/dev/oiio/dist/macosx/`

Note1: Depending on your OS, macosx may be linux, linux64, etc.

#### Remove -Werror compilation flags

Open the osl/src/CMakeLists.txt file and change lines

` set ( CMAKE_C_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Werror")`
` set ( CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Werror" )`

by

` set ( CMAKE_C_FLAGS "${CMAKE_CXX_FLAGS} -Wall")`
` set ( CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall" )`

#### Edit llvm search path

Cmake was not able to find llvm installed on my system. I had to make
the following edit. Open the osl/src/cmake/externalpackages.cmake

Change:

` find_library ( LLVM_LIBRARY`
` NAMES LLVM-2.7 LLVM-2.8svn LLVM-2.8 LLVM-2.9svn`
` PATHS /usr/local/lib /opt/local/lib )`
` find_path ( LLVM_INCLUDES llvm/LLVMContext.h`
` PATHS /usr/local/include /opt/local/include`

by

` find_library ( LLVM_LIBRARY`
` NAMES LLVM-2.7 LLVM-2.8svn LLVM-2.8 LLVM-2.9svn`
` PATHS /usr/local/lib /opt/local/lib /usr/lib/llvm/lib )`
` find_path ( LLVM_INCLUDES llvm/LLVMContext.h`
` PATHS /usr/local/include /opt/local/include /usr/include`

#### Install locally

`make`

## Installing BRL-CAD with OSL mode on

#### Get BRL-CAD

`cd /home/dude/dev`

`mkdir brlcad`

`cd brlcad`

`svn co https://brlcad.svn.sourceforge.net/svnroot/brlcad/brlcad/trunk/ brlcad`

#### Set OSL path

`export OSLHOME=/home/dude/dev/osl/dist/macosx/`

Note1: Depending on your OS, macosx may be linux, linux64, etc.

#### Install locally

I use the following to set up to install BRL-CAD:

`cd /home/dude/dev`

`mkdir brlcad-build`

`mkdir brlcad-bin`

`cd brlcad-build`

`cmake ../brlcad -DBRLCAD-ENABLE_COMPILER_WARNINGS=OFF -DBRLCAD-ENABLE_ALL_LOCAL_LIBS=ON -DBRLCAD-ENABLE_OSL=ON -DCMAKE_INSTALL_PREFIX=/home/dude/dev/brlcad-bin/ -DBRLCAD-ENABLE_STRICT=OFF`

I hope it's enough to have the code compiling. Please, edit this entry
with any additional step you needed to perform in order to get it
working

# Running an example

## Compiling some shaders

Use the OSL compiler, oslc, to convert .osl shaders to .oso. Compile all
shaders in brlcad/src/other/osl/shaders. For example

`cd /home/dude/dev/osl/dist/macosx/bin`

`./oslc glass.osl`

It will generate a `glass.oso`. Copy it to the directory of binaries of
BRL-CAD

`cp glass.oso /home/dude/dev/brlcad-bin/bin`

Also, copy the scene I've been using to perform tests

`cp /home/dude/dev/brlcad/db/cornell-kunigami.g /home/dude/dev/brlcad-bin/bin`

Run with the following script:

` #!/bin/sh`
` ./rt -M -p55 -P1 -R -H 1000 -J3 -o output.png \`
`  $*\`
`  cornell-kunigami.g\`
`  'all.g' \`
`  <<EOF`
` viewsize 6.000000000000000e+03;`
` orientation 0.000000000000000e+00 9.961946980917455e-01 8.715574274765824e-02  0.000000000000000e+00;`
` eye_pt 2.780000000000000e+02 3.709445330007912e+02 -4.544232590366239e+02;`
` start 0; clean;`
` end;`
` EOF`