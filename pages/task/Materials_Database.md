BRL-CAD uses simple material properties, presently limited to density,
for calculating weights, moments of inertia and other geometric
analyses. There is presently no centralized repository for specifying
material properties, so users have to recreate and manually share
inputs.

This website would provide a comprehensive means for specifying,
storing, importing, export, and reusing material properties. If you're
interested in this web development idea, there is prior proof-of-concept
web work of relevance that can be built upon or you could start from
scratch. The latter approach from scratch would be somewhat discouraged
unless your implementation idea was vastly different and better.

# References

-   rtweight
    -   binary that calculates weight of a BRL-CAD geometry model
-   .density
    -   default input file used by rtweight, see BRL-CAD man page for
        rtweight for the format

We have a preliminary material database dataset with all of the fields
we're interested in (name, density, young's modulus, equivalence
factors, etc).

# Requirements

-   Ability to run shell scripts
-   Ability to navigate a UNIX/Linux command-prompt
-   Familiarity with web development technologies