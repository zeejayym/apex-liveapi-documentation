---
title: "InteractionEvents"
description: ""
icon: "code"
date: "2024-02-10T00:44:31+01:00"
lastmod: "2024-02-10T00:44:31+01:00"
draft: false
toc: true
weight: 220
---

## Events

{{< alert context="info" text="This documentation is a work in progress, and we actively welcome contributions. If you have suggestions for improvements or new features, feel free to open a pull request on our GitHub repository. [Contribute here](https://www.github.com/zeejayym/liveapi-documentation). We appreciate your input in making our documentation better for everyone." />}}

### playerRespawnTeam

- **Description**: Called when respawning teammates.

- **Notes**: `{"team":}` is actually the player(s) respawned, seperated by comma.

- **Schema**:

    ```json
    {
    "player": {
        "type": "object",
        "properties":
        {
        "object": {"type": "Player"}
        }
    },
    "respawned": {"type": "string"},
    "timestamp": {"type": "number"},
    "category": "playerRespawnTeam"
    },    
    ```

- **Example:**

```json
{"player":{"name":"GoldGorilla","teamId":16,"pos":{"x":-1061.63,"y":18399.3,"z":-5144.13},"angles":{"x":0,"y":-76.5527,"z":0},"squadIndex":0,"teamName":"Team15","character":"Crypto","skin":"MortalCoil"},"respawned":"XenonXantus","timestamp":1638392689,"category":"playerRespawnTeam"},
```

### playerRevive

- **Description**: Called when a player revives a member, or multiple members of their team.

- **Schema**:

    ```json
    {
        "player": {
        "type": "object",
        "properties":
        {
            "object": {"type": "Player"}
        }
        },
        "revived": {
        "type": "object",
        "properties":
        {
            "object": {"type": "Player"}
        }
        },
        "timestamp": {"type": "number"},
        "category": "playerRevive"
    },
    ```

- **Example:**

```json
{"player":{"name":"XenonXantus","teamId":16,"pos":{"x":-9534.92,"y":12763.7,"z":-5974.84},"angles":{"x":0.00559509,"y":-19.3241,"z":-0.00561655},"squadIndex":2,"teamName":"Team15","character":"Revenant","skin":"SacredDivinity"},"revived":{"name":"GermaniumGazelle","teamId":16,"pos":{"x":-9505.75,"y":12753.3,"z":-5974.84},"angles":{"x":0,"y":163.169,"z":0},"squadIndex":1,"teamName":"Team15","character":"Rampart","skin":"Packin'Paisley"},"timestamp":1638392803,"category":"playerRevive"},
```

### inventoryPickUp

- **Description**: Called when a player picks up an item.

- **Schema**:

    ```json  
    {
        "player": {
        "type": "object",
        "properties":
        {
            "object": {"type": "Player"}
        }
        },
        "item": {"type": "string"},
        "quantity": {"type": "number"},
        "timestamp": {"type": "number"},
        "category": "inventoryPickUp"
    },
    ```

- **Example:**

```json
{"player":{"name":"NeodymiumNightingale","teamId":17,"pos":{"x":-13724.5,"y":-16733.3,"z":-5566.75},"angles":{"x":0,"y":94.4385,"z":0},"squadIndex":1,"teamName":"Team16","character":"Fuse","skin":"TropicStreak"},"item":"Syringe","quantity":2,"timestamp":1638392794,"category":"inventoryPickUp"},
```

### inventoryDrop

- **Description**: Called when a player drops an item.

- **Notes**: `extraData` is called when additional weapon atachments are dropped along with the weapon.


- **Schema**:

    ```json  
    {
        "player": {
        "type": "object",
        "properties":
        {
            "object": {"type": "Player"}
        }
        },
        "item": {"type": "string"},
        "extraData": {
            "type": "array",
            "items": {"type": "string"}
        },
        "quantity": {"type": "number},
        "timestamp": {"type": "number},
        "category": "inventoryDrop"
    },
    ```

- **Example:**

```json
{"player":{"name":"SilverSabertoothedcat","teamId":15,"pos":{"x":-7204,"y":12019,"z":-5884.25},"angles":{"x":0,"y":47.1533,"z":0},"squadIndex":0,"teamName":"Team14","character":"Mirage","skin":"Orchid"},"item":"ShotgunShells","quantity":16,"timestamp":1638392819,"category":"inventoryDrop"},
```

