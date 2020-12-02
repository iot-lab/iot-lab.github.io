---
title: MQTT
group: tools
description: This document shows how to exchange simple messages using the MQTT broker deployed in IoT-LAB and the mosquitto CLI clients installed on the SSH frontends. In this document, you will learn how to connect to the broker and then, you will subscribe to an MQTT topic and publish messages to an MQTT topic.
---

## Introduction

MQTT (MQ Telemetry Transport) is a protocol designed on top of TCP/IP and based
on a publish/subscribe principle.


<figure style="text-align:center">
  <img src="{{ '/assets/images/docs/mqtt/' | relative_url}}pub-sub-model.png" style="width:500px;"/><br/>
  <figcaption>The MQTT publish subscribe model (<a href="https://www.researchgate.net/publication/327661439_The_Addition_of_Geolocation_to_Sensor_Networks">Source</a>)</figcaption>
</figure>

Each entity of a network is connected to a central broker and can either
subscribe to topics or publish to topics. When an entity publish a message to a
given topic, all subscribers of this topic receives the message. Topics use a
path likescheme.

The [Eclipse mosquitto project](https://mosquitto.org/) provide an open-source
MQTT broker as well as a C library for implementing clients and the
`mosquitto_pub` and `mosquitto_sub` command line interface clients.

The FIT IoT-LAB testbed provides an instance of the Eclipse mosquitto broker
at **mqtt.iot-lab.info**. This instance is public and only
**port 8883 with TLS encryption** can be used.

## Connect to the IoT-LAB MQTT broker

**Important things:**

> Any FIT IoT-LAB user can connect to mqtt.iot-lab.info with its personal
> FIT IoT-LAB credentials and a certificate file that is available either here
> or on each SSH frontend in /opt/iot-lab-ca.pem.
> Authenticated FIT IoT-LAB users can only have access to `iotlab/<login>`
> topics and sub-topics. This ensures confidentiality between users when
> exchanging MQTT messages. Only TLS encryption on port 8883 is allowed on the
> broker.

### From your local computer

1. Download and install the mosquitto-clients by following the installation
  procedure. For example, on Debian-like Linux distributions, you can use
  `apt-get` as follows:
  ```sh
  $ sudo apt-get install mosquitto-clients
  ```
  Ensure the version installed is not too old. Versions >= 1.4.15 are known to work.
  ```sh
  $ mosquitto_sub -help
  mosquitto_sub is a simple mqtt client that will subscribe to a single topic and print all messages it receives.
  mosquitto_sub version 1.4.15 running on libmosquitto 1.4.15.
  ...
  ```

2. Download the certificate file from [here]({{ site.baseurl }}{% link assets/misc/docs/mqtt/iot-lab-ca.pem %}).

3. Connect to the broker using one of the mosquitto-clients command line:
  ```sh
  $ mosquitto_sub --cafile <path-to>/iot-lab-ca.pem -h mqtt.iot-lab.info -p 8883 -u <iotlab-login> -P <iotlab-passwd> -t iotlab/<io
  ```

### From an SSH frontend


1. Connect to the Saclay frontend SSH
  ```sh
  $ ssh <login>@saclay.iot-lab.info
  ```

2. The SSH frontend is shared with other users: every users can see the command
  being executed using ps on the frontend. To avoid security issues, it’s not
  recommented to not provide your credentials on the command line and hopefully
  mosquitto clients provide a file based authentication mecanism,
  using `~/.config/mosquitto_pub` and `~/.config/mosquitto_sub`.
  Create these 2 files and put the following content (replace `<iotlab-login>`
  and `<iotlab-password>` with your personal IoT-LAB credentials):
  ```
    -u <iotlab-login>
    -P <iotlab-password>
  ```
  Make sure the file access rights are correct:
  ```sh
  login@saclay:~$ chmod 600 ~/.config/mosquitto_pub ~/.config/mosquitto_sub
  ```
  To encrypt the communication with the broker, the certificate file is located
  in `/opt/iot-lab-ca.pem`.

3. Connect to the broker using one of the mosquitto-clients command line:
  ```sh
  login@saclay:~$ mosquitto_sub --cafile /opt/iot-lab-ca.pem -h mqtt.iot-lab.info -p 8883 -t iotlab/<iotlab-login>/test
  ```
  **Note:** you don’t need to provide your credentials on the command line
  because they are retrieved from the config files you previously edited.


#### Troubleshooting

If the `mosquitto_pub` or `mosquitto_sub` commands return the message
`Error: Problem setting TLS options`, it’s likely because your ca file cannot
be found or is invalid. In this case, verify that the path to `iot-lab-ca.pem`
is correct in the `--cafile` option.


If the `mosquitto_pub` or `mosquitto_sub` commands periodically prints the
message `Connection Refused: not authorised`, it’s likely because your
credentials are invalid. In this case, verify if your login (`-u` option) and
password (`-P` option) are correct either in
`~/.config/mosquitto_pub`/`~/.config/mosquitto_sub` files or in the command
line (only use the latter from your local computer).

### Exchange MQTT messages

In this last section, we provide several examples of commands for exchanging
MQTT messages between the Saclay SSH frontend and your local computer.

1. From your local computer, run `mosquitto_sub` to subscribe to the
`iotlab/<iotlab-login>/test` topic:
  ```
  $ mosquitto_sub --cafile <path-to>/iot-lab-ca.pem -h mqtt.iot-lab.info -p 8883 -u <iotlab-login> -P <iotlab-passwd> -t iotlab/<iotlab-login>/test
  ```
  The command is now waiting for any messages published on the
  `iotlab/<iotlab-login>/test` topic. **Keep it open**
  **Note:** this can also be done from any FIT IoT-LAB SSH frontend
  (without `-u` and `-P` options from the command line but using the configuration
  files instead, as seen previously in section 2.2).

2. Open another terminal and connect again to the Saclay SSH frontend. Then
  publish messages to the `iotlab/<iotlab-login>/test` topic using
  `mosquitto_pub`:
  - Send one message at a time:
    ```
    login@saclay:~$ mosquitto_pub --cafile /opt/iot-lab-ca.pem -h mqtt.iot-lab.info -p 8883 -t iotlab/<iotlab-login>/test -m "Hello FIT IoT-LAB"
    ```
    You should see the message arrive in the `mosquitto_sub` command running on your local computer.
  - Run `mosquitto_pub` in interactive mode using the `-l` option:
    ```
    login@saclay:~$ mosquitto_pub --cafile /opt/iot-lab-ca.pem -h mqtt.iot-lab.info -p 8883 -t iotlab/<iotlab-login>/test -l
    Hello FIT IoT-LAB
    ```
    All messages typed in the terminal are sent after pressing Enter to the
    `mosquitto_sub` command running on your local computer.
