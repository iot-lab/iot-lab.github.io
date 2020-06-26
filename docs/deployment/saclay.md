---
title: Saclay
group: deployment
description: On the Saclay site, the nodes are deployed at Inria Saclay – Île-de-France, where they are spread across the basement and 2 rooms. Saclay site offers the most heterogeneous deployment, usefull for multi radio and interoperability scenarios.
---

## Topology
The platform is distributed over the basement of the building and 2 rooms.

<div class="row">
    <div class="col-lg-6 offset-lg-3">
        <img class="img-fluid" src="{{ '/assets/images/deployments/saclay/' | relative_url}}saclay_map.png">
    </div>
</div>

### Basement
The basement is 1250 m2 (41.5 m x 30 m). Nodes are deployed on the cable trays hanging from the ceiling. It contains the following boards:

<table class="table table-striped">
    <thead>
        <tr>
            <td><b>Board type</b></td>
            <td><b>Board id</b></td>
            <td><b>Count</b></td>
            <td><b>Radio(s)</b></td>
            <td><b>Other location</b></td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><a href="https://www.iot-lab.info/hardware/a8/">A8</a></td>
            <td>a8</td>
            <td>115</td>
            <td>802.15.4</td>
            <td>Room 1 (18), Room 2 (30)</td>
        </tr>
        <tr>
            <td><a href="{{ site.baseurl}}{% link docs/boards/microchip-samr30.md %}">SAMR30 Xplained Pro</a></td>
            <td>samr30</td>
            <td>3</td>
            <td>Sub-GHz</td>
            <td></td>
        </tr>
        <tr>
            <td><a href="https://www.st.com/en/evaluation-tools/b-l475e-iot01a.html">ST B-L475E-IOT01</a></td>
            <td>st-iotnode</td>
            <td>10</td>
            <td>BLE + WiFi + Sub-GHz</td>
            <td></td>
        </tr>
    </tbody>
</table>

### Room 1
The room 1 is 144 m2 (12 m x 12 m) and contains the following boards:

<table class="table table-striped">
    <thead>
        <tr>
            <td><b>Board type</b></td>
            <td><b>Board id</b></td>
            <td><b>Count</b></td>
            <td><b>Radio(s)</b></td>
            <td><b>Other location</b></td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><a href="https://www.iot-lab.info/hardware/a8/">A8</a></td>
            <td>a8</td>
            <td>18</td>
            <td>802.15.4</td>
            <td>Basement (115), Room 2 (30)</td>
        </tr>
        <tr>
            <td><a href="http://www.st.com/en/evaluation-tools/b-l072z-lrwan1.html">ST B-L072Z-LRWAN1</a></td>
            <td>st-lrwan1</td>
            <td>25</td>
            <td>LoRa</td>
            <td></td>
        </tr>
        <tr>
            <td><a href="{{ site.baseurl}}/docs/boards/nordic-nrf52dk">nRF52DK</a></td>
            <td>nrf52dk</td>
            <td>10</td>
            <td>BLE</td>
            <td></td>
        </tr>
        <tr>
            <td><a href="{{ site.baseurl}}/docs/boards/nordic-nrf52840dk">nRF52840DK</a></td>
            <td>nrf52840dk</td>
            <td>5</td>
            <td>802.15.4 + BLE</td>
            <td>Room 2 (5)</td>
        </tr>
        <tr>
            <td><a href="{{ site.baseurl}}/docs/boards/nordic-nrf51dk">nRF51DK</a></td>
            <td>nrf51dk</td>
            <td>5</td>
            <td>BLE</td>
            <td></td>
        </tr>
        <tr>
            <td><a href="https://microbit.org/">micro:bit</a></td>
            <td>microbit</td>
            <td>1</td>
            <td>BLE</td>
            <td></td>
        </tr>
    </tbody>
</table>

### Room 2
The room 2 is 48 m2 (12 m x 4 m)  and contains the following boards:

