---
board: ST B-L475E-IOT01A
group: boards
---

The [ST B-L475E-IOT01A](https://www.st.com/en/evaluation-tools/b-l475e-iot01a.html)
open node is multi radio capable board running on an ARM CortexM4 STM32L475VG
microcontroller.

<div style="text-align:center">
<img src="{{ '/assets/images/docs/boards/st-iotnode/' | relative_url}}st-iotnode.jpg" style="width:50%;"/>
</div>

It is possible to reset, debug and program the ARM Cortex M4 through the
embedded debugger (ST-LINK) connected to the gateway USB port. This component
also allows a UART connection to the M4.

## IoT-LAB special configuration

The serial connection baudrate should be configured at **115200 bauds** in the
firmware and use `USART2` on pins `PB7` (RX) and `PB6` (TX).

## Schematics and Datasheets

The board datasheet is available [<i class="far fa-file-pdf"/>&nbsp;here](https://www.st.com/resource/en/user_manual/dm00347848.pdf).

The cpu datasheet is available [<i class="far fa-file-pdf"/>&nbsp;here](https://www.st.com/resource/en/datasheet/stm32l475vg.pdf).

## Sensors

The board provides several sensors:
  * a temperature and humidity sensor
    [<i class="far fa-file-pdf"/>&nbsp;HTS221](https://www.st.com/resource/en/datasheet/hts221.pdf)
  * an atmospheric pressure sensor
    [<i class="far fa-file-pdf"/>&nbsp;LPS22HB](https://www.st.com/resource/en/datasheet/dm00140895.pdf)
  * an accelerometer sensor
    [<i class="far fa-file-pdf"/>&nbsp;LSM6DSL](https://www.st.com/resource/en/datasheet/lsm6dsl.pdf)
