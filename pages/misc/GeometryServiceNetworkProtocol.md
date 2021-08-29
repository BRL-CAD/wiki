[category:Geometry Service](category:Geometry_Service.md)
[category:GSNet Protocol](category:GSNet_Protocol.md)

------------------------------------------------------------------------

<table>
<tbody>
<tr class="odd">
<td>
![](../img/GSNet_Symbol.png)
</td>
<td><p>The Geometry Service Network (GSNet) Protocol is a TCP/IP based protocol designed to facilitate socketed communications between Geometry Service Nodes on a network. A Geometry Service Node is defined as any softwares that supports communication via the GSNet Protocol.<br />
__TOC__</p></td>
</tr>
</tbody>
</table>

------------------------------------------------------------------------

# GSNet Msg Description

## Header

The header of the GSNet Msg contains the information necessary for
quickly determining authenticity, type and length. Geometry Service's
network library, libNetwork, has a header byte layout that looks like
this:


|                      |                                                    |                                                                |
|----------------------|----------------------------------------------------|----------------------------------------------------------------|
| **Element**          | **Length**                                         | **Value**                                                      |
| MsgType              | int16 (2 bytes)                                    |                                                                |
| MessageLength        | int32 (4 bytes)                                    | Does \*NOT\* include the type or length, so is packet size - 6 |
| MessageUUID          | [String (Variable bytes)](GSNet_String.md) |                                                                |
| HasRegardingUUID     | Boolean (1 byte)                                   |                                                                |
| RegardingMessageUUID | [String (Variable bytes)](GSNet_String.md) |                                                                |

-   **MsgType:** 2 byte integer value that tells what type of message
    this is.
-   **MessageUUID:** Standard UUID for this message. Currently stored as
    a string.
-   **HasRegardingUUID:** Boolean flag that indicates whether there is a
    Regarding UUID or not.
-   **RegardingMessageUUID:** Standard UUID that indicates this NetMsg
    is a response to another NetMsg.

------------------------------------------------------------------------

## Data

------------------------------------------------------------------------

The Data load of a NetMsg is, obivously, the important and unique part.
Data Loads can be as small as zero (in the case of a TypeOnlyMsg) or
many kilobytes long.

Here is a list of [NetMsg types](NetMsgTypes.md) and here is a
list of [Common NetMsg Exchanges](Common_NetMsg_Exchanges.md).
