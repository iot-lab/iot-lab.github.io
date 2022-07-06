---
title: MicroPython
group: os
---

## Description

[MicroPython](https://micropython.org/) is an implementation of the
[Python](https://python.org) programming language designed for highly
constrained hardware platforms such as microcontrollers.

You can find a lot of documentation on the
[MicroPython](http://docs.micropython.org/en/latest/) website. The source
code of MicroPython is [hosted on GitHub](https://github.com/micropython/micropython).

## Basic usage with IoT-LAB

In IoT-LAB, the [Pycom boards]({{ site.baseurl }}{% link docs/boards/pycom.md %}) provides access to a MicroPython pre-installed
firmware.

Start an experiment with MicroPython using the Pycom FiPy board:

```bash
$ iotlab-experiment submit -d 120 -l 1,site=saclay+archi=pycom:fipy
$ iotlab-experiment wait
```

You can list the node assigned to your experiment with the following command:
```bash
$ iotlab-experiment get --print
{
    "associations": null, 
    "deploymentresults": {
        "0": [
            "pycom-<id>.saclay.iot-lab.info"
        ]
    }, 
    "duration": 120, 
    "firmwareassociations": null, 
    "mobilities": null, 
    "name": null, 
    "nodes": [
        "pycom-<id>.saclay.iot-lab.info"
    ], 
}
```

The MicroPython REPL can be accessed as usual via the serial redirection
mechanism (just press `Enter` once to get the REPL `>>>` prompt):
- from the SSH frontend:
  ```bash
  <login>@saclay:~$ nc pycom-<id> 20000

  >>>
  ```

- from your local computer using an SSH tunnel:
  ```bash
  $ ssh -L 20000:pycom-<id>:20000 <login>@saclay.iot-lab.info
  ```
  Then, **in another terminal**, connect to `localhost:20000` with `nc`:
  ```bash
  $ nc localhost 2000

  >>>
  ```

## Recommended local usage

Using `nc` is quite limited though: it's not easily possible to use the Ctrl+D,
Ctrl+E, etc keyboard shortcuts of the MicroPython REPL because they are first
interpreted by the Linux shell.

That's why it's recommended to only interact with the REPL via an SSH tunnel
and using local tools instead:
- `socat` to redirect the TCP:20000 port in a TTY like file locally
- `miniterm.py` from the [pyserial Python package](https://pythonhosted.org/pyserial/) because it correctly forwards
  Ctrl+D, Ctrl+E, etc shortcuts to the REPL
- the [pymakr extension of VSCode](https://docs.pycom.io/pymakr/installation/vscode/)

### Setup the local REPL redirection

1. Open the SSH tunnel:

```bash
$ ssh -L 20000:pycom-<id>:20000 <login>@saclay.iot-lab.info
```

2. Start the `socat` TCP to file redirection:

```bash
$ socat PTY,link=/tmp/ttyS0,echo=0,crnl TCP:localhost:20000
```

This command redirects the stream from `localhost:20000` (which itself is
connected to the serial port via the SSH tunnel) to the local pseudo-terminal
in `/tmp/ttyS0`.

This way, `/tmp/ttyS0` acts a local TTY, exactly like the board was plugged
directly on the computer.

### Access the REPL with miniterm

From this point, you can use `miniterm.py` to connect to the REPL:

```
miniterm.py /tmp/ttyS0 115200
--- Miniterm on /tmp/ttyS0  115200,8,N,1 ---
--- Quit: Ctrl+] | Menu: Ctrl+T | Help: Ctrl+T followed by Ctrl+H ---

>>>
```

Use the `Ctrl+D` to reset the board, `Ctrl+E` to switch to _paste mode_.

### Access the REPL with `pymakr`

This [pycom documentation page](https://docs.pycom.io/pymakr/installation/vscode/)
explains how to install the pymakr extension of the VSCode editor.

Edit the Pymakr global settings and change/add the `address` field as follows:
```json
    "address": "/tmp/ttyS0"
```

Then use the control in the bottom menu of VSCode to Run/Upload/Download
MicroPython scripts.

<div style="text-align:center">
<img src="{{ '/assets/images/docs/oses/micropython/' | relative_url}}pymakr-controls.png" style="width:300px;"/>
</div>
