---
title: CLI
group: tools
description: IoT-LAB testbed provides a REST API client in the form of command-line tools. Indeed you should easily perform the main testbed features and it’s a good way to automate and script your experiments.
---

## Installation

The best way to install the CLI tools on your computer is to use pip

``` bash
$ pip install --user iotlabcli
```

> We remind you that it's not mandatory to install them on your computer as they are installed by default on all IoT-LAB SSH fronted servers.

## Commands

You can find one command for each main testbed features:

* **[iotlab-auth](#auth-command)**: credentials storage
* **[iotlab-status](#status-command)**: manage testbed status informations
* **[iotlab-experiment](#experiment-command)**: manage experiment lifecycle
* **[iotlab-node](#node-command)**: manage nodes interaction like power supply management or flashing firmware
* **[iotlab-profile](#profile-command)**: manage power consumption and radio monitoring profiles

We highly recommend you to follow the [getting started tutorial](/tutorials/getting-started/cli-tools/)

### Auth command

If you don't want to specify your credentials everytime you launch a command (login/password) you can store your credentials only once.

``` bash
$ iotlab-auth -u <login>
```

Don't forget that you must repeat this step from each computer or IoT-LAB SSH frontend where you will use CLI tools.

You can also add a SSH key to your account with the following command:
```bash
iotlab-auth --add-ssh-key
```

It will use `~/.ssh/id_rsa.pub` as default, but you can specify the identity file to use with the `-i` option.

### Status command

##### Get testbed nodes list

``` bash
$ iotlab-status --nodes
{
    "items": [
        {
            "archi": "m3:at86rf231",
            "camera": 0,
            "mobile": 0,
            "mobility_type": " ",
            "network_address": "m3-1.grenoble.iot-lab.info",
            "site": "grenoble",
            "state": "Alive",
            "uid": "2354",
            "x": "20.10",
            "y": "26.76",
            "z": "-0.04"
        },
        ...
    ]
}
```

Filter by archi, site and state
``` bash
$ iotlab-status --nodes --archi m3 --site grenoble --state Alive
```

##### Get testbed sites

It gives a list of sites with available nodes sort by archi properties

``` bash
iotlab-status --sites
```

##### Get running experiments list

``` bash
iotlab-status --experiments-running
```

### Experiment command

##### Submit an experiment

When you submit an experiment you can choose between two modes, alias or physical submission. With alias mode your submission is based on a set of alias
nodes properties in the form of `<number>,<properties1+properties2>`. In this case, thanks to the IoT-LAB scheduler which allocate you automatically the nodes which corresponds to the properties and ensure you that they are in the same radio neighborhood.<br><br>
An example of experiment submission for a duration of 20 minutes with 10 M3 nodes on Grenoble site:<br><br>
``` bash
$ iotlab-experiment submit -n alias_example -d 20 -l 10,archi=m3:at86rf231+site=grenoble
{
    "id": 100000
}
```
You can note that when your submission is accepted the scheduler gives you an experiment id.<br><br>
For a physical submission you specify a set of nodes hostname in the form of `<site>,<archi>,<nodes_ids_list>`. We remind you that all IoT-LAB nodes hostname are in the form of `<archi>-<id>.<site>.iot-lab.info` whith as an example `m3-1.grenoble.iot-lab.info`.<br><br>
An example of experiment submission with 4 M3 nodes on Grenoble site (`m3-{1,2,3,10}.grenoble.iot-lab.info`):<br>

``` bash
$ iotlab-experiment submit -n physical_example -d 20 -l grenoble,m3,1-3+10
```
When you submit an experiment whitout specify a precise date the IoT-LAB scheduler tries to start your experiment as soon as possible (ASAP mode) and schedule automatically the experiment. It's also possible to manually schedule your experiment by specifying an epoch Linux date.<br>
``` bash
$ iotlab-experiment submit -n schedule_example -d 20 -l grenoble,m3,1-3+10 -r $(date +%s -d "1 Jan 2089 00:00:00 UTC")
```
Finally it's also possible to specify a firmware and monitoring profile association during an experiment submission. For each set of nodes you can specify it in the form of `<alias_or_physical_nodes>,<firmware_path>,<profile_name>`<br><br>
An example of experiment submission with 2 M3 nodes on Grenoble site with two different firmwares association:<br>
``` bash
$ iotlab-experiment submit -n firmware_example -d 20 -l grenoble,m3,1,firmware1.elf -l grenoble,m3,2,firmware2.elf
```
An example of experiment submission with 2 M3 nodes on Grenoble site with only one monitoring association<br>
``` bash
$ iotlab-experiment submit -n profile_example -d 20 -l 2,archi=m3:at86rf231+site=grenoble,,profile1
```

##### Wait for an experiment

When your experiment submission is accepted the scheduler will start the deployment. You have to wait until your experiment is ready with the state `Running`. We provide a command which is blocked pending good state<br><br>
``` bash
$ iotlab-experiment wait
Waiting that experiment <exp_id> gets in state Running
"Running"
$ iotlab-experiment wait -i <exp_id> # if you have several experiments running on the testbed
```

It can also happen that your experiment doesn't start immediately with ASAP mode. For example, if the nodes you request with a physical submission are not available because an experiment is running using these nodes, the scheduler will accept your submission and schedule it automatically at the end of this experiment. In this case the experiment will be in a `Waiting` state. It is therefore possible to add a timeout (eg. seconds) to the command in order not to wait indefinitely for your experiment to start. You can also use an option to cancel your experiment if the timeout is reached

``` bash
iotlab-experiment wait --timeout 30
iotlab-experiment wait --timeout 30 --cancel-on-timeout
```

##### Get experiment nodes list
``` bash
$ iotlab-experiment get -n
$ iotlab-experiment get -n -i <exp_id> # if you have several experiments running on the testbed
```

##### Get experiment nodes deployment result

Get an experiment nodes deployment result with `succes=0 and error=1`. It's important to check the result before interact with a node as it can be considered unusable in case of error return.<br><br>
``` bash
$ iotlab-experiment get -d
{
    "0": [
        "m3-1.grenoble.iot-lab.info"
    ],
    "1": [
        "m3-2.grenoble.iot-lab.info"
    ]
}
$ iotlab-experiment get -d -i <exp_id> # if you have several experiments running on the testbed
```

##### Stop experiment

``` bash
$ iotlab-experiment stop
$ iotlab-experiment stop -i <exp_id> # if you have several experiments running on the testbed
```

### Node command

##### Flash firmware

``` bash
$ iotlab-node --flash firmware.elf # flash the firmware on all nodes of the experiment
$ iotlab-node -i <exp_id> --flash firmware.elf # if you have several experiments running on the testbed
$ iotlab-node --flash firmware.elf -l grenoble,m3,1+10 # flash the firmware on the nodes m3-{1,10}.grenoble.iot-lab.info
$ iotlab-node --flash firmware.elf -e grenoble,m3,1 # flash the firmware on all nodes of the experiment except m3-1.grenoble.iot-lab.info
$ iotlab-node --flash-idle # flash an idle firmware (default testbed firmware)
```

##### Start/Stop/Reset

``` bash
$ iotlab-node --stop # stop all nodes of the experiment
$ iotlab-node --start -l grenoble,m3,1+10 # start nodes m3-{1,10}.grenoble.iot-lab.info
$ iotlab-node --reset -e grenoble,m3,1 # reset all nodes of the experiment except m3-1.grenoble.iot-lab.info
```

##### Debugger

``` bash
$ iotlab-node --debug-start # start the debugger on all nodes of the experiment
$ iotlab-node --debug-stop -l grenoble,m3,1+10 # stop the debugger on the nodes m3-{1,10}.grenoble.iot-lab.info
```

##### Update monitoring configuration

``` bash
$ iotlab-node --update-profile profile_name # update monitoring configuration on all nodes of the experiment
$ iotlab-node --update-profile profile_name -l grenoble,m3,1+10 # update monitoring configuration on the nodes m3-{1,10}.grenoble.iot-lab.info
$ iotlab-node --profile-reset # reset monitoring configuration on all nodes of the experiment
```

### Profile command

##### Get monitoring profiles list

``` bash
$ iotlab-profile get -l
```

##### Add monitoring profile

``` bash
$ iotlab-profile addm3 -n profile_consumption -p dc -current -voltage -cpower -period 8244 -avg 4 # monitoring power consumption
$ iotlab-profile addm3 -n profile_rssi -rssi -channels 11 12 -num 10 -rperiod 100 # monitoring radio RSSI
$ iotlab-profile addm3 -n profile_sniffer -sniffer -channels 11 # monitoring radio sniffer
```

##### Delete monitoring profile

``` bash
$ iotlab-profile del -n profile_name
```
