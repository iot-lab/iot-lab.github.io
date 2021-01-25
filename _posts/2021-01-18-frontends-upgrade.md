---
title: SSH frontends upgrade
---
![]({{ '/assets/images/posts/' | relative_url }}fit-logo.png){: .img-fluid }

Last Monday, the 18th of January, 2021, all SSH frontends of the IoT-LAB testbed were migrated to the
latest Debian stable version, [Buster](https://www.debian.org/releases/buster/).
This migration came with the update of several softwares preinstalled on the frontends.

If you have problems with the new installed versions of tools and toolchains,
don't hesitate to send an email to `admin@iot-lab.info` or open an issue
on [https://github.com/iot-lab/iot-lab/issues](https://github.com/iot-lab/iot-lab/issues).

Here is the list of these changes:

### IoT-LAB tools

As announced in December 2020, all the IoT-LAB tools based on Python were installed to
their latest version and **for Python 3 only**.
Since Python 2 has reached his end-of-life in early 2020, it came more and more difficult for
the IoT-LAB team to continue maintaining them in the long term. If you still have code
that is not yet Python 3 compatible, we strongly encourage you to migrate it to Python 3.

Note that the Python 3 version installed on the SSH frontends is now **3.7.3**.

The table below lists the new versions of the IoT-LAB tools installed:

<table class="table table-striped">
    <thead>
        <tr>
            <td><b>IoT-LAB Tools</b></td>
            <td><b>version</b></td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><a href="https://github.com/iot-lab/cli-tools">cli-tools</a></td>
            <td>3.2.1</td>
        </tr>
        <tr>
            <td><a href="https://github.com/iot-lab/ssh-cli-tools">ssh-cli-tools</a></td>
            <td>1.0.0</td>
        </tr>
        <tr>
            <td><a href="https://github.com/iot-lab/aggregation-tools">aggregation-tools</a></td>
            <td>2.0.0</td>
        </tr>
        <tr>
            <td><a href="https://github.com/iot-lab/oml-plot-tools">oml-plot-tools</a></td>
            <td>0.7.1</td>
        </tr>
    </tbody>
</table>

### ARM GCC toolchain

The default ARM GCC toolchain is still in 4.9 version but a newer version, **9.3.1**
is installed on each frontend in `/opt/gcc-arm-none-eabi-9-2020-q2-update/`.

### Zephyr

Version 0.12.1 of the Zephyr SDK is now installed in `opt/zephyr-sdk-0.12.1`.
The way to build Zephyr firmwares on IoT-LAB has also been updated: now the
[west meta-tool](https://docs.zephyrproject.org/latest/guides/west/index.html)
is installed on the SSH frontends. `west` can be used to initialize a zephyr workspace,
download the required hals and build a Zephyr firmware.
The [Zephyr documentation page](https://www.iot-lab.info/docs/os/zephyr) was
updated following this change.
