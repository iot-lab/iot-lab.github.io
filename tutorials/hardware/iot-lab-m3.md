---
title: IoT-LAB M3
group: hardware
description: Submit an experiment with IoT-LAB M3 boards using the CLI tools.
---

![][25] **Difficulty**: Easy

![][26] **Duration**: 20 minutes

_**Prerequisites**: [Configure SSH Access](/tutorials/getting-started/ssh-access)_

_**Description**: The aim of this first tutorial is to discover the IoT-LAB testbed tools by creating and submitting your first experiment, and then interact with running nodes. You will book _onto the ssh frontend with CLI tools _two M3 nodes on the Grenoble site, set them up with a sample firmware file, and deploy it on them. Once deployed, you will interact with the firmware running on the nodes, read sensor values and send radio packets through a terminal._

![tuto_m3_clitools_exp][28]



1. Connect to the host of the site where you wish to run your experiment. In the example below, the Grenoble site is used.

    <pre>
my_computer$ <strong>ssh &lt;login&gt;@grenoble.iot-lab.info</strong></pre>

2. Download the M3 firmware that we use in this tutorial. (Or make your own)

        <login>@grenoble:**~**$ **wget https://raw.githubusercontent.com/wiki/iot-lab/iot-lab/firmwares/tutorial_m3.elf -O tutorial_m3.elf**
        --2017-06-30 16:03:17-- https://raw.githubusercontent.com/wiki/iot-lab/iot-lab/firmwares/tutorial_m3.elf
        Résolution de raw.githubusercontent.com (raw.githubusercontent.com)… 151.101.120.133
        Connexion à raw.githubusercontent.com (raw.githubusercontent.com)|151.101.120.133|:443… connecté.
        requête HTTP transmise, en attente de la réponse… 200 OK
        Taille : 141626 (138K) [application/octet-stream]
        Sauvegarde en : « tutorial_m3.elf »

        tutorial_m3.elf 100%[===============================>] 138,31K --.-KB/s ds 0,03s

        2017-06-30 16:03:17 (4,55 MB/s) — « tutorial_m3.elf » sauvegardé [141626/141626]


3. Start an experiment with 2 M3 nodes. First authenticate then submit your experiment. In the example below, you submit an experiment called “m3_exp” (-n m3_exp) for a duration of 60minutes (-d 60) on 2 nodes with architecture M3 on Grenoble site. The command returns the experiment Id. Remember it. It will be used in the commands shown below, `<exp_id>`.

        <login>@grenoble:~$ iotlab-auth -u
        <login>@grenoble:~$ iotlab-experiment submit -n m3_exp -d 60 -l 2,archi=m3:at86rf231+site=grenoble

4. Wait a moment until the experiment is launched (state is Running) and get the nodes list.

        <login>@grenoble:~$ iotlab-experiment get -i  -s
        <login>@grenoble:~$ iotlab-experiment get -i  -r
        <login>@grenoble:~$ iotlab-experiment wait
        <login>@grenoble:~$ iotlab-node --update tutorial_m3.elf

5. Interact with your M3 node. Provided firmwares offer an interaction menu via the serial port of the device. The serial port is available from the ssh frontend through a TCP socket on port 20000. You can use netcat for example, with `nc <device hostname> 20000`.

        <login>@grenoble:~$ nc m3- 20000

        IoT-LAB Simple Demo program
        Type command
            h:    print this help
            t:    temperature measure
            l:    luminosity measure
            p:    pressure measure
            u:    print node uid
            d:    read current date using control_node
            s:    send a radio packet
            b:    send a big radio packet
            e:    toggle leds blinking
        Type Enter to stop printing this help
        cmd >

6. Test some commands to get sensors measures (t, l, p)

        cmd > l
        Luminosity measure: 7.324219E-1 lux

7. Test packet sending
    * Open a second terminal to connect to the serial port of another node
    * Make one of the nodes send a radio packet:

            <login>@grenoble:~$ nc m3- 20000
            cmd > s
            cmd >
            radio > Packet sent

    * Check that the other node has received the radio packet:

            <login>@grenoble:~$ nc m3- 20000
            cmd >
            radio > Got packet from A569. Len: 16 Rssi: -66: 'Hello World!: 0'


<div class="alert alert-secondary" markdown="1">
### Go further

* Follow the [Nodes Serial Link Aggregation][29] tutorial to see how to interact easily with all your nodes
* Follow the command-line [Experiment CLI client ][30]and [Node CLI client][31] tutorials
</div>

<div class="alert alert-info" markdown="1">
### Practical Tips

* Get M3 UID(s) for Grenoble site
    * See documentation <a href="https://github.com/iot-lab/iot-lab/wiki/Getting-attributes-for-IoT-LAB-nodes" class="alert-link">here</a>
* Access M3 serial port directly from your computer
    * Open a SSH tunnel between your computer and the M3 node

                ssh -L 20000:m3-:20000 @grenoble.iot-lab.info

    * In another terminal, run `nc` locally as if you were on the ssh frontend.

                nc localhost 20000

</div>


[1]: https://www.iot-lab.info/wp-content/themes/alienship-1.2.5-child/templates/parts/fit-iotlab3.png
[2]: https://www.iot-lab.info/news/ "News"
[3]: https://www.iot-lab.info/what-is-iot-lab/ "Platform"
[4]: https://www.iot-lab.info/what-is-iot-lab/ "What is IoT-LAB?"
[5]: https://www.iot-lab.info/deployment/ "Deployment"
[6]: https://www.iot-lab.info/hardware/ "Hardware"
[7]: https://www.iot-lab.info/robots/ "Robots"
[8]: https://www.iot-lab.info/about-us/ "About us"
[9]: https://www.iot-lab.info/dev-center/ "Dev Center"
[10]: https://www.iot-lab.info/dev-center/ "Software Development"
[11]: https://www.iot-lab.info/tutorials/ "Tutorials"
[12]: https://www.iot-lab.info/operating-systems/ "Operating Systems"
[13]: https://www.iot-lab.info/libraries/ "Libraries"
[14]: https://www.iot-lab.info/drivers/ "Drivers"
[15]: http://api.iot-lab.info "REST API documentation"
[16]: https://www.iot-lab.info/community/ "Community"
[17]: https://www.iot-lab.info/community/ "Share your experience"
[18]: https://www.iot-lab.info/education/ "Education"
[19]: https://www.iot-lab.info/publications/ "Publications"
[20]: https://www.iot-lab.info/charter/ "Charter"
[21]: https://www.iot-lab.info/get_started/ "Get Started"
[22]: https://www.iot-lab.info/testbed/drawgantt "Testbed activity"
[23]: https://www.iot-lab.info/testbed/ "Login"
[24]: https://www.iot-lab.info/ "FIT/IoT-LAB"
[25]: https://www.iot-lab.info/wp-content/uploads/2014/02/difficulty.jpg
[26]: https://www.iot-lab.info/wp-content/uploads/2014/02/duration.jpg
[27]: https://www.iot-lab.info/tutorials/ssh-access "Configure your SSH access"
[28]: https://www.iot-lab.info/wp-content/uploads/2017/06/tuto_m3_clitools_exp.jpg
[29]: https://www.iot-lab.info/tutorials/serial-aggregator "Nodes serial link aggregation"
[30]: https://www.iot-lab.info/tutorials/iotlab-experimenttools-client "Experiment CLI client"
[31]: https://www.iot-lab.info/tutorials/iotlab-nodetools-client "Node CLI client"
[32]: https://github.com/iot-lab/iot-lab/wiki/Getting-attributes-for-IoT-LAB-nodes
