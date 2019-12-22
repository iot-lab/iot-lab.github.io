---
title: Run Script
group: tools
description: A good practice when you want to launch a long-running and large-scale experiment is to schedule in advance and make a reservation. In this mode you cannot control your experiment interactively with for example retrieve the serial nodes output on the frontend server. This is why the run script feature is made. When you submit an experiment or while the experiment is running you can configure a script association which allow to automatically executes a script on the frontend server. This script runs whith your user identity in a screen session (background mode with a detached terminal).
---

## Script association

In this example we configure a script association which store the serial nodes ouput on the frontend server. The first step is to write the script. It can be written in any language (Python, Ruby) and we provide you a Bash shell script example. You can see in the script that we use another tool, the `serial aggregator`. You can also note that the EXP_ID environment variable is setted and could be used in your script. ($HOME is your home directory path on the frontend server). Create a file with serial_script name and copy the content of the script.

``` bash
#!/bin/bash

# Redirect all serial nodes output to a file
readonly OUTFILE="${HOME}/.iot-lab/${EXP_ID}/serial_output"

echo "Launch serial_aggregator with exp_id==${EXP_ID}" >&2
serial_aggregator -i ${EXP_ID} 2> /dev/null 1> ${OUTFILE}
```

Now we can submit an experiment and specify the script association. We also configure a firmware association with a firmware which prints sensors values on the serial port.


``` bash
$ ssh <login>@grenoble.iot-lab.info
$ iotlab-auth -u <login> # store your credentials if you haven't done it before, it will be used by serial_aggregator command in the serial_script
$ wget ?????/assets/firmwares/docs/run-script/sensors.elf .
$ iotlab-experiment submit -d 20 -l 5,archi=m3:at86rf231+site=grenoble,sensors.elf --site-association grenoble,script=serial_script
```

The site association format is `<site>,script=<script_path>` where site is the frontend server site name.


## Script execution

You must wait that the experiment is running and visualize the [screen](https://linux.die.net/man/1/screen) session. 

``` bash
<login>@grenoble:~$ iotlab-experiment wait
<login>@grenoble:~$ screen -ls # print screen sessions list
<login>@grenoble:~$ screen -r # attach to screen session, use Ctr+a d shortcut to detach 
```

Verify that the serial_output file is generated with serial nodes output.

``` bash
<login>@grenoble:~$ cat .iot-lab/last/serial_output # .iot-lab/last is a symlink to your last experiment directory .iot-lab/<exp_id>
Accelerometer x: 156 y: 104 z: -752
Magnetometer x: 29 y: -449 z: 20
Accelerometer x: 152 y: 104 z: -756
Magnetometer x: 30 y: -450 z: 19
Accelerometer x: 152 y: 100 z: -756
Magnetometer x: 30 y: -450 z: 23
Pressure: 976hPa, Temperature:33.71°C
Accelerometer x: 156 y: 108 z: -752
Magnetometer x: 30 y: -451 z: 23
```

You may also find a log file with the standard error redirection (stderr) for debugging your script execution 

``` bash
<login>@grenoble:~$ cat .iot-lab/last/run_script.log
```

You can visualize the status of your script execution and kill it manually `(succes=0 and error=1)`

``` bash
<login>@grenoble:~$ iotlab-experiment script --status
{
 "0": { "grenoble.iot-lab.info": "Running"}
}
<login>@grenoble:~$ iotlab-experiment script --kill
{
 "0": ["grenoble.iot-lab.info"]
}
<login>@grenoble:~$ iotlab-experiment script --status
{
 "0": { "grenoble.iot-lab.info": "Idle"}
}
```

As you can specify a script association at experiment submission, it’s also possible to run a script when the experiment is running. If there is already a script execution in progress it will stop it and execute the new one.

``` bash
<login>@grenoble:~$ iotlab-experiment script --run grenoble,script=serial_script
{
 "0": ["grenoble.iot-lab.info"]
}
```

## Advanced usage

### Script config

It's also possible to add a script config file to your script association. Indeed you can pass to the script some additional environment variables. Create a file with serial_config name and use this format

``` bash
VAR1=value1
VAR2=value2
```
Run the script as follows (`<site>,script=<script_path>,scriptconfig=<config_path>`)

``` bash
<login>@grenoble:~$ iotlab-experiment script --run grenoble,script=serial_script,scriptconfig=serial_config
```
The variables will be accessible in the script with `$VAR1` and `$VAR2` .

### Cleanup

When the experiment is stopped or you kill manually the script execution a SIGTERM signal is sent to the script. It's possible to catch it and do some post script actions like cleanup.

You can find below an example of script which catch the signal

``` bash
#!/bin/bash
trap 'catch_signal; exit' SIGTERM

catch_signal() {
 echo "Catch SIGTERM signal" >&2
 # cleanup actions here
}
```

