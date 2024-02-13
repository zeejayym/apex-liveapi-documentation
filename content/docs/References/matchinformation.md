---
title: "MatchInformation"
description: ""
icon: "code"
date: "2024-02-10T00:44:31+01:00"
lastmod: "2024-02-10T00:44:31+01:00"
draft: false
toc: true
weight: 200
---
## Events

{{< alert context="info" text="This documentation is a work in progress, and we actively welcome contributions. If you have suggestions for improvements or new features, feel free to open a pull request on our GitHub repository. [Contribute here](https://www.github.com/zeejayym/apex-liveapi-documentation). We appreciate your input in making our documentation better for everyone." />}}

### MatchSetup

Sent during the first phase of a match. This event gives a full description of what match is being played.
  
{{< alert context="success" text="**Important Update**: `MatchSetup.startingLoadout`  was introduced in the Season 20 update on 2/13/2024." />}}

  {{< table "table-striped-columns" >}}

  | Field Name     | Type         | Tag | Description                              |
  |----------------|--------------|-----|------------------------------------------|
  | `timestamp`      | uint64       | 1   | The timestamp when the match starts.     |
  | `category`       | string       | 2   | The category of the match setup event.   |
  | `map`            | string       | 3   | The map where the match is taking place. |
  | `playlistName`   | string       | 4   | The name of the playlist.                |
  | `playlistDesc`   | string       | 5   | The description of the playlist.         |
  | `datacenter`     | Datacenter   | 6   | Datacenter information.                  |
  | `aimAssistOn`    | bool         | 7   | Indicates if aim assist is enabled.      |
  | `serverId`       | string       | 8   | The server ID.                           |
  | `startingLoadout` | LoadoutConfiguration | 10 | |
  {{< /table >}}

  **Datacenter Message Fields**

{{< table "table-striped-columns" >}}

| Field Name     | Type         | Tag | Description                    |
|----------------|--------------|-----|--------------------------------|
| `name`         | string       | 1   | The name of the datacenter.    |

{{< /table >}}

### GameStateChanged

Sent whenever the match changes phases (e.g., prematch, playing).


{{< table "table-striped-columns" >}}

| Field Name | Type   | Tag | Description                                     |
|------------|--------|-------|-------------------------------------------------|
| `timestamp`  | uint64 | 1   | The timestamp when the game state changed.      |
| `category`   | string | 2   | The category of the game state change event.    |
| `state`      | string | 3   | The new state of the game after the change.     |

{{< /table >}}

### CharacterSelected

Occurs when any player has locked in a character during legend select.

{{< table "table-striped-columns" >}}

| Field Name | Type   | Tag | Description                                                       |
|------------|--------|-----|-------------------------------------------------------------------|
| `timestamp`  | uint64 | 1   | The timestamp when the character was selected.                    |
| `category`   | string | 2   | The category of the event, e.g., "character_selected".            |
| `player`     | Player | 3   | The player who has selected a character.                          |

{{< /table >}}


### MatchStateEnd

Event to summarize the match after it has ended.

{{< table "table-striped-columns" >}}

| Field Name | Type     | Tag | Description                                                    |
|------------|----------|-----|----------------------------------------------------------------|
| `timestamp`  | uint64   | 1   | The timestamp when the match ended.                            |
| `category`   | string   | 2   | The category of the event, e.g., "match_state_end".            |
| `state`      | string   | 3   | The final state of the match.                                  |
| `winners`    | Player[] | 4   | A list of players who won the match.                           |

{{< /table >}}

### RingStartClosing

Fired whenever the ring begins moving in a match.

{{< table "table-striped-columns" >}}

| Field Name     | Type   | Tag | Description                                                     |
|----------------|--------|-----|-----------------------------------------------------------------|
| `timestamp`      | uint64 | 1   | The timestamp when the ring started closing.                    |
| `category`       | string | 2   | The category of the event, e.g., "ring_start_closing".          |
| `stage`          | uint32 | 3   | The current stage of the ring closing.                          |
| `center`         | Vector3| 4   | The center point of the ring.                                   |
| `currentRadius`  | float  | 5   | The current radius of the ring.                                 |
| `endRadius`      | float  | 6   | The radius of the ring at the end of the closing phase.         |
| `shrinkDuration` | float  | 7   | The duration of time for the ring to finish closing.            |

{{< /table >}}

### RingFinishedClosing

Used when the ring has finished moving and prior to it moving again.

{{< table "table-striped-columns" >}}

| Field Name     | Type    | Tag | Description                                                        |
|----------------|---------|-----|--------------------------------------------------------------------|
| `timestamp`      | uint64  | 1   | The timestamp when the ring finished closing.                      |
| `category`       | string  | 2   | The category of the event, e.g., "ring_finished_closing".          |
| `stage`          | uint32  | 3   | The stage of the match when the ring finished closing.             |
| `center`         | Vector3 | 4   | The center point of the ring after it has finished closing.        |
| `currentRadius`  | float   | 5   | The current radius of the ring after it has finished closing.      |
| `shrinkDuration` | float   | 7   | The duration of time until the ring starts moving again.           |

{{< /table >}}

### PlayerConnected

Used when a player has connected to the match.

{{< table "table-striped-columns" >}}

| Field Name | Type    | Tag | Description                                         |
|------------|---------|-----|-----------------------------------------------------|
| `timestamp`  | uint64  | 1   | The timestamp when the player connected.            |
| `category`   | string  | 2   | The category of the event, e.g., "player_connected".|
| `player`     | Player  | 3   | The player who has connected to the match.          |

{{< /table >}}


### PlayerDisconnected

Used when a player has disconnected, even temporarily.

{{< table "table-striped-columns" >}}

| Field Name    | Type    | Tag | Description                                                             |
|---------------|---------|-----|-------------------------------------------------------------------------|
| `timestamp`     | uint64  | 1   | The timestamp when the player disconnected.                             |
| `category`      | string  | 2   | The category of the event, e.g., "player_disconnected".                 |
| `player`        | Player  | 3   | The player who has disconnected.                                        |
| `canReconnect`  | bool    | 4   | Indicates if the player can reconnect to the match.                     |
| `isAlive`       | bool    | 5   | Indicates if the player was alive in the game at the time of disconnect.|

{{< /table >}}

### PlayerStatChanged

Generic event for a change in player stats.

{{< table "table-striped-columns" >}}

| Field Name   | Type    | Tag | Description                                                     |
|--------------|---------|-----|-----------------------------------------------------------------|
| `timestamp`    | uint64  | 1   | The timestamp when the player stat changed.                     |
| `category`     | string  | 2   | The category of the event, e.g., "player_stat_changed".         |
| `player`       | Player  | 3   | The player whose stat has changed.                              |
| `statName`     | string  | 4   | The name of the stat that changed.                              |
| `newValue`     | uint32  | 5   | The new value of the stat.                                      |

{{< /table >}}

### PlayerUpgradeTierChanged
{{< alert context="success" text="**Important Update**: `PlayerUpgradeTierChange`  was introduced in the Season 20 update on 2/13/2024." />}}

Event used to notify when a player goes above their current tier level.

{{< table "table-striped-columns" >}}

| Field Name   | Type    | Tag | Description                                                       |
|--------------|---------|-----|-------------------------------------------------------------------|
| `timestamp`    | uint64  | 1   | The timestamp when the player's upgrade tier changed.             |
| `category`     | string  | 2   | The category of the event, e.g., "player_upgrade_tier_changed".   |
| `player`       | Player  | 3   | The player whose upgrade tier has changed.                        |
| `level`        | int32   | 4   | The new level of the player after the upgrade tier change.        |

{{< /table >}}



