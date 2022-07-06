---
title: Strasbourg
group: deployment
description: "The Strasbourg site is located at the ICube laboratory from the Strasbourg University."
---

## Topology

The Strasbourg testbed offers two types of environment in order to test large scale IoT MAC layers and routing protocols:

* **Experiment Room**: a semi-controlled environment inside a dedicated room with limited radio interferences
* **Smart Building**: a realistic environment inside a large building close to real deployment

### Experiment Room

This environment is the original Strasbourg IoT-LAB deployment. It starts in 2008 with the SensLAB project with a dense grid of 256 wsn430 nodes. In 2014 with the IoT-LAB project, we add A8 and M3 nodes. Some of the nodes on top of mobile robots provide also reproductible mobility with predefined trajectories. In 2020, we remove the wsn430 nodes and introduce Zigduino nodes. The main topology characteristics are:

* **Semi-controled environment**: a dedicated room of 200m2
* **Limited radio interferences**: an isolated room inside the basement of the building
* **Limited physical obstacles**: all nodes are in the same open space
* **Dense grid**: all nodes are **1 meter apart** spaced with regular 3D grid topology
* Contains:
  * M3, A8 and Zigduino nodes interoperable with IEEE 802.15.4 radio technology

<div class="row mb-3">
    <div class="col-lg-6">
        <a href="{{ '/assets/images/deployments/strasbourg/' | relative_url }}strasbourg-grid-m3.png" data-toggle="lightbox" data-gallery="gallery">
            <img class="img-fluid" src="{{ '/assets/images/deployments/strasbourg/' | relative_url }}strasbourg-grid-m3.png">
        </a>
        <small class="text-muted">Strasbourg IoT-LAB Room</small>
    </div>
</div>

<div class="row mb-3">
    <div class="col p-1">
        <a href="{{ '/assets/images/deployments/strasbourg/' | relative_url }}strasbourg-iot-room1.jpeg" data-toggle="lightbox" data-gallery="gallery">
            <img class="img-thumbnail img-fluid" src="{{ '/assets/images/deployments/strasbourg/' | relative_url }}strasbourg-iot-room1.jpeg">
        </a>
    </div>
    <div class="col p-1">
        <a href="{{ '/assets/images/deployments/strasbourg/' | relative_url }}strasbourg-iot-room2.jpeg" data-toggle="lightbox" data-gallery="gallery">
            <img class="img-thumbnail img-fluid" src="{{ '/assets/images/deployments/strasbourg/' | relative_url }}strasbourg-iot-room2.jpeg">
        </a>
    </div>
    <div class="col p-1">
        <a href="{{ '/assets/images/deployments/strasbourg/' | relative_url }}strasbourg-iot-room3.jpeg" data-toggle="lightbox" data-gallery="gallery">
            <img class="img-thumbnail img-fluid" src="{{ '/assets/images/deployments/strasbourg/' | relative_url }}strasbourg-iot-room3.jpeg">
        </a>
    </div>
</div>

<div class="embed-responsive embed-responsive-16by9">
<iframe class="embed-responsive-item" width="560" height="315" src="https://www.youtube.com/embed/JC385RAqoiY" allowfullscreen></iframe>
</div>

### Smart Building

This environment is named **iBat** for **i**ntelligent **Bat**iment. Started in 2016, iBat is an extension of the original Strasbourg IoT-LAB deployment in order to add the following topology characteristics:

* **Realistic environment**: inside the offices and corridors of ICube laboratory
* **Real radio interferences**: human activity (Wi-Fi networks, Bluetooth)
* **Real physical obstacles**: offices and corridors walls
* **Large grid**: all nodes are **10 meters apart** spaced
* **Real deployment**: use cases *smart building* or *IIoT*
* **Real sensors data**: temperature, humidity, light, sound and presence
* Contains:
  * Zigduino nodes interoperable with IEEE 802.15.4 and LoRaWAN radio technology

<div class="row mb-3">
    <div class="col-lg-6">
        <a href="{{ '/assets/images/deployments/strasbourg/' | relative_url }}strasbourg-grid-zigduino.jpeg" data-toggle="lightbox" data-gallery="gallery">
            <img class="img-fluid" src="{{ '/assets/images/deployments/strasbourg/' | relative_url }}strasbourg-grid-zigduino.jpeg">
        </a>
        <small class="text-muted">Strasbourg iBat</small>
    </div>
</div>


<div class="row mb-3">    
    <div class="col p-1">
        <a href="{{ '/assets/images/deployments/strasbourg/' | relative_url }}strasbourg-zigduino-deployment01.jpeg" data-toggle="lightbox" data-gallery="gallery">
            <img class="img-thumbnail img-fluid" src="{{ '/assets/images/deployments/strasbourg/' | relative_url }}strasbourg-zigduino-deployment01.jpeg">
        </a>
    </div>
    <div class="col p-1">
        <a href="{{ '/assets/images/deployments/strasbourg/' | relative_url }}strasbourg-zigduino-deployment02.jpeg" data-toggle="lightbox" data-gallery="gallery">
            <img class="img-thumbnail img-fluid" src="{{ '/assets/images/deployments/strasbourg/' | relative_url }}strasbourg-zigduino-deployment02.jpeg">
        </a>
    </div>
    <div class="col p-1">
        <a href="{{ '/assets/images/deployments/strasbourg/' | relative_url }}strasbourg-zigduino-deployment03.jpeg" data-toggle="lightbox" data-gallery="gallery">
            <img class="img-thumbnail img-fluid" src="{{ '/assets/images/deployments/strasbourg/' | relative_url }}strasbourg-zigduino-deployment03.jpeg">
        </a>
    </div>
</div>

<div class="embed-responsive embed-responsive-16by9">
<iframe class="embed-responsive-item" width="560" height="315" src="https://www.youtube.com/embed/mQS4kv-tJ2A" allowfullscreen></iframe>
</div>
