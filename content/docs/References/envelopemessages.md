---
title: "EnvelopeMessages"
description: ""
icon: "code"
date: "2024-04-14T00:44:31+01:00"
lastmod: "2024-04-14T00:44:31+01:00"
draft: false
toc: true
weight: 210
---

{{< alert context="info" text="This documentation is a work in progress, and we actively welcome contributions. If you have suggestions for improvements or new features, feel free to open a pull request on our GitHub repository. [Contribute here](https://www.github.com/zeejayym/apex-liveapi-documentation). We appreciate your input in making our documentation better for everyone." />}}

## Messages

### Request
Envelope message for any Live API request. This allows a single uniform data structure for requests to be made and for the game to receive them. Specifically, there is only one possible action per request. You can request an acknowledgement of your request by setting `withAck` to `true`. 

Acknowledgements will come in the form of a Response message. More information can be found with that event.

A single example to create a `CustomMatch_JoinLobby` request in python is as follows:
```python
req = Request()
req.customMatch_JoinLobby.roleToken = "<some token>"
req.withAck = True
```

{{< alert context="info" text="For more information, consult the Protobuf documentation for your language of choice and look at details regarding the `oneof` field (https://protobuf.dev/programming-guides/proto3/#oneof)" />}}

#### Message Properties

{{< table "table-striped-columns" >}}

| Field Name  | Type    | Tag | Description                                                         |
|-------------|---------|-----|---------------------------------------------------------------------|
| `withAck`   | bool  | 1   | Receive an acknowledgement of the request having been received.    |
| `preSharedKey`    | string  | 2   | Preshared key to use with the request. Only necessary if the connecting game has a preshared key specified through `cl_liveapi_requests_psk`.       |
| `actions`            | oneof | -   | Action of Request (oneof options below table) |

{{< /table >}}

#### oneof Options
Custom Match specific requests (reserved 10 -> 30)

{{< table "table-striped-columns" >}}

| Field Name                    | Type                        | Tag  | Description                             |
|-------------------------------|-----------------------------|------|-----------------------------------------|
| `changeCam`                   | ChangeCamera                | 4    | `ChangeCamera` message.                 |
| `pauseToggle`                 | PauseToggle                 | 5    | `PauseToggle` message.                  |
| `customMatch_CreateLobby`     | CustomMatch_CreateLobby     | 10   | `CustomMatch_CreateLobby` message.      |
| `customMatch_JoinLobby`       | CustomMatch_JoinLobby       | 11   | `CustomMatch_JoinLobby` message.        |
| `customMatch_LeaveLobby`      | CustomMatch_LeaveLobby      | 12   | `CustomMatch_LeaveLobby` message.       |
| `customMatch_SetReady`        | CustomMatch_SetReady        | 13   | `CustomMatch_SetReady` message.         |
| `customMatch_SetMatchmaking`  | CustomMatch_SetMatchmaking  | 14   | `CustomMatch_SetMatchmaking` message.   |
| `customMatch_SetTeam`         | CustomMatch_SetTeam         | 15   | `CustomMatch_SetTeam` message.          |
| `customMatch_KickPlayer`      | CustomMatch_KickPlayer      | 16   | `CustomMatch_KickPlayer` message.       |
| `customMatch_SetSettings`     | CustomMatch_SetSettings     | 17   | `CustomMatch_SetSettings` message.      |
| `customMatch_SendChat`        | CustomMatch_SendChat        | 18   | `CustomMatch_SendChat` message.         |
| `customMatch_GetLobbyPlayers` | CustomMatch_GetLobbyPlayers | 19   | `CustomMatch_GetLobbyPlayers` message.  |
| `customMatch_SetTeamName`     | CustomMatch_SetTeamName     | 20   | `CustomMatch_SetTeamName` message.      |
| `customMatch_GetSettings`     | CustomMatch_GetSettings     | 21   | `CustomMatch_GetSettings` message.      |

{{< /table >}}

### Any
Use [protobuf.dev's](https://protobuf.dev/reference/protobuf/google.protobuf/#any) documentation of the `Any` message for more information. This documentation will relate to its use in Apex LiveAPI. 

{{< table "table-striped-columns" >}}

| Field Name  | Type    | Tag | Description                                                         |
|-------------|---------|-----|---------------------------------------------------------------------|
| `type_url`   | string  | 1   | A URL that describes the type of the serialized message. LiveAPI messags use the `type.googleapis.com/rtech.liveapi.<MESSAGE TYPE>` format.    |
| `value`    | bytes  | 2   | Serialized protocol buffer of the above specified type.       |

{{< /table >}}

### Response
Message used to indicate the response to a request made to the API. Only the requesting part will receive this message and this message is only sent if the request required an acknowledgement by setting `withAck` to `true` in the Request object. This message is always sent within a `LiveAPIEvent` and never on its own to allow any applications to have a uniform method of reading events over the wire.

{{< alert context="warning" text="If `success` is `true`, it does not mean that the Request has finished or that it was completed correctly. In this case, it means that it was successfully received and contains no issues (it is a well-formed request)." />}}

{{< table "table-striped-columns" >}}

| Field Name  | Type    | Tag | Description                                                         |
|-------------|---------|-----|---------------------------------------------------------------------|
| `success`   | bool  | 1   | Indicates if error has occurred.    |
| `result`    | Any  | 3   |  Serialized protocol buffer of game message in an `Any` Message OR context of request in case of error. |

{{< /table >}}

### LiveAPIEvent
Envelope for all LiveAPI Events. Any game events or responses to requests will be sent using this message. The specific event or message is stored in the `gameMessage` field.

In order to read the message successfully, check the type contained in `gameMessage` and create an instance of that type where you can unpack the data to Protobuf has several ways of doing type to instance lookups that will allow you to do this after you've generated bindings. 

For example, to read and unpack any LiveAPIEvent in Python, the following can be done (assume `pb_msg` contains the LiveAPIEvent object):

```py
from events_pb2 import *
from google.protobuf import symbol_database

[ ... ]

result_type = pb_msg.gameMessage.TypeName()
msg_result = symbol_database.Default().GetSymbol(result_type)()
pb_msg.gameMessage.Unpack(msg_result) # msg_result now holds the actual event you want to read
```

{{< table "table-striped-columns" >}}

| Field Name  | Type    | Tag | Description                                                         |
|-------------|---------|-----|---------------------------------------------------------------------|
| `event_size`   | fixed32  | 1   | Size of protobuf event.    |
| `gameMessage`    | Any  | 3   |  Serialized protocol buffer of game message in an `Any` Message |

{{< /table >}}