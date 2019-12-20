---
title: BBC micro:bit
group: boards
---

The microbit open node corresponds to the official
[BBC micro:bit](https://microbit.org/) board. It runs on an nRF51 ARM CortexM0
microcontroller from Nordic with BLE radio.

<div style="text-align:center">
<img src="{{ '/assets/images/docs/boards/microbit/' | relative_url}}microbit.png" style="width:50%;"/>
</div>

The microbit open node can reset, debug and program the ARM Cortex M0 through the
embedded debugger (DapLink) connected to the gateway USB port. This component also
allows a UART connection to the M0.

## IoT-LAB special configuration

The serial connection baudrate should be configured at **115200 bauds** in the
firmware and use the first UART on pin 25 (RX) and 24 (TX).

## Schematics and Datasheets

The hardware configuration is available [here](https://tech.microbit.org/hardware/).

The boards is running on an [<i class="far fa-file-pdf"/>&nbsp;nrf51822](https://infocenter.nordicsemi.com/pdf/nRF51822_PS_v3.1.pdf).
