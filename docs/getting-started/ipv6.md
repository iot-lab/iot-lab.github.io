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

The previous address can be shortened to:

```
2001:660:5307:30ff::1
```

This 128 bits address is often divided into 2 parts:

* the **most-significant 64 bits** are used as the routing prefix,
**2001:660:5307:30ff::/64** in the previous example.
* the **least-significant 64 bits** correspond to the address of the host, **::1**
in the previous example. Generally, they are constructed from the MAC address of
the host to guarantee the uniqueness of an IPv6 address in a subnet or randomly
generated for privacy reason.

Some prefixes are reserved for very specific uses:

* **fe80::/10** is used for unicast addresses called **link-local**. This type of address only
allows 2 network nodes to communicate if they share a direct physical link.
* **fd00::/8** is intended for **Unique Local Address** addresses. These addresses
correspond to private addresses in IPv4 and are not routable.

## For boards based on a microcontroller

In order for an embedded board to communicate in IPv6 with a host on the Internet, it needs an IPv6 **global** unicast address. To do this, another embedded board play the role of Border Router (BR) and must be added in the network. It will be responsible for propagating an IPv6 global prefix and assign an address to the device. We speak here of BR, because it's on the border between a radio network (e.g. 802.15.4) and a classic Ethernet network. Technically, the IPv6 traffic between the SSH frontend and the BR radio interface is routed via a virtual network interface (i.e. TUN or TAP interface) and the IPv6 traffic is encapsulated on the BR's serial link.

![ipv6-m3]({{ '/assets/images/docs//ipv6-micro.png' | relative_url }}){:.img-fluid}

To do so we provide a pool of global IPv6 /64 prefixes per site that can be used to build an IPv6 network. They are listed in the table below:

| Site | Number of subnets| from | to |
| ---- | -----------------| ---- | -- |
| Grenoble   | 128 | 2001:660:5307:3100::/64 | 2001:660:5307:317f::/64 |
| Lille      | 128 | 2001:660:4403:0480::/64 | 2001:660:4403:04ff::/64 |
| Paris      | 128 | 2001:660:330f:a280::/64 | 2001:660:330f:a2ff::/64 |
| Saclay     | 64  | 2001:660:3207:04c0::/64 | 2001:660:3207:04ff::/64 |
| Strasbourg | 32  | 2001:660:4701:f0a0::/64 | 2001:660:4701:f0bf::/64 |
{: .table .table-striped}

See the dedicated section of the documentation to know how to use this feature:
- [RIOT]({{ '/docs/os/riot#border-router-and-ipv6-networking-on-iot-lab' | relative_url }}) using ETHOS (Ethernet Over Serial);
- [Contiki-NG]({{ '/docs/os/contiki-ng#border-router-and-ipv6-networking-on-iot-lab' | relative_url }}) using SLIP (Serial Line Internet Protocol).

## For boards running an embedded Linux

Boards running an embedded Linux have 2 interfaces:

* 1x Ethernet interface
* 1x Serial link interface with their co-microcontroller

It's therefore quite possible to build an IPv6 network with the co-microcontroller acting as a Border Router and communicating with other nodes by radio (e.g. 802.15.4). Unlike the setup with a microcontroller on the SSH frontend, the creation of the virtual network interface and IPV6 traffic encapsulation is done directly on the embedded Linux node with the co-microcontroller serial's link.

We give you an example of an IPV6 configuration with IoT-LAB A8-M3 boards:


* **a global IPv6 address on the Ethernet interface** constructed as follows:

```
[ A8-M3 Prefixes 64 bits ] + [ node ID 64 bits = hexa(node ID) ] /128
```

E.g. for node-a8-1 on Strasbourg site:

```
[ 2001:660:4701:f080 ] + [ 0000:0000:0000:0001 ] /128
```

Finally, the shortened address:

```
  2001:660:4701:f080::1/128
```

* **an IPv6 /64 prefix for its M3 co-microcontroller**, statically routed via the site server and defined as follows:

```
[ A8-M3 prefix range start + hexa(node ID) ] ::/64
```

 E.g. associated M3 subnet for node-a8-1 on Strasbourg site:

```
[ 2001:660:4701:f080 + 1 ] ::/64

```

or

```
  2001:660:4701:f081::/64 as IPv6
```

For all availables A8-M3 prefixes, see [IoT-LAB IPv6 subnets]({{ '/docs/getting-started/ipv6-subnets/' | relative_url }}).


You can note that during an experiment IoT-LAB A8-M3 nodes are directly accessible via SSH in IPv6 from Internet.

```
ssh -6 root@2001:660:4701:f080::1
```

In addition on the embedded LInux node you can display the IPV6 configuration with the following environment variables

```
root@node-a8-1:~# printenv
...
INET6_PREFIX_LEN=64
INET6_PREFIX=2001:660:4701:f081
GATEWAY6_ADDR=2001:660:4701:f080:ff::
INET6_ADDR=2001:660:4701:f080::1/64
...
```

The following figure shows the IPv6 infrastructure for IoT-LAB A8-M3 nodes on one IoT-LAB site:

![ipv6-a8]({{ '/assets/images/docs/ipv6-a8.png' | relative_url }})
