---
title: Update of IoT-LAB tools
---
![]({{ '/assets/images/posts/' | relative_url }}tools.png){: .img-fluid }
{: .text-center}

We would like to inform you about tools updates we made on the IoT-LAB SSH frontends.
{: .lead}

## GNU Toolchain for ARM

Version 7.2 of the GNU Toolchain for ARM is now installed in /opt/gcc-arm-none-eabi-7-2017-q4-major in addition to the actual one, version 4.9, which is still used by default. To know more on how to use it or set it as the default version, see the [IoT-LAB wiki](https://github.com/iot-lab/iot-lab/wiki/Versions-of-the-GNU-toolchain-for-ARM).

## IoT-LAB CLI Tools

For a better user experience, we released a [new version of IoT-LAB command-line tools](https://pypi.org/project/iotlabcli/) (v2.5.3). It mainly consists in renaming, adding a common prefix to the different commands.

Thus now you should use:

* **iotlab-experiment** (experiment-cli)
* **iotlab-node** (node-cli)
* **iotlab-profile** (profile-cli)
* **iotlab-auth** (auth-cli)
* **iotlab-robot** (robot-cli)
* **iotlab-ssh** (open-a8-cli)

All legacy names are always available to ensure compatibility with old scripts and tools. A deprecated message is printed when using legacy commands.  
Of course you are encouraged to update.
