---
id: 5821
title: New features released on April, 25
date: 2017-04-26T09:46:39+00:00
author: Julien Vandaele
layout: post
guid: https://www.iot-lab.info/?p=5821
permalink: /new-features-released-on-april-25/
categories:
  - Uncategorized
---
<div class="pf-content">
  <p>
    The whole FIT IoT-LAB testbed was closed on April 25th afternoon for upgrade operations.
  </p>
  
  <p>
    Here is the details of the new features available from today.
  </p>
  
  <h3>
    Run Script
  </h3>
  
  <p>
    We finally release a feature we would like to provide from a long time ago.<br /> For sure, it is really convenient to be able to specify a firmware that will be flashed automatically at the experiment starting, as much as to specify a profile for the automatic monitoring setup. But we are quite sure that you may have already say to yourself: &#8220;I just miss something to launch my own script automatically after that&#8221;.
  </p>
  
  <p>
    We finally had some time to integrate this feature in our Open REST API, letting the possibility to specify a script that will be run in background on the SSH frontends. You can launch this script manually at any time during your experiment or you can specify this script at experiment submission. In this last case, it will be launched automatically at experiment starting.
  </p>
  
  <p>
    We made this new feature easy to use by providing it to the CLI tools.<br /> Follow <a href="https://www.iot-lab.info/tutorials/run-script/" title="Run Script tutorial" target="">this tutorial</a> to get an introduction of this feature and learn how it works.
  </p>
  
  <h3>
    CLI Tools 2.4.0
  </h3>
  
  <p>
    Version 2.4.0 of our IoT-LAB CLI tools is here, with new interesting features:
  </p>
  
  <ul>
    <li>
      a <tt>script</tt> subcommand, enabling the use of the new Run Script feature explained just above
    </li>
    <li>
      an <tt>update-idle</tt> and a <tt>profile-reset</tt> commands, to respectively set firmware and profile to defaults
    </li>
    <li>
      a <tt>profile-load</tt> command, to update profiles
    </li>
    <li>
      improvement in filtering possibilities in commands
    </li>
  </ul>
  
  <p>
    This new version is now available on <a href="https://pypi.python.org/pypi/iotlabcli/2.4.0" title="iotlabcli on PyPI" target="">PyPI</a>, easy to install with this command:
  </p>
  
  <pre>pip install iotlabcli --upgrade</pre>
  
  <p>
    You will also find on <a href="https://pypi.python.org/pypi/iotlabcli/2.4.0" title="iotlab-cli on PyPI" target="">the module page</a> the complete changelog.
  </p>
</div>