### inventoryUse

- **Description**: Called when a player uses an item.

- **Schema**:

    ```json  
    {
        "player": {
        "type": "object",
        "properties":
        {
            "object": {"type": "Player"}
        }
        },
        "item": {"type": "string"},
        "quantity": {"type": "number},
        "timestamp": {"type": "number},
        "category": "inventoryUse"
    },
    ```

- **Example:**

```json
{"player":{"name":"OsmiumOctopus","teamId":11,"pos":{"x":-5499.93,"y":-16464.7,"z":-5995.5},"angles":{"x":0,"y":12.041,"z":0},"squadIndex":0,"teamName":"Team10","character":"Lifeline","skin":"Purgatory"},"item":"ShieldCell","quantity":1,"timestamp":1638392824,"category":"inventoryUse"},
```

### bannerCollected


- **Description**: Called when a player collects a banner from their teammate's deathbox.

- **Notes**: `playerOne` is who collected the banner and `playerTwo` is who's banner was collected.

- **Schema**:

    ```json  
    {
        "player": {
        "type": "object",
        "properties":
        {
            "object": {"type": "Player"}
        }
        },
        "collected": {
        "type": "object",
        "properties":
        {
            "object": {"type": "Player"}
        }
        },
        "timestamp": {"type": "number"},
        "category": "bannerCollected"
    },
    ```

- **Example:**

```json
{"player":{"name":"LanthanumLoon","teamId":20,"pos":{"x":10257.2,"y":-9799.83,"z":-5232},"angles":{"x":0,"y":-179.566,"z":0},"squadIndex":2,"teamName":"Team19","character":"Lifeline","skin":"CheckeredPast"},"collected":{"name":"FleroviumFowl","teamId":20,"pos":{"x":-4599.63,"y":1747,"z":-6074.25},"angles":{"x":0,"y":59.2383,"z":0},"squadIndex":0,"teamName":"Team19","character":"Ash","skin":"Arctic"},"timestamp":1638392519,"category":"bannerCollected"},
```

### playerAbilityUsed

- **Description**: Called when a player uses a character ability.

- **Schema**:

    ```json  
    {
        "player": {
        "type": "object",
        "properties":
        {
            "object": {"type": "Player"}
        }
        },
        "linkedEntity": {"type": "string"},
        "timestamp":  {"type": "number"},
        "category": "playerAbilityUsed"
    },
    ```

- **Example:**

```json
{"player":{"name":"KryptonKrill","teamId":8,"pos":{"x":-3486.47,"y":-2680.73,"z":-6328},"angles":{"x":0,"y":-4.8019,"z":0},"squadIndex":1,"teamName":"Team07","character":"Fuse","skin":"Scallywag"},"linkedEntity":"Tactical(KnuckleCluster)","timestamp":1638392519,"category":"playerAbilityUsed"},
```

### ziplineUsed

- **Description**: Called when a player uses a zipline, either one in map, or Pathfinder's.

- **Schema**:

    ```json
    {
        "player": {
        "type": "object",
        "properties":
        {
            "object": {"type": "Player"}
        }
        },
        "linkedEntity": {"type": "string"},
        "timestamp": {"type": "number"},
        "category": "ziplineUsed"
    },
    ```

- **Example:**

```json
{"player":{"name":"DarmstadtiumDolphin","teamId":17,"pos":{"x":-8071.9,"y":-24911,"z":-4458.88},"angles":{"x":0,"y":112.804,"z":0},"squadIndex":2,"teamName":"Team16","character":"Horizon","skin":"Clearwater"},"linkedEntity":"zipline","timestamp":1638392570,"category":"ziplineUsed"},
```

### grenadeThrown

- **Description**: Called when a grenade is thrown.

- **Note**: This will also be called on for certain abilities from legends.

- **Schema**:

    ```json
    {
        "player": {
        "type": "object",
        "properties":
        {
        "object": {"type": "Player"}
        }
        },
        "linkedEntity": {"type": "string"},
        "timestamp": {"type": "number"},
        "category": "grenadeThrown"
    },
    ```

- **Example:**

