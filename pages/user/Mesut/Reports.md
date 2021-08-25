# Report Week 6

The cmake errors has solved by adding UNKNOWN and IMPORTED files in
cmake files.
I have added dm-qt.c in libdm and mged, dm-qt.h in include. dm-qt.c in
libdm contains the empty functions for the display manager. The dm-qt.c
file in mged connects the display manager with mged. In CMakeLists.txt
(root/libdm/mged) I have added a option for qt and included the added
files for compiling. In dm.h, dm-generic.c and attach.c i have added
macros for dm-qt. BRL-CAD will compile with Strict=off.

Now it is possible to attach a new dm with the command:

``` dos
attach qt
```

After attaching a qt window I have gotten a memory leak. Through
implementing the Qm_dm_init() function the problem get solved and
attaching will cause no error and nothing happens.



# Report Week 5

I have used the functions in dm_X.c and deleted all function bodies and
renamed them to qt_function. In dm-generic.c I have changed X_open to
qt_open for testing. I have to implement a cmake macro for qt, add it
to dm-generic.c and remove X_ changes.

After that I have tried to built BRLCAD. Through Warnings I couldn't
compile it. So I have changed to Un-Strict Mode in cmake and
successfully compiled libdm.

In the next step I have tried to link Qt with BRLCAD. After I added only
find_package in CMakeLists.txt I have gotten following error:

``` dos
CMake Error at CMakeLists.txt:456 (_message):
  Attempting to ignore non-existent file UNKNOWN, in directory
  /home/kane/Development/brlcad/src/libdm
Call Stack (most recent call first):
  misc/CMake/BRLCAD_CMakeFiles.cmake:128 (message)
  CMakeLists.txt:375 (CMAKEFILES)
  /usr/share/cmake-2.8/Modules/FindQt4.cmake:374 (ADD_LIBRARY)
  /usr/share/cmake-2.8/Modules/FindQt4.cmake:906 (_QT4_ADJUST_LIB_VARS)
  src/libdm/CMakeLists.txt:16 (FIND_PACKAGE)
```



The CMake file with definition:

``` dos
# Qt library
FIND_PACKAGE(Qt4)
if(QT4_INSTALLED)
  option(BRLCAD_ENABLE_QT "Use QT." OFF)
endif

if(BRLCAD_ENABLE_QT)
  CONFIG_H_APPEND(BRLCAD "#define HAVE_QT 1\n")
  # Qt library include
  include(${QT_INCLUDES})
  include(${QT_USE_FILE})
  add_definitions(${QT_DEFINITIONS})

  # Qt link used libraries, core and gui is linked by default
  #target_link_libraries(core ${QT_LIBRARIES})
  #target_link_libraries(gui ${QT_LIBRARIES})
endif
```



= Report Week 4 = I have tested many approaches for the Display Manager
and tried to change the default Qt Application structure to encapsulate
it in the qt_open() function. So every Qt display manager will work as
a own application.

The main goal is to get a working structure of the C++ Display Manager
Class with the dm Structure in "dm.h".




= Report Week 3 = I started with the structure of the Qt Display
Manager. I have realized, that it is not possible to use the OO approach
directly. The function pointers in the structure "dm" can't be used for
pointing on member functions (methods).
So I decided to encapsulate a drawing class and instantiate it as a
global variable in the qt_dm.cpp. The functions are used as interfaces
to this class.



# Report Week 2

I have built BRL-CAD successfully on Linux and Windows.
I have released two Patches in this week:

- Refactor and manage libbn tolerance uses by providing an interface
default (e.g., an init macro) and making everyone use that where it is
hardcoded to 0.0005 presently.

-I have added a relative float check (following to:
<http://randomascii.wordpress.com/2012/02/25/comparing-floating-point-numbers-2012-edition/>)
and fixed some FIXME section with it. I am not certain about it. If the
algorithm is suitable for brlcad, i could change the rest of vmath.h.

On both I am waiting for Feedback.

# Report Week 1

I have built BRL-CAD from svn on ubuntu (12.04).
I have installed and built all depencies on Windows, but I get following
build errors (only a few of them, the errors repeating):

``` dos
On libpoints-static:
448>points_scan.l(130): error C2065: 'PLATE': not declared
448>points_scan.l(145): error C2065: 'SYMMETRY':  not declared
448>points_scan.l(160): error C2065: 'CYLINDER':  not declared
```

Same on: libpoints \[…\]

scriptsort:

``` dos
cl: Command line error D8021: invalid numeric argument / Wno-error.
```

intro-to-tcltk_presentation_html, Konfiguration; imod: no error or
warning message
All projects with libged depencies, even though libged-static build is
successful:

``` dos
590> LINK: fatal error LNK1104: File ".. \ .. \ debug \ lib \ libged.lib" can not be opened.
```

All projects with libtclcad depencies, even though libtclcad -static
build is successful:

``` dos
614> LINK: fatal error LNK1104: File ".. \ .. \ debug \ lib \ libtclcad.lib" can not be opened.
```


Mged_tclindex:

``` dos
618> Generating .. / ../../Debug/share/brlcad/7.21.0/tclscripts/pl-dm/pkgIndex.tcl
618> The command ".. \ .. \ bin \ .. \ debug \ btclsh.exe" is either misspelled or
618> could not be found.
618> C: \ Program Files (x86) \ MSBuild \ Microsoft.Cpp \ v4.0 \Microsoft.CppCommon.targets (151.5): error MSB6006: "cmd.exe" exited with code 9009.
[…]
--> 851 successful and 74 errors"
```