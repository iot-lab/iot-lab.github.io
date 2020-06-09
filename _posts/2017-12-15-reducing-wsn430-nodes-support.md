---
title: Reducing WSN430 nodes support
---

![]({{ '/assets/images/posts/' | relative_url }}tuto_wsn430-300x300.png){: .img-fluid }
{: .text-center }

We will gradually reduce WSN430 nodes support after good and loyal services during ten years on the IoT-LAB testbed.
{: .lead}

Originally, we had four sites with different hardware nodes:

* WSN430 v1.3b (TI CC1101 radio chipset) on **Grenoble** and **Strasbourg** sites
* WSN430 v1.4 (TI CC2420 radio chipset) on **Euratech** and **Rennes** sites

Since Thursday 30 November:

* we stopped WSN430 v1.3b nodes on the Grenoble site
* we stopped WSN430 v1.4 nodes on the Rennes site and shut down this site

Since we have an issue on the consumption monitoring software, which appears not consistent, and we no longer have the skills on this software, we deactivated this monitoring feature at the same time (i.e. WSN430 Profile management). On remaining WSN430 (i.e. in Euratech and Strasbourg), you are still able to launch experiments, flash firmwares and start/stop/reset nodes.

Next summer:

* we will stop WSN430 v1.4 nodes on the Euratech site and shutdown this site

The Strasbourg site will continue to provide WSN430 v1.3b nodes until further notice.
