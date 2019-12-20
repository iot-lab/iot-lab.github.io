---
title: Microchip SAMR30 Xplained Pro
group: boards
---

The SAMR30 open node is based on an
[<i class="far fa-file-pdf"/>&nbsp;Microchip SAM R30 Xplained Pro evaluation kit](http://ww1.microchip.com/downloads/en/DeviceDoc/50002612A.pdf)
built on top of an Microchip ARM Cortex M0 micro-controller. This open node
also contains an SubGHz radio interface.

<div style="text-align:center">
<img src="{{ '/assets/images/docs/boards/samr30/' | relative_url}}samr30.jpg" style="width:50%;"/>
</div>

The SAMR30 Open Node can reset, debug and program the ARM Cortex M0 through the
embedded debugger (EDBG) connected to the gateway USB port. This component also
allows a UART connection to the M0. The input power source is configured
through the power management.

## IoT-LAB special configuration

The serial connection baudrate should be configured at **115200 bauds** in the
firmware.

## Schematics and Datasheets

In details, the main hardware components  contained in the node are :
  * [<i class="far fa-file-pdf"/>&nbsp;ATSAMR30G18A](http://ww1.microchip.com/downloads/en/DeviceDoc/70005303B.pdf)
  * Radio interface [<i class="far fa-file-pdf"/>&nbsp;AT86RF212](AT86RF212)
