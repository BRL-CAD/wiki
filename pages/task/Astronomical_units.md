BRL-CAD internally converts all units to a base unit representation
(millimeters) in order for calculations to be robust and devoid of
scaling effects, aliasing, and other floating point representation
issues. With [double-precision floating
point](http://en.wikipedia.org/wiki/Double_precision_floating-point_format),
we can already readily create objects within our observable universe
(about 10^29) to scale but there is untested support for astronomical
units and lots of room for there to be computational issues.

This task involves performing a comprehensive review of BRL-CAD's
support for astronomical units, making sure that everything works as
expected, and fixing anything that isn't working correctly. You'll need
to be familiar with the basics of modeling with BRL-CAD so you can
create representative objects at difference reference scales.

BRL-CAD provides more than a dozen different primitive shapes that are
used to construct more complex shapes. As each primitive type has its
own mathematics specific to solving equations of intersection, all
primitives will need to be individually tested at different scales.

# References

-   src/libbu/units.c
-   src/librt/primitives

# Requirements

-   Familiarity with C
-   Basic familiarity modeling with BRL-CAD