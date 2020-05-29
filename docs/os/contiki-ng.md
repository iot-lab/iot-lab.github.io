---
title: Contiki-NG
group: os
---

## Description

Contiki-NG is an open-source, cross-platform operating system for Next-Generation IoT devices. It focuses on dependable (secure and reliable) low-power communication and standard protocols, such as IPv6/6LoWPAN, 6TiSCH, RPL, and CoAP. Contiki-NG comes with extensive documentation, tutorials, a roadmap, release cycle, and well-defined development flow for smooth integration of community contributions.

Unless explicitly stated otherwise, Contiki-NG sources are distributed under the terms of the 3-clause BSD license. This license gives everyone the right to use and distribute the code, either in binary or source code format, as long as the copyright license is retained in the source code.

Contiki-NG started as a fork of the Contiki OS and retains some of its original features.

<small>Source: <a href="https://github.com/contiki-ng/contiki-ng" target="blank">Contiki-NG on GitHub</a></small>

## Support for IoT-LAB boards

### Setup
Due to licensing compatibility issues on hardware drivers, IoT-LAB boards support is not present in Contiki-NG official release.
However, the Contiki-NG's build system enables compiling with arch directory at arbitrary paths. So we use this feature and provide such a directory with the [<i class="fab fa-github"></i> iot-lab/iot-lab-contiki-ng](https://github.com/iot-lab/iot-lab-contiki-ng) repository:

```bash
git clone https://github.com/iot-lab/iot-lab-contiki-ng.git
cd iot-lab-contiki-ng
```

It also includes a Contiki-NG release (version 4.4) as a git submodule, so, if you don't have to work with your specific Contiki-NG version, you can retrieve the submodule version with the following command:

```bash
git submodule update --init
```

### Compilation options

The Contiki-NG TARGET name for this port is iotlab, so in order to compile an application you need to invoke GNU make as follows:
Here are make targets/variables and values to use with IoT-LAB boards:
- `TARGET=iotlab`
- `BOARD=m3` for an IoT-LAB M3 or `BOARD=a8-m3` for an IoT-LAB A8-M3
- `ARCH_PATH`: path (absolute or relative) to the IoT-LAB arch directory

For example, here is the set of commands to use to compile the hello-world example from the submodule release for the IoT-LAB M3 board:
```bash
cd contiki-ng/examples/hello-world
ARCH_PATH=../../../arch make TARGET=iotlab BOARD=m3 savetarget
ARCH_PATH=../../../arch make
```

_Note: An ARM compiler (v.7) is available on the SSH frontends._{: .text-warning}

## Border Router and IPv6 networking on IoT-LAB

To connect to the serial link of your border router and propagate an IPv6 prefix through your network, Contiki-NG provides the `tunslip6` tool. It bridges the Contiki-NG border router (one of your experimentation node) to the host (SSH frontend) via a tun interface, using SLIP (Serial Line Internet Protocol) to encapsulate and pass IP traffic to and from the other side of the serial line.

Usually, Tunslip needs sudo privileges to be able to create a dedicated tun interface. Since the command has to be launched from the SSH frontend to have access to serial link, where you are not part of the sudoers, you have to use a wrapper we developed:

```bash
sudo tunslip6.py -v2 -L -a <node-id> -p 20000 fd00::1/64
```

- The usual `-s` option to specify the local device, is replaced by the `-a` and `-p` options to specify respectively server address and server port. It points at the TCP redirection of the border router serial link.
- `fd00::1/64` is the virtual network interface (i.e. TUN) IPv6 address. This address is of the form `<ipv6_prefix>::1`. The prefix can be replaced by another local prefix, or even by a global prefix (see [IPv6]({{ '/docs/getting-started/ipv6' | relative_url }})).
