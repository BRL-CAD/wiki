BRL-CAD has support for dozens of different 3D geometry file formats. We
do not, however, have an importer for the X3D geometry format.

Your project involves implementing import support for the X3D file
format as robustly and comprehensively as possible. There are several
potential 3rd party libraries that can be used or (not recommended, but
acceptable) you can write your own parser library. You'll minimally need
to implement import support for all geometry entities including
polygonal and NURBS geometries, any hierarchical information, material
properties, and (time permitting) faithful round-tripping (import and
export).

Difficulty: Easy

Languages: C/C++