## Description

[NetMsg](IBME_GeometryService#NetMsg_Class "wikilink") that contains a
UUID (in unicode string format) that represents the newly obtained
sessionID. Extends [GenericOneStringMsg](GenericOneStringMsg "wikilink")
(thus contains those fields also). The String field from
[GenericOneStringMsg](GenericOneStringMsg "wikilink") is used as the
UUID (SessionID) field.

## Failure Codes

If a [NewSessionFAIL](NewSessionFAIL "wikilink") message is displayed,
this indicates that the SessionID failed to create. <BSRJ>

## Byte Format

No additional fields beyond that of the [Common
Header](NetMsgTypes "wikilink") and
[GenericOneStringMsg](GenericOneStringMsg "wikilink")

## Google Code In

This page was edited for [Google_Code_In](Google_Code_In "wikilink")
by BSRJ.