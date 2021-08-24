# Project (End term) Summary

## Introduction

This project aimed to wrap BRL-CAD's primitives in python. The
python-bindings allows for easy and simple access to the BRL-CAD APIs
for geometry construction and manipulation. One of the wonderful project
which illustrates the power of Python-BRLCAD can be found at
<https://github.com/ncsaba/returnboard>

I started my work with Python-BRLCAD as Google Summer of Code student.
To know more about GSoC please visit
<http://www.google-melange.com/gsoc/homepage/google/gsoc2014>

## Tasks Accomplished

-   I have implemented the primitives for python-brlcad.
-   Also I have wrapped Open Nurbs library to be used in Python by using
    pybindgen.

## Tasks Remaining

-   Binuif is not implemented as a primitive.
-   Constraints api is not mature thus not implemented.

## Important Links

-   Python-BRLCAD git repository
    <https://github.com/raj12lnm/python-brlcad>
-   OpenNurbs-Python git repository
    <https://github.com/raj12lnm/OpenNurbs-Python>
-   Dev Logs are [here](User:Krajkreddy/GSOC14/summary "wikilink")

## Way forward

-   Python-BRLCAD now contains most brlcad primitives. With the
    availability of OpenNurbs library wrapped in python now we have the
    resources to even extend the support for brep in python-brlcad.