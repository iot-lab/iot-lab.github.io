---
title: IoT-LAB Gateway
---

The new generation is more generic and can host several open node like the M3 or A8 open nodes. Some IoT-LAB nodes will be assigned on the platform to host other type of open nodes using the USB dedicated port; it will also  involve to customize the firmware.

An IoT-LAB host node embeds the gateway node and the control node dedicated to monitor the open node. The main processor board is a [Variscite VAR-SOM-AM35 CPU](http://www.variscite.com/products/system-on-module-som/cortex-a8/var-som-am35-cpu-ti-am3517-am3505) like the A8 open node. Regarding connectivity, the board offers three USB ports, three Ethernet ports and the dedicated open node connector.

The board can be powered either : over ethernet (PoE) or by an external power supply (jack connector). The host node monitors the open node power supply mode : main supply or by a external battery (connector).

The dedicated open node connector offers a USB port to control the open node, a UART port, a I2C bus, an ethernet port and several GPIOs.

The main processor controls the "co-processor" which is a [STM32](http://www.st.com/web/catalog/mmc/FM141/SC1169/SS1031/LN1565/PF164485) and a wireless chip [AT86RF231](http://www.atmel.com/images/doc8111.pdf) like the M3 open node.


This host node can also measure current and voltage (+3.3v, +5.0v, external battery) supplying the open-node. It is performed thanks to the co-processor connected to an [INA226](http://www.ti.com/product/ina226&DCMP=analog_signalchain_mr&HQS=ina226-pr).

The detailed architecture of the host-node is illustrated below :

<img src="{{ '/assets/images/archives/' | relative_url}}iotlabgateway-archi.png" style="width:50%;"/>

The complete schematics is avaible  [<i class="far fa-file-pdf"/>]({{ site.baseurl }}{% link assets/misc/archives/iotlabgateway-schematics.pdf %})
