---
id: 5743
title: Contiki 3.x Support
date: 2017-04-11T17:10:25+00:00
author: Julien Vandaele
layout: post
guid: https://www.iot-lab.info/?p=5743
permalink: /contiki-3-x-support/
categories:
  - Uncategorized
---
<div class="pf-content">
  <p>
    We have updated <a href="https://github.com/iot-lab/contiki" title="iot-lab/contiki" target="_blank">our Contiki repository</a> with the official one, providing support for Contiki 3.x.
  </p>
  
  <p>
    From now, you will be able to test your Contiki solutions on the IoT-LAB testbed, using the last features provided by the Contiki OS, like, for example, the last er-coap implementation or the RPL/TSCH network.
  </p>
  
  <p>
    This release comes with dedicated IoT-LAB examples, available in the <tt>examples/iotlab</tt> directory, including new examples on er-coap and RPL/TSCH. We have updated our <a href="https://www.iot-lab.info/tutorials/#Contiki" title="" target="_blank">Contiki tutorials</a> and also just published a new one on <a href="https://www.iot-lab.info/tutorials/contiki-coap-rpl-tsch/" target="_blank">Running CoAP on top of a RPL/TSCH network</a>.
  </p>
  
  <p>
    Our <tt>master</tt> branch will now regularly be updated with the official repository master branch. Just run a <code>git pull</code> if you want to synchronize your local repository with the IoT-LAB one. Afterward, you will be able to easily retrieve the last Contiki updates with this set of commands:
  </p>
  
  <pre>
git remote add contiki https://github.com/contiki-os/contiki
git fetch contiki
git merge contiki/master
</pre>
  
  <p>
    For those who prefer to continue working with Contiki 2.7, we created an <tt>iotlab-2-7</tt> branch containing the previous <tt>master</tt> branch. Note that the support brought in this branch for the WSN430 node has not been tested in the current <tt>master</tt> branch. But we are open to feedback and contributions to bring support for this in Contiki 3.x as well. Don&#8217;t hesitate to open a pull request on <a href="https://github.com/iot-lab/contiki" title="" target="_blank">GitHub</a>
  </p>
  
  <div class="well">
    <h4>
      IEEE 802.15.4-2015 TSCH and IETF 6TiSCH
    </h4>
    
    <p>
      Time Slotted Channel Hopping (TSCH) is a MAC layer of the <a href="http://standards.ieee.org/getieee802/download/802.15.4e-2012.pdf">IEEE 802.15.4e-2012 amendment</a>, currently being integrated as part of the new IEEE 802.15.4-2015. <a href="https://datatracker.ietf.org/wg/6tisch">6TiSCH</a> is an IETF Working Group focused on IPv6 over TSCH.<br /> <small>source: <a href="https://github.com/contiki-os/contiki/blob/master/core/net/mac/tsch/README.md" title="" target="_blank">https://github.com/contiki-os/contiki/blob/master/core/net/mac/tsch/README.md</a></small>
    </p>
    
    <p>
      See this <a href="https://github.com/iot-lab/contiki/commits/master/platform/openlab/radio-rf2xx.c" title="" target="_blank">history</a> for details on the work done for TSCH support. </div> </div>