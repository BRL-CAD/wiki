## Description

[NetMsg](IBME_GeometryService#NetMsg_Class "wikilink") that is a
response to a previously sent
[NetMsg](IBME_GeometryService#NetMsg_Class "wikilink") subclass to
inform the sender that the action has failed. The FailureMsg references
the failed action by way of the RegardingUUID field. Extends
[GenericOneByteMsg](GenericOneByteMsg "wikilink") (thus contains those
fields also). The single byte field from
[GenericOneByteMsg](GenericOneByteMsg "wikilink") is the Failure Code.

List of failure codes are below.<BSRJ>

## Byte Format

No additional fields beyond that of the [Common
Header](NetMsgTypes "wikilink") and
[GenericOneByteMsg](GenericOneByteMsg "wikilink")

## Failure Codes

[GeometryREQFAIL](GeometryREQFAIL "wikilink")<BSRJ>

[RemHostNameSETFAIL](RemHostNameSETFAIL "wikilink")<BSRJ>

## Google Code In

This page was edited for [Google_Code_In](Google_Code_In "wikilink")
by BSRJ.