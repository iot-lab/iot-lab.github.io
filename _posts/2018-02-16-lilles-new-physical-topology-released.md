---
id: 6306
title: 'Lille&#8217;s new physical topology released'
date: 2018-02-16T11:58:57+00:00
author: Julien Vandaele
layout: post
guid: https://www.iot-lab.info/?p=6306
permalink: /lilles-new-physical-topology-released/
categories:
  - Uncategorized
---
<div class="pf-content">
  <p>
    We are proud to announce the availability of the Lille new deployment: sparser, at the building scale. The whole 256 M3 nodes are available again*.<br /> But that’s not all. We took advantage of this operation to add a new type of board in this deployment. We deployed 9 Zolertia Frirefly (3 per floor), bringing sub-1GHz communications alongside 2.4GHz.
  </p>
  
  <p>
    <strong>Why?</strong><br /> In its original deployment, released in 2014, the Lille nodes were deployed over a 225 m2 area, hosting 256 M3 nodes. The nodes were dispatched over a regular 2D-grid, plus a few number deployed vertically on wooden poles.
  </p>
  
  <p>
    The main drawback of this deployment was the density of the network – each node was able to communicate directly with any other node. Thus, we considered beneficial to propose an actual multi-hop network where the nodes are not all in range of each other. That is why we decided to make our deployment sparser and re-deploy more than half of the nodes.
  </p>
  
  <p>
    <strong>How?</strong><br /> The final scenario adopted is, in addition to the original dedicated room on the third floor, a distribution of nodes through offices, corridors, meeting or storage rooms across the three floors of our Inria Lille building, providing a connected network. Figures attached shows an overview of the new topology. Furthermore, offering such a topology, provides an actual deployment at a building scale.<br /> Details, maps and pictures will be updated soon on the <a href="/deployment/lille">Lille&#8217;s deployment page</a>.
  </p>
  
  <p>
    We hope it will answer your needs and experimentation scenarios.
  </p>
  
  <p>
    <small><em>*Be careful, coordinates of the nodes changed, and nodes ids too. Thus, experiments conduct with the same set of nodes ids, will not be ran with the same nodes and could bring different results than before.</em></small>
  </p>
  
  <p>
    <a href="https://www.iot-lab.info/wp-content/uploads/2018/02/lille_deployment_zones.png" rel="lightbox[gallery-XPzN]"><img src="https://www.iot-lab.info/wp-content/uploads/2018/02/lille_deployment_zones-724x1024.png" alt="lille_deployment_zones" width="724" height="1024" class="aligncenter size-large wp-image-6308" /></a>
  </p>
</div>