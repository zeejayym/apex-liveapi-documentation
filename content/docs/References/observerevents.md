---
title: "ObserverEvents"
description: ""
icon: "code"
date: "2023-05-22T00:44:31+01:00"
lastmod: "2023-05-22T00:44:31+01:00"
draft: false
toc: true
weight: 249
---

## Events

{{< alert context="info" text="This documentation is a work in progress, and we actively welcome contributions. If you have suggestions for improvements or new features, feel free to open a pull request on our GitHub repository. [Contribute here](https://www.github.com/zeejayym/live-api-documentation). We appreciate your input in making our documentation better for everyone." />}}

### observerSwitched

- **Description**: Called when the player switches to another observer target.

- **Note**: `targetTeam` will list all players on that team.

- **Schema**:

  ```json
  {
    "observer": {
        "type": "object",
        "properties":
        {
            "object": {"type": "player"},
        }
    },
    "target": {
        "type": "object",
        "properties":
        {
            "object": {"type": "player"},
        }
    },
    "targetTeam": {
        "type": "array",
        "object": {"type": "player"}
    },
    "timestamp": {"type": "number"},
    "category": "observerSwitched"
  },
  ```

- **Example:**

```json
{"observer":{"name":"unnamed","teamId":1,"pos":{"x":-4599.63,"y":1747,"z":-6074.25},"angles":{"x":0,"y":0,"z":0},"squadIndex":0,"teamName":"Spectator","character":"Bloodhound","skin":"Original"},"target":{"name":"AntimonyAsp","teamId":8,"pos":{"x":-23004,"y":19100.6,"z":-6327},"angles":{"x":0,"y":126.475,"z":0},"squadIndex":0,"teamName":"Team07","character":"Bangalore","skin":"CrimsonQueen"},"timestamp":1638392421,"category":"observerSwitched"},
```