<table class="table table-striped">
    <thead>
        <tr>
            <td><b>Board type</b></td>
            <td><b>Board id</b></td>
            <td><b>Count</b></td>
            <td><b>Radio(s)</b></td>
            <td><b>Other location</b></td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><a href="https://www.iot-lab.info/hardware/a8/">A8</a></td>
            <td>a8</td>
            <td>30</td>
            <td>802.15.4</td>
            <td>Basement (115), Room 1 (18)</td>
        </tr>
        <tr>
            <td><a href="https://www.iot-lab.info/hardware/m3/">M3</a></td>
            <td>m3</td>
            <td>12</td>
            <td>802.15.4</td>
            <td></td>
        </tr>
        <tr>
            <td><a href="{{ site.baseurl}}/docs/boards/microchip-samr21">SAMR21 Xplained Pro</a></td>
            <td>samr21</td>
            <td>15</td>
            <td>802.15.4</td>
            <td></td>
        </tr>
        <tr>
            <td><a href="https://www.arduino.cc/en/Main/ArduinoBoardZero">Arduino Zero</a></td>
            <td>arduino-zero</td>
            <td>3</td>
            <td>802.15.4 (XBee)</td>
            <td></td>
        </tr>
        <tr>
            <td><a href="{{ site.baseurl}}/docs/boards/nordic-nrf52840dk">nRF52840DK</a></td>
            <td>nrf52840dk</td>
            <td>5</td>
            <td>802.15.4 + BLE</td>
            <td>Room 1 (5)</td>
        </tr>
        <tr>
            <td><a href="{{ site.baseurl}}/docs/boards/nxp-frdm-kw41z">NXP FRDM-KW41Z</a></td>
            <td>frdm-kw41z</td>
            <td>5</td>
            <td>802.15.4 + BLE</td>
            <td></td>
        </tr>
        <tr>
            <td><a href="https://github.com/makerdiary/nrf52840-mdk">nRF52840-MDK</a></td>
            <td>nrf52840mdk</td>
            <td>1</td>
            <td>802.15.4 + BLE</td>
            <td></td>
        </tr>
        <tr>
            <td><a href="https://www.phytec.in/product/internet-of-things/phynode-sensor-1/">phyNode</a></td>
            <td>phynode</td>
            <td>1</td>
            <td>802.15.4</td>
            <td></td>
        </tr>
    </tbody>
</table>

## Pictures

<div class="row mb-3">
    <div class="col p-1">
        <a href="{{ '/assets/images/deployments/saclay/' | relative_url }}digiteo1.jpg" data-toggle="lightbox" data-gallery="gallery">
            <img class="img-thumbnail img-fluid" src="{{ '/assets/images/deployments/saclay/' | relative_url }}digiteo1.jpg">
        </a>
    </div>
    <div class="col p-1">
        <a href="{{ '/assets/images/deployments/saclay/' | relative_url }}digiteo2.jpg" data-toggle="lightbox" data-gallery="gallery">
            <img class="img-thumbnail img-fluid" src="{{ '/assets/images/deployments/saclay/' | relative_url }}digiteo2.jpg">
        </a>
    </div>
    <div class="w-100"></div>    
    <div class="col p-1">
        <a href="{{ '/assets/images/deployments/saclay/' | relative_url }}lora.jpg" data-toggle="lightbox" data-gallery="gallery">
            <img class="img-thumbnail img-fluid" src="{{ '/assets/images/deployments/saclay/' | relative_url }}lora.jpg">
        </a>
    </div>
    <div class="col p-1">
        <a href="{{ '/assets/images/deployments/saclay/' | relative_url }}parking.jpg" data-toggle="lightbox" data-gallery="gallery">
            <img class="img-thumbnail img-fluid" src="{{ '/assets/images/deployments/saclay/' | relative_url }}parking.jpg">
        </a>
    </div>
</div>

## GPS

TODO

Ground floor rooms 1 and 2 are equipped with a set of GPS repeaters that are relaying the GPS signal indoor.

## Live camera

You can follow your experiment live on the A8 node with identifier 145
[here](http://demo-fit.saclay.inria.fr).
