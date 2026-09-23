---
board: Raspberry Pico WH
group: boards
---

The Raspberry Pi Pico WH board is based on the [RP2040 microcontroller](https://pip-assets.raspberrypi.com/categories/686-raspberry-pi-pico-w/documents/RP-008312-DS-2-pico-w-datasheet.pdf), featuring a dual-core ARM Cortex-M0+ processor.

The board includes an Infineon CYW43439 wireless chip providing
2.4 GHz Wi-Fi and Bluetooth connectivity.

The Pico WH is the Raspberry Pi Pico W variant with pre-soldered headers.

<div style="text-align:center"> 
<img src="{{ '/assets/images/docs/boards/raspberry-pico-wh/' | relative_url}}
raspberry-pico-wh.png" style="width:20%;"/> 
</div>

## IoT-LAB special configuration

In IoT-LAB, the Raspberry Pi Pico WH is connected to a [Debug Probe](https://www.raspberrypi.com/documentation/microcontrollers/debug-probe.html#about-the-debug-probe) used for
remote programming, debugging and serial communication.

* Firmware is remotely programmed through the Debug Probe using the RP2040 SWD
interface.  The SWD interface is connected to the Pico WH debug interface on pins `SWCLK`, `SWDIO` and `GND`.

* The serial console is connected through UART0 on pins `GP0` (UART0 TX) and `GP1` (UART0 RX). The serial connection should be configured at **115200 bauds**.

## Datasheet and documentation

You can find access to the documentation on the [Pico microcontroller boards](https://www.raspberrypi.com/documentation/microcontrollers/pico-series.html).