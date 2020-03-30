---
title: User account
group: getting-started
description: Create an account which gives you a full access to the testbed and discover the IoT experimental facility.
---

## Signup

If you want to register on IoT-LAB testbed you have just to fill the [signup form](https://www.iot-lab.info/testbed/signup). You will receive an e-mail to your address, that will allow you to activate your account. This activation link is valid for 24 hours. In case you don't validate your account in time you will have to make a new request.

## Mailing-list

As a new user you are automatically subscribed to the IoT-LAB users mailing-list `user AT iot-lab.info`. This mailing list is mainly dedicated to technical questions around IoT-LAB usage and maintenance announcements. So keep an eye on it in order to keep inform about the testbed activity. It's possible to unsuscribe whenever you want with the `Mailing list` tab in your [Account](https://www.iot-lab.info/testbed/account) page.

## Account expiration

Each year an account deactivation campaign is launched. The goal is to automatically deactivate inactive accounts. We consider that a user is inactive if he hasn't submitted an experience for more than a year. You will be notify by e-mail in case of your account is disabled. You can contact us if you want to reactivate your account by giving your reasons to the following address: `admin AT iot-lab.info`. 

## User Home directories

As soon as your account is created you can access your home directory on each IoT-LAB site server. On these servers you have everything you need to run experiments, compile firmwares, interact with node's serial link and so on. By default disk quotas are applied with 2GB soft limit and 2.5GB hard limit. Moreover when you use the monitoring feature IoT-LAB nodes write the results in your home directory (`~/.iot-lab/<exp_id>/`). This data is not taken into account in the calculation of the quota. But we set up an automatic cleaning system and your monitoring directory will be deleted:

* if the disk space is less than 2Gb and the data is more than 6 months old
* if the disk space is greater than 2Gb and the data is more than 1 month old

 Also note that backup/recovery of your home directories, in the event of a hardware fault, is not always guaranteed by IoT-LAB team. We provide best-effort mode and we strongly encourage you to regularly perform your own backups.

Please consult the [Terms of use](/docs/getting-started/terms-of-use) before starting to work with the testbed. 