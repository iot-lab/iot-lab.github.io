---
group: contiki
title: Public IPv6 (6LoWPAN/RPL) network with M3 nodes
---

<i class="fas fa-grin-beam-sweat"></i> **Difficulty**: High  
<i class="fas fa-stopwatch"></i> **Duration**: 45 minutes

_**Prerequisites**: [Configure SSH Access]({{ site.baseurl }}{% link
docs/getting-started/ssh-access.md %}) , [Get and compile firmware for M3 and
A8-M3 nodes]({{ site.baseurl }}{% link
learn/tutorials/contiki/contiki-compilation.md %})_

_**Description**: The aim of this tutorial is to discover the basics of Contiki
uIP stack & tools for IoT-LAB IPv6. You will reserve some nodes on the Grenoble
site, set them up with the two provided firmwares using CLI tools, and create a
simple IPv6 network in IoT-LAB. You will access nodes over HTTP over IPv6 from
the SSH frontend, using a Contiki tunslip6 bridge._


1. Log into the Web portal with your account credentials.

2. Submit a new experiment:
    * Set an experiment name (no spaces nor funny chars in
    the experiment name)
    * Duration: **60 minutes** and starting "**As soon as
    possible**"
    * Choose ten nodes with Architecture m3 (at86rf231) / Site =
    grenoble / Number = 10 and click *Add to experiment*

3. Wait experiment state *Running* in the Schedule dashboard section. After click
   on experiment details and visualize which nodes you are booked and verify that
   you have *Success* in the deployment result.

4. Download firmware binaries on SSH frontend:

   <pre class="highlight">
   <strong>ssh &lt;login&gt;@&lt;site&gt;.iot-lab.info</strong>
   </pre>

   * **Border Router**: bridge between the server and the IoT-LAB IPv6 network

   <pre class="highlight"> &lt;login&gt;@&lt;site&gt;~$ wget --no-check-certificate
   https://raw.githubusercontent.com/wiki/iot-lab/iot-lab/firmwares/contiki/border-router.iotlab-m3
   -O border-router.iotlab-m3 </pre>

   * **HTTP server**: simple IPv6 node

   <pre class="highlight">
   &lt;login&gt;@&lt;site&gt;~$  wget --no-check-certificate https://raw.githubusercontent.com/wiki/iot-lab/iot-lab/firmwares/contiki/http-server.iotlab-m3 -O http-server.iotlab-m3
   </pre>

   View [Border Router](https://github.com/iot-lab/contiki/tree/master/examples/ipv6/rpl-border-router) and [HTTP Server](https://github.com/iot-lab/contiki/tree/master/examples/ipv6/http-server) source code on GitHub.

5. Choose an available [IPv6 subnets]({{ '/docs/getting-started/ipv6-subnets/' |
   relative_url }}) for the site you are experimenting on. For example in Grenoble
   testbed:
   * we choose *2001:660:5307:3100::/64*

6. Choose one node in your nodes list to implement the Border Router (BR) node:
   * we chose node m3-1.

7. Start tunslip6 on the SSH frontend

   <pre class="highlight">
   &lt;login&gt;@&lt;site&gt;~$ sudo tunslip6.py -v2 -L -a m3-1 -p 20000 2001:660:5307:3100::1/64
   slip connected to ``172.16.10.1:20000''

   15:38:19 opened tun device ``/dev/tun0''
   0000.000 ifconfig tun0 inet `hostname` up
   0000.004 ifconfig tun0 add 2001:660:5307:3100::1/64
   0000.005 ifconfig tun0 add fe80::660:5307:3100:1/64
   0000.007 ifconfig tun0

   tun0      Link encap:UNSPEC  HWaddr 00-00-00-00-00-00-00-00-00-00-00-00-00-00-00-00
             inet adr:192.168.1.4  P-t-P:192.168.1.4  Masque:255.255.255.255
             adr inet6: 2001:660:5307:3100::1/64 Scope:Global
             adr inet6: fe80::660:5307:3100:1/64 Scope:Lien
             UP POINTOPOINT RUNNING NOARP MULTICAST  MTU:1500  Metric:1
             RX packets:0 errors:0 dropped:0 overruns:0 frame:0
             TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
             collisions:0 lg file transmission:500
             RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)
   </pre>
   * **Note 1:** **leave the terminal open** (you don’t want to kill tunslip6, it bridges the BR to the front-end network)
   * **Note 2:** If you have an error “overlaps with routes”, it’s because another experiment is using the same ipv6 prefix (e.g. : 2001:660:5307:3100::/64).You can view currently used IPv6 prefixes on the frontend SSH with this command:
   <pre class="highlight">
   &lt;login&gt;@&lt;site&gt;~$ ip -6 route
   2001:660:5307:30fff::/64 dev eth0  proto kernel  metric 256  mtu 1500 advmss 1440 hoplimit 4294967295
   2001:660:5307:3100::/64 dev tun0  proto kernel  metric 256  mtu 1500 advmss 1440 hoplimit 4294967295
   fe80::/64 dev eth1  proto kernel  metric 256  mtu 1500 advmss 1440 hoplimit 4294967295
   fe80::/64 dev eth0  proto kernel  metric 256  mtu 1500 advmss 1440 hoplimit 4294967295
   fe80::/64 dev tun0  proto kernel  metric 256  mtu 1500 advmss 1440 hoplimit 4294967295
   default via 2001:660:5307:30ff:ff:: dev eth0  metric 1  mtu 1500 advmss 1440 hoplimit 4294967295
   </pre>
   * **Note 3:** if you did not already authenticate using _iotlab-auth_, do it now:
   <pre class="highlight">
   &lt;login&gt;@&lt;site&gt;~$ iotlab-auth -u login
   </pre>

