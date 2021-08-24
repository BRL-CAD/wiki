## Description

[NetMsg](IBME_GeometryService#NetMsg_Class "wikilink") that contains a
single serialized Geometry object. Extends
[GenericMultiByteMsg](GenericMultiByteMsg "wikilink") (thus contains
those fields also). The String field from
[GenericMultiByteMsg](GenericMultiByteMsg "wikilink") is used as the
Data field.

## Failure Codes

If a [GeometryREQFAIL](GeometryREQFAIL "wikilink") message is displayed,
this indicates that the GeometryCHUNK object has failed. <BSRJ>

Note: You can read all [Failure](Failure "wikilink") codes.

## Related Subjects

[GeometryREQ](GeometryREQ "wikilink")

[GeometryMANIFEST](GeometryMANIFEST "wikilink")

## Byte Format

No additional fields beyond that of the [Common
Header](NetMsgTypes "wikilink") and
[GenericMultiByteMsg](GenericMultiByteMsg "wikilink")

## Google Code In

This page was edited for [Google_Code_In](Google_Code_In "wikilink")
by BSRJ.