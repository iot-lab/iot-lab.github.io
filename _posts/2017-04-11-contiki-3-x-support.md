---
title: Contiki 3.x Support
---

We have updated [our Contiki repository](https://github.com/iot-lab/contiki "iot-lab/contiki") with the official one, providing support for Contiki 3.x.
{: .lead}

From now, you will be able to test your Contiki solutions on the IoT-LAB testbed, using the last features provided by the Contiki OS, like, for example, the last er-coap implementation or the RPL/TSCH network.

This release comes with dedicated IoT-LAB examples, available in the <tt>examples/iotlab</tt> directory, including new examples on er-coap and RPL/TSCH. We have updated our [Contiki tutorials]({{ site.baseurl }}{% link learn/index.html %}).

Our <tt>master</tt> branch will now regularly be updated with the official repository master branch. Just run a `git pull` if you want to synchronize your local repository with the IoT-LAB one. Afterward, you will be able to easily retrieve the last Contiki updates with this set of commands:

<pre>git remote add contiki https://github.com/contiki-os/contiki
git fetch contiki
git merge contiki/master
</pre>

For those who prefer to continue working with Contiki 2.7, we created an <tt>iotlab-2-7</tt> branch containing the previous <tt>master</tt> branch. Note that the support brought in this branch for the WSN430 node has not been tested in the current <tt>master</tt> branch. But we are open to feedback and contributions to bring support for this in Contiki 3.x as well. Don’t hesitate to open a pull request on [GitHub](https://github.com/iot-lab/contiki)


#### IEEE 802.15.4-2015 TSCH and IETF 6TiSCH

Time Slotted Channel Hopping (TSCH) is a MAC layer of the [IEEE 802.15.4e-2012 amendment](http://standards.ieee.org/getieee802/download/802.15.4e-2012.pdf), currently being integrated as part of the new IEEE 802.15.4-2015\. [6TiSCH](https://datatracker.ietf.org/wg/6tisch) is an IETF Working Group focused on IPv6 over TSCH.

source: [https://github.com/contiki-os/contiki/blob/master/core/net/mac/tsch/README.md](https://github.com/contiki-os/contiki/blob/master/core/net/mac/tsch/README.md)

See this [history](https://github.com/iot-lab/contiki/commits/master/platform/openlab/radio-rf2xx.c) for details on the work done for TSCH support.
