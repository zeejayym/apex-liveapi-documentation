---
title: "InteractionEvents"
description: ""
icon: "code"
date: "2024-02-10T00:44:31+01:00"
lastmod: "2024-02-10T00:44:31+01:00"
draft: false
toc: true
weight: 230
---

{{< alert context="info" text="This documentation is a work in progress, and we actively welcome contributions. If you have suggestions for improvements or new features, feel free to open a pull request on our GitHub repository. [Contribute here](https://www.github.com/zeejayym/apex-liveapi-documentation). We appreciate your input in making our documentation better for everyone." />}}

## Messages

### PlayerRespawnTeam

Sent when a player is respawned and comes back into the game.

{{< table "table-striped-columns" >}}

| Field Name   | Type   | Tag | Description                                            |
|--------------|--------|-----|--------------------------------------------------------|
| `timestamp`  | uint64 | 1   | The timestamp when the player was respawned.           |
| `category`   | string | 2   | The category of the event, e.g., "player_respawn_team".|
| `player`     | Player | 3   | The player who was respawned.                    

{{< /table >}}

### PlayerRevive

Occurs when a player finishes assisting a downed player.

{{< table "table-striped-columns" >}}

| Field Name  | Type   | Tag | Description                                        |
|-------------|--------|-----|----------------------------------------------------|
| `timestamp` | uint64 | 1   | The timestamp when the revive occurred.            |
| `category`  | string | 2   | The category of the event, e.g., "player_revive".  |
| `player`    | Player | 3   | The player performing the revive.                  |
| `revived`   | Player | 4   | The player who was revived.                        |

{{< /table >}}

### ArenasItemSelected

Specific Arenas-only event that occurs when players select an item.

{{< table "table-striped-columns" >}}

| Field Name  | Type    | Tag | Description                                                 |
|-------------|---------|-----|-------------------------------------------------------------|
| `timestamp` | uint64  | 1   | The timestamp when the item was selected.                 |
| `category`  | string  | 2   | The category of the event, e.g., "arenas_item_selected".  |
| `player`    | Player  | 3   | The player who selected the item.                         |
| `item`      | string  | 4   | The item selected.                                        |
| `quantity`  | int32   | 5   | The quantity of the item selected.                        |

{{< /table >}}

### ArenasItemDeselected

Specific Arenas-only event that occurs when players deselect an item.

{{< table "table-striped-columns" >}}

| Field Name  | Type    | Tag | Description                                                 |
|-------------|---------|-----|-------------------------------------------------------------|
| `timestamp` | uint64  | 1   | The timestamp when the item was deselected.                 |
| `category`  | string  | 2   | The category of the event, e.g., "arenas_item_deselected".  |
| `player`    | Player  | 3   | The player who deselected the item.                         |
| `item`      | string  | 4   | The item deselected.                                        |
| `quantity`  | int32   | 5   | The quantity of the item deselected.                        |

{{< /table >}}

### InventoryPickUp

Event that occurs when a player has picked up loot into their inventory.

{{< table "table-striped-columns" >}}

| Field Name  | Type    | Tag | Description                                      |
|-------------|---------|-----|--------------------------------------------------|
| `timestamp` | uint64  | 1   | The timestamp when the item was picked up.       |
| `category`  | string  | 2   | The category of the event, e.g., "inventory_pick_up". |
| `player`    | Player  | 3   | The player who picked up the item.               |
| `item`      | string  | 4   | The item picked up.                              |
| `quantity`  | int32   | 5   | The quantity of the item picked up.              |

{{< /table >}}

### InventoryDrop

Event that occurs when a player has dropped loot from their inventory.

{{< table "table-striped-columns" >}}

| Field Name   | Type      | Tag | Description                                      |
|--------------|-----------|-----|--------------------------------------------------|
| `timestamp`  | uint64    | 1   | The timestamp when the item was dropped.         |
| `category`   | string    | 2   | The category of the event, e.g., "inventory_drop". |
| `player`     | Player    | 3   | The player who dropped the item.                 |
| `item`       | string    | 4   | The item dropped.                                |
| `quantity`   | int32     | 5   | The quantity of the item dropped.                |
| `extraData`  | string[]  | 6   | Any attachments or extra data related to the item.|

{{< /table >}}

### InventoryUse

Used to indicate the player has used a consumable item from their inventory.

{{< table "table-striped-columns" >}}

| Field Name  | Type    | Tag | Description                                         |
|-------------|---------|-----|-----------------------------------------------------|
| `timestamp` | uint64  | 1   | The timestamp when the consumable item was used.    |
| `category`  | string  | 2   | The category of the event, e.g., "inventory_use".   |
| `player`    | Player  | 3   | The player who used the item.                       |
| `item`      | string  | 4   | The consumable item used.                           |
| `quantity`  | int32   | 5   | The quantity of the item used.                      |

{{< /table >}}

### BannerCollected

Event used when a teammate banner has been picked up.

{{< table "table-striped-columns" >}}

| Field Name   | Type    | Tag | Description                                    |
|--------------|---------|-----|------------------------------------------------|
| `timestamp`  | uint64  | 1   | The timestamp when the banner was collected.   |
| `category`   | string  | 2   | The category of the event, e.g., "banner_collected". |
| `player`     | Player  | 3   | The player who collected the banner.           |
| `collected`  | Player  | 4   | The player whose banner was collected.         |

{{< /table >}}

### PlayerAbilityUsed

Used to indicate that the player has activated one of their legend's abilities.

{{< table "table-striped-columns" >}}

