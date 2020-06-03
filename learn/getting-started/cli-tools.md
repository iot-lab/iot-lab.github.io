---
group: getting-started
title: CLI tools
---

<i class="fas fa-grin-beam-sweat"></i> **Difficulty**: Easy  
<i class="fas fa-stopwatch"></i> **Duration**: 20 minutes

_**Prerequisites**: [IoT-LAB M3 board]({{ site.baseurl }}{% link docs/boards/iot-lab-m3.md %}) / [Configure SSH Access]({{ site.baseurl }}{% link docs/getting-started/ssh-access.md %})_

_**Description**: The aim of this first tutorial is to discover the IoT-LAB testbed tools by creating and submitting your first experiment, and then interact with running nodes. You will book onto the SSH frontend with CLI tools two M3 nodes on the Grenoble site, set them up with a sample firmware file, and deploy it on them. Once deployed, you will interact with the firmware running on the nodes, read sensor values and send radio packets through a terminal._

1. Connect to the SSH frontend and launch your first experiment.

    <pre class="highlight">
    ssh &lt;login&gt;@grenoble.iot-lab.info
    # only once to store credentials on the SSH frontend
    &lt;login&gt;@grenoble~$ iotlab-auth -u &lt;login&gt;
    &lt;login&gt;@grenoble~$ wget {{ site.url }}{{ 'assets/firmwares/tutorial_m3.elf' | relative_url}} .
    &lt;login&gt;@grenoble~$ iotlab-experiment submit -n first-exp -d 20 -l 2,archi=m3:at86rf231+site=grenoble,tutorial_m3.elf
    # wait until the experiment's state is <i>Running</i>
    &lt;login&gt;@grenoble~$ iotlab-experiment wait
    </pre>


2. View the nodes that have been assigned to you by the scheduler.

    <pre class="highlight">
    &lt;login&gt;@grenoble~$ iotlab-experiment get -n
    {
    "items": [
            {
            "archi": "m3:at86rf231",
            "network_address": "m3-1.grenoble.iot-lab.info",
            "site": "grenoble",
            ...
            }
        ]
    }

    </pre>

3. Read the node's serial port link (i.e. UART). It's forwarded onto the SSH frontend with TCP socket on port <strong>20000</strong>. To do this you must open one terminal per node on the SSH frontend. Keep the previous terminal for one node and open another one for the other node.

    <pre class="highlight">
    # Replace &lt;id1&gt; by one of those obtained above
    &lt;login&gt;@grenoble~$ nc m3-&lt;id1&gt; 20000
    </pre>

    <pre class="highlight">
    ssh &lt;login&gt;@grenoble.iot-lab.info
    # Replace &lt;id2&gt; by the other one
    &lt;login&gt;@grenoble~$ nc m3-&lt;id2&gt; 20000
    </pre>

4. Play with the firmware shell and read sensors value (e.g. type t+ENTER) or send radio packets (e.g. type s+ENTER). You can note that as the scheduler provides you some nodes with the same radio neighborhood, when you send a radio packet (i.e. broadcast mode) from one node the other one should display good reception information on the serial port.

    <pre class="highlight">
    &lt;login&gt;@grenoble~$ nc m3-&lt;id1&gt; 20000
    cmd >

    IoT-LAB Simple Demo program
    Type command
	    h:	print this help
	    t:	temperature measure
	    l:	luminosity measure
	    p:	pressure measure
	    u:	print node uid
	    d:	read current date using control_node
	    s:	send a radio packet
	    b:	send a big radio packet
	    e:	toggle leds blinking
    </pre>


## Go Further

* Consult the [CLI-tools]({{ site.baseurl }}{% link docs/tools/cli.md %}) documentation.
* Learn how to aggregate all the serial port links of your nodes with [Serial Aggregator]({{ site.baseurl }}{% link docs/tools/serial-aggregator.md %}) tool.
