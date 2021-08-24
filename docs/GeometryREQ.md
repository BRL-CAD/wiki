## Description

[NetMsg](IBME_GeometryService#NetMsg_Class "wikilink") that contains
either a UUID or string Path that references a piece of Geometry.
Extends [GenericOneStringMsg](GenericOneStringMsg "wikilink") (thus
contains those fields also). The String field from
[GenericOneStringMsg](GenericOneStringMsg "wikilink") is used as the
UUID or Path field, depending on the Request Type.

## Warning Messages

If you want to disconnect this request,
[DisconnectREQ](DisconnectREQ "wikilink") is displayed. <BSRJ>

## Failure Codes

If a [GeometryREQFAIL](GeometryREQFAIL "wikilink") message is displayed,
this indicates that the GeometryREQ has failed. <BSRJ>

Note: You can read all [Failure](Failure "wikilink") codes.

## Related Subjects

[NewHostOnNet](NewHostOnNet "wikilink")

[GeometryCHUNK](GeometryCHUNK "wikilink")

[GeometryMANIFEST](GeometryMANIFEST "wikilink")

## Byte Format

|             |               |
|-------------|---------------|
| **Element** | **Length**    |
| RequestType | byte (1 byte) |

### Request Types

|                 |                                                |
|-----------------|------------------------------------------------|
| **RequestType** | **Description**                                |
| 0               | The Data is a UUID for the Geometry requested. |
| 1               | The Data is a path to the Geometry requested.  |

## Google Code In

This page was edited for [Google_Code_In](Google_Code_In "wikilink")
by BSRJ.