---
title: IPv6
group: getting-started
description: IPv6 connectivity for the IoT-LAB testbed
---

## Overview

[IPv6](https://en.wikipedia.org/wiki/IPv6) is the most recent version of the
[IP](https://en.wikipedia.org/wiki/Internet_Protocol) protocol developed by the
[IETF](https://en.wikipedia.org/wiki/Internet_Engineering_Task_Force). IPv6
offers larger address and solves the problem of [IPv4 address
exhaustion](https://en.wikipedia.org/wiki/IPv4_address_exhaustion) and also
offers [new features](https://en.wikipedia.org/wiki/IPv6#Comparison_with_IPv4).
An IPv6 address is represented by a series of **128 bits** or 16 bytes, and is
represented with a hexadecimal notation. For example, a public IPv6 address,
so-called **global unicast** address that is to say **routable** can have the full
representation:

```
2001:0660:5307:30ff:0000:0000:0000:0001
```

* One or more leading zeros from any groups of hexadecimal digits are removed;
this is usually done to either all or none of the leading zeros. For example,
the group `0042` is converted to `42`.
* A series of 0 contiguous is replaced only once by `::` and can be shortened to:

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

## IoT-LAB IPv6 support

You will find all avaibles IPv6 prefixes per sites in
  [IoT-LAB IPv6 subnets]({{ '/docs/getting-started/ipv6-subnets/' | relative_url }}).

### M3 nodes, Custom nodes

[Dedicated subnets]({{ '/docs/getting-started/ipv6-subnets/' | relative_url }})
 for M3 nodes allow you to map a global IPv6 /64 prefix on a M3
node acting as a border router (BR). All M3 subnets of a site can be used on any
M3 node of the same site. Technically, the IPv6 traffic between the
infrastructure and the BR radio interface is routed via a TUN/SLIP interface
mounted inside the IoT-LAB server and attached to the serial port of the M3
node. Our tunslip6.py script automatically creates TUN/SLIP interface with the
selected IPv6 prefix mapped to the chosen M3 node. Collision or usurpation
between users experiments are also taken into account.

The following figure shows the IPv6 infrastructure for M3 nodes on one IoT-LAB site:
![ipv6-m3]({{ '/assets/images/docs//ipv6-m3.png' | relative_url }})


### A8 nodes

A8 open nodes running embedded GNU/Linux have 2 interfaces:

* 1x Ethernet interface
* 1x Serial interface with M3 node

The A8 open node is configured with:

* **a global IPv6 address on the Ethernet interface** constructed as follows:

```
[ Open A8 Prefixes 64 bits ] + [ node ID 64 bits = hexa(node ID) ] /128
```

E.g. for node-a8-1 on Strasbourg site:

```
[ 2001:660:4701:f080 ] + [ 0000:0000:0000:0001 ] /128
```

Finally, the shortened address:

```
  2001:660:4701:f080::1/128
```

* **an IPv6 /64 subnet for its M3 node**, statically routed via the site server and defined as follows:

```
[ A8 prefix range start + hexa(node ID) ] ::/64
```

 E.g. associated M3 subnet for node-a8-1 on Strasbourg site:

```
[ 2001:660:4701:f080 + 1 ] ::/64

```

or

```
  2001:660:4701:f081::/64 as IPv6
```

For all availables A8 prefixes, see [IoT-LAB IPv6 subnets]({{ '/docs/getting-started/ipv6-subnets/' | relative_url }}).

The following figure shows the IPv6 infrastructure for A8 nodes on one IoT-LAB site:
![ipv6-a8]({{ '/assets/images/docs/ipv6-a8.png' | relative_url }})
