---
title: SSH-CLI
group: tools
description: IoT-LAB testbed provides a SSH command-line tools to interact with embedded Linux nodes as A8 nodes. Indeed when you submit an experiment we boot nodes with a Linux image and they are reachable by SSH only from the frontend server of the site (ipv4 private network). When you launch commands from your computer you are transparently connecting to the nodes through the SSH frontend as a gateway server.
--- 

## Installation

The best way to install the SSH-CLI tools on your computer is to use pip

``` bash
$ pip install --user iotlabsshcli
```

> We remind you that it's not mandatory to install them on your computer as they are installed by default on all IoT-LAB SSH fronted servers.

## Requirement

 You must verify that your SSH public key used by command-line tools has been recorded in your IoT-LAB user profile. You can find how to configure your IoT-LAB SSH access in the following [getting started documentation](/docs/getting-started/ssh-access/)

 Don't forget that if you launch commands directly from the SSH frontend server you must also add your public ssh key of your home directory (internal auto-generated key readable with `<login>@<site>:~$ cat ~/.ssh/id_rsa.pub`). Moreover you have a different public ssh key for each SSH frontend servers.
 
## Commands

### Boot wait

When you submit an experiment with embedded Linux nodes they won't be directly available by SSH even if the experiment state is `Running`. Indeed the experiment is ready as soon as we have started (power supply on) all the experiment nodes. You could wait for a full boot with the following command

``` bash
$ iotlab-ssh wait-for-boot # wait boot of all experiment nodes
$ iotlab-ssh --verbose wait-for-boot # show verbose output
$ iotlab-ssh wait-for-boot --max-wait 60 # maximum waiting time in seconds (120 by default)
$ iotlab-ssh wait-for-boot -l saclay,a8,1 # wait for a8-1.saclay.iot-lab.info
$ iotlab-ssh wait-for-boot -e saclay,a8,1 # wait for all experiment nodes except a8-1.saclay.iot-lab.info
```

### Flash firmware on the A8-M3 node

The A8 node embeds a M3 node that we name [A8-M3](/docs/boards/iot-lab-a8-m3). It gives access to sensors and radio communication with standalone M3 nodes.

``` bash
$ iotlab-ssh flash-m3 <firmware.elf> -l saclay,a8,2-3+5-7+9-10
{
    "flash-m3": {
        "0": [
            "node-a8-2.saclay.iot-lab.info",
            "node-a8-3.saclay.iot-lab.info",
            "node-a8-5.saclay.iot-lab.info",
            "node-a8-6.saclay.iot-lab.info",
            "node-a8-7.saclay.iot-lab.info",
            "node-a8-9.saclay.iot-lab.info",
            "node-a8-10.saclay.iot-lab.info"
        ]
    }
}
```

### Reset the A8-M3 node

``` bash
$ iotlab-ssh reset-m3 -l saclay,a8,2
{
    "reset-m3": {
        "0": [
            "node-a8-2.saclay.iot-lab.info"
        ]
    }
}
```

### Run a command

``` bash
$ iotlab-ssh --verbose run-cmd "uname -a" -l saclay,a8,2-3
Connecting via SSH proxy saclay.iot-lab.info:22 -> node-a8-2.saclay.iot-lab.info:22
[node-a8-2.saclay.iot-lab.info]     Linux node-a8-2 3.18.5-iotlab+ #9 Thu Sep 1 16:17:22 CEST 2016 armv7l GNU/Linux
[node-a8-3.saclay.iot-lab.info]     Linux node-a8-3 3.18.5-iotlab+ #9 Thu Sep 1 16:17:22 CEST 2016 armv7l GNU/Linux
{
    "run-cmd": {
        "0": [
            "node-a8-2.saclay.iot-lab.info",
            "node-a8-3.saclay.iot-lab.info"
        ]
    }
}
```

It's also possible to run command on frontend server

``` bash
$ iotlab-ssh --verbose run-cmd "uname -a" --frontend
[saclay.iot-lab.info]       Linux saclay 3.16.0-4-amd64 #1 SMP Debian 3.16.36-1+deb8u1 (2016-09-03) x86_64 GNU/Linux
{
    "run-cmd": {
        "0": [
            "saclay.iot-lab.info"
        ]
    }
}
```

### Copy file on frontend ~/shared/.iotlabsshcli directory

The `shared` directory on the frontend is mounted by A8 nodes during experiment. It's a simple way to access permanent files from the nodes without copy them. Indeed between two experiments the Linux image filesystem of the node is removed and rebuild from scratch.

``` bash 
$ iotlab-ssh copy-file test.tar.gz
{
    "run-cmd": {
        "0": [
            "saclay.iot-lab.info"
        ]
    }
}
```

### Run script

A screen session is launched on the node to run the script in background mode. When the script ends, the screen session is terminated.

``` bash
$ iotlab-ssh run-script /tmp/test.sh -l saclay,a8,2
{
    "run-script": {
        "0": [
            "node-a8-2.saclay.iot-lab.info"
        ]
    }
}

root@node-a8-2:~# screen -ls
There is a screen on:
       1877.<login>-<exp_id>   (Detached)
1 Socket in /tmp/screens/S-root.
```


Similar to run command you can pass the `--frontend` option if you want to launch the script on the frontend server.
