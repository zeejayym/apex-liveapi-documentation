---
title: "MatchInformation"
description: ""
icon: "code"
date: "2024-02-10T00:44:31+01:00"
lastmod: "2024-02-10T00:44:31+01:00"
draft: false
toc: true
weight: 230
---
## Events

{{< alert context="info" text="This documentation is a work in progress, and we actively welcome contributions. If you have suggestions for improvements or new features, feel free to open a pull request on our GitHub repository. [Contribute here](https://www.github.com/zeejayym/live-api-documentation). We appreciate your input in making our documentation better for everyone." />}}

### matchSetup

- **Description**: Prints list of match information on match start

- **Note**: `targetTeam` will list all players on that team.

- **Schema**:

  ```json
  {
    "map": {"type": "string"},
    "playlistName": {"type": "string"},
    "playlistDesc": {"type": "string"},
    "datacenter": 
      {
        "name": {"type": "string"}
      }
    ,
    "aimAssistOn": {"type": "boolean"},
    "serverId": {"type": "number"},
    "timestamp": {"type": "number"},
    "category": "matchSetup"
  },
  ```

- **Example:**

```json
{"map":"mp_rr_olympus_mu1","playlistName":"Olympus(Season9)","playlistDesc":"Fighttobethelastsquadstanding.","datacenter":{"name":"westus"},"aimAssistOn":true,"serverId":"838911:1000:00000000","timestamp":1638392356,"category":"matchSetup"},
```

### gameStateChanged

- **Description**: Called when, waiting for player, character select, match start, resolution, match end.

- **Schema**:

  ```json
  {
    "state": {"type": "string"},
    "timestamp": {"type": "number"},
    "category": "gameStateChanged"
  },
  ```

- **Example:**

```json
{"state":"PickLoadout","timestamp":1638392379,"category":"gameStateChanged"},
```

### characterSelected

- **Description**: Called during character select.

- **Schema**:

  ```json
  {
    "player":{
     "type": "object",
     "properties":
      {
        "object": {"type": "player"}
      }
    },
    "timestamp": {"type": "number"},
    "category": "characterSelected"
  },

  ```

- **Example:**

```json
{"player":{"name":"StrontiumSquirrel","teamId":21,"pos":{"x":-4599.63,"y":1747,"z":-6074.25},"angles":{"x":0,"y":0,"z":0},"squadIndex":0,"teamName":"Team20","character":"Seer","skin":"Wishbone"},"timestamp":1638392385,"category":"characterSelected"},
```

### matchStateEnd

- **Description**: Winner names separated by comma.

- **Schema**:

  ```json
  {
    "state": "WinnerDetermined",
    "winners": { 
     "type": "array",
     "object": {"type": "player"}
     },
    "timestamp": {"type": "number"},
    "category": "matchStateEnd"
  },

  ```

- **Example:**

```json
{"state":"WinnerDetermined","winners":[{"name":"BotAPZincZebra","teamId":10,"pos":{"x":-4078.81,"y":-10303.9,"z":-4095.95},"angles":{"x":0,"y":-139.746,"z":0},"teamName":"Team9","squadIndex":2,"nucleusHash":"22686ffa854e16ef7655c417d6bd994eac96a0f390065e74072e693c61703f12249c50d0dd34da80427b9ddfeba6cfc8016f1ef9ee9294fd89a8bf43ac494746","character":"MadMaggie","skin":"Snakeskin"},{"name":"BotAPLivermoriumLeech","teamId":10,"pos":{"x":4564.75,"y":-17402.4,"z":-3401},"angles":{"x":0,"y":-56.6455,"z":0},"teamName":"Team9","squadIndex":1,"nucleusHash":"f0b2e9d56100ed8bc9202216ae69f1dbf995fbcd8456a565479d9d3bfd5fe9a777a7bd5ddb1e069342b64137436467ef3445fbea132a7edc05172af2cebee14e","character":"Seer","skin":"Limelight"},{"name":"BotAPLanthanumLoon","teamId":10,"pos":{"x":4564.75,"y":-17402.4,"z":-3401},"angles":{"x":0,"y":-103.887,"z":0},"teamName":"Team9","squadIndex":0,"nucleusHash":"fa7e56bc4c966d656cd9817706c66848644d69051f7bdf71605d5d81002bb7d6455f35d288e8e6c7cb125cf8118f9d77c4911d05b6e1451e7b6ded04a97d074c","character":"Gibraltar","skin":"Bloodline"}],"timestamp":1646863807,"category":"matchStateEnd"},

```


### ringStartClosing

- **Description**: Called when the circle starts closing.

- **Schema**:

  ```json
  {
    "stage": {"type": "number"},
    "timestamp": {"type": "number"},
    "category": "ringStartClosing"
  },
  ```

- **Example:**

```json
{"stage":0,"timestamp":1638392668,"category":"ringStartClosing"},
```

### ringFinishedClosing

- **Description**: Called when the circle closes.

- **Schema**:

  ```json
  {
    "stage": {"type": "number"},
    "timestamp": {"type": "number"},
    "category": "ringFinishedClosing"
  },
  ```

- **Example:**

```json
{"stage":0,"timestamp":1638392668,"category":"ringFinishedClosing"},
```

### playerConnected

- **Description**: Called when a player connects to the server.

- **Schema**:
  ```json
  {
    "player": {
     "type": "object",
     "properties":
      {
       "object": {"type": "player"}
      }
    },
    "timestamp":  {"type": "number"},
    "category": "playerConnected"
  },
  ```

- **Example:**

```json
{"player":{"name":"AntimonyAsp","teamId":8,"pos":{"x":-4599.63,"y":1747,"z":-6074.25},"angles":{"x":0,"y":0,"z":0},"squadIndex":0,"teamName":"Team07"},"timestamp":1638392355,"category":"playerConnected"},
```

### playerDisconnected

- **Description**: Called when a player leaves the server..

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
    "timestamp":  {"type": "number"},
    "category": "playerDisconnected"
  },
  ```

- **Example:**

```json
{"player":{"name":"ArgonAnteater","teamId":7,"pos":{"x":-4599.63,"y":1747,"z":-6074.25},"angles":{"x":0,"y":107.666,"z":0},"squadIndex":0,"character":"Gibraltar","skin":"Shell-Shocked"},"timestamp":1638393256,"category":"playerDisconnected"},

```


### playerStatChanged

- **Description**: Called when a players stat has been updated.

- **Notes**: Tracks changes in kills, assists, revives given and respawns given

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
    "statName":  {"type": "string"},
    "newValue":  {"type": "number"},
    "timestamp":  {"type": "number"},
    "category": "playerStatChanged"
  },
  ```

- **Example:**

```json
{"player":{"name":"Dresav","teamId":5,"pos":{"x":41305.1,"y":10671.5,"z":7405.44},"angles":{"x":0,"y":104.484,"z":0},"teamName":"Razer","squadIndex":0,"nucleusHash":"742914e6251d6d5eba1edc86078773ab4e89f95201a8036abdafcb2075b0279e81f0c48c399306c3a9cbab02b96bfdc7a151aa9dbd2578b3ae9d62d9d81b1b8c","character":"Gibraltar","skin":"GoldenGuardian"},"statName":"kills","newValue":4,"timestamp":1648604082,"category":"playerStatChanged"},
```

