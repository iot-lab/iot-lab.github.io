---
title: Websocket client
group: tools
description: The websocket client is a powerful tool to aggregate serial port (UART) of all your experiment nodes even from different sites. This client automatically connects to the websocket server of each site and gather all connections in one call. Each websocket server connects to the devices of its site.
---

## Restrictions

Like the usual serial redirection on the TCP:20000, it's not possible to connect
to a given device if a TCP connection on port 20000 is already opened (with
`nc` for example).
The websocket client can have up to **2 connections opened on the same device**
at a time : these 2 connections are multiplexed on top of the single TCP
connection.

Due to performance reasons, it is not possible to have more than
**15 opened connections at a time**.

The bandwidth per serial port is also **limited to 115200 bauds**.

## Installation

The `iotlab-ws` command line is part of the
[iotlabwscli Python package](https://pypi.org/project/iotlabwscli/). You can
install it using pip:

```bash
$ pip install --user iotlabwscli
```

## Play with the websocket client

#### 1. Launch an experiment

To illustrate the websocket client features we will launch an experiment with:

* a duration of 30 minutes
* three M3 nodes on Saclay site
* a firmware with an interactive shell on the serial port

**Using the webportal**

In the Webortal go to the
[New Experiment](https://www.iot-lab.info/testbed/experiment) page and select nodes by `node properties` and attach the preset firmware (iotlab_m3_tutorial).

**Using the command-line tools**

With command-line tools run the following commands:

``` bash
$ wget https://iot-lab.github.io/www/assets/firmwares/docs/monitoring/tutorial_m3.elf
$ iotlab-auth -u <login> # optionally store your credentials if you haven't done it before.
$ iotlab-experiment submit -d 20 -l 3,archi=m3:at86rf231+site=saclay,tutorial_m3.elf
$ iotlab-experiment wait
$ iotlab-experiment get -ni
```

#### 2. The iotlab-ws command

By default simply run `iotlab-ws` to connect to all devices in your experiment:

``` bash
$ iotlab-ws
Connected to m3-10.saclay
Connected to m3-12.saclay
Connected to m3-11.saclay
m3-12.saclay: 
m3-12.saclay: 
m3-12.saclay: IoT-LAB Simple Demo program
m3-12.saclay: Type command
m3-12.saclay: 	h:	print this help
m3-12.saclay: 	t:	temperature measure
m3-12.saclay: 	l:	luminosity measure
m3-12.saclay: 	p:	pressure measure
m3-12.saclay: 	u:	print node uid
m3-12.saclay: 	d:	read current date using control_node
m3-12.saclay: 	s:	send a radio packet
m3-12.saclay: 	b:	send a big radio packet
m3-12.saclay: 	e:	toggle leds blinking
m3-12.saclay: 
m3-12.saclay:  Type Enter to stop printing this help
....
```

**Note:** Hit "h" to stop the flood and print the help menu.


When you use the `Space+Enter` combination you write `Space+newline` on the
serial port of **all nodes in the experiment**. You can find below a summary of
how to write on the serial port with `serial_aggregator` command.

<table class="table table-striped">
    <thead>
        <tr>
            <td><b>String</b></td>
            <td><b>Send</b></td>
        </tr>
    </thead>
    <tbody>
    <tr>
        <td>'msg'</td>
        <td>'msg\n'  to all nodes</td>
    </tr>
    <tr>
        <td>'saclay,m3,1-3+5;msg'</td>
        <td>'msg\n' to nodes m3-1, m3-2, m3-3 and m3-5 on Saclay site</td>
    </tr>
    <tr>
        <td>'saclay,m3,1;msg'</td>
        <td>'msg\n' to nodes m3-1 on Saclay site</td>
    </tr>
    </tbody>
</table>

For example, you can print the brightness measurement to all nodes by
entering 'l+Enter' and thus send 'l\n' to the serial port of all nodes :

``` bash
l
m3-<id1>.saclay;cmd > Luminosity measure: 4.8828125E-1 lux
m3-<id1>.saclay;
m3-<id2>.saclay;cmd > Luminosity measure: 4.8828125E-1 lux
m3-<id2>.saclay;
```

Send a radio packet from only one device and verify the good reception on the
other devices. Type `saclay,m3,<id1>;s+Enter' to send `s\n` on the serial port
of `m3-<id1>.saclay`:

``` bash
saclay,m3,<id1>;s
m3-<id1>.saclay;cmd >
m3-<id1>.saclay;radio > Packet sent
m3-<id1>.saclay;
m3-<id2>.saclay;cmd >
m3-<id3>.saclay;cmd >
m3-<id2>.saclay;radio > Got packet from 9982. Len: 16 Rssi: -69: 'Hello World!: 1'
m3-<id2>.saclay;
m3-<id3>.saclay;radio > Got packet from 9982. Len: 16 Rssi: -69: 'Hello World!: 1'
m3-<id3>.saclay;
```

It's also possible to run iotlab-ws with some usual IoT-LAB command line tools
options:
- use `-i` to specify the experiment identifier:
  ```bash
  $ iotlab-ws -i <exp_id>
  ```
  This is useful if you have several experiments running on the testbed at the
  same time.
- use `-l` to specify the devices to connect to:
```bash
$ iotlab-ws -l saclay,m3,1-3 -l grenoble,m3,1-5 -l lille,m3,10
```

Finally it's important to remember that the serial port access is **exclusive**
and thus it's possible to connect `iotlab-ws` to a device if the `nc` command
is already connected to the serial redirection of the device.
In this case, you will obtain this message:

``` bash
$ nc m3-<id> 20000
Connected to m3-<id>.saclay
Disconnected from m3-<id>.saclay: Cannot connect to node m3-<id>
0
```
