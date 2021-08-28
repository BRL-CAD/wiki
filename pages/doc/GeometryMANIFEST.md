## Description

[NetMsg](IBME_GeometryService#NetMsg_Class.md) that contains a
list of Geometry objects.

## Failure Codes

If a [GeometryREQFAIL](GeometryREQFAIL.md) message is displayed,
this indicates that the GeometryMANIFEST has failed to create list of
geometry objects. <BSRJ>

Note: You can read all [Failure](Failure.md) codes.

## Related Subjects

[GeometryREQ](GeometryREQ.md)

[GeometryCHUNK](GeometryCHUNK.md)

## Byte Format

|                 |              |
|-----------------|--------------|
| **Element**     | **Length**   |
| ItemsInManifest | int (4 byte) |

*Repeated for each Item*

|         |                                      |
|---------|--------------------------------------|
| DataLen | int (4 bytes)                        |
| Data    | variable (equal to value of DataLen) |

## Google Code In

This page was edited for [Google_Code_In](../Google_Code_In.md)
by BSRJ.