8. Deploy the Border Router (BR) node on selected node using the CLI tool iotlab-node.
   <pre class="highlight">
   &lt;login&gt;@&lt;site&gt;~$ iotlab-node --update ~/border-router.iotlab-m3 -l grenoble,m3,1
   {
        "0": [
            "m3-1.grenoble.iot-lab.info"
        ]
   }
   </pre>

9. Get the Border Router IPv6 address from tunslip output:
   <pre class="highlight">
   ...
   Platform starting in 1...
   GO!
   [in clock_init() DEBUG] Starting systick timer at 100Hz

   0473.257 *** Address:2001:660:5307:3100::1 => 2001:0660:5307:3100
   0473.257  Starting 'Border router process' 'Web server'Got configuration message of type P
   0473.257 Setting prefix 2001:660:5307:3100::
   0473.257 Server IPv6 addresses:
   0473.257  <strong>2001:660:5307:3100::2354</strong>
   0473.257  fe80::2354
   </pre>

10. Ping6 BR node using global address:

    <pre class="highlight">
    &lt;login&gt;@&lt;site&gt;~$ ping6 2001:660:5307:3100::2354
    </pre>

11. View BR’s web-interface:


    <pre class="highlight">
    &lt;login&gt;@&lt;site&gt;~$ lynx -dump http://[2001:660:5307:3100::2354]
    </pre>
    **Note:** here, you could also use your web browser (Firefox, Chrome) with your own IPv6 connection
    You should see a web page with no neighbors and no routes.

    <pre class="highlight">
       Neighbors

       Routes
    </pre>

12. Deploy one HTTP server node picking another node (here node 2)

    <pre class="highlight">
    &lt;login&gt;@&lt;site&gt;~$ iotlab-node --update ~/http-server.iotlab-m3 -l grenoble,m3,2
    {
        "0": [
            "m3-2.grenoble.iot-lab.info"
        ]
    }
    </pre>

13. Check the BR’s web interface to see the newcomer.

