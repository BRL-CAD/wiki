------------------------------------------------------------------------

# Geometry Service Requirements

-   Geometry versioning: revision history of geometry changes such as
    who did what to the model and for which analysis, when changes were
    made, by whom, etc.
-   Direct association of stored geometry with external data
-   Multi-user access controls that allow multiple people to work on the
    same models at the same time
-   Programmable access-controlled interface that utilizes reuseable
    code for consistent end-to-end access to geometric data.
-   Dynamic geometry
-   Geometry articulation and editing constraints
-   Unified repository of geometry in one storage location.
-   Reuse of identical geometry parts (single instancing).
-   Improved/advanced collaboration.




# Identified Executables

-   Thin Client
    -   Any Language
    -   Provides:
        -   Communicates with Geometry Engine via GS Protocol
        -   Gui Interface
    -   [GS Dev Thin Client
        Requirements](GS_Dev_Thin_Client_Requirements.md)


\*Geometry Engine

-   -   C++
    -   Provides:
        -   Geometry Management (via SVN)
        -   Geometry Conversion, Import, Export
        -   RayTracing
        -   Communications with external Geometry Engines
        -   Communications with external Geometry Repositories
        -   Communications with any other application that implements
            the GS Protocol
    -   [GS Dev Geometry Engine
        Requirements](GS_Dev_Geometry_Engine_Requirements.md)




# Visual Conception

<center>


![](/wiki/img/GS_Concept_local.jpg)
A Thin Client connected to a Geometry Service, all running on one
physical machine




![](/wiki/img/GS_Concept_Multi_med.jpg)
Thin Clients connected to Geometry Services, each running on independent
physical machines, but connected to a 'headless' Geometry Service. The
'headless' geometry service also serves other enterprise level
applications.

</center>









