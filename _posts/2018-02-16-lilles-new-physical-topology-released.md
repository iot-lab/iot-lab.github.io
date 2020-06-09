---
title: Lille&#8217;s new physical topology released
---

![]({{ '/assets/images/posts/' | relative_url }}lille_deployment_zones.png){: .img-fluid }

We are proud to announce the availability of the Lille new deployment: sparser, at the building scale. The whole 256 M3 nodes are available again*.  
But that’s not all. We took advantage of this operation to add a new type of board in this deployment. We deployed 9 Zolertia Frirefly (3 per floor), bringing sub-1GHz communications alongside 2.4GHz.
{: .lead}

### **Why?**  
In its original deployment, released in 2014, the Lille nodes were deployed over a 225 m2 area, hosting 256 M3 nodes. The nodes were dispatched over a regular 2D-grid, plus a few number deployed vertically on wooden poles.

The main drawback of this deployment was the density of the network – each node was able to communicate directly with any other node. Thus, we considered beneficial to propose an actual multi-hop network where the nodes are not all in range of each other. That is why we decided to make our deployment sparser and re-deploy more than half of the nodes.

### **How?**  
The final scenario adopted is, in addition to the original dedicated room on the third floor, a distribution of nodes through offices, corridors, meeting or storage rooms across the three floors of our Inria Lille building, providing a connected network. Figures attached shows an overview of the new topology. Furthermore, offering such a topology, provides an actual deployment at a building scale.  
Details, maps and pictures will be updated soon on the [Lille’s deployment page]({{ site.baseurl }}{% link docs/deployment/lille.md %})

We hope it will answer your needs and experimentation scenarios.

<small>_*Be careful, coordinates of the nodes changed, and nodes ids too. Thus, experiments conduct with the same set of nodes ids, will not be ran with the same nodes and could bring different results than before._</small>
