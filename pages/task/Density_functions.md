BRL-CAD implements material properties through a simple table lookup. An
object can be tagged as being a particular material, which prescribes a
specific homogenous material density throughout that object. That
density is then used for calculating mass and moments of inertia.

This task involves implementing support for material objects that can
describe non-homogenous densities. Material objects can describe
variable densities based on a prescribed parameterization such as
distance to exterior, shotline thickness, distance from medial axis,
some probability distribution function, or other parameterization
mechanism. Material objects should be BRL-CAD database objects that can
be referenced (by name) by other database objects. Density is the main
material property that must be provided, though the framework should
support the addition for other properties such as compressive strength,
hardness, and more in the future.

# References

-   include/raytrace.h
-   include/db5.h
-   src/gtools/gqa.c
-   src/rt/viewweight.c
-   man gqa, man rtweight
-   <http://en.wikipedia.org/wiki/List_of_materials_properties>
-   <http://en.wikipedia.org/wiki/Probability_density_function>
-   <http://en.wikipedia.org/wiki/Probability_mass_function>
-   <http://en.wikipedia.org/wiki/Probability_distribution>

# Requirements

-   Familiarity with C