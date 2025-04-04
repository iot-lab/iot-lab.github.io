---
board: Qorvo DWM3001
title: Qorvo DWM3001
group: boards
---


The `dwm3001` boards available in IoT-LAB are Qorvo [DWM3001-CDK](https://www.qorvo.com/products/p/DWM3001CDK) boards. They are build around a [DWM3001C module](https://www.qorvo.com/products/p/DWM3001C) which contains a nRF52833 ARM CortexM4 microcontroller from Nordic with BLE and a [DW3110](https://www.qorvo.com/products/p/DW3110) UWB (Ultra-Wide Band) transceiver.

<div style="text-align:center">
<img src="{{ '/assets/images/docs/boards/dwm3001/' | relative_url}}DWM3001CDK.png" style="width:30%;"/>
</div>

The `dwm1001` board can reset, debug and program the ARM Cortex M4
through the embedded debugger (JLink) connected to the gateway USB port. This
component also allows a UART connection to the M4.

## IoT-LAB special configuration

The serial connection baudrate should be configured at **115200 bauds** in the
firmware and use UART0 on pin 15 (RX) and 19 (TX).


 
