---
title: "IntermediaryMessages"
description: "Not used directly, but as part of other messages."
icon: "code"
date: "2024-02-10T00:44:31+01:00"
lastmod: "2024-02-10T00:44:31+01:00"
draft: false
toc: true
weight: 190
---

{{< alert context="info" text="This documentation is a work in progress, and we actively welcome contributions. If you have suggestions for improvements or new features, feel free to open a pull request on our GitHub repository. [Contribute here](https://www.github.com/zeejayym/apex-liveapi-documentation). We appreciate your input in making our documentation better for everyone." />}}

## Messages

Not used directly, but as part of other messages.

## Init

This message is sent upon successfully connecting over WebSockets

{{< table "table-striped-columns" >}}

| Field Name  | Type    | Tag | Description                                                         |
|-------------|---------|-----|---------------------------------------------------------------------|
| `timestamp`   | uint64  | 1   | The timestamp when the connection was successfully initialized.    |
| `category`    | string  | 2   | The category of the message, e.g., "traffic_initialization".       |
| `gameVersion` | string  | 3   | The version of the game client.                                     |
| `apiVersion`  | Version | 4   | The version of the API being used, as defined by the `Version` message. |
| `platform`    | string  | 5   | The platform the client is running on.                              |
| `name`        | string  | 6   | Session name specified by `cl_liveapi_session_name`.                |

{{< /table >}}

## Vector3

{{< table "table-striped-columns" >}}

| Field Name | Type  | Tag | Description           |
|------------|-------|-----|-----------------------|
| `x`          | float | 1   | The X coordinate.     |
| `y`          | float | 2   | The Y coordinate.     |
| `z`          | float | 3   | The Z coordinate.     |

{{< /table >}}

## Player

{{< table "table-striped-columns" >}}

| Field Name       | Type    | Tag | Description                                       |
|------------------|---------|-----|---------------------------------------------------|
| `name`             | string  | 1   | The player's name.                                |
| `teamId`           | uint32  | 2   | The player's team ID.                             |
| `pos`              | Vector3 | 3   | The player's position.                            |
| `angles`           | Vector3 | 4   | The player's viewing angles.                      |
| `currentHealth`    | uint32  | 5   | The player's current health.                      |
| `maxHealth`        | uint32  | 6   | The player's maximum health.                      |
| `shieldHealth`     | uint32  | 7   | The player's current shield health.               |
| `shieldMaxHealth`  | uint32  | 8   | The player's maximum shield health.               |
| `nucleusHash`      | string  | 9   | Unique identifier for the player.                 |
| `hardwareName`     | string  | 10  | The name of the player's hardware.                |
| `teamName`         | string  | 11  | The name of the player's team.                    |
| `squadIndex`       | uint32  | 12  | The player's squad index.                         |
| `character`        | string  | 13  | The character the player has selected.            |
| `skin`             | string  | 14  | The skin the player has selected for the character.|

{{< /table >}}

## CustomMatch_LobbyPlayer

{{< table "table-striped-columns" >}}

| Field Name    | Type   | Tag | Description                           |
|---------------|--------|-----|---------------------------------------|
| `name`          | string | 1   | The player's name.                    |
| `teamId`        | uint32 | 2   | The player's team ID.                 |
| `nucleusHash`   | string | 3   | Unique identifier for the player.     |
| `hardwareName`  | string | 4   | The name of the player's hardware.    |

{{< /table >}}

## Datacenter

{{< table "table-striped-columns" >}}

| Field Name | Type   | Tag | Description             |
|------------|--------|-----|-------------------------|
| `timestamp`  | uint64 | 1   | The timestamp.          |
| `category`   | string | 2   | The category of event.  |
| `name`       | string | 3   | The name of datacenter. |

{{< /table >}}

## Version

{{< table "table-striped-columns" >}}

| Field Name  | Type   | Tag | Description                 |
|-------------|--------|-----|-----------------------------|
| `major_num`   | uint32 | 1   | The major version number.   |
| `minor_num`   | uint32 | 2   | The minor version number.   |
| `build_stamp` | uint32 | 3   | The build stamp.            |
| `revision`    | string | 4   | The version revision.       |

{{< /table >}}

## InventoryItem

{{< alert context="success" text="**Important Update**: `InventoryItem` was introduced in the Season 20 update on 2/13/2024." />}}

{{< table "table-striped-columns" >}}

| Field Name | Type   | Tag | Description                                     |
|------------|--------|-----|-------------------------------------------------|
| `quantity`   | int32  | 1   | The quantity of the item.                       |
| `item`       | string | 2   | The item identifier.                            |
| `extraData`  | string | 3   | Any mods or additional info on the item.       |

{{< /table >}}

## LoadoutConfiguration

{{< alert context="success" text="**Important Update**: `LoadoutConfiguration` was introduced in the Season 20 update on 2/13/2024." />}}

{{< table "table-striped-columns" >}}

| Field Name | Type             | Tag | Description                                                      |
|------------|------------------|-----|------------------------------------------------------------------|
| `weapons`    | InventoryItem[]  | 1   | A list of `InventoryItem` representing the weapons in the loadout. |
| `equipment`  | InventoryItem[]  | 2   | A list of `InventoryItem` representing the equipment in the loadout. |

{{< /table >}}


## CustomMatch_LobbyPlayers
Response to the `CustomMatch_GetLobbyPlayers`, contains the list of all players in the lobby.

{{< table "table-striped-columns" >}}

| Field Name   | Type                         | Tag | Description                                                          |
|--------------|------------------------------|-----|----------------------------------------------------------------------|
| `playerToken`  | string                       | 1   | Custom match lobby join code.                             |
| `players`      | CustomMatch_LobbyPlayer[]    | 2   | A list of `CustomMatch_LobbyPlayer` representing all players in the lobby. |

{{< /table >}}

