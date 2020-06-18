---
title: First experiment with board running an embedded Linux
description: Learn how to run an experiment and interact with boards running an embedded Linux using the command line interface (CLI tools).
---

_**Description**: The aim of this first tutorial is to discover the IoT-LAB testbed tools by creating and submitting your first experiment, and then interact with running nodes. You will book onto the SSH frontend with CLI tools two A8-M3 nodes on the Saclay site. Once deployed, you will connect by SSH to the Linux nodes (i.e. A8 nodes) and interact with the embed M3 co-microcontroller. Thus you will learn how to flash a sample firmware file on it and read sensor values and send radio packets through the serial port link (i.e. UART)_


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

The board you will use here has a co-microcontroller, providing sensing and communication features. First, download the firmware you will use later for this co-microcontroller in your _~/shared_ directory:
```bash
wget {{ site.url }}{{ 'assets/firmwares/tutorial_a8_m3.elf' | relative_url}} -P shared
```

Then, submit a _20_-minutes experiment, named _first-exp_, using 2 IoT-LAB A8-M3 boards (_m3:at86rf231_) from the _grenoble_ site:
```bash
iotlab-experiment submit -n first-exp -d 20 -l 2,archi=a8:at86rf231+site=grenoble
```

Wait until the experiment's state is _Running_
```bash
iotlab-experiment wait
```

## Connect to the embedded Linux system

Get the nodes list assigned to your experiment by the scheduler:
```bash
iotlab-experiment get -n
{
    "items": [
        {
            "archi": "a8:at86rf231",
            "camera": null,
            "mobile": "0",
            "mobility_type": " ",
            "network_address": "a8-101.grenoble.iot-lab.info",
            "production": "YES",
            "site": "grenoble",
            "state": "Alive",
            "uid": "2587",
            "x": "19.75",
            "y": "4.50",
            "z": "2.63"
        },
        {
            "archi": "a8:at86rf231",
            "camera": null,
            "mobile": "0",
            "mobility_type": " ",
            "network_address": "a8-100.grenoble.iot-lab.info",
            "production": "YES",
            "site": "grenoble",
            "state": "Alive",
            "uid": "3185",
            "x": "19.75",
            "y": "3.90",
            "z": "2.63"
        }
    ]
}
```
Here, the experiment is running with the **a8-100** and the **a8-101** nodes in Grenoble.

Embedded Linux boards need between 30 seconds and 2 minutes to boot, depending on the testbed activity. Once it's done, they are accessible with a root access through SSH. The hostname to use is the node id prefixed by _node-_.

```bash
ssh root@node-a8-<id1>
```

From this minimal embedded Linux system, most unix commands are supported. For example you can test the network connectivity between your two boards:
```bash
ping node-a8-<id2>
```

## Flash the co-microcontroller

The `~/shared` directory in which you downloaded the firmware previously is automatically mounted by NFS in the embedded Linux environment. Thus, you have an easy access to the firmware.

Use the _iotlab_flash_ script that interfaces with Open On-Chip Debugger (OpenOCD) to flash it:
```bash
iotlab_flash ~/shared/tutorial_a8_m3.elf
```

> You can also find <i>iotlab_reset</i> script to reset the M3 co-microcontroller.

## Interact with the co-microcontroller

The co-microcontroller serial port link (i.e. UART) is available under /dev/ttyA8_M3. You can use the pySerial console application to access to it, using a baudrate speed of 500 kB/s:

```bash
miniterm.py --echo /dev/ttyA8_M3 500000
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
ssh root@node-a8-<id2>
miniterm.py --echo /dev/ttyA8_M3 500000
```

## Go Further

*  Learn how to interact remotely with embedded Linux boards and automate actions such as waiting for the end of the boot or flashing a firmware on the co-microcontroller by reading the [SSH-CLI]({{ site.baseurl }}{% link docs/tools/ssh-cli.md %}) documentation.
