---
board: Microchip SAMR34
title: Microchip SAMR34 Xplained Pro
group: boards
---

The SAMR34 board is based on an
[<i class="far fa-file-pdf"/>&nbsp;Microchip SAM R34 Xplained Pro evaluation kit](https://ww1.microchip.com/downloads/en/DeviceDoc/SAM-R34-Xplained-Pro-User-Guide-DS50002803D.pdf)
built on top of an Microchip ARM Cortex M0+ micro-controller. This board
also provides a LoRa radio transceiver.

<div style="text-align:center">
<img src="{{ '/assets/images/docs/boards/samr34/' | relative_url}}samr34.jpg" style="width:50%;"/>
</div>

The SAMR34 board can reset, debug and program the ARM Cortex M0 through the
embedded debugger (OpenOCD) connected to the gateway USB port. This component also
allows a UART connection to the M0. The input power source is configured
through the power management.

## IoT-LAB special configuration

The serial connection baudrate should be configured at **115200 bauds** in the
firmware.

## Schematics and Datasheets

In details, the main hardware components  contained in the node are :
  * [<i class="far fa-file-pdf"/>&nbsp;ATSAMR34J18](https://ww1.microchip.com/downloads/en/DeviceDoc/SAM-R34-R35-Low-Power-LoRa-Sub-GHz-SiP-Data-Sheet-DS70005356C.pdf)
