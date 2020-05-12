---
title: Radio characterization
group: tools
description: We provide a dedicated tool to run experiments on the testbed that can map out the radio connectivity of nodes between each other.
---

## Principle

All the nodes of an experiment are in receive mode (RX) at the start. Then each node, in turn, will pass in transmitter mode (TX) and send broadcast 802.15.4 raw packets with a time delay. Each node receiving the packets will record the good reception information with radio Received Signal Strength Indication (RSSI) and Link Quality indicator (LQI) values. This packet sending step will be performed for a given list of radio channels and transmission power.

We can summarize as follows:

```sh
for every channel:
    for every txpower:
        for every node:
            send_packets(nb_packets, packet_size, delay)
            collect_all_receiver_logs
            clear_all_receiver_logs
```

To perform the different step on the nodes (send packets, collect, clear) we use the serial port on which we send commands. Thanks to the
[serial aggregator](/docs/tools/serial-aggregator/) tool which allows us to aggregate all serial ports of nodes very easily. We also manage error detection when receiving packets (eg. CRC16 & Magic Number, ...)


## Firmware

The firmware that runs on the nodes is based on [RIOT OS](https://riot-os.org/) and used the [GNRC network stack](https://riot-os.org/api/group__net__gnrc.html) to send 802.15.4 packets. You can find the source code [here](https://github.com/iot-lab/iot-lab-radio/blob/master/iotlabradio/riot/radio-characterization/main.c). When a node sends packets the firmware builds each packet with a fixed header of 16 bytes as follows:


    0       7 8     15 16    23 24    31
    +--------+--------+--------+--------+
    | magic number (*)|   CRC value     |
    +--------+--------+--------+--------+
    |  len(node id)   |   node id       |
    +--------+--------+--------+--------+
    |  packet number  |   txpower       |
    +--------+--------+--------+--------+
    |  channel        |   packet size   |
    +--------+--------+--------+--------+
    \                                   \
    /        Each bytes is filled       /  0 or more bytes
    \    with packet number (padding)   \
    +-----------------------------------+

    (*) = 0xADCE

This firmware is originally based on the work of <a href="cedric.adjih@inria.fr">Cedric Adjih</a>:

- [Firmware](https://github.com/adjih/openlab/tree/radio-exp/devel/radio_test) source code
- [Paper](https://www.researchgate.net/publication/304285486_Lessons_Learned_from_Large-scale_Dense_IEEE802154_Connectivity_Traces) published at IEEE CASE 2015 conference


## Launch a characterization

The first step is to launch an experiment on IoT-LAB testbed and flash the firmware on nodes. The following example shows you how to book nodes
on Grenoble site that are automatically allocated by the scheduler. If you want specific nodes or topologies you will have to adapt it.
Another important point is that we use the serial aggregator tool to collect the data, so we need to run the radio setup on the IoT-LAB SSH frontend.

```sh
ssh <login>@grenoble.iot-lab.info
<login>@grenoble:~$ source /opt/riot.source (eg. compilation toolchain)
<login>@grenoble:~$ git clone --recursive https://github.com/iot-lab/iot-lab-radio
<login>@grenoble:~$ cd iot-lab-radio
<login>@grenoble:~$ make -C iotlabradio/riot/radio-characterization (eg. BOARD=iotlab-m3 in the Makefile)
<login>@grenoble:~$ cp iotlabradio/riot/radio-characterization/bin/iotlab-m3/radio-characterization.elf .
<login>@grenoble:~$ iotlab-experiment submit -d 60 -l 10,archi=m3:at86rf231+site=grenoble,radio-characterization.elf
<login>@grenoble:~$ iotlab-experiment wait
<login>@grenoble:~$ iotlab-radio
```

This setup is launched by default with following parameters:

- all channels: [11..26]
- all txpower: [-17, -12, -9, -7, -5, -4, -3, -2, -1, 0, 1, 2, 3]
- number of packets: 100
- packet size: 50 bytes
- delay: 1 ms

Of course you can modify this configuration with iotlab-radio command and choose another board when you compile the firmware.

Another point is the time needed to carry out a characterization in order to choose an experiment duration. By default we use a default timeout of 5 seconds (can be changed with command option) to wait for the good firmware execution of the commands (set channel, set txpower, send packets, show logs, clear logs). Only send packets command timeout (`default timeout + delay*0,001*nb_packets`) is blocking. Indeed it's an assumption on the time it takes for other nodes to receive the packets. For other commands all the nodes send an acknowledgement and we're checking the good reception (maybe less than timeout).

So you should estimate the maximum duration with this formula:

```sh
duration (seconds) = nb_channel*(timeout +
                                 nb_power*timeout +
                                 nb_power*nb_nodes*(3*timeout + delay*0,001*nb_packets))
```

## Radio logs data

At the end of each characterization we save log files as follows:

```sh
logs/<exp_id>/<%Y%m%d-%H%M%S>/config.json
logs/<exp_id>/<%Y%m%d-%H%M%S>/<channel>/<txpower>/<node_id>.json
```

Thus if you launch a setup with m3-1 and m3-2 on the Grenoble site for channel=[11, 12] and txpower=[-4, -3] you will obtain this tree structure on your filesystem:

```sh
.../11/-4/m3-1.json
.../11/-4/m3-2.json
.../11/-3/m3-1.json
.../11/-3/m3-2.json
.../12/-4/m3-1.json
.../12/-4/m3-2.json
...
```

In each JSON file you can find a list of all packets sended/received by a node during the radio characterization.

For example when one node send packets (for given channel and txpower values) we use this log format:


```
{"nb_error": 0, "node_id": "126", "power": -17, "channel": 11,  "nb_pkt": 100,
 "send": [{"pkt_num": 0, "pkt_send": 1}, {"pkt_num": 1, "pkt_send": 1}, ...]}
```

* **nb_error**: number of delivery failures
* **node_id**: sender node id
* **power**: radio transmission power
* **channel**: radio channel
* **nb_pkt**: number of packets sent
* **send**: sent packets list
  * **pkt_num**: packet number
  * **pkt_send**: 1=Success/0=Failure (*)
    
(*) Result of gnrc_netapi_send function of RIOT OS.

For one node which received packets (for given channel and txpower values) we use this log format:

```
{"nb_generic_error": 0, "nb_magic_error": 0, "nb_crc_error": 0, "nb_control_error": 0, "nb_pkt": 67, "node_id": "112", "power": -17, "channel": 11,
 "recv": [{"lqi": 255, "pkt_num": 0, "rssi": -91}, { "lqi": 244, "pkt_num": 1, "rssi": -91}, ...]}
```

* **nb_generic_error**: number of unknown packet error
* **nb_magic_error**: number of magic number packet error
* **nb_crc_error**:  number of corruption packet data error
* **nb_control_error**: number of control packet data error (**)
* **node_id**: sender node id (*)
* **power**: radio transmission power (*)
* **channel**: radio channel (*)
* **nb_pkt**: number of packets received
* **recv**: received packets list
  * **pkt_num**: packet number (*)
  * **rssi**: RSSI value
  * **lqi**: LQI value

(*) These values are extracted from packet data received

(**) Packet data values has been changed (eg. sender node id|packet size|channel|power)


## Parsing radio logs data

we provide a command to parse the radio logs obtained. You can run it as follows:

```
<login>@grenoble:~$ iotlab-radio-parse -p logs/<exp_id>/<%Y%m%d-%H%M%S>
```      

The parsing uses [Pandas Python library](https://pandas.pydata.org/) to generate three csv files in the logs directory. Feel free to use this library to analyze and plotting the parsing results.


* **recv-logs.csv**: all packets received (*) by nodes with the following format

  ```csv
  channel,power,rx_node,tx_node,pkt_num,rssi,lqi
  11,-3,11,14,0,-75,255
  11,-3,11,14,1,-75,255
  11,-3,11,14,2,0,0
  ...
  ```

  This is a total number (eg. theoretical) of packets received that you can calculate with this formula `(nb_channel*nb_power*nb_nodes*(nb_nodes-1)*nb_packet)`. You can find the packets that have not been received during radio characterization with LQI and RSSI values equal to 0.

* **send-logs.csv**: all packets sent by nodes with the following format

  ```csv
  channel,power,tx_node,pkt_num,pkt_send
  11,-3,11,0,1
  11,-3,11,1,1
  ...
  ```

  pkt_send = 0 in case of packet transmission error

* **error-logs.csv**: all packet reception errors

  ```csv
  channel,power,rx_node,tx_node,generic,magic_number,crc,control
  11,-3,11,14,0,0,0,0
  11,-3,11,15,0,0,0,0
  ...
  ```


