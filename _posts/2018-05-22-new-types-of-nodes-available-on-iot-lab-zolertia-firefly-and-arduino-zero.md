---
title: 'New boards available on IoT-LAB: Zolertia Firefly and Arduino Zero'
---
![]({{ '/assets/images/posts/' | relative_url }}firefly-4-zolertia.jpg)
![]({{ '/assets/images/posts/' | relative_url }}ArduinoZero.png)
{: .text-center}

After the addition of SAMR21 and LoRa boards we want to formally announce the availability of new types of boards on some IoT-LAB sites, which will permit a wider range of possibilities on the testbed.
{: .lead}

- **9 [Zolertia Firefly]({{ site.baseurl }}{% link docs/boards/zolertia-firefly.md %}) boards**, featuring two radios (2.4 GHz 802.15.4 Zigbee and
sub-GHz), have been deployed on the Lille site. They are deployed throughout
the building and, depending on the firmware you flash, will enable heterogeneous
networking with co-located regular M3 boards.
- **3 [Arduino Zero]({{ site.baseurl }}{% link docs/boards/arduino-zero.md %}) boards** with XBee shields have been deployed on the Saclay site.
They are close to the existing M3 and SAMR21 boards and thus allow to test
802.15.4 (2.4GHz) interoperability between different types of radio.

If you have some hardware that you would like to see deployed on Iot-LAB, check
out this [documentation]({{ site.baseurl }}{% link docs/boards/add-new-board.md %}) to implement the initial support and we will help you to finalize the on site deployment.

Don’t hesitate to reach out to us on [https://github.com/iot-lab/iot-lab/issues/](https://github.com/iot-lab/iot-lab/issues/) for any issue you might have with the new boards.
