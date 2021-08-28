## Description

[NetMsg](IBME_GeometryService#NetMsg_Class.md) that contains a
Hostname string and is sent to all attached Hosts whenever a new Host
attaches to the Geometry Service network. Extends
[GenericOneStringMsg](GenericOneStringMsg.md) (thus contains
those fields also). The String field from
[GenericOneStringMsg](GenericOneStringMsg.md) is used as the
Hostname field.

## Byte Format

No additional fields beyond that of the [Common
Header](../misc/NetMsgTypes.md) and
[GenericOneStringMsg](GenericOneStringMsg.md)
