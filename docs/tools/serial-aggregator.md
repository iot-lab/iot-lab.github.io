---
title: Serial aggregator
group: tools
description: The serial aggregator is a great tool to aggregate serial port (UART) of your experiment nodes. Indeed during an experiment with embedded nodes like M3 nodes you have a direct access to the serial port communication (Read/Write).It's forward by the IoT-LAB node on the SSH frontend server with a TCP socket on port 20000. When you launch a large-scale experiment it would be boring to open a terminal for each node and read the serial port. We provide you a tool which allow to aggregate multiple serial communication channels at once. Thanks to the asynchore python library which provide an asynchronous socket handler.
---

## Play with serial aggregator

### Launch an experiment

To illustrate the serial aggregator features we will launch an experiment with:

* a duration of 30 minutes
* three M3 nodes on Grenoble site
* a firmware with an interactive shell on the serial port

In the Webortal go to the [New Experiment](https://www.iot-lab.info/testbed/experiment) page and select nodes by `node properties` and attach the preset firmware (iotlab_m3_tutorial).

With command-line tools use these commands:

``` bash
$ wget {{ site.url }}{{ '/assets/firmwares/tutorial_m3.elf' | relative_url}} .
$ iotlab-auth -u <login> # optionally store your credentials if you haven't done it before.
$ iotlab-experiment submit -d 20 -l 3,archi=m3:at86rf231+site=grenoble,tutorial_m3.elf
$ iotlab-experiment wait
$ iotlab-experiment get -ni
```
### Use serial_aggregator command

Go to the frontend SSH server and launch the command

``` bash
$ ssh <login>@grenoble.iot-lab.info
<login>@grenoble:~$ serial_aggregator
1578319670.958905;Aggregator started
1578319671.676831;m3-101;
1578319671.677245;m3-101;
1578319671.678689;m3-101;IoT-LAB Simple Demo program
1578319671.679006;m3-101;Type command
1578319671.679342;m3-101;	h:	print this help
1578319671.679809;m3-101;	t:	temperature measure
1578319671.680298;m3-101;	l:	luminosity measure
1578319671.680771;m3-101;	p:	pressure measure
1578319671.681240;m3-101;	u:	print node uid
1578319671.681808;m3-101;	d:	read current date using control_node
1578319671.682343;m3-101;	s:	send a radio packet
1578319671.683018;m3-101;	b:	send a big radio packet
1578319671.683550;m3-101;	e:	toggle leds blinking
1578319671.684224;m3-101;
1578319671.684672;m3-101; Type Enter to stop printing this help
1578319671.685064;m3-101;
....
# Hit "Space+Enter" to stop the flood.
```

When you use the `Space+Enter` combination you write `Space+newline` on the serial port of all nodes. You can find below a summary of how to write on the serial port with `serial_aggregator` command.

<table class="table table-striped">
    <thead>
        <tr>
            <td><b>String</b></td>
            <td><b>Send</b></td>
        </tr>
    </thead>
    <tbody>
    <tr>
        <td>'' (empty string)</td>
        <td>nothing to anyone, allows 'blanking' lines</td>
    </tr>
    <tr>
        <td>' ' (space)</td>
        <td>' \n'  to all nodes</td>
    </tr>
    <tr>
        <td>'msg'</td>
        <td>'msg\n'  to all nodes</td>
    </tr>
    <tr>
        <td>'m3,1-3+5;msg'</td>
        <td>'msg\n' to nodes m3-1, m3-2, m3-3 and m3-5</td>
    </tr>
    <tr>
        <td>'m3-1;msg'</td>
        <td>'msg\n' to nodes m3-1</td>
    </tr>
    <tr>
        <td>'csv;msg;with;semicolons'</td>
        <td>'csv;msg;with;semicolons\n'  to all nodes as 'csv;' is not a valid node identifier</td>
    </tr>
    </tbody>
</table>

Send print the brightness measurement to all nodes

``` bash
# Type 'l+Enter' to send 'l\n' to all nodes serial port
l
1417707771.347801;m3-<id1>;cmd > Luminosity measure: 4.8828125E-1 lux
1417707771.347801;m3-<id1>;
1417707771.347844;m3-<id2>;cmd > Luminosity measure: 4.8828125E-1 lux
1417707771.347941;m3-<id2>;
```

Send a radio packet from only one node and verify the good reception on the other node

``` bash
# Type 'm3-<id1>;s+Enter' to send 's\n' on m3-<id1> serial port
 m3-<id1>;s
1417708038.478605;m3-<id1>;cmd >
1417708038.478860;m3-<id1>;radio > Packet sent
1417708038.480531;m3-<id2>;cmd >
1417708038.480865;m3-<id2>;radio > Got packet from 9982. Len: 16 Rssi: -69: 'Hello World!: 1'
1417708038.480962;m3-<id2>;
```

It's also possible to launch serial_aggregator command with options

``` bash
<login>@grenoble:~$ serial_aggregator -h
<login>@grenoble:~$ serial_aggregator -i <exp_id>         # in case of several experiments running on the testbed
<login>@grenoble:~$ serial_aggregator -l grenoble,m3,1-4  # filter nodes with only m3-{1,2,3,4}
```

Finally it's important to understand that the serial port access is **exclusive** and you cannot use `serial_aggregator` command in the same time of `nc` command or IoT-LAB Websocket client for example. You will obtain an error

``` bash
<login>@grenoble:~$ nc m3-<id> 20000
m3-<id>.grenoble.iot-lab.info [172.16.10.100] 20000 (?) : Connection refused
```

## Advanced usage


### Run serial aggregator with Linux nodes and embed co-microcontroller

As a prerequisite you should consult this [tutorial]({{ site.baseurl }}{% link learn/tutorials/getting-started/linux-cli-tools.md %}) to learn how to run an experiment with Linux nodes. It is possible to forward the serial port (i.e. UART) of the co-microcontroller with a TCP socket on port 20000. To do this an initd script is provided on the Linux nodes which uses the socat command.

``` bash
$ ssh <login>@grenoble.iot-lab.info
<login>@grenoble:~$ ssh root@node-a8-1
root@node-a8-1:~# /etc/init.d/serial_redirection start
Starting serial_redirection: 0
```
Then you can use serial_aggregator with a Linux node like a standard microcontroller by specifying the following option


``` bash
<login>@grenoble:~$ serial_aggregator --with-a8
```

### Run serial aggregator on your computer

You can run the serial_aggregator directly from your computer using ssh tunnel. The input and output will be directly available on your computer.

``` bash
my_computer$ ssh <login>@grenoble.iot-lab.info "serial_aggregator -i <exp_id>"
```

Moreover with `socat`, you can easily wrap it in a tcp socket:

``` bash
my_computer$ socat tcp-listen:20000,fork,reuseaddr exec:'ssh <login>@grenoble.iot-lab.info "serial_aggregator -i <exp_id>"'
```

And then connect to it

``` bash
my_computer$ nc localhost 20000
p  # type 'p+Enter'
1417708815.199245;m3-7;Pressure measure: 9.845237E2 mabar
1417708815.199423;m3-7;
1417708815.199607;m3-6;Pressure measure: 9.848386E2 mabar
1417708815.199768;m3-6;
...
```

Every time you connect and disconnect, the serial_aggregator program will start and stop, so the connections will take a few seconds to get ready.

### Use Serial aggregator as a Python library

It's very easy to write a Python script that uses the serial aggregator tool as a library. Below you can find an example of Python script that runs Serial aggregator on all nodes (with tutorial firmware) of the current experiment and displays the output that is written to the serial ports with the temperature command. As the serial links are accessible on the frontend SSH you need to create and launch this script on your home directory.

```bash
$ ssh <login>@grenoble.iot-lab.info
# edit and copy the content of the script
<login>@grenoble:~$ vi serial_lib.py
<login>@grenoble:~$ python serial_lib.py
1589473705.352797;Aggregator started
m3-13: Chip temperature measure: 3.6552082E1
m3-11: Chip temperature measure: 3.8052082E1
m3-10: Chip temperature measure: 3.7220833E1
m3-10: Chip temperature measure: 3.7220833E1
m3-11: Chip temperature measure: 3.809375E1
# you can filter the nodes list serial links
<login>@grenoble:~$ python serial_lib.py -l grenoble,m3,<list_ids>
...
```

***Python script:***


```python
#!/usr/bin/env python

from __future__ import print_function
import argparse
import time
import iotlabaggregator.common
from iotlabaggregator.serial import SerialAggregator


def read_line(identifier, line):
    print("{}: {}".format(identifier, line))


def main():
    """ Launch serial aggregator.
    """
    parser = argparse.ArgumentParser()
    iotlabaggregator.common.add_nodes_selection_parser(parser)
    opts = parser.parse_args()
    opts.with_a8 = False # redirect a8-m3 serial port
    nodes = SerialAggregator.select_nodes(opts)
    with SerialAggregator(nodes, line_handler=read_line) as aggregator:
        while True:
            try:
                # send 't' on all serial links
                # if you want to specify a list of nodes use
                # aggregator.send_nodes([m3-<id1>, m3-<id2>], 't')
                aggregator.broadcast("t")
                time.sleep(2)
            except KeyboardInterrupt:
                print("Interrupted by user ...")
                break


if __name__ == "__main__":
    main()
```
