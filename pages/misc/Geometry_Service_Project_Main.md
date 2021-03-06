[category:Geometry Service](category:Geometry_Service.md)

|                                    |                                                                                                                                                                                                                                                                                                                                                                               |
|------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ![](../img/GS_Symbol.png) | The Geometry Service Project (GS) is the internal name for a project under development that aims to restructure the geometry management services within BRL-CAD and provide a new user interface. More specifically, the restructuring aims to leverage an object-oriented design and encapsulate much of the existing functionality in BRL-CAD through three C++ interfaces. |

------------------------------------------------------------------------

### The Geometry Service consists of three major pieces

-   **Geometry Engine**: The Geometry Engine(GE) is a stateless library
    built on top of the existing BRL-CAD Libraries: libbu, libbn, libdm,
    libged, librt, etc. The GE contains all geometric processing
    functions to include Format Converters, Tessilation, and image
    processors.

<!-- -->

-   **Geometry Service**: The Geometry Service(GS) is an application
    that expands on the functionality of the Geometry Engine (GE) by
    adding Multi-user Communications and Session Management, Access
    Controls, Multithread capabilities and SVN utilities.

<!-- -->

-   **"New" GUI Project**: Currently nicknamed "G3D", it is a standalone
    client that provides visualization of geometry and captures user
    input. G3D is designed to be connected to a Geometry Service over
    the network via the Geometry Service Network (GSNet) Protocol.

------------------------------------------------------------------------

### QuickLinks

<center>

|                                                         |                               |                                                             |
|:-------------------------------------------------------:|-------------------------------|:-----------------------------------------------------------:|
|         ![](../img/Users_128px.png)          | ???????? ???????? ???????? ???????? ???????? ???????? |       ![](../img/Developer_128px.png)        |
| [**User Pages**](Geometry_Service_User_Main.md) |                               | [**Developer Pages**](Geometry_Service_Dev_Main.md) |

</center>

------------------------------------------------------------------------

### Implementation Particulars

-   The Geometry Service will be written in C/C++ to allow
    runtime-extensibility and reuse of code in future projects.
-   The Geometry Service leverages the proven and stable functionalities
    in BRL-CAD's libraries and binaries.
-   The Geometry Service provides an easy to use and extensible network
    protocol (GSNet Protocol) for interacting with a running Geometry
    Server.
-   The Geometry Engine provides a clean and easy to use API for
    BRL-CAD's libraries and binaries.
-   Each of the three major pieces will be stand-alone products

------------------------------------------------------------------------
