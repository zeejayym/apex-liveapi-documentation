---
weight: 100
date: "2024-02-10T22:37:22+01:00"
draft: false
author: "ZJ"
title: "Quickstart Guide for Apex Legends LiveAPI 2.0 with Python"
icon: "rocket_launch"
toc: true
description: "Get started with LiveAPI 2.0. This guide provides a comprehensive introduction to the LiveAPI 2.0 using Python."
publishdate: "2023-05-03T22:37:22+01:00"
tags: ["Beginners"]
---

{{< alert context="info" text="**Note from the Author:** For experienced developers, adapting this guide to your preferred programming language should be straightforward. This resource is primarily aimed at helping beginners get started. Much of the information is available in `LiveAPI/readme.txt` within your Apex Legends installation directory, but here we provide additional depth and context." />}}

This guide provides a comprehensive introduction to using Apex Legends' LiveAPI 2.0 with Python, aimed at developers interested in building applications that interact with Apex Legends data in real-time. 

{{< alert context="info" text="This documentation is a work in progress, and we actively welcome contributions. If you have suggestions for improvements or new features, feel free to open a pull request on our GitHub repository. [Contribute here](https://www.github.com/zeejayym/apex-liveapi-documentation). We appreciate your input in making our documentation better for everyone." />}}

## Requirements

