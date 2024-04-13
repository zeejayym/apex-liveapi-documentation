---
title: "ObserverEvents"
description: ""
icon: "code"
date: "2024-02-10T00:44:31+01:00"
lastmod: "2024-02-10T00:44:31+01:00"
draft: false
toc: true
weight: 240
---

{{< alert context="info" text="This documentation is a work in progress, and we actively welcome contributions. If you have suggestions for improvements or new features, feel free to open a pull request on our GitHub repository. [Contribute here](https://www.github.com/zeejayym/apex-liveapi-documentation). We appreciate your input in making our documentation better for everyone." />}}

## Messages

### ObserverSwitched

Event when the observer camera switches from viewing one player to another

{{< table "table-striped-columns" >}}

| Field Name   | Type          | Tag | Description                                                                  |
|--------------|---------------|-----|------------------------------------------------------------------------------|
| `timestamp`    | uint64        | 1   | The timestamp when the observer camera switch occurred.                      |
| `category`     | string        | 2   | The category of the event, e.g., "observer_switched".                        |
| `observer`     | Player        | 3   | The observer who is switching the view.                                      |
| `target`       | Player        | 4   | The new target player that the observer camera is switching to.              |
| `targetTeam`   | Player[]      | 5   | A list of `Player` objects representing the team of the new target player.   |

{{< /table >}}

### ObserverAnnotation

Used by observers to annotate events uniquely

{{< table "table-striped-columns" >}}

| Field Name        | Type   | Tag | Description                                                      |
|-------------------|--------|-----|------------------------------------------------------------------|
| `timestamp`         | uint64 | 1   | The timestamp when the annotation was made.                      |
| `category`          | string | 2   | The category of the event, e.g., "observer_annotation".          |
| `annotationSerial`  | int32  | 3   | A serial number uniquely identifying the annotation event.       |

{{< /table >}}
