---
board: Decawave DWM1001
title: Decawave DWM1001
group: boards
---


The `dwm1001` board available in IoT-LAB are Decawave [DWM1001-DEV](https://www.decawave.com/product/dwm1001-development-board/) boards. They are build around a [DWM1001C module](https://www.qorvo.com/products/p/DWM1001C) which contains a nRF52832 ARM CortexM4 microcontroller from Nordic with BLE and a [DW1000](https://www.qorvo.com/products/p/DW1000) UWB (Ultra-Wide Band) transceiver.

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

Some parameters (notably the antenna delays) of the boards are factory-calibrated by Decawave/Qorvo. The calibration parameters can be read by the firmware from the One-Time Programmable memory (OTP) of the DW1000 chip.

The antenna delays for some of IoT-LAB boards are as follows:


| Node                          | Device UID | Delay Hex | Delay Decimal |
| :---:                         | :---:      | :---:     | :---:         |
| dwm1001-1.lille.iot-lab.info  | 122E       | 404A      | 16458         |
| dwm1001-2.lille.iot-lab.info  | 0420       | 404B      | 16459         |
| dwm1001-3.lille.iot-lab.info  | 0C28       | 4049      | 16457         |
| dwm1001-4.lille.iot-lab.info  | 0BA1       | 4058      | 16472         |
| dwm1001-5.lille.iot-lab.info  | DB27       | 404D      | 16461         |
| dwm1001-6.lille.iot-lab.info  | 0295       | 404E      | 16462         |
| dwm1001-7.lille.iot-lab.info  | 8E2B       | 4049      | 16457         |
| dwm1001-8.lille.iot-lab.info  | 8089       | 4058      | 16472         |
| dwm1001-9.lille.iot-lab.info  | 08A6       | 4058      | 16472         |
| dwm1001-10.lille.iot-lab.info | D6B0       | 4058      | 16472         |
| dwm1001-11.lille.iot-lab.info | D1B6       | 4034      | 16436         |
| dwm1001-12.lille.iot-lab.info | DC19       | 4039      | 16441         |
| dwm1001-13.lille.iot-lab.info | 4827       | 404B      | 16459         |
| dwm1001-14.lille.iot-lab.info | D4B6       | 4035      | 16437         |
{:.table-bordered}
 
