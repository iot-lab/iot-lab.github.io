---
title: SSH-CLI
group: tools
---

IoT-LAB testbed provides a SSH command-line tools to interact with embedded Linux nodes as Open A8 nodes. Indeed when you submit an experiment we boot nodes with a Linux image and they are reachable by SSH only from the frontend server of the site (ipv4 private network). When you launch commands from your computer you are transparently connecting to the nodes through the frontend SSH as a gateway server. 


#### Installation

The best way to install the SSH-CLI tools on your computer is to use pip

```$ pip install --user iotlabsshcli```

> We remind you that it's not mandatory to install them on your computer as they are installed by default on all IoT-LAB SSH fronted servers.

#### Requirement

 You must verify that your SSH public key used by command-line tools has been recorded in your IoT-LAB user profile. You can find how to configure your IoT-LAB SSH access in the following [getting started documentation](/docs/getting-started/ssh-access/)
 
 Don't forget that if you launch commands directly from the SSH frontend server you must also add your public ssh key of your home directory (internal auto-generated key readable with `<login>@<site>:~$ cat ~/.ssh/id_rsa.pub`). Moreover you have a different public ssh key for each SSH frontend servers.
 
#### Commands

##### Boot wait

When you submit an experiment with embedded Linux nodes they won't be directly available by SSH even if the experiment state is `Running`. Indeed the experiment is ready when we have started (power supply on) all the experiment nodes. You should wait for a full boot with the following command 

```
$ iotlab-ssh wait-for-boot # wait boot of all experiment nodes
$ iotlab-ssh --verbose wait-for-boot # show verbose output
$ iotlab-ssh wait-for-boot --max-wait 60 # maximum waiting time in seconds (120 by default)
$ iotlab-ssh wait-for-boot -l grenoble,a8,1 # wait for a8-1.grenoble.iot-lab.info 
$ iotlab-ssh wait-for-boot -e grenoble,a8,1 # wait for all experiment nodes except a8-1.grenoble.iot-lab.info 
```

