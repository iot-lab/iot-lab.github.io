---
group: riot
title: Public IPv6 (6LoWPAN/RPL) network with M3 nodes
---

<i class="fas fa-grin-beam-sweat"></i> **Difficulty**: Medium
<i class="fas fa-stopwatch"></i> **Duration**: 45 minutes

_**Prerequisites**: [Configure SSH Access]({{ site.baseurl }}{% link
docs/getting-started/ssh-access.md %}) , [RIOT basics]({{ site.baseurl }}{% link
docs/os/riot.md %})_

_**Description**: The goal of this tutorial is to discover the basics of RIOT
GNRC stack & tools for IoT-LAB IPv6. You will reserve 2 M3 nodes on the Saclay
site, build 2 firmwares and flash them on the M3 nodes, and create a simple
IPv6 network in IoT-LAB. Finally, you’ll access nodes using UDP over IPv6 from
the SSH frontend (or any Host with a global IPv6 address), using the
`ethos_uhcpd.py` tool provided on the frontend._

1. Connect to Saclay site host: 
  ```
  my_computer$ ssh <login>@saclay.iot-lab.info
  ```

2. Start an experiment with 2 M3 nodes called `riot_m3`:
  ```
  login@saclay:~$ iotlab-auth -u <login>
  login@saclay:~$ iotlab-experiment submit -n riot_m3 -d 60 -l 2,archi=m3:at86rf231+site=saclay
  ```
  Remember the experiment identifier returned by the last command. It’ll be
  used in the commands shown below, `<exp_id>`. The requested experiment
  duration is **60** minutes.

3. Wait a moment until the experiment is launched (state is Running) and get
   the nodes list. For the next of this tutorial we suppose that you obtained
   **m3-1.saclay.iot-lab.info** and **m3-2.saclay.iot-lab.info** nodes
   ```
   login@saclay:~$ iotlab-experiment get -i <exp_id> -p
   login@saclay:~$ iotlab-experiment get -i <exp_id> -n
   ```

