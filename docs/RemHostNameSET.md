## Description

[NetMsg](IBME_GeometryService#NetMsg_Class.md) that contains the
Hostname string value of the Application sending the
[NetMsg](IBME_GeometryService#NetMsg_Class.md). The intent is to
inform the remote application of the local Hostname.Extends
[GenericOneStringMsg](GenericOneStringMsg.md) (thus contains
those fields also). The String field from
[GenericOneStringMsg](GenericOneStringMsg.md) is used as the
Hostname field.

If the Hostname string value is created, a
[RemHostNameSETOK](RemHostNameSETOK.md) message is displayed.
<BSRJ>

If a [RemHostNameSETFAIL](RemHostNameSETFAIL.md) message is
displayed, this indicates that the RemHostNameSET failed to create
Hostname string value. <BSRJ>

## Byte Format

No additional fields beyond that of the [Common
Header](NetMsgTypes.md) and
[GenericOneStringMsg](GenericOneStringMsg.md)

## Google Code In

This page was edited for [Google_Code_In](Google_Code_In.md)
by BSRJ.
