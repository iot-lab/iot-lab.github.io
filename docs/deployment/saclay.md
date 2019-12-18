---
title: Saclay
group: deployment
---

The Saclay testbed is located at [Saclay – Île-de-France](https://goo.gl/maps/zgfEtm1wkp7qPhya6).

## Resources

<table class="table table-striped">
    <thead>
        <tr>
            <td><b>Type</b></td>
            <td><b>IoT-LAB name</b></td>
            <td><b>Count</b></td>
            <td><b>Radio</b></td>
            <td><b>Location</b></td>
        </tr>
    </thead>
    <tbody>
    <tr>
        <td><a href="https://www.iot-lab.info/hardware/a8/">A8</a></td>
        <td>a8</td>
        <td>163</td>
        <td>802.15.4</td>
        <td>Basement (115), Room 2 (30), Room 1 (18)</td>
    </tr>
    <tr>
        <td><a href="https://www.iot-lab.info/hardware/m3/">M3</a></td>
        <td>m3</td>
        <td>12</td>
        <td>802.15.4</td>
        <td>Room 2</td>
    </tr>
    <tr>
        <td><a href="{{ site.baseurl}}/docs/boards/microchip-samr21">SAMR21 Xplained Pro</a></td>
        <td>samr21</td>
        <td>15</td>
        <td>802.15.4</td>
        <td>Room 2</td>
    </tr>
    <tr>
        <td><a href="{{ site.baseurl}}/docs/boards/microchip-samr30">SAMR30 Xplained Pro</a></td>
        <td>samr30</td>
        <td>3</td>
        <td>Sub-GHz</td>
        <td>Basement</td>
    </tr>
    <tr>
        <td><a href="https://www.arduino.cc/en/Main/ArduinoBoardZero">Arduino Zero</a></td>
        <td>arduino-zero</td>
        <td>3</td>
        <td>802.15.4 (XBee)</td>
        <td>Room 2</td>
    </tr>
    <tr>
        <td><a href="http://www.st.com/en/evaluation-tools/b-l072z-lrwan1.html">ST B-L072Z-LRWAN1</a></td>
        <td>st-lrwan1</td>
        <td>25</td>
        <td>LoRa</td>
        <td>Room 1</td>
    </tr>
    <tr>
        <td><a href="{{ site.baseurl}}/docs/boards/nordic-nrf52dk">nRF52DK</a></td>
        <td>nrf52dk</td>
        <td>10</td>
        <td>BLE</td>
        <td>Room 1</td>
    </tr>
    <tr>
        <td><a href="{{ site.baseurl}}/docs/boards/nordic-nrf52840dk">nRF52840DK</a></td>
        <td>nrf52840dk</td>
        <td>10</td>
        <td>802.15.4 + BLE</td>
        <td>Room 1 (5) and Room 2 (5)</td>
    </tr>
    <tr>
        <td><a href="{{ site.baseurl}}/docs/boards/nordic-nrf51dk">nRF51DK</a></td>
        <td>nrf51dk</td>
        <td>5</td>
        <td>BLE</td>
        <td>Room 1</td>
    </tr>
    <tr>
        <td><a href="https://microbit.org/">micro:bit</a></td>
        <td>microbit</td>
        <td>1</td>
        <td>BLE</td>
        <td>Room 1</td>
    </tr>
    <tr>
        <td><a href="https://www.st.com/en/evaluation-tools/b-l475e-iot01a.html">ST B-L475E-IOT01</a></td>
        <td>st-iotnode</td>
        <td>10</td>
        <td>BLE + WiFi + Sub-GHz</td>
        <td>Basement</td>
    </tr>
    <tr>
        <td><a href="https://www.microchip.com/DevelopmentTools/ProductDetails/ATSAMR30-XPRO">SAMR30 Xplained</a></td>
        <td>samr30</td>
        <td>3</td>
        <td>Sub-GHz</td>
        <td>Basement</td>
    </tr>
    <tr>
        <td><a href="{{ site.baseurl}}/docs/boards/nxp-frdm-kw41z">NXP FRDM-KW41Z</a></td>
        <td>frdm-kw41z</td>
        <td>5</td>
        <td>802.15.4 + BLE</td>
        <td>Room 2</td>
    </tr>
    <tr>
        <td><a href="https://github.com/makerdiary/nrf52840-mdk">nRF52840-MDK</a></td>
        <td>nrf52840mdk</td>
        <td>1</td>
        <td>802.15.4 + BLE</td>
        <td>Room 2</td>
    </tr>
    <tr>
        <td><a href="https://www.phytec.in/product/internet-of-things/phynode-sensor-1/">phyNode</a></td>
        <td>phynode</td>
        <td>1</td>
        <td>802.15.4</td>
        <td>Room 2</td>
    </tr>
    </tbody>	
</table>

Ground floor rooms 1 and 2 are equipped with a set of GPS repeaters that are relaying the GPS signal indoor.

## Topology
The platform is distributed over the basement of the building and 2 rooms.

    Room 1: 12 m x 12 m
    Room 2: 12 m x 4 m
    Basement: 41.5 m x 30 m

<div class="container">
    <div class="text-center">
        <img class="pt-3 px-3" src="{{ '/assets/images/deployments/saclay/' | relative_url}}saclay_map.png" style="width:50%;">
    </div>
</div>

## Pictures

<div class="container">
<div class="row">
    <div class="col">
        <img class="pt-3 px-3" src="{{ '/assets/images/deployments/saclay/' | relative_url}}digiteo1.jpg" style="width:100%;">
    </div>
    <div class="col">
        <img class="pt-3 px-3" src="{{ '/assets/images/deployments/saclay/' | relative_url}}digiteo2.jpg" style="width:100%;">
    </div>
    <div class="col">
        <img class="pt-3 px-3" src="{{ '/assets/images/deployments/saclay/' | relative_url}}lora.jpg" style="width:100%;">
    </div>
</div>
<div class="row">
    <div class="col"></div>
    <div class="col">
        <img class="pt-3 px-3" src="{{ '/assets/images/deployments/saclay/' | relative_url}}parking.jpg" style="width:100%;">
    </div>
    <div class="col"></div>
</div>
</div>

## Live camera

You can follow your experiment live on the A8 node with identifier 145
[here](http://demo-fit.saclay.inria.fr).
