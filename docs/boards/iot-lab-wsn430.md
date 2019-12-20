---
title: IoT-LAB WSN430
group: boards
---

The WSN430 open node is a WSN430 node based on a low power MSP430-based platform, with a fully functional ISM radio interface and a set of standard sensors. Concerning the radio, two versions are developed: Version 1.3b presents an open 868MHz radio interface while version 1.4 has an IEEE 802.15.4 radio interface at 2.4GHz. 

<div style="text-align:center">
<img src="{{ '/assets/images/docs/boards/wsn430/' | relative_url}}archiopenwsn.png" style="width:50%;"/>
</div>

## Schematics and Datasheets

<div style="text-align:center">
<img src="{{ '/assets/images/docs/boards/wsn430/' | relative_url}}wsn430.png" style="width:50%;"/>
</div>

In details, the hardware components are :

**Micro-controller MSP430** - The MSP430 core used is  a [MSP430F1611 MCU](http://www.ti.com/product/msp430f1611), offering 48kbyte ROM, and 10kbyte RAM. 2 USARTs modules provide SPI, I2C, and UART communications. We also get various I/O lines, interruptables or not, a 6 channels ADC  and a 2 channels ADC/DAC (12 bit resolution).

**Sensors** -  3 physical sensors are mounted on WSN430 nodes :
  * Temperature ([Maxim DS1722](http://www.maximintegrated.com/datasheet/index.mvp/id/2766)), with digital SPI output (connected on USART1 module).
  * Sound (omnidirectional microphone, Kingstate KEEG1540), with analog output. (connected on ADC5)
  * Ambient light ([Taos TSL2550](http://www.alldatasheet.com/datasheet-pdf/pdf/203052/TAOS/TSL2550.html)), with digital I2C output. (connected on USART0 module)

**Radio** - WSN430 nodes in version 1.3b have a 868MHz radio interface. The radio chip is the [TI CC1101](http://www.ti.com/product/cc1101) (software and pin compatible with previous CC1100 version). Two types of antenna are available, the main one being an omnidirectionnal PCB antenna. There is an
option for an external SMA antenna (The SMA connector is not mounted, but pads exists). The type is selected thanks to 2 capacitors (C5, C25 on design board) mounted or not. Note that the PCB antenna is designed to be used with a Varta Polyex battery at the node bottom for right radio propagation.


WSN430 nodes in version 1.4 have a 2.4GHz radio interface. The radio chip is the [TI CC2420](http://www.ti.com/product/cc2420) radio chipset, offering a IEEE802.15.4-compliant interface. The chosen antenna is an omnidirectional SMD chip (reference Fractus Compact Reach Xtend). 

**Serial Number** -  An EEPROM serial number is available thanks to a Maxim [<i class="far fa-file-pdf"/>&nbsp;DS2411](http://datasheets.maximintegrated.com/en/ds/DS2411.pdf) chip, giving each node a unique identifier, readable by the MPS430 firmware over a 1-Wire interface.

**Flash memory** - Additionnal external flash memory is provided on a 1MByte chip ([ST M25P80](http://www.micron.com/parts/nor-flash/serial-nor-flash/m25p80-vmc6g)) accessed through SPI bus.

**Battery charger** - The power supply is controlled by a [Microchip MCP73861](http://www.microchip.com/wwwproducts/Devices.aspx?dDocName=en020210) chip. It allows battery charge,  and is supervised by MSP430 through 2 digital outputs (connected to MSP430 GPIOs).

**Three LEDs (green, red, blue)**

The SensLAB node hardware is described in details in an [<i class="far fa-file-pdf"/>&nbsp;ANR report](http://github.com/iot-lab/iot-lab/wiki/Docs/senslab-deliverable-d1.1a.pdf)  

Here are the two WSN430 schematics, one for each of the radio chips:
  * [<i class="far fa-file-pdf"/>&nbsp;WSN430V1.3B schematics (CC1101 radio)](http://github.com/iot-lab/iot-lab/wiki/Docs/3-wsn430-v1.3b-schema.pdf)
  * [<i class="far fa-file-pdf"/>&nbsp;WSN430V1.4 schematics (CC2420 radio)](http://github.com/iot-lab/iot-lab/wiki/Docs/3-wsn430-v1.4-schema.pdf) 

## Dock

The WSN430 can be used stand-alone using an additional board called "Dock" and a JTAG programmer which allows to program and debug software on the WSN430. More details on [[Hardware_Wsn430 dock]]

## Bugs

  * CC2420 interrupt line (radio packet reception) not wired to the MSP430.
  * Sound sensor is not usable (noise registration)