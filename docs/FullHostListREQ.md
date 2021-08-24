## Description

[NetMsg](IBME_GeometryService#NetMsg_Class.md) that indicates a
Remote Host's desire to receive a complete list of hosts attached to the
recipient. This is a 'MsgType Only' NetMsg and carries no body.

## Successful Request

A [FullHostList](FullHostList.md) will be displayed if
FullHostListREQ is successful. <BSRJ>

## Warning Messages

If you want to disconnect the request,
[DisconnectREQ](DisconnectREQ.md) message is displayed. <BSRJ>

## Byte Format

No additional byte information beyond the Common Header is required.

## Google Code In

This page was edited for [Google_Code_In](Google_Code_In.md)
by BSRJ.