| Field Name     | Type    | Tag | Description                                                     |
|----------------|---------|-----|-----------------------------------------------------------------|
| `timestamp`    | uint64  | 1   | The timestamp when the ability was used.                        |
| `category`     | string  | 2   | The category of the event, e.g., "player_ability_used".         |
| `player`       | Player  | 3   | The player who used the ability.                                |
| `linkedEntity` | string  | 4   | The specific ability used, e.g., "Tactical (Eye of the Allfather)" for Bloodhound's tactical.|

{{< /table >}}

### LegendUpgradeSelected

{{< alert context="success" text="**Important Update**: `LegendUpgradeSelected` was introduced in the Season 20 update on 2/13/2024." />}}

Signals that a player has selected an upgrade at a particular tier level.

{{< table "table-striped-columns" >}}

| Field Name     | Type    | Tag | Description                                              |
|----------------|---------|-----|----------------------------------------------------------|
| `timestamp`    | uint64  | 1   | The timestamp when the upgrade was selected.             |
| `category`     | string  | 2   | The category of the event, e.g., "legend_upgrade_selected". |
| `player`       | Player  | 3   | The player who selected the upgrade.                     |
| `upgradeName`  | string  | 4   | The name of the upgrade selected.                        |
| `upgradeDesc`  | string  | 5   | The description of the upgrade selected.                 |
| `level`        | int32   | 6   | The tier level of the upgrade.                           |

{{< /table >}}

### ZiplineUsed

Indicates that a player has started using the zipline.

{{< table "table-striped-columns" >}}

| Field Name     | Type    | Tag | Description                                         |
|----------------|---------|-----|-----------------------------------------------------|
| `timestamp`    | uint64  | 1   | The timestamp when the zipline was used.            |
| `category`     | string  | 2   | The category of the event, e.g., "zipline_used".    |
| `player`       | Player  | 3   | The player who used the zipline.                    |
| `linkedEntity` | string  | 4   | The specific zipline used, if identifiable.         |

{{< /table >}}

### GrenadeThrown

Used to indicate that a player has tossed a grenade.

{{< table "table-striped-columns" >}}

| Field Name     | Type    | Tag | Description                                                      |
|----------------|---------|-----|------------------------------------------------------------------|
| `timestamp`    | uint64  | 1   | The timestamp when the grenade was thrown.                       |
| `category`     | string  | 2   | The category of the event, e.g., "grenade_thrown".               |
| `player`       | Player  | 3   | The player who threw the grenade.                                |
| `linkedEntity` | string  | 4   | The type of grenade or ability used, e.g., "Ultimate (Rolling Thunder)" for Bangalore's ultimate.|

{{< /table >}}

### BlackMarketAction

Event specifying that a player has picked up loot from Loba's Black Market. This event may fire in quick succession to the InventoryPickUp event.


{{< table "table-striped-columns" >}}

| Field Name  | Type   | Tag | Description                                        |
|-------------|--------|-----|----------------------------------------------------|
| `timestamp` | uint64 | 1   | The timestamp when the action occurred.            |
| `category`  | string | 2   | The category of the event, e.g., "black_market_action". |
| `player`    | Player | 3   | The player who interacted with the Black Market.   |
| `item`      | string | 4   | The item picked up from the Black Market.          |

{{< /table >}}


### WraithPortal

Used to indicate a player has traversed a Wraith Portal.


{{< table "table-striped-columns" >}}

| Field Name  | Type   | Tag | Description                                         |
|-------------|--------|-----|-----------------------------------------------------|
| `timestamp` | uint64 | 1   | The timestamp when the Wraith Portal was used.      |
| `category`  | string | 2   | The category of the event, e.g., "wraith_portal".   |
| `player`    | Player | 3   | The player who traversed the Wraith Portal.         |

{{< /table >}}


### WarpGateUsed

Used to indicate a player has traversed a Warp Gate.


{{< table "table-striped-columns" >}}

| Field Name  | Type   | Tag | Description                                      |
|-------------|--------|-----|--------------------------------------------------|
| `timestamp` | uint64 | 1   | The timestamp when the Warp Gate was used.       |
| `category`  | string | 2   | The category of the event, e.g., "warp_gate_used". |
| `player`    | Player | 3   | The player who used the Warp Gate.               |

{{< /table >}}


### AmmoUsed

Used to indicate that a player has used ammo. This event may not fire immediately and updates may be batched to save bandwidth.


{{< table "table-striped-columns" >}}

| Field Name    | Type    | Tag | Description                                                    |
|---------------|---------|-----|----------------------------------------------------------------|
| `timestamp`   | uint64  | 1   | The timestamp when ammo was used.                              |
| `category`    | string  | 2   | The category of the event, e.g., "ammo_used".                  |
| `player`      | Player  | 3   | The player who used the ammo.                                  |
| `ammoType`    | string  | 4   | The type of ammo used.                                         |
| `amountUsed`  | uint32  | 5   | The amount of ammo used.                                       |
| `oldAmmoCount`| uint32  | 6   | The ammo count before usage.                                   |
| `newAmmoCount`| uint32  | 7   | The ammo count after usage.                                    |

{{< /table >}}


### WeaponSwitched

Used to indicate that a player has switched weapons, either to a weapon in their inventory or swapped with a weapon on the ground.


{{< table "table-striped-columns" >}}

| Field Name   | Type   | Tag | Description                                                    |
|--------------|--------|-----|----------------------------------------------------------------|
| `timestamp`  | uint64 | 1   | The timestamp when the weapon switch occurred.                 |
| `category`   | string | 2   | The category of the event, e.g., "weapon_switched".            |
| `player`     | Player | 3   | The player who switched weapons.                               |
| `oldWeapon`  | string | 4   | The weapon switched from.                                      |
| `newWeapon`  | string | 5   | The weapon switched to.                                        |

{{< /table >}}

