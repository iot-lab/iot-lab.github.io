---
id: 7822
title: New web terminal available on the testbed webportal and websocket CLI tools
date: 2019-03-19T15:25:41+00:00
author: Alexandre Abadie
layout: post
guid: https://www.iot-lab.info/?p=7822
permalink: /new-web-terminal-webportal/
categories:
  - Uncategorized
---
<div class="pf-content">
  <p>
    We would like to inform you about new features available that simplify the access to the serial port of FIT IoT-LAB nodes .
  </p>
  
  <h3>
    Direct access via the testbed webportal
  </h3>
  
  <p>
    It is now possible to access the serial port of all nodes but the A8 from the experiment details page on the testbed webportal.<br /> Each node in an experiment now provides a <i>terminal icon</i> in the list of supported actions: just click on it and a web terminal pops up with direct access to the serial port of the node.
  </p>
  
  <p>
    This makes the user experience as simple as possible when using FIT IoT-LAB via the testbed webportal!
  </p>
  
  <p>
    There are things to take into account though:
  </p>
  
  <ul>
    <li>
      The access to the serial port is similar to the netcat access on port 20000 from the SSH frontends: only one TCP connection at a time is possible. This means that you cannot use the web terminal if a TCP connection is already opened using netcat. And vice-versa.
    </li>
    <li>
      The serial stream transport uses a websocket connection between the browser and the FIT IoT-LAB web server. For performance reasons, only 2 websocket connections on a single node are allowed at a time and 10 websocket connections per site per user in total are allowed.
    </li>
  </ul>
  
  <p>
    Discover this new feature by following our <a href="https://www.iot-lab.info/tutorials/getting-started-tutorial/">new getting started tutorial</a>.
  </p>
  
  <h3>
    New websocket CLI Tools
  </h3>
  
  <p>
    The access to the node serial port via websockets also makes it possible to aggregate serial input/output of nodes from different sites on a single computer. To do this, we released a new CLI tool: the <a href="https://github.com/iot-lab/ws-cli-tools">ws-cli-tools</a>.<br /> It is open source, compatible with Python 2 and Python 3 and available on <a href="https://pypi.org/project/iotlabwscli/">PyPI</a>.
  </p>
  
  <p>
    Just follow the <a href="https://github.com/iot-lab/ws-cli-tools/blob/master/README.rst">README</a> on github to learn how to install and use it with the FIT IoT-LAB testbed.
  </p>
</div>