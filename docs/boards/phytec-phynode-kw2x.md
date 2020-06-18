---
board: Phytec PhyNODE-KW2X
group: boards
---

The Phytec PhyNODE-KW2X provides a 802.15.4 radio interface and run on a NXP
Kinetis KW21D256 microcontroller

<div style="text-align:center">
<img src="{{ '/assets/images/docs/boards/phynode-kw2x/' | relative_url}}phynode-kw2x.jpg" style="width:300px;"/>
</div>

The PhyNODE-KW2X board can reset, debug and program the ARM Cortex M4+ through
the embedded debugger (OpenOCD) connected to the gateway USB port. This
component also allows a UART connection to the M4. The input power source is
configured through the power management.

## IoT-LAB special configuration

The serial connection baudrate should be configured at **115200 bauds** in the
firmware.
