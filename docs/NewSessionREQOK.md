## Description

[NetMsg](IBME_GeometryService#NetMsg_Class "wikilink") that is a
response to a previously sent [NewSessionREQ](NewSessionREQ "wikilink")
[NetMsg](IBME_GeometryService#NetMsg_Class "wikilink") to inform the
Remote Host that the new Session request has succeeded.

## Byte Format

|             |                                                          |
|-------------|----------------------------------------------------------|
| **Element** | **Length**                                               |
| DataLen     | int (4 bytes)                                            |
| SessionUUID | UUID (equal to value of DataLen, but should be 16 bytes) |