## Personal Information

Name: Djimeli Konrad Niba

E-mail address: djkonro35@gmail.com

IRC-nick: konrado

### Project priority : 2

## Project Title: STEP Multiple Protocol Parsing

## Abstract

`   Standard for the Exchange of Product model data (STEP)  is an ISO standard for the computer-interpretable representation and exchange of product manufacturing information which can be used to represent 3D objects in Computer-aided design (CAD) and related information. BRL-CAD makes use of the STEPcode project to implement its step-g importer, which is currently adapted to a specific STEP application protocol (AP).Some examples  of commonly  encountered application protocol  includes AP203(Configuration Controlled Design) which defines the geometry, topology, and configuration management data of solid models for mechanical parts and assemblies, AP214(Automotive Design) which had everything an AP203 file includes, but adds colors, layers, geometric dimensioning and tolerance, and design intent, and AP242(Managed Model-based 3D Engineering) which has everything an AP203 and AP214  file includes, but adds updated kinematics support.The goal of the project is to make it possible for STEPcode to generate a parser, which supports multiple  application protocols simultaneously.`

## Detailed description:

### Introduction

`   STEPcode has the ability to generate c++ classes for the various STEP application protocols which are used for parsing STEP files. Developing a step-g parser that would have the ability to parse various STEP files could be achieved by determining the file schema using the FILE_SCHEMA instance within the file header and then switching to appropriate parser but this would not be efficient as there would be so much repeated code generated and it would also lead to an increase in compile and build time of BRL-CAD thus the need for a unified parser.`
`   The ability to support many protocols within one framework is one of the key strengths of STEP. All the protocols are all built on the same set of Integrated Resources, so they all use the same definitions for the same information. For example, AP203 and AP214 use the same definitions for three dimensional geometry, assembly data and basic product information. Therefore making it possible to enable  STEPcode generate a parser, which supports multiple application protocols simultaneously.`

### Developing Merged Express schema

`   The first step in developing an application that works with several application protocols is to construct a merged express schema that covers all of the different entity types that we must work with. This would require a good understanding of the Express data modeling language and the various STEP application protocol schemas to be merged as the merged express schema would be a union of all of the application protocol definitions .`

### Generating reliable C++ classes

`   In generating reliable C++ classes which supports multiple APs simultaneously, we would require some familiarization with how STEPcode presently supports  a single AP.`
`   STEPcode begins by generating C++ classes for each AP from their respective EXPESS definitions using exp2cxx. When an application is linked to this classes a  STEPfile object is created  `
``
``
`     STEPfile( Registry & r, InstMgr & i, const std::string filename = "", bool strict = true );`

The STEPfile constructor instantiates a Registry and InstMgr reference
which is used to initialize entity registry. Thus generating a
dictionary with all entity definition, for validating entities passed to
the program by comparing against those found in the dictionary and thus
returns a valid instance if its definition is found in the dictionary.

`   As we move to multiple APs, we must become more aware of this matching process, and may place some of it under application control. These issues could be avoided by using the combined schemas so that classes are only matched once.`

-   If we intend to create fully conforming datasets for several APs, we
    need more than a common subset of definitions. The conformance
    classes for each AP will probably mandate a number of AP-specific
    relationship objects like the **cc_design_\*** entities of AP203
    or the **applied_\*** entities of AP214.

<!-- -->

-   For this project we would need AP-specific classes for each AP that
    we must support. The physical schema (EXPRESS) of our application
    would be a union of all of the AP definitions. There are two ways to
    produce the classes.
    -   We could manually merge the AP long form or short form schemas
        into one, resolve any conflicts, and then generate classes from
        the merged schema.
    -   An expedient alternative is to generate C++ classes from each
        individual schema into the same directory. If there are
        duplicate entity definitions, the latter source files will
        simply overwrite earlier ones. We must use caution with this
        technique. The APs should not have many structure conflicts,
        since the APs are all based on the same integrated resources,
        but there may be a few.

`   As seen above we would be using the first options for generating C++ classes  for our various application protocols.`
`   `
`   `**`Select`**` types in particular, are prone to variability between  APs. When an AP is converted from short form to long form, selects are trimmed to eliminate types outside the AP scope. In extreme cases, the select contains just one type. Consequently, if you compare several long form schemas, the same select type definition may vary widely between them. For example, consider some definitions from AP203 and AP214.`
``
`       AP203  TYPE unit`
`          TYPE unit = SELECT `
`           (named_unit);`
`          END_TYPE; -- unit`
``
`    AP214  TYPE unit`
`       TYPE unit = SELECT `
`        (derived_unit, named_unit); `
`       END_TYPE; -- 10303-41: measure_schema`
`   An application will have problems if C++ classes are generated from a definition that does not have all of the required types. To avoid this, we would have to generate the classes for these selects from the most inclusive EXPRESS schema available,like the merged schema.`

### Adding support for AP242

`   Updating the unified schema to add support for AP242 needs to be handled with some caution .There some issues to be considered, for example;`

-   The definitions for geometric_tolerance and several related types
    have been changed.

