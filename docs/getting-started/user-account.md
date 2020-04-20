---
title: User account
group: getting-started
description: IoT-LAB is an open testbed, but you need an account to have access to it.
---

## Registration

If you want to register on the IoT-LAB testbed you just have to fill the [Sign up form](https://www.iot-lab.info/testbed/signup). After submitting, you will receive an activation link by email, valid for 24 hours. Once activated, you will receive your credentials (login and password) by email. Of course, we recommend you to change your password on your first connection to the webportal.

Some lightnings about some fields of the registration form:
- **Email**: We ask for an academic or professional email address. <span class="text-warning">Why? Which forbidden domains ?</span>
- **User category / Organization / City / Country**: These information are asked for statistical purpose. We have to periodically provide these statistics about users to our funders, to understand if users are mainly from academic, with which proportion from companies, and from where. It helps to show that it is mainly adopted and to get new fundings.
- **Motivations**: This information let us understand what users do or need.

Finally, register implies accepting and respecting the [IoT-LAB Terms of Service]({% link docs/getting-started/terms-of-use.md %})

## SSH access

The SSH protocol is used to connect and authenticate users to the the SSH frontends of IoT-LAB sites and to embedded Linux boards. To that end, you have to associate your computer(s) SSH key(s) to your account.

### Generate a new key

Run the following command in a terminal which generates a SSH key pair.
```bash
$ ssh-keygen -t rsa
```
When you're prompted to "Enter a file in which to save the key", press Enter. This accepts the default file location.
```bash
Enter a file in which to save the key (/home/you/.ssh/id_rsa): [Press enter]
```
For Windows users, you can use this command with Git Bash or Ubuntu on Windows or even use the [Puttygen](https://www.puttygen.com/) key generator tool (see [Generate SSH Keys on Windows 10](https://ubuntu.com/tutorials/tutorial-ssh-keygen-on-windows) for instructions).

### Associate your key to your account

#### From the webportal
1. Copy the SSH key to your clipboard, by copying the output of the following command.

   If your SSH key file has a different name than the example code, modify the filename to match your current setup. When copying your key, don't add any newlines or whitespace.

   ```bash
   $ less ~/.ssh/id_rsa.pub
   ```
2. From the webportal, once signed in, click the Account icon <i class="fas fa-user"></i> on the right to access to your account management
3. Click on the **SSH Keys** tab.
4. Paste your clipboard into text area.
5. Click the **Update SSH keys** button.

#### With the CLI tools
Use the following command:
```bash
iotlab-auth --add-ssh-key
```

It will use `~/.ssh/id_rsa.pub` as default, but you can specify the identity file to use with the `-i` option.

Note that it is possible to have several SSH keys for your account, to access from different computers.

### Test your access

Each IoT-LAB site has a SSH frontend reachable at the following address `<site>.iot-lab.info`. For example, try to connect to the Grenoble's frontend:

``` bash
$ ssh <login>@grenoble.iot-lab.info
```
## User storage

All users have a quota of 2Go to store their data on each IoT-LAB site frontend.

Automatic monitoring data are not taken into account in this quota. But, since it can produce a lot of data (stored in `~/.iot-lab/<exp_id>` directory), a cleaning system is set up. It removes monitoring directories older than 6 months. Directories exceeding 2GB are deleted after only 1 month. So, think about saving/exporting your large dataset elsewhere.

Also note that backup/recovery of your home directories, in case of a hardware failure, is not always guaranteed. We provide a best-effort service and you are strongly encouraged to perform your own backups regularly.

## Users mailing-list

As a new user, you are automatically subscribed to the IoT-LAB users mailing-list (_users AT iot-lab.info_). This mailing list is mainly dedicated to maintenance announcements and questions about IoT-LAB usage. So keep an eye on it in order to stay informed of the testbed availability. You can manage your subscription from the webportal on the [Account](https://www.iot-lab.info/testbed/account) page, <i class="far fa-envelope"></i> **Mailing list** tab.

## Account expiration

Each year an account deactivation campaign is launched to deactivate inactive accounts. A user account is considered inactive if no experiment has been running for more than a year. The users concerned are notified by email. If you want to reactivate your account, you can reply to this email giving your motivations.
