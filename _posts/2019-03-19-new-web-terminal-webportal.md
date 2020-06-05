---
title: New web terminal available on the testbed webportal and websocket CLI tools
---

![]({{ '/assets/images/posts/' | relative_url }}terminal-icon.png){: .img-fluid }
{: .text-center}

We would like to inform you about new features available that simplify the access to the serial port of FIT IoT-LAB nodes.
{: .lead}

## Direct access via the testbed webportal

It is now possible to access the serial port of all nodes but the A8 from the experiment details page on the testbed webportal.  
Each node in an experiment now provides a _terminal icon_ in the list of supported actions: just click on it and a web terminal pops up with direct access to the serial port of the node.

This makes the user experience as simple as possible when using FIT IoT-LAB via the testbed webportal!

There are things to take into account though:

- The access to the serial port is similar to the netcat access on port 20000 from the SSH frontends: only one TCP connection at a time is possible. This means that you cannot use the web terminal if a TCP connection is already opened using netcat. And vice-versa.
- The serial stream transport uses a websocket connection between the browser and the FIT IoT-LAB web server. For performance reasons, only 2 websocket connections on a single node are allowed at a time and 10 websocket connections per site per user in total are allowed.

This new feature is used in The first experiment for beginners in video of the [Learn]({{ site.baseurl }}{% link learn/index.html %}) page.

## New websocket CLI Tools

The access to the node serial port via websockets also makes it possible to aggregate serial input/output of nodes from different sites on a single computer. To do this, we released a new CLI tool: the [ws-cli-tools](https://github.com/iot-lab/ws-cli-tools).  
It is open source, compatible with Python 2 and Python 3 and available on [PyPI](https://pypi.org/project/iotlabwscli/).

See the [Websocket client]({{ site.baseurl }}{% link docs/tools/websocket-client.md %}) documentation to learn how to install and use it with the FIT IoT-LAB testbed.
