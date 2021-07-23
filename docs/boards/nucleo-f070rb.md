---
board: Nucleo F070RB
title: Nucleo-F070RB
group: boards
---

The Nucleo F070RB board is based on an
[<i class="far fa-file-pdf"/>&nbsp;MB1136 reference board](https://www.st.com/resource/en/user_manual/dm00105823-stm32-nucleo64-boards-mb1136-stmicroelectronics.pdf)
built on top of an STM32 micro-controller in LQFP64 package.

<div style="text-align:center">
<img src="{{ '/assets/images/docs/boards/nucleo-f070rb/' | relative_url}}nucleo-f070rb.jpg" style="width:40%;"/>
</div>

The Nucleo-F070RB board can reset, debug and program the STM32 through the
embedded debugger (ST-LINK) connected to the gateway USB port. The input power source is configured
through the power management.

## IoT-LAB special configuration

The serial connection baudrate should be configured at **115200 bauds** in the
firmware.

## Schematics and Datasheets

In details, the main hardware components  contained in the node are :
  * [<i class="far fa-file-pdf"/>&nbsp;STM32 Nucleo-64 board](https://www.farnell.com/datasheets/2308719.pdf)

## Extensions

Nodes in **Nantes site** are equipped with wireless extensions.

STMicroelectronics X-NUCLEO-IDB05A2 BLUETOOTH Low Energy (BLE) Expansion Board provides a demonstration and development platform for the BlueNRG-M0 BLE Network Processor Module.
The BlueNRG-M0 is Bluetooth v4.2 compliant and FCC and IC certified.It supports simultaneous master/slave roles and can behave as a Bluetooth Low Energy sensor and hub device at the same time.
