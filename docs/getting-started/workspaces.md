---
title: Workspaces
group: getting-started
description: This document describes the preconfigured workspaces of IoT-LAB. These workspaces contain all tools that can be used to interact with the different ressources of the testbed.
---

## Introduction

In order to simplify the setup of all the required tools required for
IoT-LAB usage, we provided several workspaces where they are already installed:
- common development tools such as `git`, `make`, `gdb`, etc
- IoT related tools: aiocoap, mqtt clients, etc
- ARM GCC toolchains
- tools for interacting directly with the devices: `nc`, `serial_aggregator`,
  `sniffer_aggregator`, etc
- [IoT-LAB CLI Tools](https://github.com/iot-lab/ssh-cli-tools)
- [SSH-CLI](https://github.com/iot-lab/ssh-cli-tools)
- [WS-CLI](https://github.com/iot-lab/ws-cli-tools)

## The SSH frontends

An SSH frontend is available on each IoT-LAB site. From each frontend, you
can directly access and interact with the devices hosted in the corresponding
site.

To connect to an SSH frontend, you have to
[configure your SSH access]({{ site.baseurl }}{% link docs/getting-started/ssh-access.md %}).
Once done, you will have access to the frontend of any site.

An SSH frontend can also be used to temporarily store your development files,
experiment results, etc. You just have to make sure that you stay within the
limits of the user allowed storage as described in the
[user account documentation]({{ site.baseurl }}{% link docs/getting-started/user-account.md %}).

**Note:** since IoT-LAB is made for experimentation, we recommend to retrieve your
experiment locally, on your computer.

### Sniffing and monitoring storage

When you enable a monitoring profile (for radio sniffing or power consumption)
in an experiment, all results of the monitoring are stored in a specific
directory in your user home directory:
- for radio sniffing: `~/.iot-lab/<exp_id>/radio`
- for power consumption: `~/.iot-lab/<exp_id>/consumption`

The monitoring data are stored in the OML format.

You can find more information on the different monitoring usage in the
[consumption monitoring]({{ site.baseurl }}{% link docs/tools/consumption-monitoring.md %})
and [radio monitoring]({{ site.baseurl }}{% link docs/tools/radio-monitoring.md %}) pages.

### Shared directory with Open Linux boards



## The virtual machine

### Description

In parallel of the SSH frontend, IoT-LAB provides a virtual machine which allow
users to use IoT-LAB tools from their computer.

The IoT-LAB virtual machine is built using [Packer](https://www.packer.io/). For
details on the virtual machine setup, see
[<i class="fab fa-github"></i> this Github repository](https://github.com/iot-lab/iot-lab-packer).

To run the virtual machine on your computer, you have to install
[VirtualBox](https://www.virtualbox.org/).

For example, to install VirtualBox on Ubuntu:

```bash
$ sudo add-apt-repository multiverse
$ sudo apt-get update
$ sudo apt-get install virtualbox
```

## Start the VM

The virtual machine is available in two formats.

### Using the Open Virtual Appliance (OVA) file

An [OVA file](https://www.iot-lab.info/vagrant-box/iotlab-vm.ova) (Open Virtual Appliance format)

The OVA file has to be downloaded locally from
[here](https://www.iot-lab.info/vagrant-box/iotlab-vm.ova) and imported directly in VirtualBox.

This VM already contains the iot-lab repository from where you can start with
running the command:

```bash
$ make

Welcome to the IoT-LAB development environment setup.

targets:
	setup-aggregation-tools
	setup-cli-tools
	setup-contiki
	setup-iot-lab-contiki-ng
	setup-iot-lab.wiki
	setup-oml-plot-tools
	setup-openlab
	setup-riot
	setup-wsn430
	setup-zephyr

	pull
```

### Using vagrant

[Vagrant](https://www.vagrantup.com/) is a virtual machine environment
management tool. To start the IoT-LAB virtual machine using Vagrant, you first have
to clone the [<i class="fab fa-github"></i> iot-lab repository](https://github.com/iot-lab/iot-lab):

```bash
$ git clone https://github.com/iot-lab/iot-lab
```

Then, from the `iot-lab` directory, run the commands:

```bash
$ vagrant up
$ vagrant ssh
```
