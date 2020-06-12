---
group: getting-started
title: Linux CLI tools
---

<i class="fas fa-grin-beam-sweat"></i> **Difficulty**: Intermediate  
<i class="fas fa-stopwatch"></i> **Duration**: 30 minutes

_**Prerequisites**: [IoT-LAB A8-M3 board]({{ site.baseurl }}{% link docs/boards/iot-lab-a8-m3.md %}) / [Configure SSH Access]({{ site.baseurl }}{% link docs/getting-started/ssh-access.md %})_

_**Description**: The aim of this first tutorial is to discover the IoT-LAB testbed tools by creating and submitting your first experiment, and then interact with running nodes. You will book onto the SSH frontend with CLI tools two A8-M3 nodes on the Saclay site. Once deployed, you will connect by SSH to the Linux nodes (i.e. A8 nodes) and interact with the embed M3 co-microcontroller. Thus you will learn how to flash a sample firmware file on it and read sensor values and send radio packets through the serial port link (i.e. UART)


1. Connect to the SSH frontend and launch your first experiment.

    <pre class="highlight">
    ssh &lt;login&gt;@saclay.iot-lab.info
    # only once to store credentials on the SSH frontend
    &lt;login&gt;@saclay~$ iotlab-auth -u &lt;login&gt;
    &lt;login&gt;@saclay~$ iotlab-experiment submit -n first-exp -d 20 -l 2,archi=a8:at86rf231+site=saclay
    # wait until the experiment's state is <i>Running</i>
    &lt;login&gt;@saclay~$ iotlab-experiment wait
    </pre>


2. View the nodes that have been assigned to you by the scheduler.

    <pre class="highlight">
    &lt;login&gt;@saclay~$ iotlab-experiment get -n
    {
    "items": [
            {
            "archi": "a8:at86rf231", 
            "network_address": "a8-1.saclay.iot-lab.info", 
            "site": "saclay", 
            ...
            }
        ]
    } 

    </pre>


3. Download the firmware file on the SSH frontend in the <strong>shared</strong> directory. This directory is automatically mounted by NFS by all Linux nodes during the experiment.

    <pre class="highlight">
    &lt;login&gt;@saclay~$ wget {{ site.url }}{{ 'assets/firmwares/tutorial_a8_m3.elf' | relative_url}} -P shared
    </pre>

4. Connect by SSH to one A8 Linux node with root user. When your experiment is running, A8 Linux nodes still need some time to boot, it can take between 30 seconds and 2 minutes depending on the testbed activity. Another important point to understand is the name of the Linux node you have to use. You must prefix the name with the string <strong>node-</strong>. In the example above the scheduler has assigned you the node <strong>a8-1.saclay.iot-lab.info</strong> and the Linux A8 node will be accessible with the name <strong>node-a8-1.saclay.iot-lab.info</strong>.

    <pre class="highlight">
    &lt;login&gt;@saclay~$ ssh root@<strong>node-a8-1</strong>.saclay.iot-lab.info
    The authenticity of host 'node-a8-1.saclay.iot-lab.info (10.0.44.1)' can't be established.
    RSA key fingerprint is 2b:a9:fc:bc:d5:77:27:24:06:fc:46:a2:87:17:e9:b0.
    Are you sure you want to continue connecting (yes/no)? yes
    Warning: Permanently added 'node-a8-1.saclay.iot-lab.info,10.0.44.1' (RSA) to the list of known hosts.
    root@node-a8-1:~#
    </pre>

    > As you are handling a Linux node it is necessary to have an IP and a DNS name dedicated to it. The scheduler assigns you IoT-LAB nodes with the DNS name of the gateway (GW) which is a hardware (i.e. administration board not accessible by users) in charge of deploying the experiment with for example powering the Linux node. 

