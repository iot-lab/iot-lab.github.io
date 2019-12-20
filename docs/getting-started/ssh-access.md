---
title: SSH access
group: getting-started
description: When you fill the IoT-LAB testbed signup form we ask you optionally to add your SSH public key. Indeed when you work on the testbed you will have to connect to the frontend servers or embedded Linux nodes by SSH. This documentation shows you how to configure manually your SSH access.
---

## Requirement

If you don't have a key you need to create one on your computer. You can run the following `ssh-keygen` command in a terminal which generates a key pairs for SSH. The SSH public key is the content of the `id_rsa.pub` file.
On windows computer you can use the [Puttygen](https://www.puttygen.com/) key generator tool.

```
you@yourpc:~$ ssh-keygen -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/home/you/.ssh/id_rsa):
Created directory '/home/you/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/you/.ssh/id_rsa.
Your public key has been saved in /home/you/.ssh/id_rsa.pub.
The key fingerprint is:
14:13:be:59:3c:ab:fa:df:78:8e:39:fc:72:9c:9e:7d you@yourpc
The key's randomart image is:
+--[ RSA 2048]----+
|        +.       |
|       . +       |
|        o +      |
|       . + o     |
|        S .      |
|         .       |
|        .. . .   |
|       .  +==o  E|
|      ....=O* .. |
+-----------------+

you@yourpc:~$ ls ~/.ssh/
id_rsa  id_rsa.pub
```

## Update your user account

Log into the [IoT-LAB Webportal](https://www.iot-lab.info/testbed/account). Then choose the SSH Keys tab and copy/paste your public key. Save it by clicking on `Update SSH Keys` button. You can also note that it's possible to have several keys for your account.

## Test your SSH access

Each IoT-LAB site has a SSH frontend reachable with the following address `<site>.iot-lab.info`. For example try to connect to the Grenoble frontend server:

```
ssh <login>@grenoble.iot-lab.info
```
