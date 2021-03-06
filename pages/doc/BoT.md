The “Bag o’ Triangles” (BoT) is a BRL-CAD primitive object used for
representing triangle mesh objects. BoT objects may be surfaces or
solids; topologically closed or open; clockwise, counter-clockwise, or
unoriented; and with an optional global or per-face thickness for
surfaces depending on the BoT mesh type.

# Determining the mode of a BoT

Reading the 'mode' parameter in MGED will report the BoT mesh type:

`mged> get YOUR_BOT_NAME mode`
`volume`
`mged> get YOUR_BOT_NAME orient`
`rh`

That example shows that "YOUR_BOT_NAME" is a volume mode bot that has
a right-hand (counter-clockwise) face orientation.

# BoT types

There are four primary BoT mesh modes implemented in BRL-CAD:

1.  **“surf” is a surface-only object with no volume information.**

    Rays hitting a surf object should return a hit with a
    zero-thickness. Our obj, ply, and dxf importers presently create
    BoTs marked as this type.

2.  **“volume” is an explicit solid object that is topologically closed
    and should enclose some non-zero volume of space.**

    Our proe export plugin; the stl, intaval, fastgen, and enf
    importers; and the make, inside, E, and facetize commands create
    BoTs marked as this type.

3.  **“plate” is an implicit solid object defined by a surface (which
    may or may not be topologically closed) and a specified thickness
    (similar to extrude).**

    There can be e either a global thickness or a per-face thickness.
    The thickness is specified to either be centered about the surface
    (1/2 + 1/2 thickness) or a bidirectional extrusion distance (1 + 1
    thickness). The shotliner mimics FASTGEN’s raytrace behavior when
    encountering this type of BoT object. Our fastgen and intaval
    converters create BoTs marked as this type.

4.  **“plate_nocos” is a plate mode specialization that is identical in
    all respects except that shotlining ignores the obliquity angle.**

    This means that rays hitting this type of BoT return a segment
    distance equal to the BoT’s thickness regardless of the angle of
    intersection. None of our tools directly generate this object
    type.


The first three modes are exactly what one would expect in order to
represent the variety of triangle meshes that are commonly created by
other CAD systems. The last mode, mode \#4 (plate_nocose), is obviously
a peculiar curiosity and prime for removal (in my opinion), but was
undoubtedly added for some analysis customization. Some investigative
research would have to be performed if we decide to deprecate this mode
type (if you’re someone using this mode type, please speak up).

There’s also obviously not much difference between a \#1 (surf) and a
\#3 (plate) with a zero thickness except the following: a) plates are
defined as implicitly solid (by definition), b) surfaces are not solid
(by definition), and c) there are a variety of plate mode raytrace
behaviors implemented specifically to mimic FASTGEN behavior.

# BoT Advantages over STL

There are three primary advantages to using BoTs in BRL-CAD instead of
STL:

1.  **STL only supports one object per file.**

    This can be worked around (by managing multiple files), but BRL-CAD
    inherently supports an arbitrary number of objects per file that can
    be easily grouped together as needed ensuring that common components
    stay grouped together.

2.  **STL equivalently only implements surfaces (what we call "surf"
    mode) with no regard to topology, connectivity, or closure.**

    You can write code to assume the geometry is well connected and/or
    encloses a volume and that a ray that enters a face will exit some
    other face(s), but nothing in the format requires it. This can
    impact analysis validity and verifiability. Our “volume” mode BoTs
    are specifically tailored for analysis purposes, requiring that the
    mesh be topologically connectable and closed.

3.  **STL only supports single-precision floating point.**

    We support both single- and double-precision in BRL-CAD, defaulting
    to double-precision for supporting detailed models more accurately.
    This can also impact analysis validity, particularly for highly
    complex models, where error can accumulate and compound more rapidly
    with single-precision data. Double-precision does necessarily use
    more memory, twice as much, but doesn't generally have a meaningful
    performance impact.


STL is definitely in wider use but only because it is basically a lowest
common denominator “dumb” format with no structure. Going from most any
format to STL is almost always a lossy conversion.