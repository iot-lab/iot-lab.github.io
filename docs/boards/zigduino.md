---
board: Zigduino
group: boards
---

The [Zigduino board](http://www.logos-electro.com/store/zigduino-r2) (r2) is an Arduino-compatible microcontroller platform that integrates a SOC with a 8-Bit AVR MCU and a IEEE 802.15.4 radio chip (ATmega128RFA1).

<div style="text-align:center">
<img src="{{ '/assets/images/docs/boards/zigduino/' | relative_url}}zigduino.png" style="width:50%;"/>
</div>

The Zigduino board can reset and program through serial port connected to the gateway USB port.

## IoT-LAB special configuration

Most of the Zigduino nodes are deployed in the Strasbourg site with sensors. Some of these nodes are also combined with a LoRa modem in order to offer a dual radio stack IEEE 802.15.4/LoRaWAN.

Two available IoT-LAB nodes archis:

* **Zigduino (atmega128rfa1)**: a basic Zigduino nodes with embedded sensors
  * Primary serial port (console output): **57600 bauds**
  * Sensors
    * [Grove Temperature Humidity sensor](https://wiki.seeedstudio.com/Grove-Temperature_and_Humidity_Sensor_Pro/) (pin 14, A0)
    * [Grove Light sensor](https://wiki.seeedstudio.com/Sensor_light/) (pin 15, A1)
    * [Grove Loudness sensor](https://wiki.seeedstudio.com/Grove-Loudness_Sensor/) (pin 16, A2)
    * [Grove PIR Motion sensor](https://wiki.seeedstudio.com/Grove-PIR_Motion_Sensor/) (pin 4, D4)
* **Zigduino (atmega128rfa1_rn2483)**: extension of previous **Zigduino (atmega128rfa1)**
  * Secondary serial port (LoRa modem): **57600 bauds**
  * [RN2483](https://ww1.microchip.com/downloads/en/DeviceDoc/RN2483-LoRa-Technology-Module-Command-Reference-User-Guide-DS40001784G.pdf) modem with 1.0.3 firmware (LoRaWAN Class A only)
    * TX (pin 1, TXD1)
    * RX (pin 0, RXD1)

## Software

* [Contiki 3.1 with avr-zigduino platform](https://github.com/icube-inetlab/contiki-avr-zigduino)
* [Arduino Zigduino board](https://github.com/icube-inetlab/arduino-zigduino-package)

## Documentation

* [Zigduino r2 manual](http://wiki.logos-electro.com/zigduino-r2-manual)

## Schematics and Datasheets

* [<i class="far fa-file-pdf"/>&nbsp;Zigduino r2 schematic](http://www.logos-electro.com/s/zigduino-v6c-schematic.pdf)
* [<i class="far fa-file-pdf"/>&nbsp;Zigduino r2 pinout](http://www.logos-electro.com/s/zigduino-r2-pinout.pdf)
* [<i class="far fa-file-pdf"/>&nbsp;ATmega128RFA1](https://ww1.microchip.com/downloads/en/DeviceDoc/Atmel-8266-MCU_Wireless-ATmega128RFA1_Datasheet.pdf)
