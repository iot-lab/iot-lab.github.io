---
title: User account
group: getting-started
description: IoT-LAB is an open testbed, but you need an account to have access to it.
---

## Registration

If you want to register on the IoT-LAB testbed you just have to fill the [Sign up form](https://www.iot-lab.info/testbed/signup).

Some lightnings about some fields of the registration form:
- **Email**: We ask for an academic or professional email address. So classic emails such as `"@[gmail|aol|yahoo|hotmail].com"` are not accepted.
- **User category / Organization / City / Country**: These information are asked for statistical purpose. We have to periodically provide these statistics about users to our funders, to understand if users are mainly from academic, with which proportion from companies, and from where. It helps to show that it is mainly adopted and to get new fundings.
- **Motivations**: This information let us understand what users do or need.

After submitting, you will receive an activation link by email, valid for 24 hours. Once activated, you will receive another email with your login information.

If you don't have provided a SSH key at registration, you may want to configure your [SSH access]({{ '/docs/getting-started/ssh-access' | relative_url }}) to be able to connect to the different site servers.

Finally, register implies accepting and respecting the [IoT-LAB Terms of Service]({{ '/docs/getting-started/terms-of-use' | relative_url }})

## User storage

All users have a quota of 2Go to store their data on each IoT-LAB site frontend.

Automatic monitoring data are not taken into account in this quota. But, since it can produce a lot of data (stored in `~/.iot-lab/<exp_id>` directory), a cleaning system is set up. It removes monitoring directories older than 6 months. Directories exceeding 2GB are deleted after only 1 month. So, think about saving/exporting your large dataset elsewhere.

Also note that backup/recovery of your home directories, in case of a hardware failure, is not always guaranteed. We provide a best-effort service and you are strongly encouraged to perform your own backups regularly.

## Users mailing-list

As a new user, **you are automatically subscribed to the IoT-LAB users mailing-list** (_users AT iot-lab.info_). This mailing list is mainly dedicated to maintenance announcements and questions about IoT-LAB usage. So keep an eye on it in order to stay informed of the testbed availability. You can manage your subscription from the webportal on the [Account](https://www.iot-lab.info/testbed/account) page, <i class="far fa-envelope"></i> **Mailing list** tab -- here is a direct link to [unsubscribe](https://sympa.inria.fr/sympa/signoff/iot-lab-users).

## Account expiration

Each year an account deactivation campaign is launched to deactivate inactive accounts. A user account is considered inactive if no experiment has been running for more than a year. The users concerned are notified by email. If you want to reactivate your account, you can reply to this email giving your motivations.
