---
group: riot
title: MQTT-SN with public IPv6 network and A8-M3 nodes
---

<i class="fas fa-grin-beam-sweat"></i> **Difficulty**: High
<i class="fas fa-stopwatch"></i> **Duration**: 45 minutes

_**Prerequisites**: [Configure SSH Access]({{ site.baseurl }}{% link
docs/getting-started/ssh-access.md %}) , [RIOT basics]({{ site.baseurl }}{% link
docs/os/riot.md %})_

_**Description**: The goal of this tutorial is to discover the MQTT procotol and its contrained variant called MQTT-SN with RIOT on IoT-LAB. You will reserve 3 A8 nodes on the Saclay site, build and flash the required firmwares on the A8-M3 nodes, create a simple IPv6 network in IoT-LAB. Finally, from the saclay SSH frontend host, you’ll publish MQTT messages to the test/riot topic. The messages will be displayed by the MQTT-SN client running on the RIOT node. The first node will be used as a border router for propagating an IPv6 prefix through its wireless interface, the second node will be used a as MQTT broker (using the mosquitto.rsmb application) and the third node will run a RIOT application containing a shell and a MQTT-SN client to connect to the brober._

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

7. Build the required firmware for the other node. RIOT
   [gnrc_networking example](https://github.com/RIOT-OS/RIOT/tree/master/examples/gnrc_networking)
   will be used for this purpose. 
   ```
   login@saclay:~/A8/riot/RIOT$ make DEFAULT_CHANNEL=<channel> BOARD=iotlab-a8-m3 -C examples/gnrc_networking clean all
   login@saclay:~/A8/riot/RIOT$ cp examples/gnrc_networking/bin/iotlab-a8-m3/gnrc_networking.elf ~/A8/
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

9. Now, **in another terminal**, log on the remaining A8 node, `node-a8-2`. We
   are going to configure and start the MQTT-SN broker as follows:
   ```
   my_computer$ ssh <login>@saclay.iot-lab.info
   login@saclay:~$ ssh root@node-a8-2
   ```
   Edit a file `config.conf` (vim config.conf) with the following content:
   ```
   # add some debug output
   trace_output protocol
   
   # listen for MQTT-SN traffic on UDP port 1885
   listener 1885 INADDR_ANY mqtts
     ipv6 true
   
   # listen to MQTT connections on tcp port 1886
   listener 1886 INADDR_ANY
     ipv6 true
   ```
   Important, note the global IPv6 address of this node, since we’ll use it to
   connect to the MQTT broker from the node:
   ```
   root@node-a8-2:~# ip -6 -o addr show eth0
   2: eth0    inet6 2001:660:3207:400::66/64 scope global        valid_lft forever preferred_lft forever
   2: eth0    inet6 fe80::fadc:7aff:fe01:98fc/64 scope link        valid_lft forever preferred_lft forever
   ```
   And finally start the broker:
   ```
   root@node-a8-2:~# broker_mqtts config.conf
   20170715 001526.077 CWNAN9999I Really Small Message Broker
   20170715 001526.084 CWNAN9998I Part of Project Mosquitto in Eclipse
   (http://projects.eclipse.org/projects/technology.mosquitto)
   20170715 001526.088 CWNAN0049I Configuration file name is config.conf
   20170715 001526.099 CWNAN0053I Version 1.3.0.2, Jul 11 2017 14:55:20
   20170715 001526.102 CWNAN0054I Features included: bridge MQTTS 
   20170715 001526.104 CWNAN9993I Authors: Ian Craggs (icraggs@uk.ibm.com), Nicholas O'Leary
   20170715 001526.111 CWNAN0300I MQTT-S protocol starting, listening on port 1885
   20170715 001526.115 CWNAN0014I MQTT protocol starting, listening on port 1886
   ```
   You now have a running MQTT/MQTT-SN broker running on `node-a8-2`.

   This broker is reachable :
   - from the SSH frontend using MQTT on port **1886**
   - from any M3 nodes behind the border router using MQTT-SN on port **1885** (in
     our case, `node-a8-3`, see below)

10. Finally, **in a third terminal**, log on the SSH frontend, build and flash
   the RIOT MQTT-SN example firmware on the M3:
   ```
   my_computer$ ssh <login>@saclay.iot-lab.info
   login@saclay:~$ source /opt/riot.source
   login@saclay:~$ cd ~/A8/riot/RIOT
   login@saclay:~/A8/riot/RIOT$ make BOARD=iotlab-a8-m3 -C examples/emcute_mqttsn
   login@saclay:~/A8/riot/RIOT$ iotlab-ssh flash-m3 examples/emcute_mqttsn/bin/iotlab-a8-m3/emcute_mqttsn.elf -l saclay,a8,3
   ```
   You can now login to the A8 and connect to the M3 via the serial port to
   access the RIOT shell:
   ```
   login@saclay:~$ ssh root@node-a8-3
   root@node-a8-2:~# miniterm.py /dev/ttyA8_M3 500000 -e
   > help
   Command        
         Description
   ---------------------------------------
   con                  connect to MQTT broker
   discon               disconnect from the current broker
   pub                  publish something
   sub                  subscribe topic
   unsub                unsubscribe from topic
   will                 register a last will
   reboot               Reboot the node
   ps                   Prints information about running threads.
   ping6                Ping via ICMPv6
   random_init          initializes the PRNG
   random_get           returns 32 bit of pseudo randomness
   ifconfig             Configure network interfaces
   ncache               manage neighbor cache by hand
   routers              IPv6 default router list
   ```
   Use the `con` command to connect to the MQTT-SN broker on `node-a8-2` and
   subscribe to the `test/riot` topic using the `sub` command.
   ```
   > con 2001:660:3207:400::66 1885
   > sub test/riot
   ```

11. In **a fourth terminal**, connect to the SSH frontend and use the
   preinstalled [mosquitto client CLI](https://packages.debian.org/fr/stretch/mosquitto-clients)
   to publish and subscribe to topics on the MQTT broker running on `node-a8-2`
   ```
   login@saclay:~$ mosquitto_pub -h 2001:660:3207:400::66 -p 1886 -t test/riot -m iotlab
   ```
   On the RIOT shell (`node-a8-3`, third terminal), you get the following message:
   ```
   ### got publication for topic 'test/riot' [1] ###
   iotlab
   ```

If everything works as described, you are able to use MQTT-SN with RIOT on IoT-LAB. **Congratulations !**
<br/>
Now play with `mosquitto_sub` on the frontend side (fourth terminal) and the
`pub` command in the RIOT node shell (third terminal) to exchange messages from
the node to the frontend.
