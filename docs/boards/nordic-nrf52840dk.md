---
title: Nordic nRF52840DK
group: boards
---

The NRF52840DK open node is a [Nordic nRF52840DK](http://infocenter.nordicsemi.com/pdf/nRF52840_DK_User_Guide_v1.2.pdf)
This open node provides a BLE radio interface and a 802.15.4 radio interface.

<div style="text-align:center">
<img src="https://www.nordicsemi.com/-/media/Images/Products/DevKits/nRF52-Series/nRF52840-DK/nRF52840-DK.png" style="width:20%;"/>
</div>

The nRF52840DK Open Node can reset, debug and program the ARM Cortex M4 through
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
    [HTS221](https://www.st.com/resource/en/datasheet/hts221.pdf)
  * an atmospheric pressure sensor
    [LPS22HB](https://www.st.com/resource/en/datasheet/dm00140895.pdf)
  * an accelerometer sensor
    [LSM6DSL](https://www.st.com/resource/en/datasheet/lsm6dsl.pdf)
  * an accelerometer sensor
    [LSM303AGR](https://www.st.com/resource/en/datasheet/lsm303agr.pdf)

## Example firmware

IoT-LAB provides an [example firmware](https://raw.githubusercontent.com/wiki/iot-lab/iot-lab/firmwares/custom/nrf52840dk-saul.elf)
that can be used on nRF52840-DK boards.
This firmware is based on [RIOT-OS saul example](https://github.com/RIOT-OS/RIOT/tree/master/examples/saul).
The firmware can interact with the HTS221 and LSM6DSL sensors, as well as with
the 4 on-boards LEDs and buttons.
Example of RIOT shell commands:
<pre>
% list available commands
help
% list available actuators and sensors
saul
% read temperature value
saul read 8
% read relative humidity value
saul read 9
</pre>