4. Get the code of the 2020.10 release of [RIOT](https://github.com/RIOT-OS/RIOT)
   from GitHub: 
   ```
   login@saclay:~$ mkdir -p ~/riot
   login@saclay:~$ cd ~/riot
   login@saclay:~/riot$ git clone https://github.com/RIOT-OS/RIOT.git -b 2020.10-branch
   login@saclay:~/riot$ cd RIOT
   ```
  **Note:** you can also use the RIOT development code (e.g the master branch) but
  this will be at your own risk: this tutorial may not fully work.

5. Build the required firmware for the border router node. The node `m3-1` will
   act as the border router in this experiment. The border firmware is built
   using the RIOT
   [gnrc_border_router example](https://github.com/RIOT-OS/RIOT/tree/master/examples/gnrc_border_router).

   **Important note 1:** we build this firmware with a baudrate of **500000**.
   This is mandatory for ethos_uhcpd.py script to work effectively since the
   UART baudrate of the M3 is 500000.

   **Important note 2:** to minimize radio interferences with other users
   experiments, the firmwares used can be built for different 802.15.4 channel
   (default is 26, allowed values goes from 11 to 26).<br/>
   To do this, add **DEFAULT_CHANNEL=&lt;channel&gt;** option to the make commands.
   ```
   login@saclay:~/riot/RIOT/$ source /opt/riot.source
   login@saclay:~/riot/RIOT/$ make ETHOS_BAUDRATE=500000 DEFAULT_CHANNEL=<channel> BOARD=iotlab-m3 -C examples/gnrc_border_router clean all
   ```

   Use the CLI-Tools to flash the gnrc_border_router firmware that you have
   just built on the first M3 node. Here we use m3-1 but it may  change in your
   case:
   ```
   login>@saclay:~/riot/RIOT/$ iotlab-node --flash examples/gnrc_border_router/bin/iotlab-m3/gnrc_border_router.elf -l saclay,m3,1
   ```

6. Now you can configure the network of the border router on `m3-1` and
   propagate an IPv6 prefix with `ethos_uhcpd.py`.
   ```
   login@saclay:~$ sudo ethos_uhcpd.py m3-1 tap0 2001:660:3207:04c1::1/64
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
   our LLN, 2001:660:3207:04c1::/64. You can find informations about IPv6
   subnetting for M3 nodes here.

   - **Note 1:** **leave the terminal open** (you don’t want to kill
     `ethos_uhcpd.py`, it bridges the BR to the front-end network)
   - **Note 2:** If you have **an error "Invalid prefix – Network overlapping with routes"**,
     it’s because another experiment is using the same ipv6 prefix (e.g. **2001:660:3207:04c1::/64**).

     You can view currently used IPv6 prefixes on the frontend SSH with this command:
      ```
      login@saclay:~$ ip -6 route
      2001:660:3207:4bf::/64 dev eth0  proto kernel  metric 256 
      2001:660:3207:4c1::/64 via fe80::2 dev tap0  metric 1024 
      fe80::/64 dev eth1  proto kernel  metric 256 
      fe80::/64 dev eth0  proto kernel  metric 256 
      fe80::/64 dev tap0  proto kernel  metric 256 
      default via 2001:660:3207:4bf:ff:: dev eth0  metric 1024
      ```
   - **Note 3:** If you have **an error "Device or resource busy"**, it’s
     because another user is using the same tap interface (e.g. **tap0**).
     Just use another one.<br/>
     You can view currently used tap interfaces using the same command than in
     the previous note.

7. Now, **in another terminal**, SSH to the SSH frontend and build the required
   firmware for the other node. RIOT [gnrc_networking example](https://github.com/RIOT-OS/RIOT/tree/master/examples/gnrc_networking)
   will be used for this purpose.
   ```
   login@saclay:~$ cd riot/RIOT
   login@saclay:~/riot/RIOT/$ source /opt/riot.source
   login@saclay:~/riot/RIOT/$ make DEFAULT_CHANNEL=<channel> BOARD=iotlab-m3 -C examples/gnrc_networking clean all
   ```
   Use the CLI-Tools to flash the gnrc_networking firmware that you have just
   built on the first M3 node. Here we use `m3-2` but it may change in your case:
   ```
   login@saclay:~/riot/RIOT/$ iotlab-node --flash examples/gnrc_networking/bin/iotlab-m3/gnrc_networking.elf -l saclay,m3,2
   ```

8. You can now interact with the second M3 node. `m3-2` using `nc`.
   ```
   my_computer$ ssh <login>@saclay.iot-lab.info
   login@saclay:~$ nc m3-2 20000
   ```

   You now have access to the RIOT shell and can ping another Internet host
   using IPv6 (let’s try a Google DNS host):
   ```
   > help
   > ping6 2001:4860:4860::8888
   ping6 2001:4860:4860::8888
   12 bytes from 2001:4860:4860::8888: id=83 seq=1 hop limit=50 time = 36.113 ms
   12 bytes from 2001:4860:4860::8888: id=83 seq=2 hop limit=50 time = 34.839 ms
   12 bytes from 2001:4860:4860::8888: id=83 seq=3 hop limit=50 time = 36.918 ms
   --- 2001:4860:4860::8888 ping statistics ---
   3 packets transmitted, 3 received, 0% packet loss, time 2.06113456 s
   rtt min/avg/max = 34.839/35.956/36.918 ms
   ```

   Use RIOT shell `ifconfig` command to get the IP of the M3 node:
   ```
   > ifconfig
   Iface  7   HWaddr: 29:02  Channel: 26  Page: 0  NID: 0x23
           Long HWaddr: 36:32:48:33:46:df:a9:02 
           TX-Power: 0dBm  State: IDLE  max. Retrans.: 3  CSMA Retries: 4 
           AUTOACK  CSMA  MTU:1280  HL:64  6LO  RTR  RTR_ADV  IPHC  
           Source address length: 8
           Link type: wireless
           inet6 addr: ff02::1/128  scope: local [multicast]
           inet6 addr: fe80::1711:6b10:65fd:bd36/64  scope: local
           inet6 addr: ff02::1:fffd:bd36/128  scope: local [multicast]
           inet6 addr: 2001:660:3207:4c1:1711:6b10:65fd:bd36/64  scope: global
           inet6 addr: ff02::2/128  scope: local [multicast]
   ```

   The global prefix has been successfully propagated, the IP on the M3 is
   `2001:660:3207:4c1:1711:6b10:65fd:bd36`. Verify that it answers to "ping"
   from the **SSH frontend** (and from any computer with a global IPv6):
   ```
   login@saclay:~$ ping6 -c 3 2001:660:3207:4c1:1711:6b10:65fd:bd36
   PING 2001:660:3207:4c1:1711:6b10:65fd:bd36(2001:660:3207:4c1:1711:6b10:65fd:bd36) 56 data bytes
   64 bytes from 2001:660:3207:4c1:1711:6b10:65fd:bd36: icmp_seq=1 ttl=61 time=45.7 ms
   64 bytes from 2001:660:3207:4c1:1711:6b10:65fd:bd36: icmp_seq=2 ttl=61 time=46.5 ms
   64 bytes from 2001:660:3207:4c1:1711:6b10:65fd:bd36: icmp_seq=3 ttl=61 time=44.9 ms
   
   --- 2001:660:3207:4c1:1711:6b10:65fd:bd36 ping statistics ---
   3 packets transmitted, 3 received, 0% packet loss, time 2003ms
   rtt min/avg/max/mdev = 44.919/45.759/46.595/0.684 ms
   ```

   Still on `m3-2`, let’s verify that UDP packets can be received from the
   SSH frontend. Use the `udp` command in the `gnrc_networking` shell to start
   an UDP server on the M3 node:
   ```
   > udp server start 8888
   udp server start 8888
   Success: started UDP server on port 8888
   ```

   Then from the SSH frontend, send a message by udp:
   ```
   login@saclay:~$ echo "hello" > /dev/udp/2001:660:3207:4c1:1711:6b10:65fd:bd36/8888
   ```

   Verify that the packet is received by the M3 node:
   ```
   > PKTDUMP: data received:
   ~~ SNIP  0 - size:   5 byte, type: NETTYPE_UNDEF (0)
   000000 68 65 6c 6c 6f
   ~~ SNIP  1 - size:   8 byte, type: NETTYPE_UDP (4)
      src-port: 49568  dst-port:  8888
      length: 13  cksum: 0x45fb6
   ~~ SNIP  2 - size:  40 byte, type: NETTYPE_IPV6 (2)
   traffic class: 0x00 (ECN: 0x0, DSCP: 0x00)
   flow label: 0x92520
   length: 13  next header: 17  hop limit: 52
   source address: 2001:660:3207:4bf::17
   destination address: 2001:660:3207:4c1:1711:6b10:65fd:bd36
   ~~ SNIP  3 - size:  24 byte, type: NETTYPE_NETIF (-1)
   if_pid: 7  rssi: 18  lqi: 255
   src_l2addr: 36:32:48:33:46:d4:9a:22
   dst_l2addr: 36:32:48:33:46:df:a9:02
   ~~ PKT    -  4 snips, total size:  77 byte
   ```

If everything works as described, the Border Router is correctly configured. **Congratulations !**
