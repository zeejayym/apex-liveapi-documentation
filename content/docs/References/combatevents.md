---
title: "CombatEvents"
description: ""
icon: "code"
date: "2023-05-22T00:44:31+01:00"
lastmod: "2023-05-22T00:44:31+01:00"
draft: false
toc: true
weight: 210
---

## Events

{{< alert context="info" text="This documentation is a work in progress, and we actively welcome contributions. If you have suggestions for improvements or new features, feel free to open a pull request on our GitHub repository. [Contribute here](https://www.github.com/zeejayym/live-api-documentation). We appreciate your input in making our documentation better for everyone." />}}

### playerDamaged

- **Description**: Called when a player damages another player.
- **Schema**:

  ```json
  {
    "attacker": {
        "type": "object",
        "properties": {
            "name": {"type": "string"},
            "teamId": {"type": "integer"}
        }
    },
    "victim": {
        "type": "object",
        ...
    },
    "damage": {"type": "number"},
    "weapon": {"type": "string"}
  }
  ```

- **Example:**

```json
{"attacker":{"name":"OsmiumOctopus","teamId":11,"pos":{"x":6575,"y":-23746.4,"z":-5431.75},"angles":{"x":0,"y":-71.8506,"z":0},"squadIndex":0,"teamName":"Team10","character":"Lifeline","skin":"Purgatory"},"victim":{"name":"ArgonAnteater","teamId":7,"pos":{"x":6562.25,"y":-23790.6,"z":-5431.75},"angles":{"x":0,"y":-177.813,"z":0},"squadIndex":0,"teamName":"Team06","character":"Gibraltar","skin":"Shell-Shocked"},"weapon":"Melee","damageInflicted":26,"timestamp":1638392459,"category":"playerDamaged"},
```

### playerKilled

- **Description**: Called when a player dies.

- **Schema**:

  ```json
  {
    "attacker": {
      "type": "object",
      "properties":
      {
         "object": {"type": "player"}
      }
    },
    "victim": {
      "type": "object",
      "properties":
      {
         "object": {"type": "player"}
      }
    },
    "awardedTo": {
      "type": "object",
      "properties":
      {
         "object": {"type": ["player", null] }
      }
    },
    "weapon": {"type": "string"},
    "timestamp": {"type": "number"},
    "category": "playerKilled"
  },
  ```

- **Example:**

```json
{"attacker":{"name":"World"},"victim":{"name":"RadonRattlesnake","teamId":11,"pos":{"x":6154.77,"y":-22605.4,"z":-4178.88},"angles":{"x":0,"y":103.667,"z":0},"squadIndex":1,"teamName":"Team10","character":"Seer","skin":"Heartthrob"},"awardedTo":{},"weapon":"OutofBounds","timestamp":1638392462,"category":"playerKilled"},
```

### playerDowned

- **Description**: Called when a player is downed by another player.

- **Schema**:

  ```json
  {
    "attacker": {
      "type": "object",
      "properties":
      {
        "object": {"type": "Player"}
      }
    },
    "victim": {
      "type": "object",
      "properties":
      {
        "object": {"type": "Player"}
      }
    },
    "weapon": {"type": "string"},
    "timestamp": {"type": "number"},
    "category": "playerDowned"
  },
  ```

- **Example:**

```json
{"attacker":{"name":"MendeleviumMollusk","teamId":6,"pos":{"x":-3082.84,"y":13232.1,"z":-5796.22},"angles":{"x":0,"y":177.231,"z":0},"squadIndex":2,"teamName":"Team05","character":"Gibraltar","skin":"Bloodline"},"victim":{"name":"KryptonKingfisher","teamId":2,"pos":{"x":-3115.94,"y":13234.2,"z":-5784.75},"angles":{"x":0,"y":-2.59277,"z":0},"squadIndex":2,"teamName":"Team01","character":"Revenant","skin":"Arachnophobia"},"weapon":"WarClubMelee","timestamp":1638392486,"category":"playerDowned"},
```

### squadEliminated

- **Description**: Called when a full team has been eliminated.

- **Schema**:

  ```json
  {
    "players": {
      "type": "array",
      "object": {"type": "player"}
    },
    "timestamp": {"type": "number"},
    "category": "squadEliminated"
  },
  ```

- **Example:**

```json
{"players":[{"name":"BotAPHafniumHummingbird","teamId":16,"pos":{"x":4564.75,"y":-17402.4,"z":-3401},"angles":{"x":0,"y":134.121,"z":0},"teamName":"Team15","squadIndex":1,"nucleusHash":"1b03b708270067e4f1c92dacaf37abd51288a2b5297ccf986307984890750595565adae06c316601e36f33fec4c2774666a83a1237bd2aa2fcbe94aa36368908","character":"Bangalore","skin":"ElectricSynapse"},{"name":"BotAPRadonRattlesnake","teamId":16,"pos":{"x":425.171,"y":236.259,"z":-3211.37},"angles":{"x":0,"y":-110.523,"z":0},"teamName":"Team15","squadIndex":2,"nucleusHash":"8e5107d26d9275c0c1b8dfa414c0fd2e3c00781d259261981d8f51ed484447955b54c8a47ce924bb0c45c62f5b04ad50b9d77a3ac67309a40f9fb9ceebeccc0b","character":"Octane","skin":"ElDiablo"},{"name":"BotAPGadoliniumGazelle","teamId":16,"pos":{"x":-757.1,"y":-1434.89,"z":-3381.13},"angles":{"x":0,"y":119.839,"z":0},"teamName":"Team15","squadIndex":0,"nucleusHash":"56df39b9c339d2b4c5adf089ef03e549d806de3fc0e91ec1f518ecdb4a30107629de033024595acf8277bf20fddc6f9c66adfdf2f9ee0ae69b1e49abacc61b1b","character":"Mirage","skin":"StuntDouble"}],"timestamp":1646863133,"category":"squadEliminated"},

```
