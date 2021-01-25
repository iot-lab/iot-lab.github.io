---
title: Zephyr
group: os
---

## Description

The Zephyr Project, a Linux Foundation hosted Collaboration Project, is an open
source collaborative effort uniting leaders from across the industry to build a
best-in-breed small, scalable, real-time operating system (RTOS) optimized for
resource-constrained devices, across multiple architectures.

See Zephyr [Getting Started](https://docs.zephyrproject.org/latest/getting_started/getting_started.html)
on the Zephyr project website.

## Use Zephyr on IoT-LAB

### Get Zephyr

The Zephyr [west meta-tool](https://docs.zephyrproject.org/latest/guides/west/index.html)
is already installed on the SSH frontend, use it to initialize the zephyrproject workspace:

```bash
ssh <login>@saclay.iot-lab.info
<login>@saclay~$ west init ~/zephyrproject
<login>@saclay~$ cd ~/zephyrproject
<login>@saclay:~/zephyrproject$ west update cmsis hal_nordic hal_stm32 hal_atmel
```

This step is the same as the [Get Zephyr step](https://docs.zephyrproject.org/latest/getting_started/index.html#get-zephyr-and-install-python-dependencies)
of the Zephyr [Getting started documentation](https://docs.zephyrproject.org/latest/getting_started/index.html) page.

### Build a Zephyr firmware

Now that everything is in place, let’s build a hello_world firmware. This
firmware is based on the sample provided in `zephyrproject/zephyr/samples/hello_world`.
The sample will be built for the nRF52DK node, which corresponds to the board
**nrf52dk_nrf52832** in Zephyr. The west meta-tool can also be used to build
this application:

```bash
<login>@saclay:~/zephyrproject$ cd zephyr
<login>@saclay:~/zephyrproject/zephyr$ west build -p auto -b nrf52dk_nrf52832 samples/hello_world
```

The generated firmware is located in the
`~/zephyrproject/zephyr/build/zephyr` directory:

```bash
<login>@saclay:~/zephyrproject/zephyr$ ls build/zephyr/zephyr.{hex,bin,elf}
build/zephyr/zephyr.bin  build/zephyr/zephyr.elf  build/zephyr/zephyr.hex
```

Use the `*.elf` or `*.bin` file to flash the nodes using the IoT-LAB tools (webportal or
cli-tools).

### IoT-LAB/Zephyr board name mapping


<table class="table table-striped">
    <thead>
        <tr>
            <td><b>Board name</b></td>
            <td><b>IoT-LAB ID</b></td>
            <td><b>Zephyr name</b></td>
        </tr>
    </thead>
    <tbody>
    <tr>
        <td>nRF52DK</td>
        <td>nrf52dk</td>
        <td>nrf52dk_nrf52832</td>
    </tr>
    <tr>
        <td>nRF52840DK</td>
        <td>nrf52840dk</td>
        <td>nrf52840dk_nrf52840</td>
    </tr>
    <tr>
        <td>nRF52832-MDK</td>
        <td>nrf52832-mdk</td>
        <td>nrf52832_mdk</td>
    </tr>
    <tr>
        <td>nRF52840-MDK</td>
        <td>nrf52840-mdk</td>
        <td>nrf52840_mdk</td>
    </tr>
    <tr>
        <td>nRF51DK</td>
        <td>nrf51dk</td>
        <td>nrf51dk_nrf51422</td>
    </tr>
    <tr>
        <td>BBC micro:bit</td>
        <td>microbit</td>
        <td>bbc_microbit</td>
    </tr>
    <tr>
        <td>NXP FRDM-KW41Z</td>
        <td>frdm-kw41z</td>
        <td>frdm_kw41z</td>
    </tr>
    <tr>
        <td>Arduino Zero</td>
        <td>arduino-zero</td>
        <td>arduino_zero</td>
    </tr>
    <tr>
        <td>ST B-L072Z-LRWAN1</td>
        <td>st-lrwan1</td>
        <td>b_l072z_lrwan1</td>
    </tr>
    <tr>
        <td>ST B-L475E-IOT01A</td>
        <td>st-iotnode</td>
        <td>disco_l475_iot1</td>
    </tr>
    <tr>
        <td>Decawave DWM1001</td>
        <td>dwm1001</td>
        <td>decawave_dwm1001_dev</td>
    </tr>
    </tbody>
</table>
