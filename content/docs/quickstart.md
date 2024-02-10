---
weight: 100
date: "2024-02-10T22:37:22+01:00"
draft: false
author: "ZJ"
title: "Quickstart Guide for LiveAPI 2.0 with Python"
icon: "rocket_launch"
toc: true
description: "Get started with LiveAPI 2.0 using Python. This guide provides a comprehensive introduction to the LiveAPI 2.0 using Python."
publishdate: "2023-05-03T22:37:22+01:00"
tags: ["Beginners"]
---

This guide provides a comprehensive introduction to using Apex Legends' LiveAPI 2.0 with Python, aimed at developers interested in building applications that interact with Apex Legends data in real-time.

{{< alert context="info" text="This documentation is a work in progress, and we actively welcome contributions. If you have suggestions for improvements or new features, feel free to open a pull request on our GitHub repository. [Contribute here](https://www.github.com/zeejayym/live-api-documentation). We appreciate your input in making our documentation better for everyone." />}}

## Requirements

- **Python  ≥ 3.9**
- **Apex Legends** 

Make sure you have Apex Legends installed on your device using the [EA app](https://www.ea.com/ea-app) or on [Steam](https://store.steampowered.com/app/1172470/Apex_Legends/) — we will not be covering the installation in this tutorial.

## Install Python

To install Python, follow the specific instructions for your operating system:

1. Visit [Python's official downloads page](https://www.python.org/downloads/) to download the latest version of Python. Make sure to select a version that is 3.9 or higher, as indicated in the requirements.
2. Run the downloaded installer. During the installation process, make sure to select the option to **Add Python to PATH**. This step is crucial as it allows you to run Python from the command line across various operating systems.
3. Follow the rest of the installation prompts to complete the setup.

After installation, you can verify that Python is correctly installed by opening your command line or terminal and entering:

```shell
python --version
```

This command should return the Python version number that you installed. If you encounter any issues, refer to [Python's official installation guide](https://wiki.python.org/moin/BeginnersGuide/Download) for more detailed instructions and troubleshooting tips.




### Setting up Your Development Environment

{{< alert context="info" text="Note: If your project is already part of a git repository, you can further streamline your setup by initializing your virtual environment within your project's directory. This approach simplifies managing project dependencies alongside your code. For example, python -m venv .venv within your project directory keeps everything contained." />}}

After installing Python, ensure you have pip (Python's package installer) by running:

```shell
python -m ensurepip --upgrade
```

Create a virtual environment for your project to manage dependencies separately from other Python projects by running:

```shell
python -m venv /path/to/new/virtual/environment
```
Replace /path/to/new/virtual/environment with the directory where you want to store your virtual environment.




### Activate Your Virtual Environment

To activate the virtual environment, use the instructions specific to your operating system:

{{< tabs tabTotal="3">}}
{{% tab tabName="macOS/Linux" %}}
Replace `/path/to/new/virtual/environment` with the path to your virtual environment.


```shell
source /path/to/new/virtual/environment/bin/activate
```

{{% /tab %}}
{{% tab tabName="Windows (Command Prompt)" %}}

Replace `/path/to/new/virtual/environment` with the path to your virtual environment.

```shell
/path/to/new/virtual/environment/Scripts/activate.bat
```

{{% /tab %}}
{{% tab tabName="Windows (PowerShell)" %}}

Replace `/path/to/new/virtual/environment` with the path to your virtual environment.

```shell
/path/to/new/virtual/environment/Scripts/Activate.ps1
```

{{% /tab %}}

{{< /tabs >}}

Once activated, the name of your virtual environment, indicated by its folder name in parentheses (e.g., `(myenv)`), should now appear before your shell's prompt, identifying that the virtual environment is currently in use.

### Install Dependencies

To utilize the WebSockets API, you must install the necessary Python packages. Execute the following command in your activated virtual environment to install the `websockets` library along with `asyncio`, which is likely already included with your Python installation:


```shell
(myenv) python -m pip install asyncio websockets
```

### Next Steps

Respawn has provided a sample python code in order to help get developers started.

%USER

```py {linenos=table,lines=["1-24"]}
# generate the protobuf bindings by doing `protoc events.proto --python_out='.'`
# before running, do `python -m pip install asyncio websockets`

import asyncio
import socket
import websockets
from events_pb2 import *

async def repl( websocket ):
    print("Connected!")

    async for message in websocket:
        try:
            incoming = LiveAPIEvent()
            incoming.ParseFromString( message )
            print( incoming )
        except:
            print( message )

async def main():
    async with websockets.serve(repl, "localhost", 7777):
        await asyncio.Future()  # run forever on port 7777

asyncio.run(main()) 
```

