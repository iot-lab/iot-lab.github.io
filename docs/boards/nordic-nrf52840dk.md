---
board: Nordic nRF52840DK
group: boards
---

The NRF52840DK board is a [<i class="far fa-file-pdf"/>&nbsp;Nordic nRF52840DK](http://infocenter.nordicsemi.com/pdf/nRF52840_DK_User_Guide_v1.2.pdf)
This board provides a BLE radio interface and a 802.15.4 radio interface.

<div style="text-align:center">
<img src="{{ '/assets/images/docs/boards/nrf52840dk/' | relative_url}}nrf52840dk.png" style="width:20%;"/>
</div>

The nRF52840DK board can reset, debug and program the ARM Cortex M4 through
the embedded debugger (OpenOCD) connected to the gateway USB port. This
component also allows a UART connection to the M4. The input power source is
configured through the power management.

## IoT-LAB special configuration

The serial connection baudrate should be configured at **115200 bauds** in the
firmware.

## Extensions with sensors

Nodes in **Saclay site (nrf52840dk-1 to nrf52840dk-10)** are equipped with an
[ST X-NUCLEO-IKS01A2](https://www.st.com/en/ecosystems/x-nucleo-iks01a2.html)
shield.
This gives access to external sensors to the `nrf52840dk` nodes:
  * a temperature and humidity sensor
    [<i class="far fa-file-pdf"/>&nbsp;HTS221](https://www.st.com/resource/en/datasheet/hts221.pdf)
  * an atmospheric pressure sensor
    [<i class="far fa-file-pdf"/>&nbsp;LPS22HB](https://www.st.com/resource/en/datasheet/dm00140895.pdf)
  * an accelerometer sensor
    [<i class="far fa-file-pdf"/>&nbsp;LSM6DSL](https://www.st.com/resource/en/datasheet/lsm6dsl.pdf)
  * an accelerometer sensor
    [<i class="far fa-file-pdf"/>&nbsp;LSM303AGR](https://www.st.com/resource/en/datasheet/lsm303agr.pdf)
