---
board: OpenMoteB
group: boards
---

The [OpenMote B board](https://www.industrialshields.com/shop/product/is-omb-001-openmote-b-721#attr=) is an  an Ultra Low-power board (sleep < 50µA) including 2 radio chips operating in the 2.4Ghz and 868MHz band. It allows scenarios mixing short and long range applications.

<div style="text-align:center">
<img src="{{ '/assets/images/boards/' | relative_url}}openmoteb.jpg" style="width:50%;"/>
</div>

Inside the IoT-LAB testbed, the OpenMote B board is associated with the [JLink Segger](https://www.segger.com/products/debug-probes/j-link/models/j-link-edu-mini/) in order to reliably flash and reset the MCU.

## IoT-LAB special configuration

The serial connection baudrate should be configured at **115200 bauds** in the
firmware.

## Schematics and Datasheets

* [<i class="far fa-file-pdf"/>&nbsp;201908-OpenMote User_Guide](https://www.industrialshields.com/attachment/download?attachment_id=208800)
