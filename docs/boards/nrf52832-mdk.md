---
title: Makerdiary nRF52832-MDK
group: boards
---


The `nrf52832-mdk` open node corresponds to the
[Makerdiary nRF52832-MDK v2](https://wiki.makerdiary.com/nrf52832-mdk/) board. It
runs on an nRF52832 ARM CortexM4 microcontroller from Nordic with BLE radio
support.

<div style="text-align:center">
<img src="{{ '/assets/images/docs/boards/nrf52832-mdk/' | relative_url}}nrf52832-mdk.jpeg" style="width:50%;"/>
</div>

The `nrf52832-mdk` open node can reset, debug and program the ARM Cortex M4
through the embedded debugger (DapLink) connected to the gateway USB port. This
component also allows a UART connection to the M4.

## IoT-LAB special configuration

The serial connection baudrate should be configured at **115200 bauds** in the
firmware and use UART0 on pin 19 (RX) and 20 (TX).

## Schematics and Datasheets

The hardware configuration is available [<i class="far fa-file-pdf"/>&nbsp;here](https://wiki.makerdiary.com/nrf52832-mdk/hardware/nRF52832-MDK_SCH_V2.0.pdf).

The board is running on an [<i class="far fa-file-pdf"/>&nbsp;nrf52832](https://infocenter.nordicsemi.com/pdf/nRF52832_PS_v1.4.pdf)
microcontroller.
