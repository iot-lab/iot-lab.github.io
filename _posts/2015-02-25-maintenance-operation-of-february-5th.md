---
title: Maintenance operation of February 5th
---

The whole FIT IoT-LAB testbed was closed on February 5th for maintenance and upgrade operations.
{: .lead}

During this day we deployed new software; here are the details:

#### Radio sniffer

We implemented new features linked to Control Nodes, that let’s you configure them as radio sniffers during experiments. Learn how to use it through this [documentation]({{ site.baseurl }}{% link docs/tools/radio-monitoring.md %}). More details on implementation are documented on [GitHub](https://github.com/iot-lab/iot-lab/wiki/Control-Node-Sniffer).

#### New Linux kernel on A8 nodes

Linux kernel of open A8 nodes have been updated to version 3.18.5. Read the [Linux nodes tutorial]({{ site.baseurl }}{% link learn/getting-started/linux-cli-tools.md %}) to discover usage and features.

#### CLI tools upgrade to version 1.5.3

See changelog : https://github.com/iot-lab/cli-tools/blob/master/CHANGELOG.md

#### New aggregation tools

Creation of a dedicated repo on GitHub – https://github.com/iot-lab/aggregation-tools. Learn how to use serial_aggregator through this [documentation]({{ site.baseurl }}{% link docs/tools/serial-aggregator.md %}). Learn how to use sniffer_aggregator through [sniffer documentation]({{ site.baseurl }}{% link docs/tools/radio-monitoring.md %}).

#### Onelab federation

As [FIT](https://www.fit-equipex.fr/ "FIT") platforms are part of the [Onelab](https://onelab.eu/ "Onelab") Experimental Facility, and to highlight this federation aspect, we updated our website and webportal to follow Onelab and FIT style guides. Moreover, Onelab users can use their email/password to Sign In on the webportal to use advanced features of the testbed.
