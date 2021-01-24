---
group: riot
title: CoAP server with public IPv6 network on M3 nodes
---

<i class="fas fa-grin-beam-sweat"></i> **Difficulty**: Medium
<i class="fas fa-stopwatch"></i> **Duration**: 45 minutes

_**Prerequisites**: [Configure SSH Access]({{ site.baseurl }}{% link
docs/getting-started/ssh-access.md %}) , [RIOT basics]({{ site.baseurl }}{% link
docs/os/riot.md %})_

_**Description**: The goal of this tutorial is to discover the basics of CoAP with RIOT on IoT-LAB. You will reserve 2 M3 nodes on the Saclay site, build and flash the required firmwares on the M3 nodes, create a simple IPv6 network in IoT-LAB. Finally, from the Saclay host (or any computer with a global IPv6 address), you’ll interact with the node running the CoAP server using the coap client available on the SSH frontend (or any other CoAP client)._

1. Connect to the Saclay site host: 
   ```
   my_computer$ ssh <login>@saclay.iot-lab.info
   ```

2. Start an experiment with two M3 nodes called `riot_coap_m3`
   ```
   login@saclay:~$ iotlab-auth -u <login> 
   login@saclay:~$ iotlab-experiment submit -n riot_coap_m3 -d 60 -l 2,archi=m3:at86rf231+site=saclay
   ```
   Remember the experiment identifier returned by the last command. It’ll be
   used in the commands shown below, `<exp_id>`. The requested experiment
   duration is **60 minutes**.

3. Wait a moment until the experiment is launched (state is Running) and get
   the nodes list. For the next of this tutorial we suppose that you obtained
   **m3-1.saclay.iot-lab.info** and **m3-2.saclay.iot-lab.info** nodes
   ```
    login@saclay:~$ iotlab-experiment get -i <exp_id> -p
    login@saclay:~$ iotlab-experiment get -i <exp_id> -n
   ```

