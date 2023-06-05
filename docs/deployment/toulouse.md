---
title: Toulouse
group: deployment
iotlab-site: toulouse
description: The Toulouse site is part of the <a href='https://locura4iot.irit.fr'>LocURa4IoT testbed</a>. The nodes are located at IUT Blagnac (IRIT/UT2J). They are spread across offices and demonstration room on the first floor of building C. This site focuses on Ultra-Wide Band (UWB) technology and is catered towards indoor localisation, but can also host experiments on other available technologies such as BLE and other topics such as time synchronisation .
---



## Topology

Toulouse testbed is deployed at a building scale, over the first floor of building C of IUT Blagnac. 
* All the nodes are currently <a href="{{ 'docs/boards/' | relative_url }}decawave-dwm1001">Qorvo's DWM1001</a>.
* Most of the nodes are fixed at a height of 2.65m and at least 30cm away from the walls and ceilings on dedicated plastic mounts.
* Some nodes are located on the floor or at an intermediate height (1,65m) to enable 3D localisation experiments.
* The walls are either load-bearing bricks walls, wood pannel walls or drywalls.
* Node positions are estimated to be known within 2cm of precision \[<a href="https://ut3-toulouseinp.hal.science/hal-03466307">Bossche2022</a>\].
* The node positions are available as a JSON file <a href="{{ 'assets/misc/docs/deployments/toulouse/' | relative_url }}positions.json">here</a>.
* Note : the node ids are not contiguous because some ids are provisioned for future use.

<div class="row justify-content-center">
    <div class="col-9">
        <figure>
            <a href="{{ '/assets/images/deployments/toulouse/' | relative_url }}locura_iotlab_map.png" data-toggle="lightbox" data-gallery="gallery-A">
                <img class="img-fluid" src="{{ '/assets/images/deployments/toulouse/' | relative_url }}locura_iotlab_map.png">
            </a>
            <figcaption>Testbed map</figcaption>
        </figure>
    </div>
</div>

## Views of node setup

<div class="row mb-3">
    <div class="col p-1">
        <figure>
            <a href="{{ '/assets/images/deployments/toulouse/' | relative_url }}demo_room.jpg" data-toggle="lightbox" data-gallery="gallery">
                <img class="img-thumbnail img-fluid" src="{{ '/assets/images/deployments/toulouse/' | relative_url }}demo_room.jpg">
            </a>
            <figcaption>Demo room</figcaption>
        </figure>
    </div>
    <div class="col p-1">
        <figure>
            <a href="{{ '/assets/images/deployments/toulouse/' | relative_url }}line.jpg" data-toggle="lightbox" data-gallery="gallery">
                <img class="img-thumbnail img-fluid" src="{{ '/assets/images/deployments/toulouse/' | relative_url }}line.jpg">
            </a>
            <figcaption>high-density mount in demo room</figcaption>
        </figure>
    </div>
</div>

<div class="row mb-3">
    <div class="col p-1">
        <figure>
            <a href="{{ '/assets/images/deployments/toulouse/' | relative_url }}wall_mount.jpg" data-toggle="lightbox" data-gallery="gallery">
                <img class="img-thumbnail img-fluid" src="{{ '/assets/images/deployments/toulouse/' | relative_url }}wall_mount.jpg">
            </a>
            <figcaption>Wall mount</figcaption>
        </figure>
    </div>
    <div class="col p-1">
        <figure>
            <a href="{{ '/assets/images/deployments/toulouse/' | relative_url }}floor.jpg" data-toggle="lightbox" data-gallery="gallery">
                <img class="img-thumbnail img-fluid" src="{{ '/assets/images/deployments/toulouse/' | relative_url }}floor.jpg">
            </a>
            <figcaption>Floor node</figcaption>
        </figure>
    </div>
</div>

<div class="row mb-3">
    <div class="col p-1">
        <figure>
            <a href="{{ '/assets/images/deployments/toulouse/' | relative_url }}single_mount.jpg" data-toggle="lightbox" data-gallery="gallery">
                <img class="img-thumbnail img-fluid" src="{{ '/assets/images/deployments/toulouse/' | relative_url }}single_mount.jpg">
            </a>
            <figcaption>Close-up of node mount</figcaption>
        </figure>
    </div>
    <div class="col p-1">
        <figure>
            <a href="{{ '/assets/images/deployments/toulouse/' | relative_url }}cabinet.jpg" data-toggle="lightbox" data-gallery="gallery">
                <img class="img-thumbnail img-fluid" src="{{ '/assets/images/deployments/toulouse/' | relative_url }}cabinet.jpg">
            </a>
            <figcaption>Cabinet mount in an office</figcaption>
        </figure>
    </div>
</div>

----------

_Toulouse IoT-LAB site is co-funded by the CNRS and University Toulouse Jean Jaurès_

<div class="row justify-content-center">
    <div class="col-2">
        <img class="img-fluid" src="{{ '/assets/images/deployments/toulouse/' | relative_url }}LOGO_CNRS.png">
    </div>
    <div class="col-6">
        <img class="img-fluid" src="{{ '/assets/images/deployments/toulouse/' | relative_url }}LOGO_UT2J.png">
    </div>
</div>

