---
title: Radio characterization
group: tools
description: |
    We provide a (beta) dedicated tool to run experiments on the testbed that can map out the connectivity of nodes between each other.
    It's been tested almost only IoT-LAB M3 nodes 
---

## Principle

The tool uses a [RIOT]({% link docs/os/riot.md %})-based firmware.

The tool presents as a CLI program with a certain number of subcommands to start a radio characterization experiment,
parse the results from a radio characterization experiment, and also draw the results (through matplotlib)

1. The tool can start an experiment for you, with nodes selection, site selection etc...
2. It redirects the serial communication from all the nodes to a local socket 
3. It then communicates with the nodes firmware to test out message emissions between the nodes:

    Example run with 3 nodes:
    * for each channel, txpower pair:
        * selects node 1
        * node 2-3 listen for incoming broadcasts
        * node 1 broadcasts a number of messages
        * the tool queries nodes 2-3 to see which messages were received, and by whom
        
        * selects node 2, node 1+3 listen, node 2 broadcasts, same thing
        * selects nodes 3, node 1-2 listen, node 3 broadcasts, same thing

4. Once the experiment is over, it parses the logs of all the nodes, it can then know link quality between a source node
and a receiving node, mainly the PDR (packet Delivery Ratio).
5. Once the experiment results are parsed, the tool has generated a number of data files (by default, in the `experiments/<id>/` folder in the current working directory), see [Generated files](#generated-files)
    
In order to use the tool, you have to install it through `pip install iotlabradiotest`, or connect to a site's frontend
using X redirection `ssh -X <username>@site.iot-lab.info` and use the tool there.

## Limitations

* Depending on the number It can take a few seconds per step. You can estimate your experiment minimum run time with formula : ``experiment run time = nb_nodes * nb_channels * nb_txpower * packets_interval * packets_numbers``
* Some options for plotting results work only if nodes are on the same z level, and not aligned (all nodes with same x or same y).

## Subcommands 

`iotlab-radiotest --help` to get the full CLI help

All subcommands, except `ls` and `start`, take an experiment ID as parameter e.g. `-i 185555`, if left empty 
the subcommand will treat the latest radio characterization experiment.

### start

`iotlab-radiotest start` will:
* start the experiment with the firmware
* run the background listening for the outputs on the serial link,
* collect the outputs
* parse the results


    Usage: iotlab-radiotest start [OPTIONS]
    
      Start a Radio-Test experiment
    
    Options:
      --start_time DATE               Date-Time When to start the experiment,
                                      otherwise the experiment is started ASAP
      --config YAML_CONFIG_FILE       config file to use
      -s, --site SITE                 site on which to start the experiment
      -rt, --radio.txpowers COMMA-SEPARATED-FLOAT
                                      list of transmission powers in dBm
      -rc, --radio.channels COMMA-SEPARATED-INTEGER
                                      list of radio channel: 11 -> 26 for 802.15.4
      -ps, --packets.size INTEGER     packet size (bytes)
      -pn, --packets.numbers INTEGER  number of packets
      -pi, --packets.interval INTEGER
                                      interval between packets (ms)
      -d, --duration INTEGER          duration of the experiment in minutes
      --help                          Show this message and exit.
    
    Archis/Nodes Options (<archi> any of st-lrwan1,m3,nrf52dk,samr21,a8,samr30):
      --nodes.<archi> NODESSTRLIST  list: 1+4-6 or 1,4,5,6 for [1, 4, 5, 6]

#### Configuration

configuration is passed through CLI arguments or a yaml file. Many arguments have sensible defaults,
like the channel list (channels 11,18,25 for 802.15.4) or the packet size, numbers, intervals:

|      Parameter     | Default Value |            Unit           |
|:------------------:|:-------------:|:-------------------------:|
| radio.channel_list |    11,18,25   | Channel, or Hz (for LoRa) |
|    radio.txpower   |       3       |            dBm            |
|    packets.size    |       30      |           bytes           |
|   packets.number   |      100      |                           |
|  packets.interval  |      100      |             ms            |
|      duration      |       20      |            min            |


To use a config file instead of passing many command line arguments, use the `--config <path_to_config_yaml>` argument. 

Example config.yaml:

    site: lille
    nodes:
      m3: 12-14
      samr21: [1, 2]
    radio:
      txpower: [-7,0,3]

Then,

    iotlab-radiotest start --config config.yaml

will keep the default values for most of the parameters but use the Lille site, and use different TX power (-7, 0 and 3 dBm).
It will use `IoT-LAB M3` nodes m3-12, m3-13, m3-14 and `SAMR21` nodes samr21-1, samr21-2. 

You can also modify a single value in the config by using  CLI arguments.
With the above config.yaml, these command lines are equivalent 

```
    iotlab-radiotest start --config config.yaml
    iotlab-radiotest start --site lille --nodes.m3 12-14 --radio.txpower -7,0,3 --nodes.samr21 1,2
```

### parse

`iotlab-radiotest parse -i <experiment_id>` parses the results independently from the `start`.

    Usage: iotlab-radiotest parse [OPTIONS]
    
      Parse results of a Radio-Test experiment
    
    Options:
      -i, --id INTEGER  IoT-LAB experiment id  [default: (latest experiment)]
      --help            Show this message and exit.
      


    

### clean

`iotlab-radiotest clean` cleans up parsed results for an experiment.

    Usage: iotlab-radiotest clean [OPTIONS]
    
      delete parsed experiment data
    
    Options:
      -i, --id INTEGER  IoT-LAB experiment id  [default: (latest experiment)]
      --help            Show this message and exit.
      
### ls

`iotlab-radiotest ls` lists the experiments in the folder

    Usage: iotlab-radiotest ls [OPTIONS]
    
      List Radio-Test experiments
    
    Options:
      --help  Show this message and exit.

Example output:

        id  site          number of  date
                              nodes
    ------  ----------  -----------  ----------------
    174546  grenoble             67  2019-08-09 11:34
    178837  lille                44
    182203  strasbourg           20
    182205  strasbourg           20
    182210  strasbourg           20
    184652  strasbourg            3  2019-11-13 13:50
    184653  strasbourg            3  2019-11-13 13:54


### config

`iotlab-radiotest config` outputs the config of an experiment

    Usage: iotlab-radiotest config [OPTIONS]
    
      Show Radio-Test experiment config
    
    Options:
      -i, --id INTEGER          IoT-LAB experiment id  [default: (latest
                                experiment)]
      -f, --format [yaml|json]  format of the output
      --help                    Show this message and exit.


Example output:

    $ iotlab-radiotest config -i 184694
    api_url: https://www.iot-lab.info/rest/
    duration: 25
    nodes:
      m3: 10-20
    packets:
      interval: 10
      numbers: 100
      size: 30
    radio:
      channels:
      - 11
      txpowers:
      - -17.0
      - -9.0
      - 0.0
      - 3.0
    site: strasbourg
    version: 2

`version` and `api_url` are only internally-used

## Generated files

### experiments/[id]/config.yaml

Contains the description of the experiment that was started. It is the merge of the default parameter values, the passed
config file, and the passed CLI parameters.

### experiments/[id]/raw.log

Contains the output of the experiment control, example:

    2020-01-24 16:33:49,822 Starting experiment, output experiments/191460
    2020-01-24 16:33:49,824 Connect to serial_aggregator
    2020-01-24 16:33:49,834 Total items in command queue 610
    2020-01-24 16:45:46,173 Queue is empty, exiting
    2020-01-24 16:45:46,173 OK, all finished, parsing the results...
    2020-01-24 16:45:46,177 Parsing IoT-LAB raw logs from experiments/191460/raw to experiments/191460/parsed
    2020-01-24 16:45:46,457 parsing the connectivity...
    2020-01-24 16:45:46,461 Parsing from experiments/191460/parsed to experiments/191460/parsed/link-*
    2020-01-24 16:45:47,000 experiment 191460 stopped

### experiments/[id]/raw/radio-ch[channel]-tx[txpower].log

Contains the raw output of the back-and-forth communication between the tool and the nodes, for a given channel and txpower, example:

    1579880114.265313;m3-3;> channel 26
    1579880114.265834;m3-2;> channel 26
    1579880114.266399;m3-3;success: set channel on interface 3 to 26
    1579880114.266750;m3-3;> 
    1579880114.267048;m3-2;success: set channel on interface 3 to 26
    1579880114.267398;m3-2;> 
    1579880114.267775;m3-1;> channel 26
    1579880114.268040;m3-1;success: set channel on interface 3 to 26
    1579880114.268299;m3-1;> 
    1579880114.270788;samr21-15;> channel 26
    1579880114.271287;samr21-14;> channel 26
    1579880114.271540;samr21-14;success: set channel on interface 3 to 26
    1579880114.272031;samr21-13;> channel 26
    1579880114.272267;samr21-13;success: set channel on interface 3 to 26

### experiments/[id]/parsed/avg-ch[channel]-tx[txpower].log

Contains, for each node in he set, the average of the links from all the other nodes. Can be useful to identify nodes that
are in a bad spot (e.g. located near a Wifi AP on a channel close to the one we target)

### experiments/[id]/parsed/merge-ch[channel]-tx[txpower].log

Contains the PDR, LQI, RSSI of each link between two nodes
Example line:
 
    m3-1,m3-2,100,100,-43,255
    
Describes the link between m3-1 and m3-2, 100 packets were seen, 100 packets were valid, the average RSSI and LQI 
(as reported by the radio module) is -43 dBm and 255 (maximum value) respectively. You can ignore the lines where
the second element (tx_node) is empty. 

### experiments/[id]/parsed/link-[link_quality]-tx[txpower].log

link_quality can be good, bad or unbalanced.

Taking a threshold at 90% PDR:
* a good link is a link that is good (PDR >= 90%) for all the channels.
* a bad link is a link that is bad (PDR < 90%) for all the channels.
* an unbalanced link is a link that is not consistently good or bad
 
### experiments/[id]/parsed/graph-tx[txpower].json
 
Roughly the same thing as the link-* file, but it's a `networkx`-loadable graph file in JSON format, which contains
the graph of the links between the nodes, with PDR/LQI/RSSI in the edges' data