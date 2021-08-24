## Description

[NetMsg](IBME_GeometryService#NetMsg_Class "wikilink") that indicates a
Remote Host's desire to instantiate a new Session on the
GeometryService. This is a 'MsgType Only' NetMsg and carries no body. A
[NewSessionREQFAIL](NewSessionREQFAIL "wikilink") message may be
received in response.

## Byte Format

|             |                                                                |
|-------------|----------------------------------------------------------------|
| **Element** | **Length**                                                     |
| Username    | [String (Variable bytes)](IBME_NETWORKPROTO_STRING "wikilink") |
| Password    | [String (Variable bytes)](IBME_NETWORKPROTO_STRING "wikilink") |