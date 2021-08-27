## Description

[NetMsg](IBME_GeometryService#NetMsg_Class.md) that is a
response to a previously sent [NewSessionREQ](NewSessionREQ.md)
[NetMsg](IBME_GeometryService#NetMsg_Class.md) to inform the
Remote Host that the new Session request has succeeded.

## Byte Format

|             |                                                          |
|-------------|----------------------------------------------------------|
| **Element** | **Length**                                               |
| DataLen     | int (4 bytes)                                            |
| SessionUUID | UUID (equal to value of DataLen, but should be 16 bytes) |
