---
title: Grenoble
group: deployment
iotlab-site: grenoble
description: On the Grenoble site, the nodes are deployed at Inria Grenoble – Rhône-Alpes. They are spread across corridors of the the ground floor. This site is very popular for large network and multi-hop experimentations.
---

## Topology

Grenoble testbed is deployed at a building scale, over the ground floor of Inria building, through corridors in the raised floors and dropped ceilings. 

* The nodes in the raised floors are fixed horizontally under the tiles.
* The nodes in the dropped ceilings are fixed vertically to the wall at a height of 2.6 m and 3.2 m.

We have also added an extension with a room (i.e. K on the plan) to plug in the new boards and manage LoRa deployment with a [The Things Network](https://www.thethingsnetwork.org/) gateway.

<div class="row">
<div class="col-lg-6" markdown="1">
Here is the distribution of nodes:
- **J corridor**
  - floor: <tt>m3-[1-69]</tt>
  - ceiling: <tt>m3-[359-380]</tt>, <tt>a8-[1-58]</tt>
- **F1 corridor**:
  - floor: <tt>m3-[70-94]</tt>
  - ceiling: <tt>a8-[59-77]</tt>
- **F2 corridor**:
  - floor: <tt>m3-[95-178]</tt>
- **F3 corridor**:
  - floor: <tt>m3-[179-205]</tt>
  - ceiling: <tt>a8-[78-94]</tt>
- **F4 corridor**:
  - floor: <tt>m3-[206-289]</tt>
  - ceiling: <tt>a8-[95-148]</tt>
- **G corridor**:
  - floor: <tt>m3-[290-358]</tt>
  - ceiling: <tt>a8-[149-228]</tt>
- **K room**:
  - <tt>nucleo-wl55jc-[1-5]</tt>
  - <tt>samr34-[1-2]</tt>
  - <tt>rpi3-[1-5]</tt>
</div>
<div class="col-lg-6">
    <br>
    <br>
    <a href="{{ '/assets/images/deployments/grenoble/' | relative_url }}plan.png" data-toggle="lightbox" data-gallery="gallery">
        <img class="img-fluid" src="{{ '/assets/images/deployments/grenoble/' | relative_url }}plan.png">
    </a>
</div>
</div>

See the video and photos below to visit the deployment across the building.

<div class="embed-responsive embed-responsive-16by9">
  <iframe class="embed-responsive-item" width="560" height="315" src="https://www.youtube.com/embed/xxNPQyY-xzw" allowfullscreen></iframe>
</div>

<div class="row mb-3">
    <div class="col p-1">
        <a href="{{ '/assets/images/deployments/grenoble/' | relative_url }}false-floors.png" data-toggle="lightbox" data-gallery="gallery">
            <img class="img-thumbnail img-fluid" src="{{ '/assets/images/deployments/grenoble/' | relative_url }}false-floors.png">
        </a>
    </div>
    <div class="col p-1">
        <a href="{{ '/assets/images/deployments/grenoble/' | relative_url }}false-ceilings.png" data-toggle="lightbox" data-gallery="gallery">
            <img class="img-thumbnail img-fluid" src="{{ '/assets/images/deployments/grenoble/' | relative_url }}false-ceilings.png">
        </a>
    </div>
</div>

## GPS

Some IoT-LAB A8-M3 boards deployed in Grenoble are equipped with a GPS chip. It allows to synchronize precisely data collection from these nodes together. They are located near the GPS antenna repeater at the corner of corridor J and F.

Here is the list of these 32 nodes:

+ a8-1,
a8-3,
a8-4,
a8-8,
+ a8-10,
a8-11,
a8-13,
a8-15,
+ a8-16,
a8-19,
a8-20,
a8-59,
+ a8-61,
a8-63,
a8-65,
a8-68,
+ a8-70,
a8-129,
a8-130,
a8-131,
+ a8-132,
a8-134,
a8-135,
a8-136,
+ a8-137,
a8-138,
a8-139,
a8-142,
+ a8-143,
a8-144,
a8-147,
a8-148

And its abbreviated form: `1+3-4+8+10-11+13+15-16+19-20+59+61+63+65+68+70+129-132+134-139+142-144+147-148`
