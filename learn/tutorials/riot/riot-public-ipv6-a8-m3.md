---
group: riot
title: Public IPv6 (6LoWPAN/RPL) network with A8-M3 nodes
---

<i class="fas fa-grin-beam-sweat"></i> **Difficulty**: Medium
<i class="fas fa-stopwatch"></i> **Duration**: 45 minutes

_**Prerequisites**: [Configure SSH Access]({{ site.baseurl }}{% link
docs/getting-started/ssh-access.md %}) , [RIOT basics]({{ site.baseurl }}{% link
docs/os/riot.md %})_


_**Description**: The goal of this tutorial is to discover the basics of RIOT GNRC stack & tools for IoT-LAB IPv6. You will reserve 2 A8 nodes on the Saclay site, build 2 firmwares and flash them on the A8-M3 nodes, and create a simple IPv6 network in IoT-LAB. Finally, you’ll access nodes using UDP over IPv6 from the SSH frontend (or any Host with a global IPv6 address), using RIOT network automatic configuration tools._

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

9. Now, **in another terminal**, log on the remaining A8 node, `node-a8-2`, and
   flash the `gnrc_networking` firmware on the M3:
   ```
   my_computer$ ssh <login>@saclay.iot-lab.info
   login@saclay:~$ ssh root@node-a8-2
   root@node-a8-2:~# iotlab_flash A8/gnrc_networking.elf
   ```
   Connect to the RIOT shell on the M3 using `miniterm.py`:
   ```
   root@node-a8-2:~# miniterm.py -e /dev/ttyA8_M3 500000
   ```
   From the RIOT shell, one can ping an Internet host (let’s try a Google DNS
   host):
   ```
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
           inet6 addr: fe80::3432:4833:46df:a902/64  scope: local
           inet6 addr: ff02::1:ffdf:a902/128  scope: local [multicast]
           inet6 addr: 2001:660:3207:401:3432:4833:46df:a902/64  scope: global
           inet6 addr: ff02::2/128  scope: local [multicast]
   ```
   The global prefix has been successfully propagated, the IP on the M3 is
   `2001:660:3207:401:3432:4833:46df:a902`. Verify that it answers to "ping"
   from the **SSH frontend** (and from any computer with a global IPv6):
   ```
   login@saclay:~$ ping6 -c 3 2001:660:3207:401:3432:4833:46df:a902
   PING 2001:660:3207:401:3432:4833:46df:a902(2001:660:3207:401:3432:4833:46df:a902) 56 data bytes
   64 bytes from 2001:660:3207:401:3432:4833:46df:a902: icmp_seq=1 ttl=61 time=45.7 ms
   64 bytes from 2001:660:3207:401:3432:4833:46df:a902: icmp_seq=2 ttl=61 time=46.5 ms
   64 bytes from 2001:660:3207:401:3432:4833:46df:a902: icmp_seq=3 ttl=61 time=44.9 ms
   
   --- 2001:660:3207:401:3432:4833:46df:a902 ping statistics ---
   3 packets transmitted, 3 received, 0% packet loss, time 2003ms
   rtt min/avg/max/mdev = 44.919/45.759/46.595/0.684 ms
   ```
   Still on `node-a8-2`, let’s verify that UDP packets can be received from the
   site-host. Use `udp` command from `gnrc_networking` example to start an UDP
   server on the M3 node:
   ```
   > udp server start 8888
   udp server start 8888
   Success: started UDP server on port 8888
   ```
   Then from the site host, send a message by udp:
   ```
   login@saclay:~$ echo "hello" > /dev/udp/2001:660:3207:401:3432:4833:46df:a902/8888
   ```
   The packet has been received by the M3 node:
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
   source address: 2a01:e35:2eba:eea0:21e:64ff:fefe:f394
   destination address: 2001:660:3207:401:3432:4833:46df:a902
   ~~ SNIP  3 - size:  24 byte, type: NETTYPE_NETIF (-1)
   if_pid: 7  rssi: 18  lqi: 255
   src_l2addr: 36:32:48:33:46:d4:9a:22
   dst_l2addr: 36:32:48:33:46:df:a9:02
   ~~ PKT    -  4 snips, total size:  77 byte
   ```

If everything works as described, the Border Router is correctly configured. **Congratulations !**
