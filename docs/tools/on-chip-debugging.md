---
title: On-chip debugging
group: tools
description: On-chip debugging is a feature which allow to debug embedded software running on the node. You can launch a debugger (GDB console) on the SSH frontend server and runs the firmware code on the embedded board in debugging mode. You can put break points at anywhere within your code like normal debugging process, then the embedded processor just hangs there, letting you to investigate anything (registers, memory values) which currently available on the board.
---

## Tutorial firmware compilation

To illustrate the On-chip debbuging feature we will use and compile the IoT-LAB tutorial firmware on the frontend SSH server.

``` bash
ssh <login>@grenoble.iot-lab.info
<login>@grenoble:~$ git clone https://github.com/iot-lab/iot-lab.git
<login>@grenoble:~$ cd iot-lab
<login>@grenoble:~/iot-lab$ make setup-openlab
<login>@grenoble:~/iot-lab$ cd parts/openlab
```

The tutorial firmware source code is located in `appli/iotlab_examples/tutorial/` directory. It's written with OpenLAB, a FreeRTOS port for IoT-LAB M3 and A8-M3 nodes. As we want to active debugging mode we advice you to deactivate the `WFI` (Wait For Interrupt) processor instruction. This instruction allow the core to enter a low power mode and stop executing code. You can comment it in openlab `platform.c` file (line 81) before compiling firmware.

``` bash
<login>@grenoble:~/iot-lab$ vi platform/platform.c
...
        // Enter SLEEP mode
        // asm volatile(“wfi”);
...
# :wq shortcut to exit
```

``` bash
<login>@grenoble:~/iot-lab/parts/openlab$ mkdir build.m3 ; cd build.m3/
<login>@grenoble:~/iot-lab/parts/openlab/build.m3$ cmake .. -DPLATFORM=iotlab-m3
<login>@grenoble:~/iot-lab/parts/openlab/build.m3$ make tutorial_m3
<login>@grenoble:~/iot-lab/parts/openlab/build.m3$ ls bin/tutorial_m3.elf # the binary firmware file
```

## Launch an experiment

To illustrate the on-chip debugging feature we will launch an experiment with:

* a duration of 45 minutes
* two M3 nodes on Grenoble site

