------------------------------------------------------------------------

# NetMsg Generic Templates

------------------------------------------------------------------------

The GSNet API provides several Template classes to be used or extended
from.

-   [Generic One Byte Msg](GenericOneByteMsg.md)
-   [Generic Two Byte Msg](GenericTwoBytesMsg.md)
-   [Generic Four Byte Msg](GenericFourBytesMsg.md)
-   [Generic Eight Byte Msg](GenericEightByteMsg.md)
-   [Generic Multi Byte Msg](GenericMultiByteMsg.md)
-   [Generic One String Msg](GenericOneStringMsg.md)
-   [Generic Multi-String Msg](GenericMultiStringMsg.md)

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
| 0x0042         | RUALIVE                                                | [TypeOnlyMsg](TypeOnlyMsg.md)                     | Ping without time info (necessary?)                                                                                             |
| 0x0043         | IMALIVE                                                | [TypeOnlyMsg](TypeOnlyMsg.md)                     | Pong without time info (necessary?)                                                                                             |
| 0x0050         | Failure                                                | [GenericOneByteMsg](GenericOneByteMsg.md)         | 1 byte 'error code'                                                                                                             |
| 0x0051         | Success                                                | [GenericOneByteMsg](GenericOneByteMsg.md)         | 1 byte 'success code'                                                                                                           |
| 0x0060         | PING                                                   | [GenericEightByteMsg](GenericEightByteMsg.md)     | 8 byte time stamp for start time                                                                                                |
| 0x0062         | PONG                                                   | [GenericEightByteMsg](GenericEightByteMsg.md)     | 8 byte time stamp for start time, dup of the ping value                                                                         |
| 0x0100         | GS Remote Nodename Set                                 | [GenericOneStringMsg](GenericOneStringMsg.md)     | String is the Nodename                                                                                                          |
| 0x0150         | Disconnect Request                                     | [TypeOnlyMsg](TypeOnlyMsg.md)                     |                                                                                                                                 |
| 0x0200         | New Node on Network                                    | [GenericOneStringMsg](GenericOneStringMsg.md)     | String is the Nodename                                                                                                          |
| 0x0250         | Full Nodename List Request                             |                                                           | '**'Not Implemented Yet**                                                                                                       |
| 0x0255         | Full Nodename List                                     |                                                           | '**'Not Implemented Yet**                                                                                                       |
| 0x0300         | [New Session Request](NewSessionReqMsg.md)     | [NetMsg](NetMsg.md)                               | Two strings, username and password                                                                                              |
| 0x0305         | [Session Information](SessionInfoMsg.md)       | [NetMsg](NetMsg.md)                               | One string, the session UUID                                                                                                    |
| 0x0400         | [Geometry Request](GeometryReqMsg.md)          | [GenericOneStringMsg](GenericOneStringMsg.md)     | Has additional custom fields.                                                                                                   |
| 0x0401         | [BoT Geometry Request](GeometryBoTReqMsg.md)   | [GenericOneStringMsg](GenericOneStringMsg.md)     | Requests geometry in BoT format, with exactly one BoT per region.                                                               |
| 0x0402         | [Geometry List Request](GeometryListReqMsg.md) | [GenericOneStringMsg](GenericOneStringMsg.md)     | Requests a list of geometry artifacts at given location.                                                                        |
| 0x0403         | [Geometry List Results](GeometryListResMsg.md) | [GenericMultiStringMsg](GenericMultiStringMsg.md) | Display a list of geometry artifact names.                                                                                      |
| 0x0405         | [Geometry Manifest](GeometryManifestMsg.md)    | [GenericMultiStringMsg](GenericMultiStringMsg.md) | List of 'object' names about to be received as chunks. ReUUID is the associated GeometryReqMsg UUID.                            |
| 0x0410         | [Geometry Chunk](GeometryChunkMsg.md)          | [GenericMultiByteMsg](GenericMultiByteMsg.md)     | Raw .g information. Chunks can be written to a file to produce a viable V5 .g db. ReUUID is the associated GeometryReqMsg UUID. |
