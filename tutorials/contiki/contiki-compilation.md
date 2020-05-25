---
group: contiki
title: Get and compile firmware for M3 and A8-M3 nodes
---

<i class="fas fa-grin-beam-sweat"></i> **Difficulty**: Medium  
<i class="fas fa-stopwatch"></i> **Duration**: 20 minutes

_**Prerequisites**: [Configure SSH Access]({{ site.baseurl }}{% link docs/getting-started/ssh-access.md %})_

_**Description**: Contiki OS is an operating system designed for the particular requirements of Internet of Things (IoT) scenarios. The aim of this tutorial is to understand how to setup your environment and how to compile and use Contiki with M3 and A8-M3 nodes. For these nodes, Contiki needs the toolchain arm-none-eabi-gcc. The frontend SSH servers site provide this toolchain, hence we can use it._

1.  Setup your environment

    <pre class="highlight">
    <strong>ssh &lt;login&gt;@&lt;site&gt;.iot-lab.info</strong>
    &lt;login&gt;@&lt;site&gt;~$ <strong>git clone https://github.com/iot-lab/iot-lab.git
    </strong>Cloning into 'iot-lab'...
    ...
    &lt;login&gt;@&lt;site&gt;~$ <strong>cd iot-lab</strong>
    &lt;login&gt;@&lt;site&gt;:~/iot-lab$ <strong>make</strong>

    Welcome to the IoT-LAB development environment setup.

    targets:
    setup-wsn430
    setup-openlab
    setup-contiki
    setup-riot
    setup-cli-tools
    setup-aggregation-tools

    pull</pre>

2.  Setup Contiki target

    <pre class="highlight">&lt;login&gt;@&lt;site&gt;:~/iot-lab$ <strong>make setup-contiki
    </strong>git clone https://github.com/iot-lab/contiki.git parts/contiki
    Cloning into parts/contiki...
    ...
    &lt;login&gt;@&lt;site&gt;:~/iot-lab$ <strong>cd parts/contiki</strong></pre>

3.  We run a first example provided in parts/contiki/examples/iotlab/. View and analyse the source code of this example.

    <pre class="highlight">&lt;login&gt;@&lt;site&gt;:~/iot-lab/parts/contiki$ cd examples/iotlab/03-sensors-collecting/
    &lt;login&gt;@&lt;site&gt;:~/iot-lab/parts/contiki/examples/iotlab/03-sensors-collecting$ <strong>cat README.md
    </strong>&lt;login&gt;@&lt;site&gt;:~/iot-lab/parts/contiki/examples/iotlab/03-sensors-collecting$ <strong>cat sensors-collecting.c</strong></pre>

4.  Compile the example.

    <pre class="highlight"># M3 nodes target
    &lt;login&gt;@&lt;site&gt;:~/iot-lab/parts/contiki/examples/iotlab/03-sensors-collecting$ <b>make TARGET=iotlab-m3</b>
    # A8-M3 nodes target
    &lt;login&gt;@&lt;site&gt;:~/iot-lab/parts/contiki/examples/iotlab/03-sensors-collecting$ <b>make TARGET=iotlab-a8-m3</b>
    &lt;login&gt;@&lt;site&gt;:~/iot-lab/parts/contiki/examples/iotlab/03-sensors-collecting$ ls
    ...  <strong>sensors-collecting.iotlab-m3 sensors-collecting.iotlab-a8-m3</strong> ...</pre>

5.  Submit an experiment with one M3 node associated with this firmware, with the Web Portal, or with this CLI tool command:

    <pre class="highlight">iotlab-experiment submit -n contiki -d 15 -l 1,archi=m3:at86rf231+site=grenoble+mobile=0,sensors-collecting.iotlab-m3</pre>

6.  Once it's running, connect to the serial link output to read sensors values:

    <pre class="highlight">
    user@local:~$ ssh &lt;login&gt;@grenoble.iot-lab.info
    &lt;login&gt;@grenoble:~$ nc m3-1 20000
    </pre>
