---
title: IoT-LAB A8 M3
group: boards
---

The A8 open node is based on a TI SITARA AM3505 which is a high-performance ARM Cortex-A8 microprocessor. Its 600 MHz clock speed enable to run an embedded Linux or Android.It enables to run applications used in advanced devices such as set-top box or smartphone/tablet in order to concentrate sensors information. 

<div style="text-align:center">
<img src="{{ '/assets/images/docs/boards/a8/' | relative_url}}archiopena8.png" style="width:50%;"/>
</div>

## Schematics and Datasheets

The A8 open node also contains a fully controllable and programmable STM32, using the ARM Cortex-A8 processor through an USB/FTDI device. Like the M3 open node, the STM32 gives access to sensors (tri-axis gyro and accelerometer/magnetometer) and wireless communication. The TI SITARA can be debugged through a second FTDI device via the USB port on A8 open node connector. Two external USB ports and one ethernet (on A8 open node connector) are connected to the main processor.

Concerning the power consumption, only the global + 5 volts is monitored.

As an option, a GPS module can be connected to the main processor. It can be used for time synchronisation using the PPS line. This line can be connected to the local STM32 or propagated through a open node connector GPIO. The choice is made by a jumper. 

[More information about the GPS module](https://github.com/iot-lab/iot-lab/wiki/Hardware_A8 GPS).

<div style="text-align:center">
<img src="{{ '/assets/images/docs/boards/a8/' | relative_url}}a8opennode.png" style="width:50%;"/>
</div>

 Main hardware components contained in this node are :

  * A Variscite [VAR-SOM-AM35 CPU](http://www.variscite.com/products/system-on-module-som/cortex-a8/var-som-am35-cpu-ti-am3517-am3505) which a high performance System On Module.
    * It is a board of the shell based on a [TI SITARA AM3505](http://www.ti.com/product/am3505) (600 Mhz, 256 MB)
  * A “co-microcontroller” based on [STM32F103REY](http://www.st.com/web/catalog/mmc/FM141/SC1169/SS1031/LN1565/PF164485) (72 MHz, 32bits, 64kB RAM) which controls :
    * Radio interface 2.4 GHz [AT86RF231](http://www.atmel.com/images/doc8111.pdf)
    * Tri-axis accelerometer/magnetometer [L3G4200D](http://www.st.com/web/catalog/sense_power/FM89/SC1288/PF250373)
    * Tri-axis gyrometer [LSM303DLHC](http://www.st.com/web/catalog/sense_power/FM89/SC1449/PF251940)
    * A USB device [FTDI2232H](http://www.ftdichip.com/Products/ICs/FT2232H.htm) to control UART and JTAG
  * Three LEDs (green, red, orange)
  * 3,7 V [LIPO battery](http://www.gmbattery.com/Datasheet/LIPO/LIPO-063040.pdf) (600 mAh)

Options
   * [[A8-GPS|Hardware_A8 GPS]]: A GPS device [MAX-6Q](https://www.u-blox.com/en/product/max-6-series)

The complete schematics are available [here](http://github.com/iot-lab/iot-lab/wiki/Docs/opena8-schematics.pdf).

## GPS

Some iot-lab nodes are equipped with a A8 open node with
the GPS option:

 * 165 nodes on Saclay site (all open-a8 nodes)
 * 32 nodes on Grenoble site ([open-a8 list](https://github.com/iot-lab/iot-lab/wiki/Hardware_GPS_Gre))

Both sites are equipped with an internal repeater GPS
antenna. The GPS signal reception on each node allows using the GPS clock
as a precise time synchronization mechanism. 

### Hardware

* The board GPS receiver is the [MAX-6Q](https://www.u-blox.com/en/product/max-6-series)
* The indoor GPS repeater is the [Hanger Re-Radiating Kit - HNRRKIT](https://www.gpsnetworking.com/products/hnrrkit) (Used in Grenoble)

### Usage for timing

The M3 control node and the A8-M3 associated to the A8 open node can read
by interruption the GPS PPS (Pulse Per Second) signal. This PPS
acquisition can be used to counterbalance the clock M3 drift very accurately each
second.

This local precise A8-M3 timer can be initialized by Open A8 NTP time (Network Time Protocol) through the uart link, or by using the control node unix time through the i2c link.

### Example
An example is provided allowing a [GPS Synced Sniffer on A8 open-nodes](https://github.com/iot-lab/openlab/blob/master/appli/iotlab_examples/gps_synced_sniffer/README.md). It used open-a8 nodes GPS to precisely time sniffed radio packet.


The hardware architecture diagram :

<div style="text-align:center">
<img src="{{ '/assets/images/docs/boards/a8/' | relative_url}}libtimesynchro.png" style="width:50%;"/>
</div>

## Bugs

