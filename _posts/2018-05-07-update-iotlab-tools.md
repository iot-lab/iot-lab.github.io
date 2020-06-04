---
id: 7111
title: Update of IoT-LAB tools
date: 2018-05-07T15:48:24+00:00
author: Frederic Saint-marcel
layout: post
guid: https://www.iot-lab.info/?p=7111
permalink: /update-iotlab-tools/
categories:
  - Uncategorized
---
<div class="pf-content">
  <p>
    We would like to inform you about tools updates we made on the IoT-LAB SSH frontends.
  </p>
  
  <h3>
    GNU Toolchain for ARM
  </h3>
  
  <p>
    Version 7.2 of the GNU Toolchain for ARM is now installed in /opt/gcc-arm-none-eabi-7-2017-q4-major in addition to the actual one, version 4.9, which is still used by default. To know more on how to use it or set it as the default version, see the <a href="https://github.com/iot-lab/iot-lab/wiki/Versions-of-the-GNU-toolchain-for-ARM">IoT-LAB wiki</a>.
  </p>
  
  <h3>
    IoT-LAB CLI Tools
  </h3>
  
  <p>
    For a better user experience, we released a <a href="https://pypi.org/project/iotlabcli/">new version of IoT-LAB command-line tools</a> (v2.5.3). It mainly consists in renaming, adding a common prefix to the different commands.
  </p>
  
  <p>
    Thus now you should use:
  </p>
  
  <ul>
    <li>
      <strong>iotlab-experiment</strong> (experiment-cli)
    </li>
    <li>
      <strong>iotlab-node</strong> (node-cli)
    </li>
    <li>
      <strong>iotlab-profile</strong> (profile-cli)
    </li>
    <li>
      <strong>iotlab-auth</strong> (auth-cli)
    </li>
    <li>
      <strong>iotlab-robot</strong> (robot-cli)
    </li>
    <li>
      <strong>iotlab-ssh</strong> (open-a8-cli)
    </li>
  </ul>
  
  <p>
    All legacy names are always available to ensure compatibility with old scripts and tools. A deprecated message is printed when using legacy commands.<br /> Of course you are encouraged to update.
  </p>
</div>