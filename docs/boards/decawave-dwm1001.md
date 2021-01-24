---
board: Decawave DWM1001
title: Decawave DWM1001
group: boards
---


The `dwm1001` board corresponds to the
[Decawave DWM1001-DEV](https://www.decawave.com/product/dwm1001-development-board/) board. It
runs on an nRF52832 ARM CortexM4 microcontroller from Nordic with BLE and UWB (Ultra-Wide Band) radio
support.

<div style="text-align:center">
<img src="{{ '/assets/images/docs/boards/dwm1001/' | relative_url}}dwm1001.jpeg" style="width:30%;"/>
</div>

The `dwm1001` board can reset, debug and program the ARM Cortex M4
through the embedded debugger (JLink) connected to the gateway USB port. This
component also allows a UART connection to the M4.

## IoT-LAB special configuration

The serial connection baudrate should be configured at **115200 bauds** in the
firmware and use UART0 on pin 11 (RX) and 5 (TX).

## Schematics and Datasheets

The hardware configuration is available [<i class="far fa-file-pdf"/>&nbsp;here](https://www.decawave.com/dwm1001dev/schematic/).

The board is running on an [<i class="far fa-file-pdf"/>&nbsp;nrf52832](https://infocenter.nordicsemi.com/pdf/nRF52832_PS_v1.4.pdf)
microcontroller.
