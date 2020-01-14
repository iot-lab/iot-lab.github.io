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

See [RIOT Quick Start Guide](https://github.com/RIOT-OS/RIOT/wiki/Quick-Start-Guide) in the RIOT wiki.

## Boards supported

Node type    |  Sources
-----------     |  ----------
 M3             |  [RIOT/boards/iotlab-m3](https://github.com/RIOT-OS/RIOT/tree/master/boards/iotlab-m3)
 A8-M3          |  [RIOT/boards/iotlab-a8-m3](https://github.com/RIOT-OS/RIOT/tree/master/boards/iotlab-a8-m3)
 WSN430         |  [RIOT/boards/wsn430 (1.3b)](https://github.com/RIOT-OS/RIOT/tree/master/boards/wsn430-v1_3b), [RIOT/boards/wsn430 (1.4)](https://github.com/RIOT-OS/RIOT/tree/master/boards/wsn430-v1_4)
 SAMR21         |  [RIOT/boards/samr21-xpro](https://github.com/RIOT-OS/RIOT/tree/master/boards/samr21-xpro)
 Arduino Zero   |  [RIOT/boards/arduino-zero](https://github.com/RIOT-OS/RIOT/tree/master/boards/arduino-zero)
 ST-LRWAN1      |  [RIOT/boards/b-l072z-lrwan1](https://github.com/RIOT-OS/RIOT/tree/master/boards/b-l072z-lrwan1)
 ST-IOTNODE     |  [RIOT/boards/b-l475e-iot01a](https://github.com/RIOT-OS/RIOT/tree/master/boards/b-l475e-iot01a)
 nRF52840DK     |  [RIOT/boards/nrf52840dk](https://github.com/RIOT-OS/RIOT/tree/master/boards/nrf52840dk)
 NRF52DK        |  [RIOT/boards/nrf52dk](https://github.com/RIOT-OS/RIOT/tree/master/boards/nrf52dk)
 nRF51DK        |  [RIOT/boards/nrf51dk](https://github.com/RIOT-OS/RIOT/tree/master/boards/nrf51dk)
 FRDM-KW41Z     |  [RIOT/boards/frdm-kw41z](https://github.com/RIOT-OS/RIOT/tree/master/boards/frdm-kw41z)
 Firefly        |  [RIOT/boards/firefly](https://github.com/RIOT-OS/RIOT/tree/master/boards/firefly)
 Micro:bit      |  [RIOT/boards/microbit](https://github.com/RIOT-OS/RIOT/tree/master/boards/microbit)

<br/><br/>

## Use RIOT on IoT-LAB

### Special IoT-LAB configuration

With recent versions of RIOT (2018.01+), the default version of the GNU
Toolchain for ARM (4.9) doesn't work.

RIOT recommends to use 7.2+. Before building any RIOT firmware on an SSH
frontend, ensure RIOT related environment variables are correctly set:

```sh
source /opt/riot.source
```

### Related tutorials

* [Running RPL routing with RIOT on M3 nodes](https://www.iot-lab.info/tutorials/rpl-riot)
* [Public IPv6/6LoWPAN network on M3 nodes](https://www.iot-lab.info/tutorials/riot-public-ipv66lowpan-network-with-m3-nodes/)
* [Public IPv6/6LoWPAN network on A8-M3 nodes](https://www.iot-lab.info/tutorials/riot-public-ipv66lowpan-network-with-a8-m3-nodes/)
* [CoAP server with public IPv6/6LoWPAN network on M3 nodes](https://www.iot-lab.info/tutorials/coap-using-riot-with-m3-nodes)
* [CoAP server with public IPv6/6LoWPAN network on A8-M3 nodes](https://www.iot-lab.info/tutorials/coap-riot-with-a8-m3-nodes/)
* [MQTT-SN with RIOT on A8-M3 nodes](https://www.iot-lab.info/tutorials/mqtt-sn-using-riot-with-a8-m3-nodes)
