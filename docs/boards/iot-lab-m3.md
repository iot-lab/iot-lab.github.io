---
title: IoT-LAB M3
group: boards
---

<!-- * TOC
{:toc} -->

The M3 open node is based on a STM32 (ARM Cortex M3) micro-controller. Like the WSN430 node, this new generation contains a set of sensors and a radio interface. Main evolutions are a more powerful 32-bits processing, a new ATMEL radio interface in 2.4 GHz and more sensors.


<div style="text-align:center">
<img src="{{ '/assets/images/docs/boards/m3/' | relative_url}}archiopenm3.png" style="width:50%;"/>
</div>

The M3 Open Node can reset, debug and program the STM32 on JTAG through the FTDI4232H connected to the USB. This component allows also a UART link to the STM32. The Open Node connector gives access to 3 STM32/GPIO and the STM32/I2C. Two power lines are accessible on this connector :
  * a + 5.0 volts for the board power supply
  * a 3.3 volts for the consumption monitoring of the STM32, the RF component and the sensors

The M3 Open Node can be used in standalone without a gateway connected to the M3 Open node connector. The board powering is then assumed by a battery (in2) or by the USB connector duplicated (in3). The input power source is configured through the power management.

## Schematics and Datasheets

In details, the main hardware components  contained in the node are :
  * [STM32F103REY](http://www.st.com/web/catalog/mmc/FM141/SC1169/SS1031/LN1565/PF164485) (72 MHz, 32bits, 64kB RAM)
  * Radio interface 2.4 GHz [AT86RF231](http://www.atmel.com/images/doc8111.pdf)
  * Sensors
    * Light sensor [ISL29020](http://www.intersil.com/en/products/optoelectronics/ambient-light-sensors/light-to-digital-sensors/ISL29020.html)
    * Pressure sensor [LPS331AP](http://www.st.com/web/catalog/sense_power/FM89/SC1316/PF251601)
    * Tri-axis accelerometer/magnetometer [LSM303DLHC](http://www.st.com/web/catalog/sense_power/FM89/SC1449/PF251940)
    * Tri-axis gyrometer [L3G4200D](http://www.st.com/web/catalog/sense_power/FM89/SC1288/PF250373)
  * External Nor flash (128 Mbits) [N25Q128A13E1240F](http://www.datasheet4u.com/download.php?id=683085)
  * Three LEDs (green, red, orange)
  * 3,7 V [LIPO battery](http://www.gmbattery.com/Datasheet/LIPO/LIPO-063040.pdf) (650 mAh)

The complete schematics are available [here](http://github.com/iot-lab/iot-lab/wiki/Docs/openm3-schematics.pdf).

## Bugs

  * The second UART on Open node connector is not useable (wires RX an TX inversed)
