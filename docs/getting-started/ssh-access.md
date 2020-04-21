---
title: SSH access
group: getting-started
description: The SSH protocol is used to connect and authenticate users to the the SSH frontends of IoT-LAB sites and to embedded Linux boards. To that end, you have to associate your computer(s) SSH key(s) to your account.
---

## Generate a new key

Run the following command in a terminal which generates a SSH key pair.
```bash
$ ssh-keygen -t rsa
```
When you're prompted to "Enter a file in which to save the key", press Enter. This accepts the default file location.
```bash
Enter a file in which to save the key (/home/you/.ssh/id_rsa): [Press enter]
```
For Windows users, you can use this command with Git Bash or Ubuntu on Windows or even use the [Puttygen](https://www.puttygen.com/) key generator tool (see [Generate SSH Keys on Windows 10](https://ubuntu.com/tutorials/tutorial-ssh-keygen-on-windows) for instructions).

## Associate your key to your account

1. Copy the SSH key to your clipboard, by copying the output of the following command.

   If your SSH key file has a different name than the example code, modify the filename to match your current setup. When copying your key, don't add any newlines or whitespace.

   ```bash
   $ less ~/.ssh/id_rsa.pub
   ```
2. From the webportal, once signed in, click the Account icon <i class="fas fa-user"></i> on the right to access to your account management
3. Click on the **SSH Keys** tab.
4. Paste your clipboard into text area.
5. Click the **Update SSH keys** button.

Note that it is possible to have several SSH keys for your account, to access from different computers.

## Test your access

Each IoT-LAB site has a SSH frontend reachable at the following address `<site>.iot-lab.info`. For example, try to connect to the Grenoble's frontend:

``` bash
$ ssh <login>@grenoble.iot-lab.info
```