4. Get the code of the 2020.10 release of [RIOT](https://github.com/riot-os/riot)
   from GitHub: 
   ```
   login@saclay:~$ mkdir -p ~/riot
   login@saclay:~$ cd ~/riot
   login@saclay:~/riot$ git clone https://github.com/RIOT-OS/RIOT.git -b 2020.10-branch
   login@saclay:~/riot$ cd RIOT
   ```

   **Note:** you can also use the RIOT development code (e.g the master branch)
   but this will be at your own risk: this tutorial may not fully work.

5. Build the required firmware for the border router node. The node `m3-1` will
   act as the border router in this experiment. The border router firmware is
   built using the RIOT [gnrc_border_router example]().

   - **Important note 1:** we build this firmware with a baudrate of **500000**.
     This is mandatory for `ethos_uhcpd.py` script to work effectively since
     the UART baudrate of the M3 is 500000.
   - **Important note 2:** to minimize radio interferences with other
     experiments you can build the firmwares to make them use a different
     802.15.4 channel (default is 26).<br/>
     To do so, add **DEFAULT_CHANNEL=&lt;channel&gt;** option to the make commands.

   ```
   login@saclay:~/riot/RIOT/$ source /opt/riot.source
   login@saclay:~/riot/RIOT/$ make ETHOS_BAUDRATE=500000 DEFAULT_CHANNEL=<channel> BOARD=iotlab-m3 -C examples/gnrc_border_router clean all
   ```

6. Use the CLI-Tools to flash the gnrc_border_router firmware that you have just
   built on the first M3 node. Here we use `m3-1` but it may change in your case: 
   ```
   login@saclay:~/riot/RIOT/$ iotlab-node --flash examples/gnrc_border_router/bin/iotlab-m3/gnrc_border_router.elf -l saclay,m3,1
   ```

7. Choose an available IPv6 prefix for the site you are experimenting on. For
   example in Saclay site, we choose **2001:660:3207:04c1::/64**

8. Now you can configure the network of the border router on `m3-1` and propagate
   an IPv6 prefix with `ethos_uhcpd.py`.
   ```
   login@saclay:~$ sudo ethos_uhcpd.py m3-1 tap0 2001:660:3207:04c1::1/64
   ```
   **Important note1:** Check that tap0 network interface is not already used
   and in this case choose another number
   ```
   login@saclay:~$ ip addr show | grep tap
   1406: tap0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 500
   ```
   **Important note2:** If you have **an error "overlaps with routes"**, it’s
   because another experiment is using the same ipv6 prefix (e.g.
   **2001:660:3207:04c1::/64**).
   <br/>
   You can view currently used IPv6 prefixes on the frontend SSH with this command
   ```
   login@saclay:~$ ip -6 route
   2001:660:3207:04fff::/64 dev eth0  proto kernel  metric 256  mtu 1500 advmss 1440 hoplimit 4294967295
   2001:660:3207:04c0::/64 dev tun0  proto kernel  metric 256  mtu 1500 advmss 1440 hoplimit 4294967295
   fe80::/64 dev eth1  proto kernel  metric 256  mtu 1500 advmss 1440 hoplimit 4294967295
   fe80::/64 dev eth0  proto kernel  metric 256  mtu 1500 advmss 1440 hoplimit 4294967295
   fe80::/64 dev tun0  proto kernel  metric 256  mtu 1500 advmss 1440 hoplimit 4294967295
   default via 2001:660:3207:04ff:ff:: dev eth0  metric 1  mtu 1500 advmss 1440 hoplimit 4294967295
   ```
   The network is finally configured:
   ```
   net.ipv6.conf.tap0.forwarding = 1
   net.ipv6.conf.tap0.accept_ra = 0
   ----> ethos: sending hello.
   ----> ethos: activating serial pass through.
   ----> ethos: hello reply received
   ```
   Note that we propagate another subnetwork for the border router (M3 node) in
   our LLN, `2001:660:3207:04c1::/64`.

9. Now, **in another terminal**, SSH to the SSH frontend and build the CoAP
   server firmware used for the other node. RIOT [nanocoap_server](https://github.com/RIOT-OS/RIOT/tree/master/examples/nanocoap_server)
   example will be used for this purpose.
   ```
   login@saclay:~$ cd riot/RIOT
   login@saclay:~/riot/RIOT/$ source /opt/riot.source
   login@saclay:~/riot/RIOT/$ make DEFAULT_CHANNEL=<channel> BOARD=iotlab-m3 -C examples/nanocoap_server clean all
   ```
   Use the CLI-Tools to flash the `nanoocoap_server` firmware that you have
   just built on the second M3 node. Here we use `m3-2` but it may change in
   your case:
   ```
   login@saclay:~/riot/RIOT/$ iotlab-node --flash examples/nanocoap_server/bin/iotlab-m3/nanocoap_server.elf -l saclay,m3,2
   ```

10. On the border router shell (eg. where you are running the `ethos_uhcpd.py`
   command) with the command `nib neigh` you can find the IPv6 of the node
   running nanocoap server. (type enter in the terminal of `m3-1` where you
   launched the `ethos_uhcpd.py` script : you have access to the shell or RIOT)
   ```
   >
   > help
   help
   Command              Description
   ---------------------------------------
   reboot               Reboot the node
   ps                   Prints information about running threads.
   ping6                Ping via ICMPv6
   random_init          initializes the PRNG
   random_get           returns 32 bit of pseudo randomness
   nib                  Configure neighbor information base
   ifconfig             Configure network interfaces
   fibroute             Manipulate the FIB (info: 'fibroute [add|del]')
   6ctx                 6LoWPAN context configuration toolol
   > nib neigh
   nib neigh
   [...]
   2001:660:3207:4c1:1711:6b10:65fd:bd36 dev #6 lladdr 15:11:6b:10:65:fd:bd:36  STALE REGISTERED
   ```

11. On the SSH frontend, you can now use the preinstalled CoAP client to query
   the CoAP server node. By default, the nanocoap server example of RIOT
   exposes only the board type to a CoAP `GET` request on `/riot/board`, let’s
   try it on the CoAP server node:
   ```
   login@saclay:~$ aiocoap-client coap://[2001:660:3207:4c1:1711:6b10:65fd:bd36]/riot/board
   iotlab-m3
   ```

If everything works as described, you can use CoAP with RIOT on IoT-LAB. **Congratulations !**