- **[Python ≥ 3.9](https://www.python.org/downloads)**
- **[Apex Legends](https://www.ea.com/games/apex-legends)**
- **[Protoc](https://protobuf.dev/downloads/)**

Make sure you have Apex Legends installed on your device using the [EA app](https://www.ea.com/ea-app) or on [Steam](https://store.steampowered.com/app/1172470/Apex_Legends/) — we will not be covering the installation in this tutorial.

## Install Python

To install Python, follow the specific instructions for your operating system:

  1. Visit [Python's official downloads page](https://www.python.org/downloads/) to download the latest version of Python. Make sure to select a version that is 3.9 or higher, as indicated in the requirements.
1. Run the downloaded installer. During the installation process, make sure to select the option to **Add Python to PATH**. This step is crucial as it allows you to run Python from the command line across various operating systems.
2. Follow the rest of the installation prompts to complete the setup.

After installation, you can verify that Python is correctly installed by opening your command line or terminal and entering:

```shell
python --version
```

This command should return the Python version number that you installed.

{{< alert context="warning" text=" If you encounter any issues, refer to [Python's official installation guide](https://wiki.python.org/moin/BeginnersGuide/Download) for more detailed instructions and troubleshooting tips." />}}

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

1. Replace `/path/to/new/virtual/environment` with the path to your virtual environment.


```shell
source /path/to/new/virtual/environment/bin/activate
```

{{% /tab %}}
{{% tab tabName="Windows (Command Prompt)" %}}

1. Replace `/path/to/new/virtual/environment` with the path to your virtual environment.

```shell
/path/to/new/virtual/environment/Scripts/activate.bat
```

{{% /tab %}}
{{% tab tabName="Windows (PowerShell)" %}}

1. Replace `/path/to/new/virtual/environment` with the path to your virtual environment.

```shell
/path/to/new/virtual/environment/Scripts/Activate.ps1
```

{{% /tab %}}

{{< /tabs >}}

Once activated, the name of your virtual environment, indicated by its folder name in parentheses (e.g., `(myenv)`), should now appear before your shell's prompt, identifying that the virtual environment is currently in use.

### Install Dependencies

To utilize the WebSockets API, you must install the necessary Python packages. Execute the following command in your activated virtual environment to install the `websockets` library along with `asyncio` and `protobuf`, which is likely already included with your Python installation:


```shell
python -m pip install asyncio websockets protobuf
```

## Next Steps with Apex Legends LiveAPI

Respawn Entertainment provides developers with a Python code snippet and essential documentation to kickstart integration with the LiveAPI, a powerful tool built on WebSockets and Google's Protocol Buffer (protobuf) technology. These following steps will take you through setting up your development environment, generating protobuf bindings, and running a sample WebSocket server that listens for game events.

### Set Launch Options 

To enable the LiveAPI for Apex Legends, you need to configure the game's launch options:

{{< tabs tabTotal="2">}}
{{% tab tabName="Steam" %}}

1. Navigate to your library and right-click on Apex Legends.
2. Select "Properties," then under the "General" tab, add your command line arguments to the "Launch Options" text box.

{{% /tab %}}
{{% tab tabName="EA App" %}}

1. Go to your installed games and click on Apex Legends.
2. Select "Manage" followed by "View Properties" in the dropdown.
3. Enter your command line arguments in the "Advanced Launch Options" text box.

{{% /tab %}}


{{< /tabs >}}

The necessary command line to activate the LiveAPI and connect it to your app is:

```arduino
+cl_liveapi_enabled 1 +cl_liveapi_ws_servers "ws://127.0.0.1:7777"
```

Some of the following command line parameters can be passed into the game:

{{< table "table-striped-columns" >}}

| Parameter      | Default | Description                                                   |
|-----------------|---------|---------------------------------------------------------------|
| `cl_liveapi_enabled`          | "0"  | Enable Live API functionality.                                  |
| `cl_liveapi_allow_requests`   | "1"  | Allow processing and running any incoming requests.            |
| `cl_liveapi_pretty_print_log` | "0"  | Makes the JSON output more human-readable.                     |
| `cl_liveapi_use_protobuf`     | "1"  |  Use protobuf as the serialization format. Otherwise, JSON.    |
| `cl_liveapi_ws_keepalive`     | "30" | Interval of time to send Pong to any connected server.         |
| `cl_liveapi_ws_retry_count`   | "5"  | Amount of times to retry connecting before marking the connection as unavailable. |
| `cl_liveapi_ws_retry_time`    | "30" | Time between retries.                                          |
| `cl_liveapi_ws_servers`       | ""   | Comma separated list of addresses to connect to. Must be in the form 'ws://domain.com:portNum'. |
| `cl_liveapi_ws_timeout`       | "300" | Websocket connection timeout in seconds.                      |
| `cl_liveapi_ws_lax_ssl`       | "1"   | Skip SSL certificate validation for all WSS connections. Allows the use of self-signed certificates. |
| `cl_liveapi_ws_event_delay`   | ""    | Delay (in seconds) to be used when broadcasting an event to all connections. |
| `cl_liveapi_requests_psk`     | ""    | A preshared key that will be used to validate requests. When set, if a request is received with a key that does not match, it is rejected. |
| `cl_liveapi_requests_psk_tries` | "10" | Attempts allowed when making a request with the wrong key before the connection is dropped. It will always be minimum 10 tries. |
| `cl_liveapi_session_name`       | ""  | Session name that can be used in WebSocket connections to identify this client. |

{{< /table >}}

{{< alert context="info" text="Note: This tells the game to enable the LiveAPI and connect to a WebSocket server running on the same machine at port 7777." />}}




### Installing the Protocol Buffers Compiler (protoc)

Before you can generate the protobuf bindings needed to work with Apex Legends' LiveAPI events in Python, you must have the Protocol Buffers Compiler (`protoc`) installed on your development machine.

{{< alert context="info" text="Note: `protoc` is used to compile `.proto` files into language-specific bindings, enabling your applications to work with structured data defined in protobuf format." />}}

- Download the latest version of [protoc](https://protobuf.dev/downloads/) for your operating system. 

Then proceed to installation: 

{{< tabs tabTotal="2">}}
{{% tab tabName="macOS/Linux" %}}

- Extract the downloaded file and move the protoc binary to a directory included in your system's PATH, such as /usr/local/bin.

{{% /tab %}}
{{% tab tabName="Windows" %}}

- Unzip the downloaded file and add the path to the bin directory (containing protoc.exe) to your system's PATH environment variable.

{{% /tab %}}


{{< /tabs >}}

### Preparing to use Protobuf

1. Find the LiveAPI folder within the Apex Legends installation directory:
   - For Steam users, navigate to the Apex Legends installation directory, typically found at `steamapps/common/Apex Legends/LiveAPI`.
   - For EA App users, the directory is usually located at `Electronic Arts/Apex Legends/LiveAPI`.

2. The `events.proto` file defines the structure for game events. Familiarize yourself with protobuf technology at [Google's Protocol Buffers documentation](https://protobuf.dev/).

3. To work with game events in Python, generate Python bindings from the `events.proto` file. Ensure the Protobuf Compiler (`protoc`) is installed, and run:


```shell
protoc --proto_path="<LiveAPI directory>" --python_out="<target directory>" events.proto
```

Replace `<LiveAPI directory>` and `<target directory>` with the appropriate paths.

### Python Sample Code

The script establishes a WebSocket server on localhost at port `7777`, awaiting connections. If the connection is successful, it prints "Connected!" and listens for incoming messages. These messages are expected to be in the Protocol Buffers (`protobuf`) format, are parsed into LiveAPIEvent objects and displayed. If parsing fails, the raw message is shown. The server remains active indefinitely, processing any received messages.

```py
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
    # run forever on port 7777
    async with websockets.serve(repl, "localhost", 7777):
        print("Serving on port 7777...")
        await asyncio.Future()

asyncio.run(main())
```

1. Run the script in your terminal or command prompt:

    ```shell
    python liveapi_server.py
    ```

2. Launch Apex Legends through Steam or the EA App with the configured launch options.

3. Once the game starts, it will attempt to connect to your WebSocket server at the specified address and port.

{{< alert context="warning" text="If you encounter connectivity issues or fail to receive events, try restarting Apex Legends and double-check that the launch options are set correctly. Ensure that the WebSocket server is running before launching the game. If problems persist, verify the integrity of your game files (for Steam users) or repair the game (for EA App users)." />}}

By following these steps, you have created a live connection between Apex Legends and your Python WebSocket server, allowing you to receive and process game events in real-time. This setup is ideal for developing applications or tools that interact with Apex Legends gameplay data.
