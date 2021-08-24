## Description

[NetMsg](IBME_GeometryService#NetMsg_Class.md) that contains a
single serialized Geometry object. Extends
[GenericMultiByteMsg](GenericMultiByteMsg.md) (thus contains
those fields also). The String field from
[GenericMultiByteMsg](GenericMultiByteMsg.md) is used as the
Data field.

## Failure Codes

If a [GeometryREQFAIL](GeometryREQFAIL.md) message is displayed,
this indicates that the GeometryCHUNK object has failed. <BSRJ>

Note: You can read all [Failure](Failure.md) codes.

## Related Subjects

[GeometryREQ](GeometryREQ.md)

[GeometryMANIFEST](GeometryMANIFEST.md)

## Byte Format

No additional fields beyond that of the [Common
Header](NetMsgTypes.md) and
[GenericMultiByteMsg](GenericMultiByteMsg.md)

## Google Code In

This page was edited for [Google_Code_In](Google_Code_In.md)
by BSRJ.
