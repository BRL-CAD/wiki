## Converting from STEP files to BRL-CAD databases

BRL-CAD's most pressing need in the geometry file conversion category is
support for the STEP file format, a.k.a "STandard for the Exchange of
Product model data." Step is a successor to the IGES file format and
today is the major standard used for data exchange between CAD systems.

## Partial Support

currently the tool step-g has partial support, and the toolkit
<https://github.com/stepcode/stepcode> is branched into the src/other
source tree.

## Defining ISO Documents

The source standard for STEP is ISO-10303, which consists of hundreds of
individual parts. (list parts important to brlcad)

## Existing Open Source Tools

#### Tools that work with EXPRESS (ISO10303 Part 11) schemas

-   [Expresso](http://exp-engine.sourceforge.net/), aka Express Engine,
    written in Lisp
-   [JSDAI](http://www.jsdai.net/), written in java

#### Tools that generate C++ from an EXPRESS schema

-   NIST STEP Class Libraries
    -   There is a [patched
        version](https://github.com/mpictor/StepClassLibrary) of the SCL
        that compiles with GCC 4.6
    -   [Official NIST SCL
        site](http://www.mel.nist.gov/msid/scl/SCL.htm)

<!-- -->

-   ESA and NASA also have some tools (expressik, lightcpp, pyexpress)
    that can generate code from EXPRESS schema. For some years, ESA has
    planned to release some (or all) of the code as open source;
    however, they have many higher priorities (per email with a person
    at ESA).
    -   Relevant google searches:
        -   [iso10303-11 EXPRESS SDAI python generate
            c++](http://www.google.com/search?q=iso10303-11+EXPRESS+SDAI+python+generate+c%2B%2B)
        -   [expressik
            lightcpp](http://www.google.com/search?q=expressik+lightcpp)
    -   [IFC](http://forge.osor.eu/plugins/wiki/index.php?id=175&type=g)
        contains code generated by lightcpp, but **does not include**
        lightcpp. Contains some info on lightcpp.

## BRL-CAD Specific Design Considerations