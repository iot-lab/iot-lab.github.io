---
id: 5076
title: Maintenance operation of April 4th
date: 2016-04-05T10:43:19+00:00
author: Julien Vandaele
layout: post
guid: https://www.iot-lab.info/?p=5076
permalink: /maintenance-operation-of-april-4th/
categories:
  - Uncategorized
---
<div class="pf-content">
  <p>
    The whole FIT IoT-LAB testbed was closed on April 4th for maintenance and upgrade operations.
  </p>
  
  <p>
    During this day we deployed new software; here are the details:
  </p>
  
  <ul>
    <li>
      <h4>
        <strong>Robots</strong>
      </h4>
      
      <p>
        The robots backend software has been totally refactored to ease the evolution and development of future features. In this operation, we also upgrade the ROS framework version to its last LTS (ROS Indigo); running on a recommended Ubuntu 14.04 LTS. It improves a lot robots navigation, being faster, more accurate, as you can see in this picture.<br /> <img src="https://www.iot-lab.info/wp-content/uploads/2016/04/robot_trajectory.png" alt="robot_trajectory" width="576" height="216" class="alignnone size-full wp-image-5080" /><br /> The concrete impact today for users is a slight change in the use of mobility. Mobility models have their own JSON description and are now separated from profiles association. As you associate firmware(s) and profile(s) to your experiment nodes, you may also associate a mobility. For that, since it does not impact a lot of people, we decided to delete all users profile including a mobility description. Therefore, we removed this feature from the web portal, and implemented a first solution via cli-tools. A new CLI Client, named <code>iotlab-robot</code>, has been added to get the status of robots, get the list of mobilities, and update a mobility association during an experiment.<br /> Currently, you have a total of 7 robots deployed: 
        
        <ul>
          <li>
            2 in Grenoble &#8211; m3-381 & m3-382;
          </li>
          <li>
            3 in Lille &#8211; m3-257, m3-258 & m3-259;
          </li>
          <li>
            2 in Strasbourg &#8211; m3-96 & m3-97.
          </li>
        </ul>
        
        <p>
          Learn how to use robots with this <a href="/tutorials/do-a-circuit-loop-with-a-mobile-m3-node/">tutorial</a>.
        </p>
        
        <li>
          <h4>
            <strong>CLI tools</strong>
          </h4>
          
          <p>
            CLI tools have a new release (2.0.0) to manage new robots features. As mentioned just above, a new CLI Client dedicated to robots has been added.<br /> Read the <a href="/tutorials/iotlab-robot-client/">Robot CLI Client tutorial</a>.<br /> Find more details in the commit message of release <a href="https://github.com/iot-lab/cli-tools/releases/tag/2.0.0">2.0.0</a>. </li> </ul> </div>