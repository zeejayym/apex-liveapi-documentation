---
title: "CombatEvents"
description: ""
icon: "code"
date: "2024-02-10T00:44:31+01:00"
lastmod: "2024-02-10T00:44:31+01:00"
draft: false
toc: true
weight: 220
---

## Events

{{< alert context="info" text="This documentation is a work in progress, and we actively welcome contributions. If you have suggestions for improvements or new features, feel free to open a pull request on our GitHub repository. [Contribute here](https://www.github.com/zeejayym/live-api-documentation). We appreciate your input in making our documentation better for everyone." />}}

### PlayerDamaged

Event describing a player taking damage. Details include the attacker, victim, the weapon used, and the amount of damage.

{{< table "table-striped-columns" >}}

| Field Name      | Type    | Tag | Description                                                   |
|-----------------|---------|-----|---------------------------------------------------------------|
| `timestamp`       | uint64  | 1   | The timestamp when the damage occurred.                       |
| `category`        | string  | 2   | The category of the event, e.g., "player_damaged".            |
| `attacker`        | Player  | 3   | The player who inflicted the damage.                          |
| `victim`          | Player  | 4   | The player who received the damage.                           |
| `weapon`          | string  | 5   | The weapon used to inflict damage.                            |
| `damageInflicted` | uint32  | 6   | The amount of damage inflicted.                               |

{{< /table >}}

### PlayerKilled
{{< alert context="warning" text="**WARNING:** `PlayerKilled.awardedTo` is now `reserved` as of Season 20 update on 2/13/2024." />}}

Sent when a player is killed. Details are similar to the PlayerDamaged event.
{{< table "table-striped-columns" >}}

| Field Name  | Type   | Tag | Description                                    |
|-------------|--------|-----|------------------------------------------------|
| `timestamp` | uint64 | 1   | The timestamp when the player was killed.      |
| `category`  | string | 2   | The category of the event, e.g., "player_killed". |
| `attacker`  | Player | 3   | The player who killed the victim.              |
| `victim`    | Player | 4   | The player who was killed.                     |
| `reserved`    |  | 5   |  formerly Player `awardedTo`           |
| `weapon`    | string | 6   | The weapon used to kill the player.            |

{{< /table >}}

### PlayerDowned

Event describing a player that has been downed after taking sufficient damage.

{{< table "table-striped-columns" >}}

| Field Name  | Type   | Tag | Description                                 |
|-------------|--------|-----|---------------------------------------------|
| `timestamp` | uint64 | 1   | The timestamp when the player was downed.   |
| `category`  | string | 2   | The category of the event, e.g., "player_downed". |
| `attacker`  | Player | 3   | The player who downed the victim.           |
| `victim`    | Player | 4   | The player who was downed.                  |
| `weapon`    | string | 5   | The weapon used to down the player.         |

{{< /table >}}

### PlayerAssist

Sent when a player is killed if there is an assist awarded.

{{< table "table-striped-columns" >}}

| Field Name  | Type   | Tag | Description                                    |
|-------------|--------|-----|------------------------------------------------|
| `timestamp` | uint64 | 1   | The timestamp when the assist was awarded.     |
| `category`  | string | 2   | The category of the event, e.g., "player_assist". |
| `assistant` | Player | 3   | The player who assisted in the kill.           |
| `victim`    | Player | 4   | The player who was killed.                     |
| `weapon`    | string | 5   | The weapon used to assist in the kill.         |

{{< /table >}}

### SquadEliminated

Occurs when the entire squad in a game has been eliminated.

{{< table "table-striped-columns" >}}

| Field Name  | Type      | Tag | Description                                         |
|-------------|-----------|-----|-----------------------------------------------------|
| `timestamp` | uint64    | 1   | The timestamp when the squad was eliminated.        |
| `category`  | string    | 2   | The category of the event, e.g., "squad_eliminated".|
| `players`   | Player[]  | 3   | The players in the squad that was eliminated.       |

{{< /table >}}


### GibraltarShieldAbsorbed

Occurs when Gibraltar's shield has taken any enemy damage.

{{< table "table-striped-columns" >}}

| Field Name       | Type   | Tag | Description                                                |
|------------------|--------|-----|------------------------------------------------------------|
| `timestamp`      | uint64 | 1   | The timestamp when the shield absorbed damage.             |
| `category`       | string | 2   | The category of the event, e.g., "gibraltar_shield_absorbed".|
| `attacker`       | Player | 3   | The player who inflicted damage on the shield.             |
| `victim`         | Player | 4   | Gibraltar, the player using the shield.                    |
| `damageInflicted`| uint32 | 6   | The amount of damage absorbed by the shield.               |

{{< /table >}}

### RevenantForgedShadowDamaged

{{< alert context="success" text="**Important Update**: `RevenantForgedShadowDamaged` was introduced in the Season 20 update on 2/13/2024." />}}

Occurs when Revenant, while using his Forged Shadows ultimate, takes any enemy damage.

{{< table "table-striped-columns" >}}

| Field Name       | Type   | Tag | Description                                                        |
|------------------|--------|-----|--------------------------------------------------------------------|
| `timestamp`      | uint64 | 1   | The timestamp when the Forged Shadow absorbed damage.              |
| `category`       | string | 2   | The category of the event, e.g., "revenant_forged_shadow_damaged". |
| `attacker`       | Player | 3   | The player who inflicted damage on the Forged Shadow.              |
| `victim`         | Player | 4   | Revenant, the player using the Forged Shadows ultimate.            |
| `damageInflicted`| uint32 | 6   | The amount of damage dealt to the Forged Shadow.                   |

{{< /table >}}

