One of the fundamental requirements of a production modeling pipeline
involves being able to ensure a given 3D model does not have any errors
such as overlapping objects or incorrect mass. The way this is currently
tested in BRL-CAD is by running geometry analysis tools such as
"rtweight" and "gqa" on the models. While they work, these tools have
known deficiencies.

The goal of this project is to research an improved Monte Carlo approach
based on quasi-random spherical sampling and implement a new tool that
will converge on a better answer in less time.

Using the C/C++ open source BRL-CAD ray tracing library, the program
needs to evaluate target geometry estimates for surface area,
volume/mass, and overlaps. Prior 3D modeling experience is not required.
This project is ideally suited to someone with basic knowledge of C/C++,
data structures, and trigonometry.