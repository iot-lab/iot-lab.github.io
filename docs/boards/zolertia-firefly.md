---
title: Zolertia Firefly
group: boards
---

The firefly open node is based on an
[Zolertia Firefly board](https://zolertia.io/product/firefly/)
built on top of a TI CC2538 ARM Cortex M3 micro-controller. This open node
provides 802.15.4 radio support.

<div style="text-align:center">
<img src="{{ '/assets/images/docs/boards/firefly/' | relative_url}}firefly.jpg" style="width:50%;"/>
</div>

The firefly Open Node can reset and program the ARM Cortex M3 through serial
port connected to the gateway USB port.

## IoT-LAB special configuration

The serial connection baudrate should be configured at **115200 bauds** in the
firmware.

## Schematics and Datasheets

In details, the main hardware components contained in the node is the
[<i class="far fa-file-pdf"/>&nbsp;CC2538](http://www.ti.com/lit/ds/symlink/cc2538.pdf)
