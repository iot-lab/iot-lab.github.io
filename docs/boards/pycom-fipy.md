---
board: Pycom FiPy
group: boards
---

[Pycom](https://pycom.io/) is an a complete ecosystem for easy IoT development.
The IoT-LAB testbed provides access to the
[Pycom Fipy development boards](https://docs.pycom.io/products/). These boards
can be programmed with [MicroPython](https://micropython.org/) and feature
several wireless technologies: WiFi, BLE, SigFox, NB-IoT and LoRa.

**Note:** it's not possible yet to use SigFox or NB-IoT because of missing
infrastructure and integration within the IoT-LAB testbed.

<div style="text-align:center">
<img src="{{ '/assets/images/docs/boards/pycom/' | relative_url}}fipy.jpg" style="width:300px;"/>
</div>

## Datasheet and documentation

You can find a lot of documentation on the
[Pycom website](https://docs.pycom.io/).

The Pycom FiPy is described in detail
[here](https://docs.pycom.io/datasheets/development/fipy/).

## IoT-LAB special configuration

IoT-LAB only provides access to the MicroPython REPL of the firmware
pre-installed on the boards via the usual serial redirection mechanism (use
`nc` on port `20000` from the SSH frontend).

It is not possible to reflash the MicroPython firmware running on the Pycom
Fipy boards.

Each Fipy board is plugged on the
[Pysense extension board](https://docs.pycom.io/datasheets/boards/pysense/)
which provides access to several sensors.

## Troubleshooting

Some the REPL doesn't respond after the experiment startup (e.g. no display of
`>>>` prompt when sending `Enter` on the serial port).
In this case, one way to recover the REPL is to perform a power cycle of the
board:

```bash
$ iotlab-node --stop
$ iotlab-node --start
```
