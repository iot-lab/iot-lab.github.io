---
layout: tuto-w-toc
title: First experiment with board based on a microcontroller
description: Learn how to run an experiment and interact with the boards using the command line interface (CLI tools).
---

## Access to the SSH frontend

The SSH frontend has all the tools and compilation toolchains already installed. They are also the place from where you can interact with the nodes.

You need to [Configure your SSH Access]({{ site.baseurl }}{% link docs/getting-started/ssh-access.md %}) if it's not already done.

Let's connect to the SSH frontend to use the CLI tools from there, by replacing `<login>` with your IoT-LAB login:

```bash
ssh <login>@grenoble.iot-lab.info
```

If you never used the CLI tools from this SSH frontend, you need to store your credentials with the following command:

```bash
iotlab-auth -u <login>
```

Thus, you won't need to specify your login and password at each call to CLI tools.

## Submit the experiment

First, download the firmware you will use for the experiment:
```bash
wget {{ site.url }}{{ 'assets/firmwares/tutorial_m3.elf' | relative_url}} .
```

Then submit a _20_-minutes experiment, named _first_exp_, using 2 IoT-LAB M3 nodes (_m3:at86rf231_) from the _grenoble_ site, which will run the _tutorial_m3.elf_ firmware:
```bash
iotlab-experiment submit -n first-exp -d 20 -l 2,archi=m3:at86rf231+site=grenoble,tutorial_m3.elf
```

Wait until the experiment's state is _Running_
```bash
iotlab-experiment wait
```

## Interact with the nodes

Get the nodes list assigned to your experiment by the scheduler:
```bash
iotlab-experiment get -n
{
    "items": [
        {
            "archi": "m3:at86rf231",
            "camera": null,
            "mobile": "0",
            "mobility_type": " ",
            "network_address": "m3-101.grenoble.iot-lab.info",
            "production": "YES",
            "site": "grenoble",
            "state": "Alive",
            "uid": "9181",
            "x": "0.40",
            "y": "24.63",
            "z": "-0.04"
        },
        {
            "archi": "m3:at86rf231",
            "camera": null,
            "mobile": "0",
            "mobility_type": " ",
            "network_address": "m3-102.grenoble.iot-lab.info",
            "production": "YES",
            "site": "grenoble",
            "state": "Alive",
            "uid": "a881",
            "x": "1.00",
            "y": "24.63",
            "z": "-0.04"
        }
    ]
}
```

The node's serial port link (i.e. UART) is forwarded onto the SSH frontend via TCP socket on port 20000. The netcat utility (nc) let you connect to a TCP socket and read/write from/to it.

Run the nc command replacing `<id>` with a value picked from your nodes list:
```bash
nc m3-<id1> 20000
```

The firmware is waiting for reading characters to its serial link to do respectives actions.

Here is its help:
```bash
IoT-LAB Simple Demo program
Type command
    h:	print this help
    t:	temperature measure
    l:	luminosity measure
    p:	pressure measure
    u:	print node uid
    d:	read current date using control_node
    s:	send a radio packet
    b:	send a big radio packet
    e:	toggle leds blinking
cmd>
```

Test some actions by typing the corresponding character then Enter.

If you want to see reception of radio packet by the second node, open a second terminal, and run this set of commands:
```bash
ssh <login>@grenoble.iot-lab.info
nc m3-<id2> 20000
```

## Go Further

* Consult the [CLI]({{ site.baseurl }}{% link docs/tools/cli.md %}) documentation.
* Learn how to aggregate all the serial port links of your nodes with the [Serial aggregator]({{ site.baseurl }}{% link docs/tools/serial-aggregator.md %}) tool.
