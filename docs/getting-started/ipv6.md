---
title: IPv6
group: getting-started
description: This page describes the public IPv6 support available on the IoT-LAB testbed. You will find out how to build a public IPv6 network with embedded boards.
---

## Introduction

[IPv6](https://en.wikipedia.org/wiki/IPv6) is the most recent version of the
[IP](https://en.wikipedia.org/wiki/Internet_Protocol) protocol developed by the
[IETF](https://en.wikipedia.org/wiki/Internet_Engineering_Task_Force). IPv6
offers larger address and solves the problem of [IPv4 address
exhaustion](https://en.wikipedia.org/wiki/IPv4_address_exhaustion) and also
offers [new features](https://en.wikipedia.org/wiki/IPv6#Comparison_with_IPv4).
An IPv6 address is represented by a series of **128 bits** or 16 bytes, and is
represented with a hexadecimal notation. For example, a public IPv6 address,
so-called **global unicast** address that is to say **routable**, can have the
following full representation:

```
2001:0660:5307:30ff:0000:0000:0000:0001
```

* One or more leading zeros from any groups of hexadecimal digits are removed;
this is usually done to either all or none of the leading zeros. For example,
the group `0042` is converted to `42`.
* A series of 0 contiguous is replaced only once by `::`

Thus, the previous address can be shortened to:

```
2001:660:5307:30ff::1
```

This 128 bits address is often divided into 2 parts:

* the **most-significant 64 bits** are used as the routing prefix (`2001:660:5307:30ff::/64` in our example)
* the **least-significant 64 bits** correspond to the address of the host (`::1`
in our example); generally, they are constructed from the MAC address of
the host to guarantee the uniqueness of an IPv6 address in a subnet or randomly
generated for privacy reason.

Some prefixes are reserved for very specific uses:

* **fe80::/10** is used for unicast addresses called **link-local**. This type of address only
allows 2 network nodes to communicate if they share a direct physical link.
* **fd00::/8** is intended for **Unique Local Address** addresses. These addresses
correspond to private addresses in IPv4 and are not routable.

## For boards based on a microcontroller

In order for an embedded board to communicate in IPv6 with a host on the Internet, it needs an IPv6 **global** unicast address. To do this, another embedded board play the role of Border Router (BR) and must be added in the network. It will be responsible for propagating an IPv6 global prefix and assign an address to the device. We speak here of BR, because it's on the border between a radio network (e.g. 802.15.4) and a classic Ethernet network. Technically, the IPv6 traffic between the SSH frontend and the BR radio interface is routed via a virtual network interface (i.e. TUN or TAP interface) and the IPv6 traffic is encapsulated on the BR's serial link.

<div class="col col-lg-10 offset-lg-1" markdown="1">
![ipv6-m3]({{ '/assets/images/docs//ipv6-micro.png' | relative_url }}){:.img-fluid}
</div>

To do so, we provide a pool of global IPv6 /64 prefixes per site that can be used to build an IPv6 network. They are listed in the table below:

| Site | Number of subnets| Prefixes, from |  to |
| ---- | -----------------| -------------- | --- |
| Grenoble   | 128 | 2001:660:5307:3100::/64 | 2001:660:5307:317f::/64 |
| Lille      | 128 | 2001:660:4403:0480::/64 | 2001:660:4403:04ff::/64 |
| Saclay     | 64  | 2001:660:3207:04c0::/64 | 2001:660:3207:04ff::/64 |
| Strasbourg | 32  | 2001:660:4701:f0a0::/64 | 2001:660:4701:f0bf::/64 |
{: .table .table-striped}

You can view currently used IPv6 prefixes on the frontend SSH with this command:
```bash
<login>@grenoble:~$ ip -6 route
...
2001:660:5307:3100::/64 dev tun0  proto kernel  metric 256  mtu 1500 advmss 1440 hoplimit 4294967295
2001:660:5307:3102::/64 dev tun7  proto kernel  metric 256  mtu 1500 advmss 1440 hoplimit 4294967295
2001:660:5307:3107::/64 dev tap3  proto kernel  metric 256  mtu 1500 advmss 1440 hoplimit 4294967295
...
```
Be sure to use a free one, otherwise you may get an _“overlaps with routes”_ error while creating the IPv6 over serial interface.

See the dedicated section of the OS documentation to know how to use this feature:
- with [RIOT]({{ '/docs/os/riot#border-router-and-ipv6-networking-on-iot-lab' | relative_url }}) using ETHOS (Ethernet Over Serial);
- with [Contiki-NG]({{ '/docs/os/contiki-ng#border-router-and-ipv6-networking-on-iot-lab' | relative_url }}) using SLIP (Serial Line Internet Protocol).

## For boards running an embedded Linux

During an experiment boards running an embedded Linux have an IPv6 address assigned to their Ethernet interface. They are directly accessible:
- from any other embedded Linux board currently running,
- from any board of the testbed based on a microcontroller having a public IPv6 address,
- from any IoT-LAB SSH frontend,
- and, on the whole, from any public IPv6 address on the Internet.

Each site has a /64 IPv6 prefix assigned, in which each node will be assigned its static IPv6 address.

This IPV6 configuration can be known with the following environment variables:
```bash
root@node-a8-1:~# printenv
...
GATEWAY6_ADDR=2001:660:4701:f080:ff::
INET6_ADDR=2001:660:4701:f080::1/64
...
```

## Mixing two types of boards

It is possible to test common IoT scenarios that implies communications between sensors and an application gateway, the later needing to have a more powerfull environment. Boards based on a microcontroller play the role of sensors and a board running embedded Linux, equipped with a co-microcontroller managing a radio interface, plays the role of the gateway.

In that case, it's therefore quite possible to build an IPv6 network with the co-microcontroller acting as a Border Router and communicating with other nodes by radio (e.g. 802.15.4). Unlike the setup with a microcontroller on the SSH frontend, the creation of the virtual network interface and IPV6 traffic encapsulation is done directly on the embedded Linux node using the co-microcontroller serial's link.

<div class="col col-lg-10 offset-lg-1" markdown="1">
![ipv6-a8]({{ '/assets/images/docs/ipv6-linux.png' | relative_url }}){:.img-fluid}
</div>

Each embedded Linux node has a defined /64 IPv6 prefix to build its IPv6 subnet. Each node based on a microcontroller will have a public IPv6 assigned to him with this prefix. It can be known with the following environment variables:
```bash
root@node-a8-1:~# printenv
...
INET6_PREFIX_LEN=64
INET6_PREFIX=2001:660:4701:f081
...
```

See the dedicated section of the OS documentation to know how to install and use the needed tools for that:
- [RIOT]({{ '/docs/os/riot#border-router-and-ipv6-networking-on-iot-lab' | relative_url }}) using ETHOS (Ethernet Over Serial);
- [Contiki-NG]({{ '/docs/os/contiki-ng#border-router-and-ipv6-networking-on-iot-lab' | relative_url }}) using SLIP (Serial Line Internet Protocol).
