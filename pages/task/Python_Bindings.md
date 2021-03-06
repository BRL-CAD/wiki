While it would be possible to do this using SWIG, python-brlcad is an
already on-going effort to wrap BRL-CAD functionality in python/ctypes
via ctypesgen to allow for easier scripting (see References).

The project is in its early development stage, the source code allows
for now the scripting (read/modify/write) of only a selected set of
primitives using libwdb.

The goal of this GSOC task is to wrap the libged BRL-CAD library to
match the geometry editing capabilities of mged directly from the python
command line.

# References

-   <https://github.com/kanzure/python-brlcad>
-   <https://github.com/nmz787/python-brlcad-tcl>
-   brlcad: src/libged

# Requirements

-   Strong familiarity with both C and python