---
title: Virtual Machine
group: getting-started
description: We build a virtual machine which enable users to use lightweight, reproducible, and portable IoT-LAB development environments. The virtual machine is configured with IoT-LAB Github repository, all command-line tools like CLI, SSH-CLI or WSCLI, toolchains compilation (arm-gcc) and much more.
---

## Requirement

The official IoT-LAB virtual machine is building with [Packer](https://www.packer.io/) tool. You can view the Github repository with the [IoT-LAB packer configuration](https://github.com/iot-lab/iot-lab-packer). For running the virtual machine on your computer you need to install [VirtualBox](https://www.virtualbox.org/).

Example of installation on Ubuntu 18.04 LTS:

```bash
$ sudo add-apt-repository multiverse && sudo apt-get update
$ sudo apt-get install virtualbox
```

## Up and Running

The virtual machine is available in two formats hosted on the IoT-LAB Website:

* a [Vagrant box file](https://www.iot-lab.info/vagrant-box/iotlab-vm.box)
* an [OVA file](https://www.iot-lab.info/vagrant-box/iotlab-vm.ova) (Open Virtual Appliance format)

[Vagrant](https://www.vagrantup.com/) is a virtual machine environment management tool. The vagrant box is also hosted in the official [Vagrant cloud](https://app.vagrantup.com/iotlab/boxes/iotlab-vm).


### Start the virtual machine with Vagrant box file

```bash
$ wget https://www.iot-lab.info/vagrant-box/iotlab-vm.box .
$ vagrant box add --name iotlab iotlab-vm.box
$ vagrant init iotlab
$ vagrant up
$ vagrant ssh
```


### Start the virtual machine with Vagrant Cloud

``` bash
$ vagrant init iotlab/iotlab-vm 
$ vagrant up
$ vagrant ssh
```

### Start the virtual machine without Vagrant

If you don't want to use Vagrant you can download the OVA file and just import it directly in Virtualbox.

```bash
$ wget https://www.iot-lab.info/vagrant-box/iotlab-vm.ova .
```