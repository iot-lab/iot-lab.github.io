---
title: FreeRTOS
group: os
---

## Description

FreeRTOS is designed to be small and simple. The kernel itself consists of only
three or four C files. It provides methods for multiple threads or tasks,
mutexes, semaphores and software timers. Key features are very small memory
footprint, low overhead, and very fast execution. IoT-LAB uses FreeRTOS by
default for basic development fo M3 nodes.

## Support for IoT-LAB boards

We provide a port for IoT-LAB boards based on FreeRTOS 7.0.2 version called Openlab. You can clone the
[<i class="fab fa-github"></i> iot-lab/openlab](https://github.com/iot-lab/openlab) repository as follows:


```bash
git clone https://github.com/iot-lab/openlab.git
cd openlab
```

## Compilation options

The Openlab port provides two platform support:

- `iotlab-m3` for an IoT-LAB M3
- `iotlab-a8` for an IoT-LAB A8-M3

For example, here is the set of commands to use to compile the tutorial example with Cmake build system

```bash
mkdir build.m3 && cd build.m3
cmake .. -DPLATFORM=iotlab-m3
make tutorial_m3
```

```bash
mkdir build.a8 && cd build.a8
cmake .. -DPLATFORM=iotlab-a8-m3
make tutorial_a8_m3
```
