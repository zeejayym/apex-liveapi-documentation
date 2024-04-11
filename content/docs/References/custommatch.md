---
title: "CustomMatch"
description: ""
icon: "code"
date: "2024-02-10T00:44:31+01:00"
lastmod: "2024-02-10T00:44:31+01:00"
draft: false
toc: true
weight: 210
---

{{< alert context="info" text="This documentation is a work in progress, and we actively welcome contributions. If you have suggestions for improvements or new features, feel free to open a pull request on our GitHub repository. [Contribute here](https://www.github.com/zeejayym/apex-liveapi-documentation). We appreciate your input in making our documentation better for everyone." />}}

## Messages

### ChangeCamera

Request to change the observer camera. Be aware of server conditions affecting request fulfillment.


{{< table "table-striped-columns" >}}

| Field Name          | Type              | Tag | Description                                                        |
|---------------------|-------------------|-----|--------------------------------------------------------------------|
| `target`            | oneof {poi, name} | -   | Target for the camera change: either PlayerOfInterest (poi) or name. |
| `poi`             | PlayerOfInterest  | 1   | Set the camera to an interesting player (e.g., the Kill Leader).  |
| `name`            | string            | 2   | Change camera to a player by name. Name string length limit: 256 characters. |

{{< /table >}}

### PauseToggle

Request message to toggle pause in a match type that supports it.


{{< table "table-striped-columns" >}}

| Field Name   | Type  | Tag | Description                                   |
|--------------|-------|-----|-----------------------------------------------|
| `preTimer`   | float | 1   | Pre-timer duration before the pause takes effect. |

{{< /table >}}

### CustomMatch_CreateLobby

Request to create a custom match lobby. No fields are required for this request.


### CustomMatch_JoinLobby

Request to join an existing custom match lobby identified by the `roleToken`.


{{< table "table-striped-columns" >}}

| Field Name   | Type   | Tag | Description                                |
|--------------|--------|-----|--------------------------------------------|
| `roleToken`  | string | 1   | Token identifying the lobby to join.       |

{{< /table >}}

### CustomMatch_LeaveLobby

Request to leave a custom match lobby. No fields are required for this request.


### CustomMatch_SetReady

Request to programmatically change your player's ready state in a custom match lobby.


{{< table "table-striped-columns" >}}

| Field Name  | Type   | Tag | Description                                |
|-------------|--------|-----|--------------------------------------------|
| `isReady`   | bool   | 1   | New ready state of the player.             |

{{< /table >}}

### CustomMatch_GetLobbyPlayers

Request to retrieve all connected players in a custom match lobby and lobby code or playerToken. This request will be replied to with `CustomMatch_LobbyPlayers`. No fields are required for this request.

### CustomMatch_SetMatchmaking

Request to change the state of matchmaking in a custom match lobby.


{{< table "table-striped-columns" >}}

| Field Name  | Type   | Tag | Description                                              |
|-------------|--------|-----|----------------------------------------------------------|
| `enabled`   | bool   | 1   | When true, the lobby will attempt to begin a match.      |

{{< /table >}}

### CustomMatch_SetTeam

Request to assign a particular player to a specific team.


{{< table "table-striped-columns" >}}

| Field Name           | Type   | Tag | Description                                                    |
|----------------------|--------|-----|----------------------------------------------------------------|
| `teamId`             | int32  | 1   | Team ID across the entire lobby. Observers have a teamId of 0. |
| `targetHardwareName` | string | 2   | Hardware name of the target player.                            |
| `targetNucleusHash`  | string | 3   | Nucleus hash of the target player.                             |

{{< /table >}}

### CustomMatch_KickPlayer

Request to remove a player from the currently connected custom match lobby.

{{< table "table-striped-columns" >}}

| Field Name           | Type   | Tag | Description                                                    |
|----------------------|--------|-----|----------------------------------------------------------------|
| `targetHardwareName` | string | 1   | Hardware name of the target player.                            |
| `targetNucleusHash`  | string | 2   | Nucleus hash of the target player.                             |

{{< /table >}}

### CustomMatch_SetSettings

Request to alter the settings of a custom match lobby. The request should specify all fields being set with the new value. For convinience, call `CustomMatch_GetSettings` to get the full state of settings.

{{< table "table-striped-columns" >}}

| Field Name           | Type   | Tag | Description                                                    |
|----------------------|--------|-----|----------------------------------------------------------------|
| `playlistName`       | string | 1   | Name of current custom match playlist.                         |
| `adminChat`          | bool   | 2   | Restricts chat messages to only admins.                        |
| `teamRename`         | bool   | 3   | Restricts team renaming to only admins.                        |
| `selfAssign`         | bool   | 4   | Allows players to asign themselves to teams.                   |
| `aimAssist`          | bool   | 5   | All players will use PC aim assist values.                     |
| `anonMode`           | bool   | 6   | Anonymize the display of players' names to other players.      |

{{< /table >}}

### CustomMatch_GetSettings

{{< alert context="success" text="**Important Update**: `CustomMatch_GetSettings` was introduced in the Season 20 update on 2/13/2024." />}}

Review all the current settings. This request will be replied to with `CustomMatch_SetSettings` from which you can modify and reply with any new values for your convenience. No fields are required for this request.

### CustomMatch_SetTeamName
{{< alert context="warning" text="Requires special access and is subject to text filtering." />}}

Request to set the name of a team in custom match lobby. 

{{< table "table-striped-columns" >}}

| Field Name           | Type   | Tag | Description                                                    |
|----------------------|--------|-----|----------------------------------------------------------------|
| `teamId`             | int32  | 1   | Target teamId of name change.                                  |
| `teamName`           | string | 2   | New name of team.                                              |

{{< /table >}}

### CustomMatch_SendChat
Request to programatically send a chat message to the entire custom match lobby.

{{< table "table-striped-columns" >}}

| Field Name           | Type   | Tag | Description                                                    |
|----------------------|--------|-----|----------------------------------------------------------------|
| `text`               | string | 1   | Text of chat message.                                          |

{{< /table >}}
