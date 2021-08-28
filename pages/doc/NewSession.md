## Description

[NetMsg] (IBME_GeometryService#NetMsg_Class.md) that contains a
UUID (in unicode string format) that represents the newly obtained
sessionID. Extends [GenericOneStringMsg](GenericOneStringMsg.md)
(thus contains those fields also). The String field from
[GenericOneStringMsg](GenericOneStringMsg.md) is used as the
UUID (SessionID) field.

## Failure Codes

If a [NewSessionFAIL](../misc/NewSessionFAIL.md) message is displayed,
this indicates that the SessionID failed to create. <BSRJ>

## Byte Format

No additional fields beyond that of the [Common
Header](../misc/NetMsgTypes.md) and
[GenericOneStringMsg](GenericOneStringMsg.md)

## Google Code In

This page was edited for [Google_Code_In](../Google_Code_In.md)
by BSRJ.