5. A8 nodes are running a minimal embedded Linux system and most unix commands are supported. For example you can test test the network connectivity between from your two nodes or visualize the content of the A8 directory. In the example below we assume that the second node of the experiment is <strong>node-a8-2</strong>.

    <pre class="highlight">
    root@node-a8-1:~# ping node-a8-2
    PING node-a8-2 (10.0.44.2): 56 data bytes
    64 bytes from 10.0.44.2: seq=0 ttl=64 time=5.616 ms
    64 bytes from 10.0.44.2: seq=1 ttl=64 time=1.038 ms
    64 bytes from 10.0.44.2: seq=2 ttl=64 time=0.977 ms
    root@node-a8-1:~# ls A8
    tutorial_a8_m3.elf
    </pre>

6. Flash the firmware on the M3 co-microcontroller of both nodes. To do this we provide <i>iotlab_flash</i> script that interfaces with Open On-Chip Debugger (OpenOCD) to flash the firmware.

    <pre class="highlight">
    root@node-a8-1:~# iotlab_flash shared/tutorial_a8_m3.elf
    Open On-Chip Debugger 0.10.0+dev-00554-g05e0d63-dirty (2019-09-23-09:35)
    Licensed under GNU GPL v2
    For bug reports, read
        http://openocd.org/doc/doxygen/bugs.html
    debug_level: 0
    adapter speed: 1000 kHz
    adapter_nsrst_delay: 100
    jtag_ntrst_delay: 100
    none separate
    cortex_m reset_config sysresetreq
    trst_and_srst separate srst_nogate trst_push_pull srst_open_drain connect_assert_srst
        TargetName         Type       Endian TapName            State       
    --  ------------------ ---------- ------ ------------------ ------------
    0* stm32f1x.cpu       cortex_m   little stm32f1x.cpu       reset
    target halted due to debug-request, current mode: Thread 
    xPSR: 0x01000000 pc: 0x080017f4 msp: 0x20010000
    target halted due to debug-request, current mode: Thread 
    xPSR: 0x01000000 pc: 0x080017f4 msp: 0x20010000
    auto erase enabled
    wrote 47104 bytes from file /home/root/A8/tutorial_a8_m3.elf in 2.152863s (21.367 KiB/s)
    verified 46332 bytes in 0.757233s (59.752 KiB/s)
    shutdown command invoked
    flash OK
    </pre>

    <pre class="highlight">
    ssh &lt;login&gt;@saclay.iot-lab.info
    &lt;login&gt;@saclay~$ ssh root@<strong>node-a8-2</strong>
    root@node-a8-2:~# iotlab_flash shared/tutorial_a8_m3.elf
    ...
    </pre>

    > You can also find <i>iotlab_reset</i> script to reset the M3 co-microcontroller. 

7. Read the M3 co-microcontroller serial port link (i.e. UART). The UART filename is <i>/dev/ttyA8_M3</i> with a baudrate speed of 500 kB/s.

    <pre class="highlight">
    root@node-a8-1:~# miniterm.py --echo /dev/ttyA8_M3 500000
    </pre>

    <pre class="highlight">
    root@node-a8-2:~# miniterm.py --echo /dev/ttyA8_M3 500000
    </pre>

8. Play with the firmware shell and send radio packets (e.g. type s+ENTER). You can note that as the scheduler provides you some nodes with the same radio neighborhood, when you send a radio packet (i.e. broadcast mode) from one node the other one should display good reception information on the serial port.

    <pre class="highlight">
    root@node-a8-1:~# miniterm.py /dev/ttyA8_M3 500000
    cmd > 

    IoT-LAB Simple Demo program
    Type command
	    h:	print this help
	    u:	print node uid
	    d:	read current date using control_node
	    s:	send a radio packet
	    b:	send a big radio packet
	    e:	toggle leds blinking
    </pre>


## Go Further

* Consult the [SSH-CLI]({{ site.baseurl }}{% link docs/tools/ssh-cli.md %}) command-line tools documentation. It allows you to interact remotely with Linux nodes and automate actions such as waiting for the end of the boot, flashing a firmware on the co-microcontroller. 




 
