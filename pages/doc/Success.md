## Description

[NetMsg](IBME_GeometryService#NetMsg_Class.md) that is a
response to a previously sent
[NetMsg](IBME_GeometryService#NetMsg_Class.md) subclass to
inform the sender that an action has succeeded. The SuccessMsg
references the succeeded action by way of the RegardingUUID field.
Extends [GenericOneByteMsg](GenericOneByteMsg.md) (thus contains
those fields also). The single byte field from
[GenericOneByteMsg](GenericOneByteMsg.md) is the Success Code.

List of success codes are below.<BSRJ>

## Byte Format

No additional fields beyond that of the [Common
Header](NetMsgTypes.md) and
[GenericOneByteMsg](GenericOneByteMsg.md)

## Success Codes

[NewSessionREQOK](NewSessionREQOK.md)<BSRJ>

[RemHostNameSETOK](RemHostNameSETOK.md)<BSRJ>

## Google Code In

This page was edited for [Google_Code_In](Google_Code_In.md)
by BSRJ.
