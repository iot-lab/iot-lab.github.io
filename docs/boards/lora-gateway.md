---
board: LoRa gateway
group: boards
---

## Description

The LoRa gateway device in IoT-LAB is built from the combination of a
[Raspberry 3 model b](https://www.raspberrypi.org/products/raspberry-pi-3-model-b/)
and an [ic880a LoRa concentrator](https://wireless-solutions.de/products/lora/radio-modules/ic880a-spi/).

<div style="text-align:center">
<img src="{{ '/assets/images/docs/boards/lora-gw/' | relative_url}}lora-gw.png" style="width:500px;"/>
</div>

It provides the possibility to receive and send raw LoRaWAN messages, i.e
encrypted with the AES network and application session keys of a LoRaWAN
application.

## Software

The software stack that is controlling the gateway is composed of:
- the LoRa-net [packer forwarder](https://github.com/Lora-net/packet_forwarder)
  and [lora gateway SPI driver](https://github.com/Lora-net/lora_gateway)
- the [chirpstack gateway bridge](https://www.chirpstack.io/gateway-bridge/overview/)
- the [Eclipse mosquitto MQTT broker](https://mosquitto.org/)

All these software components are running together on the gateway within the
IoT-LAB [Yocto Embedded Linux image](https://github.com/iot-lab/iot-lab-yocto):
- the packet forwarder is packaged using [this recipe](https://github.com/iot-lab/iot-lab-yocto/blob/master/meta-iotlab/recipes-support/lora-packet-forwarder/lora-packet-forwarder_4.0.1.bb)
- the lora gateway driver is packaged using [this recipe](https://github.com/iot-lab/iot-lab-yocto/blob/master/meta-iotlab/recipes-support/lora-gateway/lora-gateway_5.0.1.bb)
- the chirpstack gateway bridge is packaged using [this recipe](https://github.com/iot-lab/iot-lab-yocto/blob/master/meta-iotlab/recipes-support/lora-gateway-bridge/lora-gateway-bridge_2.6.0.bb)
- the Eclipse mosquitto broker is packaged using [this recipe](https://github.com/iot-lab/iot-lab-yocto/blob/master/meta-iotlab/recipes-connectivity/mosquitto/mosquitto.inc)

## IoT-LAB configuration

Users can control the gateway using the MQTT protocol on port 1883 from SSH
frontend.

There is no authentication required to connect to the MQTT broker
running on the gateway, indeed, the IoT-LAB infrastructure add network
filtering rules so only the user of the experiment can access to port 1883 of
the gateway.

MQTT topics follows the chipstack gateway bridge API:
- uplink topic is `gateway/<gateway identifier>/rx`
- downlink topic is `gateway/<gateway identifier>/tx`
- stats topic is `gateway/<gateway identifier>/stats`
- ack topic template is `gateway/<gateway identifier>/ack`
- config topic template is `gateway/<gateway identifier>/config`

The `gateway identifier` corresponds to the name of the lora gateway device,
for example `lora-gw-1`.

## Example of usage

Submit an experiment as usual, for example by using the IoT-LAB command line
tools:

```bash
$ iotlab-experiment submit -d 120 -l 1,site=saclay+archi=lora-gw:sx1301
$ iotlab-experiment wait
```

Once the experiment, use the `mosquitto_sub` command from the Saclay SSH
frontend to subscribe to the `gateway/lora-gw-1/rx` topic and retrieve all
LoRaWAN messages received by the gateway:

```
$ ssh <login>@saclay.iot-lab.info
<login>@saclay:~$ mosquitto_sub -h lora-gw-1 -t gateway/lora-gw-1/rx
{"rxInfo":{"mac":"b827ebfffec6b1f4","timestamp":429511027,"frequency":868100000,"channel":0,"rfChain":1,"crcStatus":1,"codeRate":"4/5","rssi":-51,"loRaSNR":10,"size":23,"dataRate":{"modulation":"LORA","spreadFactor":7,"bandwidth":125},"board":0,"antenna":0},"phyPayload":"AC+wANB+1bNwXIj0n4QiqwA8LfdqBkY="}
```

Each message is json string containing basic radio information. The encrypted
payload is in the field `phyPayload`.
