---
title: Contiki-NG
group: os
---

## Description

Contiki-NG is an open source operating system for networked, memory-constrained
systems with a particular focus on low-power wireless Internet of Things
devices. Contiki provides three network mechanisms: the uIP TCP/IP stack, which
provides IPv4 networking, the uIPv6 stack, which provides IPv6 networking, and
the Rime stack, which is a set of custom lightweight networking protocols
designed specifically for low-power wireless networks. The IPv6 stack was
contributed by Cisco and was, at the time of release, the smallest IPv6 stack to
receive the IPv6 Ready certification. To run efficiently on memory-constrained
systems, the Contiki programming model is based on protothreads. A protothread
is a memory-efficient programming abstraction that shares features of both
multi-threading and event-driven programming to attain a low memory overhead of
each protothread.
