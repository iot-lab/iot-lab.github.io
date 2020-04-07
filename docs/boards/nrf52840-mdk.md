---
board: nRF52840-MDK
title: Makerdiary nRF52840-MDK
group: boards
---

The `nrf52840-mdk` open node corresponds to the
[Makerdiary nRF52840-MDK](https://wiki.makerdiary.com/nrf52840-mdk/) board. It
runs on an nRF52840 ARM CortexM4 microcontroller from Nordic with BLE and
802.15.4 radio support.

<div style="text-align:center">
<img src="{{ '/assets/images/docs/boards/nrf52840-mdk/' | relative_url}}nrf52840-mdk.jpg" style="width:50%;"/>
</div>

The `nrf52840-mdk` open node can reset, debug and program the ARM Cortex M4
through the embedded debugger (DapLink) connected to the gateway USB port. This
component also allows a UART connection to the M4.

## IoT-LAB special configuration

The serial connection baudrate should be configured at **115200 bauds** in the
firmware and use UART0/UARTE0 on pin 19 (RX) and 20 (TX).

## Schematics and Datasheets

The hardware configuration is available [<i class="far fa-file-pdf"/>&nbsp;here](https://wiki.makerdiary.com/nrf52840-mdk/hardware/nrf52840-mdk-schematic_v1_0.pdf).

The board is running on an [<i class="far fa-file-pdf"/>&nbsp;nrf52840](https://infocenter.nordicsemi.com/pdf/nRF52840_PS_v1.0.pdf)
microcontroller.
