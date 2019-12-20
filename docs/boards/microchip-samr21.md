---
title: Microchip SAMR21 Xplained Pro
group: boards
---

The SAMR21 open node is based on an
[<i class="far fa-file-pdf"/>&nbsp;Microchip SAM R21 Xplained Pro evaluation kit](http://ww1.microchip.com/downloads/en/DeviceDoc/Atmel-42243-SAMR21-Xplained-Pro_User-Guide.pdf)
built on top of an Microchip ARM Cortex M0 micro-controller. This new open node
also contains an IEEE 802.15.4 Atmel radio interface at 2.4 GHz.

<div style="text-align:center">
<img src="{{ '/assets/images/docs/boards/samr21/' | relative_url}}samr21.jpg" style="width:50%;"/>
</div>

The SAMR21 Open Node can reset, debug and program the ARM Cortex M0 through the
embedded debugger (EDBG) connected to the gateway USB port. This component also
allows a UART connection to the M0. The input power source is configured
through the power management.

## IoT-LAB special configuration

The serial connection baudrate should be configured at **115200 bauds** in the
firmware.

## Schematics and Datasheets

In details, the main hardware components  contained in the node are :
  * [<i class="far fa-file-pdf"/>&nbsp;ATSAMR21G18A](http://ww1.microchip.com/downloads/en/devicedoc/sam-r21_datasheet.pdf)
    (48 MHz, 32bits, 32kB RAM, 256kB flash)
  * Radio interface 2.4 GHz [<i class="far fa-file-pdf"/>&nbsp;AT86RF233](http://ww1.microchip.com/downloads/en/devicedoc/atmel-8351-mcu_wireless-at86rf233_datasheet.pdf)
  * One on-board LED (orange)

## Extensions with sensors

Nodes in **Saclay site (samr21-1 to samr21-15)** are equipped with
[<i class="far fa-file-pdf"/>&nbsp;Microchip IO1 Xplained extension](http://ww1.microchip.com/downloads/en/devicedoc/atmel-8351-mcu_wireless-at86rf233_datasheet.pdf).
On those nodes, extra sensors are also available:
  * a Light sensor [<i class="far fa-file-pdf"/>&nbsp;Vishay TEMT600](http://www.vishay.com/docs/81579/temt6000.pdf)
  * a Temperature sensor [<i class="far fa-file-pdf"/>&nbsp;Atmel AT30TSE758](https://www.mouser.com/datasheet/2/36/doc8751-68941.pdf)
  * an extra LED (orange)
  * a microSD Card Connector
