---
board: Arduino Zero
group: boards
---

The [Arduino Zero](https://store.arduino.cc/arduino-zero) open node is one the
official Arduino boards and is running on a Microchip ARM Cortex M0
micro-controller.

<div style="text-align:center">
<img src="{{ '/assets/images/docs/boards/arduino-zero/' | relative_url}}arduino-zero.jpg" style="width:50%;"/>
</div>

The Arduino Zero open node can reset, debug and program the ARM Cortex M0 through the
embedded debugger (EDBG) connected to the gateway USB port. This component also
allows a UART connection to the M0.

## IoT-LAB special configuration

The serial connection baudrate should be configured at **115200 bauds** in the
firmware and use the `USART` from `SERCOM5` on pins `PB23` (RX) and `PB22` (TX).

## Schematics and Datasheets

Schematics are available on the Arduino website [<i class="far fa-file-pdf"/>&nbsp;here](https://www.arduino.cc/en/uploads/Main/ArduinoMKRZero-schematic.pdf).

The boards is running on an [<i class="far fa-file-pdf"/>&nbsp;ATSAMD21G18A](http://ww1.microchip.com/downloads/en/DeviceDoc/SAMD21-Family-DataSheet-DS40001882D.pdf).

## Extensions

Nodes in **Saclay site (arduino-zero-1 to arduino-zero-3)** are equipped with
wireless and sensors extensions:

### 802.15.4

The wireless extension is providing access to an
[<i class="far fa-file-pdf"/>&nbsp;XBee](https://www.digi.com/resources/documentation/digidocs/pdfs/90000982.pdf)
module, compatible with 802.15.4 communication protocol.

The XBee module can be controlled from the board via UART connected to Arduino
pins D0 and D1. Use the `USART` from `SERCOM0` on pins PA11 (RX) and PA10 (TX).
The baudrate must be **9600 bauds**.

### Sensors

The sensors extension is a
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
