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

### IoT-LAB setup

**1. Clone the [<i class="fab fa-github"></i> iot-lab/iot-lab](https://github.com/iot-lab/iot-lab) repository**

We provide a way to clone Zephyr within the
[<i class="fab fa-github"></i> iot-lab/iot-lab](https://github.com/iot-lab/iot-lab)
repository. Use the following commands:

```bash
ssh <login>@saclay.iot-lab.info
<login>@saclay~$ git clone https://github.com/iot-lab/iot-lab.git
Cloning into 'iot-lab'...
...
<login>@saclay~$ cd iot-lab
```

The `make` command then shows the available targets:
```bash
<login>@saclay:~/iot-lab$ make

  Welcome to the IoT-LAB development environment setup.

  targets:
	setup-aggregation-tools
	setup-cli-tools
	setup-contiki
	setup-iot-lab.wiki
	setup-oml-plot-tools
	setup-openlab
	setup-riot
	setup-wsn430
	setup-zephyr

	pull
```

**2. Clone Zephyr**

```bash
<login>@saclay~$ make setup-zephyr
make setup-zephyr
git clone --depth https://github.com/zephyrproject-rtos/zephyr.git parts/zephyr
Cloning into 'parts/zephyr'...
...
<login>@saclay:~/iot-lab$ cd parts/zephyr
```

The Zephyr code is located in the `~/iot-lab/parts/zephyr` directory.

**3. Setup the Zephyr SDK**

The Zephyr SDK, which is required to build the firmwares, is already installed
on the SSH frontend of each IoT-LAB site. The SDK can be found in
`/opt/zephyr-sdk-<version>`. Current version is 1.0.0.


You can activate it by simply running:

```sh
$ source /opt/zephyr.source
```

This command will also update your `$PATH` variable in order to include a very
recent version of CMake (>= 3.13), which is required by the Zephyr build
system.

**Note:** This command must be done in each new shell. To have the SDK setup everytime,
the command above can be added at the end of your `~/.bashrc` file.

**4. Setup the `ZEPHYR_BASE` environment variable** 

```sh
<login>@saclay:~/iot-lab/parts/zephyr$ source zephyr-env.sh
```

**Note:** this command must also be run in each new shell. To have `ZEPHYR_BASE`
correctly setup everytime, the command above can be added at the end of
your `~/.bashrc` file (use an absolute path to zephyr-env.sh). 

### Build a Zephyr firmware

Now that everything is in place, let’s build a hello_world firmware. This
firmware is based on the sample provided in `parts/zephyr/samples/hello_world`.
The sample will be built for the nRF52DK node, which corresponds to the board
**nrf52_pca10040** in Zephyr.

```bash
<login>@saclay:~/iot-lab/parts/zephyr$ cd samples/hello_world
<login>@saclay:~/iot-lab/parts/zephyr/samples/hello_world$ mkdir build-nrf52
<login>@saclay:~/iot-lab/parts/zephyr/samples/hello_world$ cd build-nrf52
<login>@saclay:~/iot-lab/parts/zephyr/samples/hello_world/build-nrf52$ cmake -DBOARD=nrf52_pca10040 ..
<login>@saclay:~/iot-lab/parts/zephyr/samples/hello_world/build-nrf52$ make
```

The generated firmware is located in the
`zephyr/samples/hello_world/build-nrf52/zephyr` directory:

```bash
<login>@saclay:~/iot-lab/parts/zephyr/samples/hello_world/build-nrf52$ ls zephyr/zephyr.{hex,bin,elf}
zephyr/zephyr.bin  zephyr/zephyr.elf  zephyr/zephyr.hex
```

Use the `*.elf` file to flash the nodes using the IoT-LAB tools (webportal or
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
        <td>nrf52dk_pca10040</td>
    </tr>
    <tr>
        <td>nRF52840DK</td>
        <td>nrf52840dk</td>
        <td>nrf52840_pca10056</td>
    </tr>
    <tr>
        <td>nRF51DK</td>
        <td>nrf51dk</td>
        <td>nrf51_pca10028</td>
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
    </tbody>
</table>
