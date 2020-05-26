---
title: Run Script
group: tools
description: Provide a script at submit or while running experiment that will be run automatically in background from the frontend server.
---

## Overview

A good practice when you want to launch a long-running and large-scale experiment is to schedule it in advance making a reservation. When the scheduler launches it, you would like it to configure itself automatically, like for example to set up the retrieving of the nodes serial output into a text file. That's what the Run Script feature is made for:  configure a script association which will be automatically executed on the frontend server. The association can be made at experiment submit or while running.

The Run Script feature is not available through the webportal, but available with CLI tools, or directly through the REST API.

## Script association

In each association command, the script path does refer to a file present in the environment from where you run the command, and will be copied to *$$$*.

### At experiment submit
Script association at submit is specified with the `--site-association` option by giving site(s) name(s) and script path.
```bash
iotlab-experiment submit [...] \
    --site-association <site>[,<site>],script=<script_path>
```

Thus, a same script can be specified for several sites:

```bash
iotlab-experiment submit [...] \
    --site-association grenoble,lille,script=my_script
```

The option can be specified multiple times, to specify a different script per site, for example:

```bash
iotlab-experiment submit [...] \
    --site-association grenoble,script=my_script_for_a8 \
    --site-association lille,script=my_script_for_m3
```

### While experiment running

It is also possible to specify a script association when the experiment is running. If there is already a script execution in progress it will be stoped to execute the new one.

``` bash
iotlab-experiment script --run <site>[,<site>],script=<script_path>
```

## Script execution

With the script subcommand, you can check the status of your script execution:
``` bash
iotlab-experiment script --status
```

and kill it manually:
``` bash
iotlab-experiment script --kill
```

_A 0 return value means success and 1 means error._

The script is executed in a [screen](https://linux.die.net/man/1/screen) session, in detached mode, with your user id. Thus, from the frontend server, you can use the `screen` command to connect to the screen session to see the script's output.
``` bash
screen -ls # print screen sessions list
screen -r # resume the detached screen session, then use Ctr+a d shortcut to detach again
```

The standard error redirection (stderr) is written in a log file in your experiment directory (~/.iot-lab/\<exp_id\>/run_script.log) for debugging your script execution.

## Advanced usage

### Script config

A script config file can be added to your script association. It can help to pass to the script some additional environment variables, like:

``` bash
VAR1=value1
VAR2=value2
```
The config file can be and added as an extra parameter to the script association as follows:
```bash
<site>[,<site>],script=<script_path>,scriptconfig=<config_file>
```
The variables will be accessible in the script (i.e. with `$VAR1` and `$VAR2` in bash).

### Cleanup

At script stop (i.e. when the experiment is stopped or when you kill it manually), a SIGTERM signal is sent. It is possible to catch it and do some post script actions like cleanup.

Here is a bash script example which catch this signal:

``` bash
#!/bin/bash
trap 'catch_signal; exit' SIGTERM

catch_signal() {
 echo "Catch SIGTERM signal" >&2
 # cleanup actions here
}
```

---


## Practical case: Store the nodes serial output into a text file

Here is a script example, in bash, using the Serial aggregator tool. Environment variables, like `HOME` (your home directory path on the frontend server), are available. `EXP_ID` is set with your experiment identifier.

``` bash
#!/bin/bash

# Redirect all nodes serial output to a file
readonly OUTFILE="${HOME}/.iot-lab/${EXP_ID}/serial_output"

echo "Launch serial_aggregator with exp_id==${EXP_ID}" >&2
serial_aggregator -i ${EXP_ID} 2> /dev/null 1> ${OUTFILE}
```

And here is the submit command using this script and the [riot-sensors.elf]({{ site.baseurl }}{% link assets/firmwares/riot-sensors.elf %}) firmware, which prints sensors values on the serial port, with 5 IoT-LAB M3 nodes on the Grenoble site.

``` bash
iotlab-experiment submit -d 20 \
    -l 5,archi=m3:at86rf231+site=grenoble,riot-sensors.elf \
    --site-association grenoble,script=serial_script.sh
```
