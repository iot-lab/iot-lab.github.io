---
title: Resources
group: getting-started
description: IoT-LAB testbed provides users with a set of resources for experimentation. In this page we are going to describe these resources and their properties. When you run an experiment on IoT-LAB you must reserve these resources. For this we use a scheduler or a resource manager to which you make a reservation request. We will learn how to select and book your resources according to your experimentation needs.
---

#### Node description

The default resource of the testbed is the node. It is on this resource that the user's experimentation takes place. You can find below a description of the main properties of a node.

<table class="table table-striped">
    <thead>
        <tr>
            <th scope="col">Property</th>
            <th scope="col">Type</th>
            <th scope="col">Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th>network_address</th>
            <td>string</td>
            <td>
                Network hostname of the node, composed as follows:<br>
                <code>&lt;node_name&gt;-&lt;id&gt;.&lt;site&gt;.iot-lab.info</code>.<br>
                <small>Example: the first M3 node of Grenoble site is <code>m3-1.grenoble.iot-lab.info</code>.</small>
            </td>
        </tr>
        <tr>
            <th scope="row">archi</th>
            <td>string</td>
            <td>
                Information about the hardware of the node, composed as follows:<br> <code>&lt;node_name&gt;:&lt;radio_chipset&gt;</code>.<br>
                <small>Example: the value for an IoT-LAB M3 is <code>m3:at86rf231</code> (node_name = m3 and radio_chipset = at86rf231).</small>
            </td>
        </tr>
        <tr>
            <th scope="row">site</th>
            <td>string</td>
            <td>Name of the IoT-LAB site where the node is located. All sites are described in the Deployment section.</td>
        </tr>
        <tr>
            <th scope="row">state</th>
            <td>string</td>
                <td>The state allows to know if the node is free (<i>Alive</i>) or already in use (<i>Busy</i>). In some cases the node may have some issues (<i>Suspected</i> or <i>Dead</i>) and is not available for booking.</td>
        </tr>
        <tr>
            <th scope="row">uid</th>
            <td>string</td>
            <td>Unique identifier of the board (16 bits). This value is calculated with microcontroller CPU architecture.<br> <small>Example: an IoT-LAB M3 node uses the STM32 unique device identifier, a 96 bit register</small></td>
        </tr>
        <tr>
            <th scope="row">x, y, z</th>
            <td>integer</td>
            <td>Coordinates of the node (in meters) in a 3D cartesian coordinate system. <span class="text-warning">On the Deployment page of each site you can find where is located the origin (0, 0, 0).</span></td>
        </tr>
        <tr class="text-warning">
            <th scope="row">mobile</th>
            <td>integer</td>
            <td>Gives information if the node is mobile on a robot (mobile=1) or fixed (mobile=0) in an experimentation room or in a building</td>
        </tr>
    </tbody>
</table>

#### Resources selection

To start an experiment on IoT-LAB you have to choose the resources that will be used. The first step is to see the list of resources available on the testbed. You can find an exhaustive list in the <a href="{{ "/docs/boards/overview" | relative_url }}">boards documentation page</a> with a hardware description, the corresponding node name and which radio technology is supported. You can also view the number of these resources deployed per site.

Then IoT-LAB makes it possible to dynamically retrieve informations on the resources of the testbed with two REST API clients:

 * the testbed Webportal with the <a href="https://www.iot-lab.info/testbed/status" target="_blank">status page</a>
 * the command line tools (CLI-tools) with the <a href="{{ "/docs/tools/cli/#status-command" | relative_url }}">iotlab-status</a> command

#### Resources booking

When you know what type of node you want you have to make a request to the scheduler to reserve them on the testbed. There are two possibilities:

1. <b>book by hostnames</b>: you simply specify a list of hostname and the scheduler will check if the nodes are available.
2. <b>book by properties</b>: you ask the scheduler for a number of nodes that match a set of properties (eg. archi, site) and it will assign you available nodes that meet the criteria.

In the second case the scheduler will make sure that the assigned nodes are in the same radio neighborhood. Thus they will be within radio range of each other. In the first case this constraint is not checked and you have to make sure that the nodes are close to each other when you reserve them. You can use 3D maps to visualize the topologies of IoT-LAB sites. They are available on the testbed Webportal in the <a href="https://www.iot-lab.info/testbed/status" target="_blank">status page</a> (eg. view on site map link) or when you <a href="https://www.iot-lab.info/testbed/experiment" target="_blank">add a new experiment</a> and select your nodes by `hostname/map` (eg. View/select nodes on map link).

Finally for both booking mode you can ask the scheduler to start your experience as soon as possible (eg. ASAP) or make a reservation for a specific date and time. With ASAP mode the scheduler will accept your reservation but you can't be sure it will start immediately. For example if another user has an ongoing experiment with nodes you want, the start of your experiment will be automatically scheduled at the end of this experiment. In this case your experiment will be in a `Waiting` state. Don't forget that you have access to your nodes only if the experiment is started with state `Running`.

To help you to reserve resources you have access to a Drawgantt in the <a href="https://www.iot-lab.info/testbed/status" target="_blank">status page</a> (eg. `Testbed Activity` tab next to Nodes Properties tab) where you can see experiments schedule on the testbed.

You can also consult the  <a href="{{ "/docs/tools/cli/#experiment-command" | relative_url }}">Cli-Tools documentation</a> to understand how to submit an experiment with both booking modes and how to make a reservation for a date.