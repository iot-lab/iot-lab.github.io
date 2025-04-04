---
title: Lille
group: deployment
description: "On the Lille site, the nodes are deployed in our two buidlings at Inria Lille – Nord Europe. The most part is spread across the <a href='#topology-in-the-a-building'>A building</a>, usefull for large network and multi-hop experimentations. An additionnal part is deployed in a structure called <a href='#le-cube'>Le Cube</a>, in the B building, with a variety of boards."
---

<div class="row">
<div class="col-lg-6" markdown="1">
## Resources
* In the [A building](#topology-in-the-a-building):
    * 256 IoT-LAB M3
    * 11 Zolertia Firefly
    * 14 Qorvo DWM1001
* A set of different boards in [Le Cube](#le-cube):
    * 5 BBC micro:bit
    * 5 IoT-LAB M3
    * 5 Microchip SAMR21
    * 5 ST B-L072Z-LRWAN1
    * 5 Zolertia Firefly
</div>
<div class="col-lg-6" markdown="1">
[![plan-lille]({{ '/assets/images/deployments/lille/' | relative_url }}plan-lille.png){: .img-fluid}](https://www.openstreetmap.org/#map=18/50.60503/3.14872)
</div>
</div>

## Topology in the A Building

Lille testbed is deployed at a building scale, over the three floors of our Inria building, through offices, corridors, meeting or storage rooms, in addition to a dedicated room. The deployment zones over the building are marked in blue in the figure below. _See the video below to visit the deployment across the building._

The dedicated room is a 225 m2 area, composed of a corridor separating a big room and 5 offices (respectively on left and right in topology figures). In this room, nodes are dispatched over the ceiling and wood posts, situated at the borders of the big room.

* Nodes on ceiling are dispatched in staggered rows over a 1.20 m x 1.20 m grid, at an overall high of 9.6 m.
* Nodes on posts are vertically hanged at an overall high of 7.60, 8.50 and 9.40 m.

Here is the distribution of nodes per floor:

* Ground floor: <tt>m3-[1-45], firefly-[1-3]</tt>
* First floor: <tt>m3-[46-111], firefly-[4-6]</tt>
* Second floor: <tt>m3-[112-129], firefly-[7-8]</tt>
* Dedicated room (2nd floor): <tt>m3-[130-256], firefly[9-11], dwm1001-[1-14]</tt>


<div class="mb-3 embed-responsive embed-responsive-16by9">
  <iframe class="embed-responsive-item" width="560" height="315" src="https://www.youtube.com/embed/kh6pTG5wgec" allowfullscreen></iframe>
</div>

<div class="row">
    <div class="col pb-3">
        <a href="{{ '/assets/images/deployments/lille/' | relative_url }}lille-deployment-zones-2.png" data-toggle="lightbox" data-gallery="gallery-A">
            <img class="img-fluid" src="{{ '/assets/images/deployments/lille/' | relative_url }}lille-deployment-zones-2.png">
        </a>
    </div>
    <div class="col pb-3">
        <a href="{{ '/assets/images/deployments/lille/' | relative_url }}fit-redeployment.png" data-toggle="lightbox" data-gallery="gallery-A">
            <img class="img-fluid" src="{{ '/assets/images/deployments/lille/' | relative_url }}fit-redeployment.png">
        </a>
    </div>
    <div class="w-100">
    </div>
    <div class="col p-1">
        <a href="{{ '/assets/images/deployments/lille/' | relative_url }}fit-lille-1.jpg" data-toggle="lightbox" data-gallery="gallery-A">
            <img class="img-thumbnail img-fluid" src="{{ '/assets/images/deployments/lille/' | relative_url }}fit-lille-1.jpg">
        </a>
    </div>
    <div class="col p-1">
        <a href="{{ '/assets/images/deployments/lille/' | relative_url }}fit-lille-2.jpg" data-toggle="lightbox" data-gallery="gallery-A">
            <img class="img-thumbnail img-fluid" src="{{ '/assets/images/deployments/lille/' | relative_url }}fit-lille-2.jpg">
        </a>
    </div>
    <div class="col p-1">
        <a href="{{ '/assets/images/deployments/lille/' | relative_url }}fit-lille-3.jpg" data-toggle="lightbox" data-gallery="gallery-A">
            <img class="img-thumbnail img-fluid" src="{{ '/assets/images/deployments/lille/' | relative_url }}fit-lille-3.jpg">
        </a>
    </div>
</div>
<small class="text-muted">© Inria / Photo C. Morel</small>

## Le Cube

There is an additional deployment in the B building, around 100 m from the other one, in a wooden structure called Le Cube. It's purpose, here, is not to experiment at a large scale, but rather to test network solutions, protocols or Operating Systems over different hardwares and radios. This deployment brings a practical way to experiment compatibility and interoperability scenarios.

Here is the list of nodes present there: <tt>firefly[12-16], m3-[260-264], microbit-[1-5], samr21-[1-5], st-lrwam1-[1-5]</tt>


<div class="row">
    <div class="col p-1">
        <a href="{{ '/assets/images/deployments/lille/' | relative_url }}fit-lille-cube-1.jpg" data-toggle="lightbox" data-gallery="gallery-cube">
            <img class="img-thumbnail img-fluid" src="{{ '/assets/images/deployments/lille/' | relative_url }}fit-lille-cube-1.jpg">
        </a>
    </div>
    <div class="col p-1">
        <a href="{{ '/assets/images/deployments/lille/' | relative_url }}fit-lille-cube-2.jpg" data-toggle="lightbox" data-gallery="gallery-cube">
            <img class="img-thumbnail img-fluid" src="{{ '/assets/images/deployments/lille/' | relative_url }}fit-lille-cube-2.jpg">
        </a>
    </div>
    <div class="col p-1">
        <a href="{{ '/assets/images/deployments/lille/' | relative_url }}fit-lille-cube-3.jpg" data-toggle="lightbox" data-gallery="gallery-cube">
            <img class="img-thumbnail img-fluid" src="{{ '/assets/images/deployments/lille/' | relative_url }}fit-lille-cube-3.jpg">
        </a>
    </div>
</div>
<small class="text-muted">© Inria / Photo J. Vandaele</small>

----------

_Le site IoT-LAB de Lille est cofinancé par l'Union Européenne avec le Fonds Européen de Développement Régional (FEDER) et par le Ministère de l'Education Nationale, de l'Enseignement Supérieur et de la Recherche._

<div class="row justify-content-center">
    <div class="col-2">
        <img class="img-fluid" src="{{ '/assets/images/deployments/lille/' | relative_url }}eu.jpg">
    </div>
    <div class="col-2">
        <img class="img-fluid" src="{{ '/assets/images/deployments/lille/' | relative_url }}feder.jpg">
    </div>
    <div class="col-2">
        <img class="img-fluid" src="{{ '/assets/images/deployments/lille/' | relative_url }}mesr.jpg">
    </div>
</div>
