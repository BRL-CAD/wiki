## Description

[FullHostListREQ](FullHostListREQ "wikilink") sends a
[NetMsg](IBME_GeometryService#NetMsg_Class "wikilink") to request <BSRJ>
that contains a list of all attached Hosts in
[String](IBME_NETWORKPROTO_STRING "wikilink") format.

## Byte Format

| **Element**       | **Length**   |
|-------------------|--------------|
| NumberOfHostnames | int (4 byte) |

*Repeated for each Item*

| **Element** | **Length**                                                     |
|-------------|----------------------------------------------------------------|
| Hostname    | [String (Variable bytes)](IBME_NETWORKPROTO_STRING "wikilink") |

## Google Code In

This page was edited for [Google_Code_In](Google_Code_In "wikilink")
by BSRJ.