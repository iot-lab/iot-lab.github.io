---
title: Resources
group: getting-started
description: IoT-LAB testbed provides users with a set of resources for experimentation. This page describes these resources and their properties and how to book them to be able to run an experiment according to your needs.
---

## Nodes properties

The basic resource of the testbed is the node: a specific board deployed at a specific position on a specific site. It is on such resources that the user's experimentation takes place. All the resources are stored into the resource manager database with a set of properties described in the table below:

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
                <code>&lt;board_name&gt;-&lt;id&gt;.&lt;site&gt;.iot-lab.info</code>.<br>
                <small>Example: the first M3 node of Grenoble site is <code>m3-1.grenoble.iot-lab.info</code>.</small>
            </td>
        </tr>
        <tr>
            <th scope="row">archi</th>
            <td>string</td>
            <td>
                Information about the hardware of the node, composed as follows:<br> <code>&lt;board_name&gt;:&lt;radio_chipset&gt;</code>.<br>
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
    </tbody>
</table>

## Browse nodes

The different tools of the testbed allow to browse them.

From the [webportal](https://www.iot-lab.info/testbed), the Testbed Status page displays a list in a table that can be filtered by site, architecture and status.

<div class="col col-lg-10 offset-lg-1" markdown="1">
![]({{ 'assets/images/docs/resources-status.png' | relative_url }}){:.img-thumbnail}
</div>

The **view on site map** link allows to show them also in an interactive 3D view, helping a lot in understanding or choosing a physical topology.  

<div class="col col-lg-10 offset-lg-1" markdown="1">
![]({{ 'assets/images/docs/resources-3dmap.png' | relative_url }}){:.img-thumbnail}
</div>

Using the [CLI tools]({% link docs/tools/cli.md %}), the `iotlab-status` command lists resources and their properties, with options to apply filters.

```bash
$ iotlab-status --nodes
{
    "items": [
        {
            "archi": "m3:at86rf231",
            "camera": 0,
            "mobile": 0,
            "mobility_type": " ",
            "network_address": "m3-1.grenoble.iot-lab.info",
            "site": "grenoble",
            "state": "Alive",
            "uid": "2354",
            "x": "20.10",
            "y": "26.76",
            "z": "-0.04"
        },
        ...
    ]
}
```

## Booking

Once you chose the [board(s)]({% link docs/boards/overview.html %}) and the [site(s)]() you want to involve in your experiment, you have to express it at the submission step so that the resources are booked for you.

At that point, there are two alternatives available to you to select nodes:

1. **by properties**, specifying a set of properties (eg. archi, site) that nodes have to match and their number;
2. **by ids**, specifying the site and board name with a list of resources ids.

The first case is the simplest if you just want a number of nodes, since you just have to express your need and the scheduler will choose the right nodes for you. Here is an example using CLI tools:
```bash
iotlab-experiment submit -d 20 -l 10,archi=m3:at86rf231+site=grenoble
```

The second case is typically used when you want to have a specific physical topology (aligned, grids, clusters, multi-hop, etc.). You saw in the nodes description that the nodes coordinates are stored. The [Deployment]() section should help you in understanding how the nodes are spread among a site and, so, in picking the right ones to setup your topology. The 3D view of the webportal is also very helpfull for that. Here is an example using CLI tools:
```bash
iotlab-experiment submit -d 20 -l grenoble,m3,1-9+23
```

<div class="alert alert-info" markdown="1">
**About radio proximity**

As IoT-LAB M3 and A8-M3 are deployed at a large-scale, you could have 2 nodes too far from each other to be able to communicate.

- In the submission **by properties** case, the scheduler will make sure that the assigned nodes are in the same radio neighborhood.
- In the submission **by ids** case, the constraint on radio proximity is not checked by the scheduler. You have to make sure that the nodes are able to communicate together.

Other boards are deployed in a smaller scale, next to each others, and do not involve this additional mechanism.
</div>

### Scheduling

For both booking mode you can ask the scheduler to start your experience as soon as possible (i.e. ASAP) or make a reservation for a specific date and time.

With the **asap** mode the scheduler will accept your reservation, but the experiment may not start right away if some of the nodes you asked for are already in use. In that case, the experiment will have a status of _Waiting_, and will be start as soon as they are free again.

Making a **reservation** amounts to precise a start date. Regarding the specified duration, the scheduler will check if the nodes requested will be available on that time slot. If not, the experiment submission will be rejected.

To help you to select available nodes or available time slot, the Testbed Status page of the webportal displays the current state of nodes in the list. Moreover, on the same page, the 'Tesbed Activity' tab gives access to a gantt diagram that allows to see past, current and future experiments over time.