14. Grab the HTTP server node’s IPv6 address from the BR’s web interface

    <pre class="highlight">
      Neighbors
    fe80::9982
      Routes
    2001:660:5307:3100::9982/128 (via fe80::9982) 16711353s
    </pre>

    Understand [M3 nodes uid /
    ipv6](https://github.com/iot-lab/iot-lab/wiki/Get-M3-and-A8-M3-nodes-uid---ipv6-address-match)
    address match.

15. Ping the HTTP server’s global address from SSH frontend

    <pre class="highlight">
    &lt;login&gt;@&lt;site&gt;~$ ping6 2001:660:5307:3100::9982
    </pre>

16. Deploy one more HTTP server node (for example m3-3)

17. Check again the BR’s web-interface and see the newcomer

    <pre class="highlight">
       Neighbors
    fe80::9982
    fe80::b868

       Routes
    2001:660:5307:3100::9982/128 (via fe80::9982) 16711418s
    2001:660:5307:3100::b868/128 (via fe80::9982) 16711403s
    </pre>

18. Download the page of the first HTTP server:

    <pre class="highlight">
    &lt;login&gt;@&lt;site&gt;~$ lynx -dump http://[2001:660:5307:3100::9982]
        Neighbors
    fe80::2354 PREFERRED
    fe80::b868

       Default Route
    fe80::2354

       Routes
    </pre>

19. Deploy HTTP servers on all remaining nodes (with –exclude iotlab-node option)

    <pre class="highlight">
    &lt;login&gt;@&lt;site&gt;~$ iotlab-node --update ~/http-server.iotlab-m3 --exclude grenoble,m3,1+2+3
    {
        "0": [
           "m3-4.grenoble.iot-lab.info",
           "m3-5.grenoble.iot-lab.info",
           "m3-7.grenoble.iot-lab.info",
           "m3-9.grenoble.iot-lab.info",
           "m3-287.grenoble.iot-lab.info",
           "m3-288.grenoble.iot-lab.info",
           "m3-289.grenoble.iot-lab.info"
        ]
    }
    </pre>

20. Check again the BR’s web-interface (reload) and see the newcomers

    <pre class="highlight">
       Neighbors
    fe80::9982
    fe80::9176
    fe80::a176
    fe80::1162
    fe80::b982
    fe80::9883
    fe80::c370
    fe80::b868

       Routes
    2001:660:5307:3100::9982/128 (via fe80::9982) 16711405s
    2001:660:5307:3100::b868/128 (via fe80::9982) 16711404s
    2001:660:5307:3100::2162/128 (via fe80::9982) 16711354s
    2001:660:5307:3100::9176/128 (via fe80::9176) 16711404s
    2001:660:5307:3100::a176/128 (via fe80::a176) 16711403s
    2001:660:5307:3100::1162/128 (via fe80::1162) 16711406s
    2001:660:5307:3100::b982/128 (via fe80::b982) 16711406s
    2001:660:5307:3100::9883/128 (via fe80::9883) 16711355s
    2001:660:5307:3100::c370/128 (via fe80::c370) 16711403s
    </pre>


    Study how RPL shapes the routing table. The RPL tree can be represented as
    shown below:


    <pre class="highlight">
    &lt;login&gt;@&lt;site&gt;~$ wget --no-check-certificate https://github.com/iot-lab/contiki/raw/master/examples/ipv6/http-server/get_rpl_tree.sh -O get_rpl_tree.sh
    &lt;login&gt;@&lt;site&gt;~$ bash get_rpl_tree.sh 2001:660:5307:3100::2354
     2001:660:5307:3100::2354
         2001:660:5307:3100::1162
         2001:660:5307:3100::9176
         2001:660:5307:3100::9883
         2001:660:5307:3100::9982
             2001:660:5307:3100::2162
         2001:660:5307:3100::a176
         2001:660:5307:3100::b982
         2001:660:5307:3100::c370
    </pre>

21. Test public access with [IPv6 Proxy](http://www.ipv6proxy.net) and use your border router url:

    <pre class="highlight">
    http://[2001:660:5307:3100::2354]
    </pre>
