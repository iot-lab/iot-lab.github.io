---
title: Yocto
group: os
---

## Description

The Yocto Project is an open-source project which allows the creation of embedded Linux distributions. The project was announced by the Linux Foundation in 2010 and launched in March, 2011, in collaboration with 22 organizations. It uses a build system based on the [OpenEmbedded](https://www.openembedded.org/) (OE) project, which uses the BitBake tool, to construct complete Linux images. The BitBake and OE components combine together to form a reference build host, historically known as Poky. You can also build U-boot bootloader and Linux Kernel as well.


## Support for Linux boards

### Boot and filesystem

The setup for Linux nodes is to used both TFTP and NFS server and U-Boot bootloader write on the NAND flash memory (eg. A8 hardware) or SD card (eg. RPI3 hardware). The bootloader will fetch the Linux kernel from the TFTP server and the kernel will mount the root filesystem from the NFS server. For each experiment submission a reference filesystem is extracted and used by all Linux nodes of an experiment. It's a volatile filesystem that will be deleted between two experiments. It's important to understand that the same filesystem is shared between all the nodes of an experiment and if for example you install a package on one of the nodes of the experiment it will be available on all the others.


### Software support

We provide a Yocto Github repository [here](https://github.com/iot-lab/iot-lab-yocto) from which we generate custom Linux images, kernel and bootloader. We have created a **meta-iotlab** layer which contains all customizations for IoT-LAB testbed like SSH keys management or IPv6 configuration. Actually we have two boards support:


<table class="table table-striped">
    <thead>
        <tr>
            <th scope="col">Hardware</th>
            <th scope="col">Yocto version</th>
            <th scope="col">Comments</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th>IoT-LAB A8-M3</th>
            <td>Krogoth</td>
            <td>Variscite VAR-SOM-AM35 (AM3505) port: <br>
                * [U-boot 2015.01](https://github.com/iot-lab/iot-lab-uboot/tree/2015.01)<br>
                * [Linux 3.19.0](https://github.com/iot-lab/iot-lab-linux/tree/3.19.0)
            </td>
        </tr>
        <tr>
            <th>Raspberry PI3b(+)</th>
            <td>Thud (eg. branch thud_port)</td>
            <td>[Meta-raspberrypi overlay](http://git.yoctoproject.org/cgit/cgit.cgi/meta-raspberrypi):
                * Linux 4.4.13
                [U-boot](https://github.com/iot-lab/iot-lab-uboot-rpi3) is built separately
            </td>
        </tr>
    </tbody>
</table>

We provide a default list of packages (eg. Opkg package manager):

* [minimal](https://github.com/iot-lab/iot-lab-yocto/blob/master/meta-iotlab/recipes-core/images/iotlab-image.inc)
* [package groups](https://github.com/iot-lab/iot-lab-yocto/blob/master/meta-iotlab/recipes-core/packagegroups/linux-node-packagegroup.bb)

You can of course ask us to add packages or Linux kernel module support for your needs. You also have the possibility to build your own packages with our repository and install them on the nodes during the experiment.
