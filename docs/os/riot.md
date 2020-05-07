---
title: RIOT
group: os
---

## Description

RIOT is a real-time multi-threading operating system that explicitly considers
devices with minimal resources but eases development across the wide range of
devices that are typically found in the Internet of Things. RIOT is based on
design objectives including energy-efficiency, reliability, real-time
capabilities, small memory footprint, modularity, and uniform API access,
independent of the underlying hardware (this API offers partial POSIX
compliance). Several libraries (e.g. Wiselib) are already available on RIOT, as
well as a full IPv6 network protocol stack including the latest standards of the
IETF for connecting constrained systems to the Internet (6LoWPAN, IPv6, RPL, TCP
and UDP).

See the documentation on the [RIOT wiki](https://github.com/RIOT-OS/RIOT/wiki).

## Compilation from IoT-LAB SSH frontend

// Do we set ARMv7 by default on SSH frontends?
{: .text-warning }

With recent versions of RIOT (2018.01+), the default version of the GNU
Toolchain for ARM (4.9) doesn't work.

RIOT recommends to use 7.2+. Before building any RIOT firmware on an SSH
frontend, ensure RIOT related environment variables are correctly set with:

```sh
source /opt/riot.source
```

## Border Router and IPv6 networking on IoT-LAB

To connect to the serial link of your border router and propagate an IPv6 prefix through your network, RIOT provides the `ethos_uhcpd` tool. It uses the serial interface, ethos (Ethernet Over Serial) and UHCP (micro Host Configuration Protocol). Ethos multiplexes serial data to separate ethernet packets from shell commands. UHCP is in charge of configuring the wireless interface prefix and routes on the Border Router.

Usually, it needs sudo privileges to be able to create a dedicated tap interface. Since the command has to be launched from the SSH frontend to have access to serial link, where you are not part of the sudoers, you have to use a wrapper we developed:

```bash
sudo ethos_uhcpd.py <node-id> tap<num> fd00::1/64
```

- `node-id` refers to the node acting as Border Router;
- `num` specifies a free tap interface (see below);
- `fd00::1/64` is the default IPv6 prefix. It can be replaced by another local prefix, or even by a global prefix (see [IPv6]({{ '/docs/getting-started/ipv6' | relative_url }})).

To list tap interface in currently in use, launch the following command on the SSH frontend:
```bash
<login>@<site>:~$ ip addr show | grep tap
```
Choose one not in the list. You could use tap0 if there is not output.
