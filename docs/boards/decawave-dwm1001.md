---
board: Decawave DWM1001
title: Decawave DWM1001
group: boards
---


The `dwm1001` board available in IoT-LAB are Qorvo (formerly Decawave) [DWM1001-DEV](https://www.qorvo.com/products/p/DWM1001-DEV) boards. They are build around a [DWM1001C module](https://www.qorvo.com/products/p/DWM1001C) which contains a nRF52832 ARM CortexM4 microcontroller from Nordic with BLE and a [DW1000](https://www.qorvo.com/products/p/DW1000) UWB (Ultra-Wide Band) transceiver.

<div style="text-align:center">
<img src="{{ '/assets/images/docs/boards/dwm1001/' | relative_url}}dwm1001.jpeg" style="width:30%;"/>
</div>

The `dwm1001` board can reset, debug and program the ARM Cortex M4
through the embedded debugger (JLink) connected to the gateway USB port. This
component also allows a UART connection to the M4.

## IoT-LAB special configuration

The serial connection baudrate should be configured at **115200 bauds** in the
firmware and use UART0 on pin 11 (RX) and 5 (TX).

## Schematics and Datasheets

The hardware configuration is available [<i class="far fa-file-pdf"/>&nbsp;here](https://www.decawave.com/dwm1001dev/schematic/).

The board is running on an [<i class="far fa-file-pdf"/>&nbsp;nrf52832](https://infocenter.nordicsemi.com/pdf/nRF52832_PS_v1.4.pdf)
microcontroller.


## Calibration of Antenna Delays

Some parameters (notably the antenna delays) of the boards are factory-calibrated. The calibration parameters can be read by the firmware from the One-Time Programmable memory (OTP) of the DW1000 chip (see section 6.3 of [DW1000 user manual](https://www.qorvo.com/products/d/da007967)).

The antenna delays for some of IoT-LAB boards are as follows:


| Node                          | Device UID | Delay Hex | Delay Decimal |
| :---:                         | :---:      | :---:     | :---:         |
| dwm1001-1.lille.iot-lab.info  | 81C1       | 404A      | 16458         |
| dwm1001-2.lille.iot-lab.info  | 8E2C       | 404B      | 16459         |
| dwm1001-3.lille.iot-lab.info  | E9A6       | 4049      | 16457         |
| dwm1001-4.lille.iot-lab.info  | 84B2       | 4058      | 16472         |
| dwm1001-5.lille.iot-lab.info  | BCE1       | 404D      | 16461         |
| dwm1001-6.lille.iot-lab.info  | AA5E       | 404E      | 16462         |
| dwm1001-7.lille.iot-lab.info  | 8DD8       | 4049      | 16457         |
| dwm1001-8.lille.iot-lab.info  | 6A12       | 4058      | 16472         |
| dwm1001-9.lille.iot-lab.info  | FB2E       | 4058      | 16472         |
| dwm1001-10.lille.iot-lab.info | 7FC2       | 4058      | 16472         |
| dwm1001-11.lille.iot-lab.info | 0EFA       | 4034      | 16436         |
| dwm1001-12.lille.iot-lab.info | 333C       | 4039      | 16441         |
| dwm1001-13.lille.iot-lab.info | 65C9       | 404B      | 16459         |
| dwm1001-14.lille.iot-lab.info | 7906       | 4035      | 16437         |
{:.table-bordered}
 
