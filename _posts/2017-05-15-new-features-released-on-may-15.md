---
id: 5909
title: New SSH CLI Tools
date: 2017-05-15T11:12:24+00:00
author: Alexandre Abadie
layout: post
guid: https://www.iot-lab.info/?p=5909
permalink: /new-features-released-on-may-15/
categories:
  - Uncategorized
---
<div class="pf-content">
  <p>
    After the release of a new version of the CLI Tools a few weeks ago, we are happy to announce the new <strong>SSH CLI Tools</strong> are now available on the testbed.
  </p>
  
  <div>
    The IoT-LAB team has specially designed these tools to remotely control the A8 nodes from the SSH frontends or from a local machine. With the SSH CLI Tools, you&#8217;ll find interesting features such as:</p> 
    
    <ul>
      <li>
        <strong>flashing/resetting the M3</strong> behind the A8
      </li>
      <li>
        <strong>waiting for the system boot</strong> of all A8 of an experiment
      </li>
      <li>
        <strong>running commands</strong> on the frontend or on the A8
      </li>
      <li>
        <strong>running a script</strong> in background on the A8
      </li>
    </ul>
  </div>
  
  <p>
    You can follow <a href="https://www.iot-lab.info/tutorials/ssh-cli-client/">this tutorial</a> on the frontend SSH to get an introduction to the SSH CLI Tools.
  </p>
  
  <p>
    The SSH CLI Tools source code is <a href="https://github.com/iot-lab/ssh-cli-tools">available on GitHub</a> so if you find bugs or potential improvements, feel free to propose a Pull Request or open an issue.
  </p>
  
  <p>
    Finally, since the SSH CLI Tools are available on PYPI, you can use them from your computer. In this case, they can be installed using pip:
  </p>
  
  <pre>
     sudo pip install iotlabsshcli
</pre>
</div>