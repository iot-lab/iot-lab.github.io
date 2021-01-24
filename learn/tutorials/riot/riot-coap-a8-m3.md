---
group: riot
title: CoAP server with public IPv6 network on A8-M3 nodes
---

<i class="fas fa-grin-beam-sweat"></i> **Difficulty**: Medium
<i class="fas fa-stopwatch"></i> **Duration**: 45 minutes

_**Prerequisites**: [Configure SSH Access]({{ site.baseurl }}{% link
docs/getting-started/ssh-access.md %}) , [RIOT basics]({{ site.baseurl }}{% link
docs/os/riot.md %})_


_**Description**: The goal of this tutorial is to discover the basics of CoAP with RIOT on IoT-LAB. You will reserve 2 A8 nodes on the Saclay site, build and flash the required firmwares on the A8-M3 nodes, create a simple IPv6 network in IoT-LAB. Finally, from the saclay host (or any computer with a global IPv6 address), you’ll interact with the node running the CoAP server using the coap client available on the SSH frontend (or any other CoAP client)._

1. Connect to Saclay SSH frontend:
   ```
   my_computer$ ssh <login>@saclay.iot-lab.info
   ```

2. Start an experiment called `riot_ipv6_a8` that contains 2 A8 nodes.
   ```
   login@saclay:~$ iotlab-auth -u <login> 
   login@saclay:~$ iotlab-experiment submit -n riot_a8 -d 60 -l 2,archi=a8:at86rf231+site=saclay
   ```

   Remember the experiment identifier returned by the last command. It’ll be
   used in the commands shown below, `<exp_id>`. The requested experiment
   duration is **60 minutes**.

3. Wait a moment until all nodes are up:
  ```
  login@saclay:~$ iotlab-ssh --verbose wait-for-boot
  ```

4. Wait a moment until the experiment is launched (state is Running) and get
   the nodes list. For the next of this tutorial we suppose that you obtained
   **a8-1.saclay.iot-lab.info** and **a8-2.saclay.iot-lab.info** nodes.
   ```
   login@saclay:~$ iotlab-experiment get -i <exp_id> -p
   login@saclay:~$ iotlab-experiment get -i <exp_id> -n
   ```

5. Get the code of the 2020.10 release of [RIOT](https://github.com/riot-os/riot)
   from GitHub:
   ```
   login@saclay:~$ mkdir -p ~/A8/riot
   login@saclay:~$ cd ~/A8/riot
   login@saclay:~/A8/riot$ git clone https://github.com/RIOT-OS/RIOT.git -b 2020.10-branch
   login@saclay:~/A8/riot$ cd RIOT
   ```
   Note that you can also use the RIOT development code (e.g the master branch)
   at your own risk : this tutorial may not fully work.<br/><br/>

   **Important note:** to minimize radio interferences with other experiments
   you can build the firmwares below to make them use a different 802.15.4
   channel (default is 26).<br>
   To do so, add **DEFAULT_CHANNEL=&lt;channel&gt;** option to the make commands.

6. Build the required firmware for the border router node. The node `node-a8-1`
   will act as the border router in this experiment. The border firmware is
   built using the RIOT
   [gnrc_border_router example](https://github.com/RIOT-OS/RIOT/tree/master/examples/gnrc_border_router)
   ```
   login@saclay:~/A8/riot/RIOT$ source /opt/riot.source
   login@saclay:~/A8/riot/RIOT$ make ETHOS_BAUDRATE=500000 DEFAULT_CHANNEL=<channel> BOARD=iotlab-a8-m3 -C examples/gnrc_border_router clean all
   login@saclay:~/A8/riot/RIOT$ cp examples/gnrc_border_router/bin/iotlab-a8-m3/gnrc_border_router.elf ~/A8/.
   ```

7. Build the required firmware for the node running the CoAP server. RIOT
   [nanocoap_server example]((https://github.com/RIOT-OS/RIOT/tree/master/examples/nanocoap_server))
   will be used for this purpose.
   ```
   login@saclay:~/A8/riot/RIOT$ make BOARD=iotlab-a8-m3 -C examples/nanocoap_server clean all
   login@saclay:~/A8/riot/RIOT$ cp examples/nanocoap_server/bin/iotlab-a8-m3/nanocoap_server.elf ~/A8/.
   ```

8. Connect to the A8 of the M3 border router: `node-a8-1`.
   ```
   login@saclay:~$ ssh root@node-a8-1
   ```
   Then flash the BR firmware on the M3 and build the required RIOT
   configuration tools: uhcpd (Micro Host Configuration Protocol) and ethos
   (Ethernet Over Serial).
   ```
   root@node-a8-1:~# iotlab_flash A8/gnrc_border_router.elf
   root@node-a8-1:~# cd ~/A8/riot/RIOT/dist/tools/uhcpd 
   root@node-a8-1:~/A8/riot/RIOT/dist/tools/uhcpd# make clean all
   root@node-a8-1:~/A8/riot/RIOT/dist/tools/uhcpd# cd ../ethos
   root@node-a8-1:~/A8/riot/RIOT/dist/tools/ethos# make clean all
   ```
   On the border router, the network can finally be configured automatically
   using the following commands:
   ```
   root@node-a8-1:~/A8/riot/RIOT/dist/tools/ethos# ./start_network.sh /dev/ttyA8_M3 tap0 2001:660:3207:401::/64 500000
   net.ipv6.conf.tap0.forwarding = 1
   net.ipv6.conf.tap0.accept_ra = 0
   ----> ethos: sending hello.
   ----> ethos: activating serial pass through.
   ----> ethos: hello reply received
   ```
   Note that we propagate another subnetwork for the border router (M3 node) in
   our LLN, `2001:660:3207:401::/64`. You can find informations about IPv6
   subnetting for A8-M3 nodes here. You can also get this prefix directly on the
   A8 node:
   ```
   root@node-a8-1:~# printenv
   INET6_PREFIX_LEN=64
   INET6_PREFIX=2001:0660:3207:401
   INET6_ADDR=2001:0660:3207:0400::1/64
   ```

9. Now, **in another terminal**, log on the remaining A8 node, `node-a8-2`, and
   flash the nanocoap_server firmware on the M3:
   ```
   my_computer$ ssh <login>@saclay.iot-lab.info
   login@saclay:~$ ssh root@node-a8-2
   root@node-a8-2:~# flash_a8_m3 A8/nanocoap_server.elf
   root@node-a8-2:~# exit
   ```

10. On the border router shell with the command `nib neigh` you can find the
   IPv6 of the node running nanocoap server. (type enter in the terminal of
   `node-a8-1` where you launched the `start_network.sh` script : you have
   access to the shell or RIOT) 
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
   2001:660:3207:401:3432:4833:46df:a902 dev #6 lladdr 15:11:6B:10:46:DF:A9:02  STALE REGISTERED
   ```

11. On the SSH frontend, you can now use the preinstalled CoAP client to query
   the CoAP server node. By default, the nanocoap server example of RIOT
   exposes only the board type to a CoAP `GET` request on `/riot/board`.<br/>
   Let’s try it on the CoAP server node:
   ```
   login@saclay:~$ aiocoap-client coap://[2001:660:3207:401:3432:4833:46df:a902]/riot/board
   iotlab-a8-m3
   ```

If everything works as described, you can use CoAP with RIOT on IoT-LAB. **Congratulations !**