```json
{"player":{"name":"AntimonyAsp","teamId":8,"pos":{"x":-4406.1,"y":-2354.71,"z":-6327.97},"angles":{"x":0,"y":86.4844,"z":0},"squadIndex":0,"teamName":"Team07","character":"Bangalore","skin":"CrimsonQueen"},"linkedEntity":"Tactical(#WPN_GRENADE_ELECTRIC_SMOKE_SHORT)","timestamp":1638392573,"category":"grenadeThrown"},
```

### blackMarketAction

- **Description**: Called when Loba's Black Market is used by a player.

- **Schema**:

    ```json
    {
        "player": {
        "type": "object",
        "properties":
        {
            "object": {"type": "Player"}
        }
        },
        "item": {"type": "string"},
        "timestamp": {"type": "number"},
        "category": "blackMarketAction"
    }
    ```

- **Example:**

```json
{"player":{"name": "(1)Hellhavens","teamId": 2,"teamName": "Team 01","squadIndex": 0},"item": "Evo Shield (Level 3)","timestamp": 1633047651,"category": "blackMarketAction"},
```

### wraithPortal

- **Description**: Called when using a portal created by Wraith.

- **Schema**:

    ```json
    {
        "player": {
        "type": "object",
        "properties":
        {
            "object": {"type": "Player"}
        }
        },
        "timestamp": {"type": "number"},
        "category": "wraithPortal"
    }
    ```

- **Example:**

```json
{"player":{"name":"ZirconiumZorilla","teamId":9,"pos":{"x":16055.1,"y":-4361.33,"z":-4936},"angles":{"x":0,"y":-172.187,"z":0},"squadIndex":1,"teamName":"Team08","character":"Wraith","skin":"RoyalGuard"},"timestamp":1638392720,"category":"wraithPortal"},
```

### ammoUsed

- **Description**: Called on weapon reload.

- **Schema**:

    ```json
    {
        "player": {
        "type": "object",
        "properties":
        {
            "object": {"type": "Player"}
        }
        },
        "ammoType":{"type": "string"},
        "amountUsed":{"type": "number"},
        "oldAmmoCount":{"type": "number"},
        "newAmmoCount":{"type": "number"},
        "timestamp": {"type": "number"},
        "category": "ammoUsed"
    }
    ```

- **Example:**

```json
{"player":{"name":"BotAPZincZebra","teamId":2,"pos":{"x":31864.7,"y":7952.82,"z":-3371.57},"angles":{"x":0,"y":-35.9797,"z":0},"teamName":"Team1","squadIndex":2,"nucleusHash":"22686ffa854e16ef7655c417d6bd994eac96a0f390065e74072e693c61703f12249c50d0dd34da80427b9ddfeba6cfc8016f1ef9ee9294fd89a8bf43ac494746","character":"Valkyrie","skin":"HypnoticNightmare"},"ammoType":"bullet","amountUsed":16,"oldAmmoCount":20,"newAmmoCount":4,"timestamp":1640211857,"category":"ammoUsed"},
```

### weaponSwitched

- **Description**: Called when the player changes in-hand item.

- **Note**: Note: `"oldWeapon": {"type": "string"}` will be null/missing if the its the first `weaponSwitched` event


- **Schema**:

    ```json  
    {
        "player": {
        "type": "object",
        "properties":
        {
            "object": {"type": "Player"}
        }
        },
        "newWeapon": {"type": "string"},
        "oldWeapon": {"type": "string"},
        "timestamp": {"type": "number"},
        "category": "weaponSwitched"
    }
    ```

- **Example:**

```json
{"player":{"name":"BotAPNitrogenNightingale","teamId":9,"pos":{"x":6052.5,"y":-22977,"z":-4065.5},"angles":{"x":0,"y":159.214,"z":0},"teamName":"Team8","squadIndex":2,"nucleusHash":"8a76eb4b4e9c40e250cff9d52c1fb9918b3537fe88ebf1160735c21f00d1264debca5c5e012c33af1be35469da787833eed527f69f8eb9b7813d95f24d028deb","character":"Revenant","skin":"NecroNightmare"},"newWeapon":"mp_weapon_revenant_scythe_primary","timestamp":1646863063,"category":"weaponSwitched"},
```
