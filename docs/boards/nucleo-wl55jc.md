---
board: Nucleo WL55JC
title: Nucleo-WL55JC
group: boards
---

The [Nucleo WL55JC](https://www.st.com/en/evaluation-tools/nucleo-wl55jc.html)
board is LoRa capable board running on ARM CortexM0+ STM32WL55JC  microcontroller.

<div style="text-align:center">
<img src="{{ '/assets/images/docs/boards/nucleo-wl55jc/' | relative_url}}nucleo-wl55jc.png" style="width:40%;"/>
</div>
<br>

It is possible to reset, debug and program the ARM Cortex M0 through the
embedded debugger (ST-LINK) connected to the gateway USB port. This component
also allows a UART connection to the M0.

## IoT-LAB special configuration

The serial connection baudrate should be configured at **115200 bauds** in the
firmware.

## Schematics and Datasheets

In details, the main hardware components  contained in the node are :
  * [<i class="far fa-file-pdf"/>&nbsp;STM32WL Nucleo-64 board](https://www.st.com/resource/en/user_manual/dm00622917-stm32wl-nucleo64-board-mb1389-stmicroelectronics.pdf)

## Sensors extension

Nodes in **Grenoble site (nucleo-wl55jc-1 to nucleo-wl55jc-5)** are equipped with the
[ST X-NUCLEO-IKS01A2](https://www.st.com/en/ecosystems/x-nucleo-iks01a2.html)
shield.
This gives access to external sensors to the nodes:
  * a temperature and humidity sensor
    [<i class="far fa-file-pdf"/>&nbsp;HTS221](https://www.st.com/resource/en/datasheet/hts221.pdf)
  * an atmospheric pressure sensor
    [<i class="far fa-file-pdf"/>&nbsp;LPS22HB](https://www.st.com/resource/en/datasheet/dm00140895.pdf)
  * an accelerometer sensor
    [<i class="far fa-file-pdf"/>&nbsp;LSM6DSL](https://www.st.com/resource/en/datasheet/lsm6dsl.pdf)
  * an accelerometer sensor
    [<i class="far fa-file-pdf"/>&nbsp;LSM303AGR](https://www.st.com/resource/en/datasheet/lsm303agr.pdf)
