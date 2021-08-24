## Description

[NetMsg](IBME_GeometryService#NetMsg_Class "wikilink") that contains the
Hostname string value of the Application sending the
[NetMsg](IBME_GeometryService#NetMsg_Class "wikilink"). The intent is to
inform the remote application of the local Hostname.Extends
[GenericOneStringMsg](GenericOneStringMsg "wikilink") (thus contains
those fields also). The String field from
[GenericOneStringMsg](GenericOneStringMsg "wikilink") is used as the
Hostname field.

If the Hostname string value is created, a
[RemHostNameSETOK](RemHostNameSETOK "wikilink") message is displayed.
<BSRJ>

If a [RemHostNameSETFAIL](RemHostNameSETFAIL "wikilink") message is
displayed, this indicates that the RemHostNameSET failed to create
Hostname string value. <BSRJ>

## Byte Format

No additional fields beyond that of the [Common
Header](NetMsgTypes "wikilink") and
[GenericOneStringMsg](GenericOneStringMsg "wikilink")

## Google Code In

This page was edited for [Google_Code_In](Google_Code_In "wikilink")
by BSRJ.