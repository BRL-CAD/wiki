# Appleseed Integration Project

Integration with appleseed (https://github.com/appleseedhq/appleseed)
has been a long-standing BRL-CAD project. In essence, the idea is to
render BRL-CAD geometry through a custom plugin to the appleseed
renderer. The ultimate goal of the project is to be able to support as
many rt features as possible.

## Progress

The appleseed integration project takes advantage of appleseed's support
for procedural objects, which allows for the creation of a custom plugin
to execute custom ray-intersect logic. By linking with librt, the plugin
is thus able to render BRL-CAD geometry. Aside from simply being able to
render the geometry, art.exe currently supports a few select rt
features. At the moment, art.exe is capable of:

-   selecting the geometry model and the regions to render
-   defining the render image pixel dimensions
-   setting the azimuth/elevation and perspective angle

As mentioned, the goal of the project is for art.exe to implement the
same features as rt.exe, so that, in a sense, they can be used
interchangeably. Therefore, if possible, it would be preferred if art
could reuse the same helper functions and variables used by rt. For
example, much of the command-line option parsing performed by art
directly comes from opt.c/usage.cpp, which was originally used by rt.
This makes the code much cleaner and easier to maintain.

## To-Do

### Separating Regions

-   The custom BRL-CAD plugin currently combines all the BRL-CAD regions
    into a single object. While this works to some extent, it would be
    more ideal to separate each region into a separate object. This
    would make other features, such as assigning region-specific colors,
    much easier to implement.

### Colors/Materials

-   Right now, the entire BRL-CAD object is rendered by appleseed as a
    single hard-coded color. However, BRL-CAD geometry supports the use
    of different colors and materials for individual primitives/regions.
    After the custom plugin has been updated to separate BRL-CAD
    regions, implementing colors/materials would be a relatively
    high-priority feature.

### Using Existing Functions

-   Although art supports setting azimuth/elevation, the current
    implementation was done as a bit of a hack; the function used to
    perform relevant calculations, do_ae(), was copied from the do.c
    file. It would be much preferred to directly use the function from
    do.c, but including do.c into the project also creates a lot of
    unresolved external symbol errors. This should be resolved soon.

### Multithreading Support

-   Both appleseed and librt are capable of multithreaded rendering, but
    at the moment, the plugin will only work on a single thread. At some
    point, multithreading support should be implemented in order to
    fully take advantage of appleseed/librt capabilities.

### Refining CMake

-   Setting up the appleseed project requires a lot of hacky and manual
    work. Once the project has progressed further, the CMake should be
    updated to make this process easier for all platforms.