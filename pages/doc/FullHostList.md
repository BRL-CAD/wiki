## Description

[FullHostListREQ](FullHostListREQ.md) sends a
[NetMsg](IBME_GeometryService#NetMsg_Class.md) to request <BSRJ>
that contains a list of all attached Hosts in
[String] (IBME_NETWORKPROTO_STRING.md) format.

## Byte Format

| **Element**       | **Length**   |
|-------------------|--------------|
| NumberOfHostnames | int (4 byte) |

*Repeated for each Item*

| **Element** | **Length**                                                     |
|-------------|----------------------------------------------------------------|
| Hostname    | [String (Variable bytes)] (IBME_NETWORKPROTO_STRING.md) |

## Google Code In

This page was edited for [Google_Code_In](../Google_Code_In.md)
by BSRJ.
