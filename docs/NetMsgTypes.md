------------------------------------------------------------------------

# NetMsg Generic Templates

------------------------------------------------------------------------

The GSNet API provides several Template classes to be used or extended
from.

-   [Generic One Byte Msg](GenericOneByteMsg "wikilink")
-   [Generic Two Byte Msg](GenericTwoBytesMsg "wikilink")
-   [Generic Four Byte Msg](GenericFourBytesMsg "wikilink")
-   [Generic Eight Byte Msg](GenericEightByteMsg "wikilink")
-   [Generic Multi Byte Msg](GenericMultiByteMsg "wikilink")
-   [Generic One String Msg](GenericOneStringMsg "wikilink")
-   [Generic Multi-String Msg](GenericMultiStringMsg "wikilink")

------------------------------------------------------------------------

# NetMsg MsgTypes

------------------------------------------------------------------------

Some NetMsgs will need to have custom bodies. Here is a list of NetMsgs,
their related MsgTypes, and links to details on that specific NetMsg:

**NOTE:** This list is \*NOT\* up-to-date as of 3.25.11

**TODO:** Replace this with Doxy files


|                |                                                        |                                                           |                                                                                                                                 |
|----------------|--------------------------------------------------------|-----------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| **MsgType ID** | **Name**                                               | **Parent Class**                                          | **Additional Info**                                                                                                             |
| 0x0042         | RUALIVE                                                | [TypeOnlyMsg](TypeOnlyMsg "wikilink")                     | Ping without time info (necessary?)                                                                                             |
| 0x0043         | IMALIVE                                                | [TypeOnlyMsg](TypeOnlyMsg "wikilink")                     | Pong without time info (necessary?)                                                                                             |
| 0x0050         | Failure                                                | [GenericOneByteMsg](GenericOneByteMsg "wikilink")         | 1 byte 'error code'                                                                                                             |
| 0x0051         | Success                                                | [GenericOneByteMsg](GenericOneByteMsg "wikilink")         | 1 byte 'success code'                                                                                                           |
| 0x0060         | PING                                                   | [GenericEightByteMsg](GenericEightByteMsg "wikilink")     | 8 byte time stamp for start time                                                                                                |
| 0x0062         | PONG                                                   | [GenericEightByteMsg](GenericEightByteMsg "wikilink")     | 8 byte time stamp for start time, dup of the ping value                                                                         |
| 0x0100         | GS Remote Nodename Set                                 | [GenericOneStringMsg](GenericOneStringMsg "wikilink")     | String is the Nodename                                                                                                          |
| 0x0150         | Disconnect Request                                     | [TypeOnlyMsg](TypeOnlyMsg "wikilink")                     |                                                                                                                                 |
| 0x0200         | New Node on Network                                    | [GenericOneStringMsg](GenericOneStringMsg "wikilink")     | String is the Nodename                                                                                                          |
| 0x0250         | Full Nodename List Request                             |                                                           | '**'Not Implemented Yet**                                                                                                       |
| 0x0255         | Full Nodename List                                     |                                                           | '**'Not Implemented Yet**                                                                                                       |
| 0x0300         | [New Session Request](NewSessionReqMsg "wikilink")     | [NetMsg](NetMsg "wikilink")                               | Two strings, username and password                                                                                              |
| 0x0305         | [Session Information](SessionInfoMsg "wikilink")       | [NetMsg](NetMsg "wikilink")                               | One string, the session UUID                                                                                                    |
| 0x0400         | [Geometry Request](GeometryReqMsg "wikilink")          | [GenericOneStringMsg](GenericOneStringMsg "wikilink")     | Has additional custom fields.                                                                                                   |
| 0x0401         | [BoT Geometry Request](GeometryBoTReqMsg "wikilink")   | [GenericOneStringMsg](GenericOneStringMsg "wikilink")     | Requests geometry in BoT format, with exactly one BoT per region.                                                               |
| 0x0402         | [Geometry List Request](GeometryListReqMsg "wikilink") | [GenericOneStringMsg](GenericOneStringMsg "wikilink")     | Requests a list of geometry artifacts at given location.                                                                        |
| 0x0403         | [Geometry List Results](GeometryListResMsg "wikilink") | [GenericMultiStringMsg](GenericMultiStringMsg "wikilink") | Display a list of geometry artifact names.                                                                                      |
| 0x0405         | [Geometry Manifest](GeometryManifestMsg "wikilink")    | [GenericMultiStringMsg](GenericMultiStringMsg "wikilink") | List of 'object' names about to be received as chunks. ReUUID is the associated GeometryReqMsg UUID.                            |
| 0x0410         | [Geometry Chunk](GeometryChunkMsg "wikilink")          | [GenericMultiByteMsg](GenericMultiByteMsg "wikilink")     | Raw .g information. Chunks can be written to a file to produce a viable V5 .g db. ReUUID is the associated GeometryReqMsg UUID. |