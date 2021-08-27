While there is existing ANSI C/C++ code for
[Brep](wikipedia:Boundary_representation.md) in BRL-CAD it is
not GPU parallel. Porting it to the GPU with OpenCL should be rather
complex because much of this code is written in object oriented C++.

So the first task you should make to start an OpenCL port of this is to
make a simplified version of the code which uses just ANSI C.
Alternatively you can also look into incorporating SYCL for the Brep
code. SYCL is a GPU parallel language based on C++ which should be
possible to interface with OpenCL.

-   <https://www.khronos.org/sycl/>
