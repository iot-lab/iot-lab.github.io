---
board: Raspberry Pi 3
group: boards
---

The [Raspberry Pi 3 Model B](https://www.raspberrypi.com/products/raspberry-pi-3-model-b/) is the third generation Raspberry Pi. It is based on the Broadcom BCM2837 system-on-chip (SoC) includes four high-performance ARM Cortex-A53 processing cores running at 1.2GHz and is linked to a 1GB LPDDR2 memory module. For connectivity it integrates BCM43438 wireless LAN and Bluetooth Low Energy (BLE) on board.

<div style="text-align:center">
<img src="{{ '/assets/images/boards/' | relative_url}}raspberry-pi-3.png" style="width:50%;"/>
</div>


## Co-microcontroller

To provide 802.15.4 connectivity all RPI3B(s) are deployed with a co-microcontroller. It can be programmed from the board through USB (see [Programming](#programming)).

Nodes in **Grenoble site (rpi3-1 to rpi3-5)** are equipped with the [SAMR21 co-microcontroller]({{ site.baseurl }}{% link docs/boards/microchip-samr21.md %})

## Ethernet
The Raspberry Pi 3 board features an Ethernet interface, enabling it to connect to a LAN and to communicate with the internet. The boards are only accessible by SSH in IPV4 via the SSH frontend and in IPV6 from the Internet.

## Power supply
Concerning the power consumption, only the global + 5 volts is monitored.

## Programming

The Raspberry Pi 3 board run an embedded Linux that is built with [Yocto]({{ site.baseurl }}{% link docs/os/yocto.md %}). You can reset, debug and program the co-microcontroller. We provide in the Linux image scripts to perform these operations (i.e. `iotlab_<flash|reset|debug>`). This component allows also a UART link (i.e. `/dev/iotlab/<tty_co_microcontroller>`)


## Schematics and Datasheets

You can find all schematics and datasheets [here](https://datasheets.raspberrypi.com/)
