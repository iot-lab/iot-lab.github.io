---
title: Maintenance operation of April 4th
---

![]({{ '/assets/images/posts/' | relative_url }}robot_trajectory.png){: .img-fluid }
{: .text-center}

The whole FIT IoT-LAB testbed was closed on April 4th for maintenance and upgrade operations.
{: .lead}

During this day we deployed new software; here are the details:

### Robots

The robots backend software has been totally refactored to ease the evolution and development of future features. In this operation, we also upgrade the ROS framework version to its last LTS (ROS Indigo); running on a recommended Ubuntu 14.04 LTS.

It improves a lot robots navigation, being faster, more accurate.The concrete impact today for users is a slight change in the use of mobility. Mobility models have their own JSON description and are now separated from profiles association. As you associate firmware(s) and profile(s) to your experiment nodes, you may also associate a mobility. For that, since it does not impact a lot of people, we decided to delete all users profile including a mobility description.

Therefore, we removed this feature from the web portal, and implemented a first solution via cli-tools. A new CLI Client, named `iotlab-robot`, has been added to get the status of robots, get the list of mobilities,and update a mobility association during an experiment. Currently, you have a total of 7 robots deployed:

* 2 in Grenoble – m3-381 & m3-382;
* 3 in Lille – m3-257, m3-258 & m3-259;
* 2 in Strasbourg – m3-96 & m3-97.

### CLI tools

CLI tools have a new release (2.0.0) to manage new robots features. As mentioned just above, a new CLI Client dedicated to robots has been added. Find more details in the commit message of release [2.0.0](https://github.com/iot-lab/cli-tools/releases/tag/2.0.0).
