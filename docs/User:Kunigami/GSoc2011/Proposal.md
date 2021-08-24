## Project description

### Project Title

Shader Enhancements

### Brief project summary

Shaders in BRL-CAD are implemented using C language. Recently Sony
released its shading language as open source, now called OSL. This is a
C-like language that works like a framework to write shaders. It was
specially developed to work with raytracers, which is also the
application of BRL-CAD shaders. To this end, an idea is to implement
BRL-CAD shaders using OSL. In this proposal I provide a brief
description of BRL-CAD shader system and OSL specification. Then I
describe a top-level approach to accomplish this task.

### Detailed project description

#### Introduction

I've little (if none) experience with shaders, but I really want to
learn about them and this project is an opportunity to both learn and
contribute to open source. To this end, I'm declaring this project to
have the greatest priority among the others I'm applying. In the past
weeks, I've been researching BRL-CAD code and OSL to better understand
how shaders sytems work. I can now devise how BRL-CAD could benefit in
using OSL language to implement their shaders.

#### BRL-CAD Shader System

A shader is implemented at liboptical with the name sh_<shader name>.c.
It may have several particular functions, but one of them is always
required and is named <shader name>_render. It returns the color of the
light that will be seen when a ray shot by the raytracer hits the
surface of an object using this shader. In general, shaders models
properties like color, transparency, reflection and diffraction. The
default shader of an object is the plastic texture, modeled by the phong
shader. There are several other types of material such as cloud, wood,
fire, etc. Lights in BRL-CAD are treated as a special type of shader
that emits light \[5\].

BRL-CAD shaders are currently written in plain C. They're mainly used by
the raytracer system, both in the stand-alone rt application or through
mged application using librt. Shaders are compiled as shared libraries
and are loaded dynamically at runtime.

#### OSL

Recently Sony opened the code of their shader language \[3\]. Chatting
at IRC and from the project description, it's clear that this language
is to be carefully analyzed in order to benefit BRL-CAD shader system,
specially because it is developed for raytracers, which is the same use
BRL-CAD current system has. OSL is a C-like language that can be used to
write shaders.

One can write individual shaders using OSL and integrate them afterwards
using shaders groups. These groups are basically a network (more
specifically, a directed acyclic graph, also known as DAG) of individual
shaders, called layers, and they're connected like UNIX pipes: the
output of one is the input of the other. Using OSL, setting up this
network is simple as coding the individual shaders and defining a set of
pairs of (ouput shader, input shader). This is like the stacking of
shaders present in BRL-CAD.

In general, the output of a shader is not a final color but instead it's
a structure called closure. It stores parametrized formulas that would
be used to evaluate the final color but the variables are maintained.
This has several advantages such as:

We can recompute colors more quickly when there are changes only in the
lights We can compute the final color for given only a direction. Given
an input and output direction, it's possible to get the amount of light
propagated from the input to the output. The last two items are quite
interesting for raytracers.

### Proposal Idea

The OSL represents a interesting framework to develop shaders. BRL-CAD
shaders could benefit from it by improving performance with the concept
of closures. Also, we could take advantage of already implemented
shaders for OSL and when developing new shaders for BRL-CAD we would be
contributing to OSL database, which is, according to \[6\] (may be
outdated) quite sparse.

There are some issues to solve first. In the OSL specification document
from January 2010, it's said that some components are assumed to exist
in order to implement shaders using OSL. One of them is the integrator,
which combines the color closure, lights and view-dependent variables.
They say in the future they would provide a way to implement them
through OSL, though I'm not sure what is the current state. If not, it
would need to be included in the project.

Here is how I plan to execute this project: study the details of BRL-CAD
and OSL shader. This includes implementing shaders for these systems as
well a simple integration test, which can be done using the single ray
shooter from BRL-CAD with no optics or shaders and plugging in the OSL
shader. This will assess the feasibility of the project as well as
provide an idea on which changes are necessary to adapt OSL shaders. So,
we'll be able to design and implement these changes to the BRL-CAD
shader system.

Reuse shaders that are already implemented with OSL and that fits the
current shaders of BRL-CAD. Then, implement possibly missing shaders.
After implementing/porting the first shader, we must check consistency
of the new shader system, testing if it works well with the raytracers.
Also, after each shader is added, we need to check if the result is
similar to the replaced one. Extra tasks that can be done, if time
allows it, is to implement new shaders with this language and/or write a
small tutorial on how to implement shaders using OSL.

### Timeline

-   Community Bonding (4 weeks)
    -   Compile OSL \[ok\]
    -   Discover how testrender application works \[ok\]
    -   Implement and compile a shader using OSL \[ok\]
    -   Test the shader with testrender \[ok\]

<!-- -->

-   Week 1 (May 23th to May 30th)
    -   Implement a sample texture/material shader (polka-dot texture)
        for BRL-CAD \[ok\]
    -   Test it by assigning it to an object and rendering it. \[ok\]

<!-- -->

-   Week 2-6 (May 30th to Jul 4th)
    -   Implement a special shader for BRL-CAD that will be an interface
        for OSL system \[ok\]
    -   Integrate a shader implemented in OSL and this interface \[ok\]

<!-- -->

-   Week 7-8 (Jul 4th to Jul 18th)
    -   Implement some BRL-CAD shaders as OSL shaders
        -   Mirror
        -   Glass
        -   Cloud
        -   Checker
    -   Check if any additional changes in the system is necessary to
        render the new shaders

<!-- -->

-   Week 9-12 (Jul 18th to Aug 15th)
    -   Resolve the multi-threading issue
    -   Extra: implement a mode in rt so the framebuffer updates the
        screen at every sample
    -   Extra: write a tutorial

### References

1.  src/liboptical/init.c
2.  src/liboptical/material.c
3.  <http://opensource.imageworks.com/?p=osl>
4.  <http://code.google.com/p/openshadinglanguage/wiki/OSL_Introduction>
5.  <http://brlcad.org/w/images/2/2c/Optical_Shaders.pdf>
6.  <http://code.google.com/p/openshadinglanguage/wiki/GSoC>