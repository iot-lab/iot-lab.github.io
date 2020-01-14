---
title: Zephyr
group: os
logo: logo-zephyr.png
---

## Description

The Zephyr Project, a Linux Foundation hosted Collaboration Project, is an open
source collaborative effort uniting leaders from across the industry to build a
best-in-breed small, scalable, real-time operating system (RTOS) optimized for
resource-constrained devices, across multiple architectures.

See Zephyr [Getting Started](https://docs.zephyrproject.org/latest/getting_started/getting_started.html)
on the Zephyr project website.

## Boards supported

Node type    |  Sources
-----------     |  ----------
 Arduino Zero   |  [zephyr/boards/arm/arduino_zero](https://github.com/zephyrproject-rtos/zephyr/tree/master/boards/arm/arduino_zero)
 ST-LRWAN1      |  [zephyr/boards/arm/b_l072z_lrwan1](https://github.com/zephyrproject-rtos/zephyr/tree/master/boards/arm/b_l072z_lrwan1)
 ST-IOTNODE     |  [zephyr/boards/arm/disco_l475_iot](https://github.com/zephyrproject-rtos/zephyr/tree/master/boards/arm/b_l475_iot)
 nRF52840DK     |  [zephyr/boards/arm/nrf52840_pca10056](https://github.com/zephyrproject-rtos/zephyr/tree/master/boards/arm/nrf52840_pca10056)
 NRF52DK        |  [zephyr/boards/arm/nrf52_pca10040](https://github.com/zephyrproject-rtos/zephyr/tree/master/boards/arm/nrf52_pca10040)
 nRF51DK        |  [zephyr/boards/arm/nrf51_pca10028](https://github.com/zephyrproject-rtos/zephyr/tree/master/boards/arm/nrf51_pca10028)
 FRDM-KW41Z     |  [zephyr/boards/arm/frdm_kw41z](https://github.com/zephyrproject-rtos/zephyr/tree/master/boards/arm/frdm_kw41z)
 Micro:bit      |  [zephyr/boards/arm/bbc_microbit](https://github.com/zephyrproject-rtos/zephyr/tree/master/boards/arm/bbc_microbit)

<br/>

## Use Zephyr on IoT-LAB

### Special IoT-LAB configuration

The Zephyr SDK is installed on all IoT-LAB SSH frontends in
`/opt/zephyr-sdk-<version>`. Current version is 1.0.0.

You can activate it by simply running:

```sh
$ source /opt/zephyr.source
```

This command will also update your `$PATH` variable in order to include a very
recent version of CMake (>= 3.13), which is required by the Zephyr build
system.

### Related tutorials

* [Compile a Zephyr sample for nRF52840DK nodes](https://www.iot-lab.info/tutorials/zephyr-compilation/)