`   The geometric_tolerance magnitude is now a length_measure_with_unit instance. Previously, it was given as the more general measure_with_unit  type. More information on this issues an other related issues can be found in the link below.`
[`http://www.steptools.com/support/stdev_docs/stpcad/update_ap242dis.html`](http://www.steptools.com/support/stdev_docs/stpcad/update_ap242dis.html)
`   `

-   The kinematics model originally introduced in AP214 has been updated
    considerably in AP242. For example

``
`                    ENTITY resulting_path`
`                Changed the supertype from a rep relationship`
`                (motion_link_relationship) to a representation`
`                (link_motion_representation_along_path), so the attributes are`
`                completely different.`
`   More information on this issues an other related issues can be found in the link below`
[`http://www.steptools.com/support/stdev_docs/stpcad/kinematics.html`](http://www.steptools.com/support/stdev_docs/stpcad/kinematics.html)
`An external C++ class may have to  be developed to handle the above issues.`

### Integrating new C++ classes with step-g

`   The next part of this project would be to ensure that step-g converter can         `

reliably make use of the merged classes in carrying out conversion,
giving the ability to support multiple APs using a single parser.

### Documentation and testing

This phase of the project would have to do with mainly testing the
functionality of the step-g converter against the newly developed
parser. Testing would actually have to be carried out after every
modification through out the development process in order to catch and
fix bugs introduced early. It would also incorporate bug fixing within
some existing part of the code, proper code commenting and an update of
the STEP manual.

## Reference

1.  <http://www.cax-if.org>
2.  <http://www.steptools.com/support/stdev_docs/stpcad/>
3.  <http://www.engen.org.au/index_htm_files/STEP_application_hdbk_63006_BF.pdf>
4.  <http://en.wikipedia.org/wiki/ISO_10303-21>

## Previous Related work (patch)

1\. vrml-g converter

`   `[`http://sourceforge.net/p/brlcad/patches/320`](http://sourceforge.net/p/brlcad/patches/320)

2\. g-stl default top level objects conversion

`   `[`http://sourceforge.net/p/brlcad/patches/301/`](http://sourceforge.net/p/brlcad/patches/301/)

## Deliverables

1.  Developing merged schema EXPRESS file for at-least AP214 and AP203
2.  Generating unified C++ classes
3.  Enabling step-g to make use unified parser

## Time-line

### 27 April – 24 May (4 weeks) Community Bonding

`   Initializing communication with mentor. Do more research on project, get setup and ready to begin coding. Learn more about STEP standards and EPRESS data modeling language.`

### 25 May – 11 June (2 weeks)

`   Developing suitable merged EXPRESS file with supports for both AP214 and AP203`

### 12 June – 20 June (1 week)

`   Rework exp2cxx to Generate C++ classes for merged EXPRESS filename`

### 21 June – 29 June (1 week)

`   Documentation, test and cleanup of code. By this time the new parser should be able to read AP214 an  AP203 files using p21read_sdai_MERGED_SCHEMA without errors.`

### 30 June – 3 July (3 days) Mid term evaluation

### 4 July – 4 August (4 weeks)

`   Updating merged file to add support for AP242 and resolving issues involved with this update to ensure C++ classes are properly generated and handled.`

### 5 August – 11 August (1 week)

`    Integrating new C++ parser with step-g.`

### 12 August – 16 August (1 week)

`    Code cleanup and documentation.`

### 17 August – 23 August (1 week)

`    Suggested “pencils down”. Further code cleanup, testing an documentation.`

### 24 August – 28 August (4 days) Final Evaluation

## Time Availability

`   I have no commitment within the Google summer of code period except for my end of semester exams which would run for about two weeks around 24 June– 11 July , but I would make up for the time by putting in more hour before this period guarantying at-least 40 hours a week.`

## About Me

-   2013 – 2014: Freshman Computer Engineering [University Of Buea
    Cameroon](http://www.ubuea.cm)
-   2014 – 2015: Freshman Computer Science and Mathematics [University
    Of Buea Cameroon](http://www.ubuea.cm)

`   My change in department was because of my passion for coding and mathematics and also due to my low interest/motivation for electronics which was a large part of the engineering curriculum. This has given me the time to focus on the thing I am very passionate about and since this is the first year computer science is being offered as a major for the undergraduate level at my university, participating in the Google summer of code would be an encouragement to others who intend to enroll into this department.`
`   I am primarily a c/c++ programmer with special interest in computer graphics, computer networking, multi-threading and artificial intelligence.`

## Why Me

`   I have always had the interest of contributing to open-source and have made some contributions to BRL-CAD like development of a vrml-g converter. Working on the vrml-g converter has given me some experience on what geometry conversion is all about, thus higher chances of success in completing this project. I would also have the opportunity to gain more experience and learn lots of new things.`

## Why STEPcode

`   I choose STEPcode because having some experience contributing to BRL-CAD on geometry conversion and given that this project encourages cross collaboration between both STEPcode and BRL-CAD it would give me the opportunity to work with a wider range of experienced developers and also improve my knowledge of computer graphics.`