In the Webortal go to the [New Experiment](https://www.iot-lab.info/testbed/experiment) page and select nodes by `node properties` (two M3 nodes on Grenoble site).

With command-line tools use these commands:

``` bash
$ iotlab-experiment submit -d 45 -l 2,archi=m3:at86rf231+site=grenoble,<path_tutorial_m3.elf>
$ iotlab-experiment wait
$ iotlab-experiment get -ni
```

## GDB session startup

Firstly, choose one node and activate the debugging mode. This feature is only provide by CLI command-line tools.

``` bash
<login>@grenoble:~$ iotlab-node --debug-start -l grenoble,m3,<id1>
{
 "0": [
 "m3-<id1>.grenoble.iot-lab.info"
 ]
}
```

Start a GDB console with your binary firmare file and the remote target (`m3-<id1>`) which listens for GDB connections on port 3333

``` bash
<login>@grenoble:~$ arm-none-eabi-gdb -ex "target remote m3-<id1>:3333" tutorial_m3.elf
GNU gdb (GNU Tools for ARM Embedded Processors) 7.8.0.20150304-cvs
...
Reading symbols from tutorial_m3.elf...done.
Remote debugging using m3-<id1>:3333
...
(gdb)
```

You can send some commands and test the connection. Visualize the registers list, show the flash memory module address at `0x08000000` and check the FLASH_WRPR register at `0x40022020` address to confirm that your device’s write-protection has been disabled (`0xffffffff` means all pages have their write protection disabled).

``` bash
(gdb) monitor reg
===== arm v7m registers
(0) r0 (/32): 0x00000000
...
(gdb)
(gdb) monitor flash probe 0
flash 'stm32f1x' found at 0x08000000
(gdb)  monitor mdw 0x40022020
0x40022020: ffffffff
(gdb)
```

Halt the processor and link the firmware to be loaded into flash memory on the Cortex-M3.

``` bash
(gdb) monitor reset halt
target halted due to debug-request, current mode: Thread
xPSR: 0x01000000 pc: 0x08002dd0 msp: 0x20010000
(gdb)
(gdb) load
Loading section .text, size 0x9148 lma 0x8000000
Loading section .ARM.exidx, size 0x8 lma 0x8009148
Loading section .rodata, size 0x3f0c lma 0x8009150
Loading section .data, size 0x8e0 lma 0x800d05c
Start address 0x8002dd0, load size 55612
Transfer rate: 16 KB/sec, 9268 bytes/write.
(gdb)
```

## Start debugging

Set a breakpoint in the code with [mac_csma_data_received](https://github.com/iot-lab/openlab/blob/master/appli/iotlab_examples/tutorial/main.c) function (line 153) and stop it when we will receive a radio packet.

``` bash
(gdb) break mac_csma_data_received
Breakpoint 1 at 0x80004b8: file /senslab/users/<login>/iot-lab/parts/openlab/appli/iotlab_examples/tutorial/main.c, line 155.
(gdb)
(gdb) info break
Num     Type           Disp Enb Address    What
1       breakpoint     keep y   0x080004b8 in mac_csma_data_received
                                           at /senslab/users/saintmar/iot-lab/parts/openlab/appli/iotlab_examples/tutorial/main.c:155
```

Now open a new terminal on the SSH frontend server and launch `serial_aggregator` command to access the serial port of the nodes. Stop the write of the firmware shell and watch that you have only one node which prints on the serial port. It's normal the other one (m3-<id1>) has just been halted.


``` bash
ssh <login>@grenoble.iot-lab.info
<login<@grenoble:~$ serial_aggregator
1578472010.325098;Aggregator started
1578472010.896501;m3-<id2>;
1578472010.896822;m3-<id2>;
1578472010.898528;m3-<id2>;IoT-LAB Simple Demo program
1578472010.898718;m3-<id2>;Type command
...
# Hit "Space+Enter" to stop the flood.
```

Perform a hard reset in the gdb console, execute the init script and continue the code execution.

``` bash
(gdb) monitor reset init
target halted due to debug-request, current mode: Thread
xPSR: 0x01000000 pc: 0x08002dd0 msp: 0x20010000
(gdb) continue
Continuing.
Note: automatically using hardware breakpoints for read-only addresses.
```

On the serial aggregator you must see the starting of the `m3-<id1>` node. Stop the write of the firmware shell and send a radio packet from the `m3-<id2>` node.

``` bash
# Hit "Space+Enter" to stop the flood.
1578472170.351334;m3-<id1>;[in event_init() INFO] Priority of event task #0: 6/7
1578472170.352871;m3-<id1>;[in event_init() INFO] Priority of event task #1: 7/7
1578472170.354122;m3-<id1>;
1578472170.354293;m3-<id1>;
1578472171.354946;m3-<id1>;Platform starting in 1...
1578472171.355190;m3-<id1>;GO!
1578472171.355755;m3-<id1>;FreeRTOS Heap Free: 19824
1578472172.355926;m3-<id1>;
1578472172.356153;m3-<id1>;
1578472172.356263;m3-<id1>;IoT-LAB Simple Demo program
1578472172.356836;m3-<id1>;Type command
1578472172.356996;m3-<id1>;	h:	print this help
...
# Hit "Space+Enter" to stop the flood.
m3-<id2>;s
1578472461.840438;m3-<id2>;cmd >
1578472461.841177;m3-<id2>;radio > Packet sent
1578472461.841465;m3-<id2>;
```

You can see in the GDB console that you reach the breakpoint previously defined. With the `list` command you can watch where we are in the execution code and GDB prints source lines. In the `mac_csma_data_received` function we print (lines 160 & 161) on the serial port that we received a radio packet.

``` bash
Breakpoint 1, mac_csma_data_received (src_addr=37249, data=0x20000a71 <mac+53> "Hello World!: 0",
    length=16 '\020', rssi=-55 '\311', lqi=lqi@entry=255 '\377')
    at /senslab/users/<login>/iot-lab/parts/openlab/appli/iotlab_examples/tutorial/main.c:155
155	{
(gdb)
(gdb) set listsize 15
(gdb) list
148	        printf("Big packet sent failed\n");
149	}
150
151
152	/* Reception of a radio message */
153	void mac_csma_data_received(uint16_t src_addr,
154	        const uint8_t *data, uint8_t length, int8_t rssi, uint8_t lqi)
155	{
156	    // disable help message after receiving one packet
157	    print_help = 0;
158	    struct node src_node = node_from_uid(src_addr);
159
160	    printf("\nradio > ");
161	    printf("Got packet from %x (%s-%u). Len: %u Rssi: %d: '%s'\n",
162	            src_addr, src_node.type_str, src_node.num,
(gdb)
```

Continue the source code execution after the breakpoint in the GDB console

``` bash
(gdb) continue
Continuing.
```

Verify that you receive the radio packet on the serial aggregator shell

``` bash
1578473269.077028;m3-<id1>;cmd >
1578473269.077925;m3-<id1>;radio > Got packet from <UID_M3_ID2> (m3-<id2>). Len: 16 Rssi: -55: 'Hello World!: 5'
1578473269.079093;m3-<id1>;
```
