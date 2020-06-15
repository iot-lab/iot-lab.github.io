---
title: IoT-LAB IPv6 Subnets
group: getting-started
description: Overview of the IPv6 subnets for all the IoT-LAB sites.
---

## For boards based on a microcontroller

<table class="table table-striped">
    <thead>
        <tr>
            <td><b>Site</b></td>
            <td><b>Number of subnets</b></td>
            <td><b>from</b></td>
            <td><b>to</b></td>
        </tr>
    </thead>
    <tbody>
    <tr>
        <td>Grenoble</td>
        <td>128</td>
        <td>2001:660:5307:3100::/64</td>
        <td>2001:660:5307:317f::/64</td>
    </tr>
    <tr>
        <td>Lille</td>
        <td>128</td>
        <td>2001:660:4403:0480::/64</td>
        <td>2001:660:4403:04ff::/64</td>
    </tr>
    <tr>
        <td>Paris</td>
        <td>128</td>
        <td>2001:660:330f:a280::/64</td>
        <td>2001:660:330f:a2ff::/64</td>
    </tr>
    <tr>
        <td>Saclay</td>
        <td>64</td>
        <td>2001:660:3207:04c0::/64</td>
        <td>2001:660:3207:04ff::/64</td>
    </tr>
    <tr>
        <td>Strasbourg</td>
        <td>32</td>
        <td>2001:660:4701:f0a0::/64</td>
        <td>2001:660:4701:f0bf::/64</td>
    </tr>
    </tbody>
</table>

## For IoT-LAB A8-M3 embedded Linux nodes

<table class="table table-striped">
    <thead>
        <tr>
            <td><b>Grenoble</b></td>
            <td><b>Global IPv6 on eth0 interface</b></td>
            <td><b>/64 subnet on M3 interface</b></td>
        </tr>
    </thead>
    <tbody>
    <tr>
        <td>node-a8-1.grenoble.iot-lab.info</td>
        <td>2001:660:5307:3000::1</td>
        <td>2001:660:5307:3001::/64</td>
    </tr>
    <tr>
        <td>node-a8-2.grenoble.iot-lab.info</td>
        <td>2001:660:5307:3000::2</td>
        <td>2001:660:5307:3002::/64</td>
    </tr>
    <tr>
        <td>...</td>
        <td>...</td>
        <td>...</td>
    </tr>
    <tr>
        <td>node-a8-228.grenoble.iot-lab.info</td>
        <td>2001:660:5307:3000::e4</td>
        <td>2001:660:5307:30e4::/64</td>
    </tr>
    </tbody>
</table>

<table class="table table-striped">
    <thead>
        <tr>
            <td><b>Paris</b></td>
            <td><b>Global IPv6 on eth0 interface</b></td>
            <td><b>/64 subnet on M3 interface</b></td>
        </tr>
    </thead>
    <tbody>
    <tr>
        <td>node-a8-1.paris.iot-lab.info</td>
        <td>2001:0660:330f:a200::1</td>
        <td>2001:0660:330f:a201::/64</td>
    </tr>
    <tr>
        <td>node-a8-2.paris.iot-lab.info</td>
        <td>2001:0660:330f:a200::2</td>
        <td>2001:0660:330f:a202::/64</td>
    </tr>
    <tr>
        <td>...</td>
        <td>...</td>
        <td>...</td>
    </tr>
    <tr>
        <td>node-a8-62.paris.iot-lab.info	</td>
        <td>2001:0660:330f:a200::3e</td>
        <td>2001:0660:330f:a23e::/64</td>
    </tr>
    </tbody>
</table>

<table class="table table-striped">
    <thead>
        <tr>
            <td><b>Saclay</b></td>
            <td><b>Global IPv6 on eth0 interface</b></td>
            <td><b>/64 subnet on M3 interface</b></td>
        </tr>
    </thead>
    <tbody>
    <tr>
        <td>node-a8-1.saclay.iot-lab.info</td>
        <td>2001:660:3207:0400::1</td>
        <td>2001:660:3207:0401::/64</td>
    </tr>
    <tr>
        <td>node-a8-2.saclay.iot-lab.info</td>
        <td>2001:660:3207:0400::2</td>
        <td>2001:660:3207:0402::/64</td>
    </tr>
    <tr>
        <td>...</td>
        <td>...</td>
        <td>...</td>
    </tr>
    <tr>
        <td>node-a8-175.saclay.iot-lab.info</td>
        <td>2001:660:3207:0400::af</td>
        <td>2001:660:3207:04af::/64</td>
    </tr>
    </tbody>
</table>

<table class="table table-striped">
    <thead>
        <tr>
            <td><b>Strasbourg</b></td>
            <td><b>Global IPv6 on eth0 interface</b></td>
            <td><b>/64 subnet on M3 interface</b></td>
        </tr>
    </thead>
    <tbody>
    <tr>
        <td>node-a8-1.strasbourg.iot-lab.info</td>
        <td>2001:660:4701:f080::1</td>
        <td>2001:660:4701:f081::/64</td>
    </tr>
    <tr>
        <td>node-a8-2.strasbourg.iot-lab.info</td>
        <td>2001:660:4701:f080::2</td>
        <td>2001:660:4701:f082::/64</td>
    </tr>
    <tr>
        <td>...</td>
        <td>...</td>
        <td>...</td>
    </tr>
    <tr>
        <td>node-a8-14.strasbourg.iot-lab.info</td>
        <td>2001:660:4701:f080::e</td>
        <td>2001:660:4701:f08e::/64</td>
    </tr>
    </tbody>
</table>
