## Description

[NetMsg](IBME_GeometryService#NetMsg_Class.md) that is a
response to a previously sent
[NetMsg](IBME_GeometryService#NetMsg_Class.md) subclass to
inform the sender that the action has failed. The FailureMsg references
the failed action by way of the RegardingUUID field. Extends
[GenericOneByteMsg](GenericOneByteMsg.md) (thus contains those
fields also). The single byte field from
[GenericOneByteMsg](GenericOneByteMsg.md) is the Failure Code.

List of failure codes are below.<BSRJ>

## Byte Format

No additional fields beyond that of the [Common
Header](NetMsgTypes.md) and
[GenericOneByteMsg](GenericOneByteMsg.md)

## Failure Codes

[GeometryREQFAIL](GeometryREQFAIL.md)<BSRJ>

[RemHostNameSETFAIL](RemHostNameSETFAIL.md)<BSRJ>

## Google Code In

This page was edited for [Google_Code_In](Google_Code_In.md)
by BSRJ.
