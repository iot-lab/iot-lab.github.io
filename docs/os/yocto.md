---
title: Yocto
group: os
---

## Description

The Yocto Project is an open-source project which allows the creation of embedded Linux distributions. The project was announced by the Linux Foundation in 2010 and launched in March, 2011, in collaboration with 22 organizations. It uses a build system based on the [OpenEmbedded](https://www.openembedded.org/) (OE) project, which uses the BitBake tool, to construct complete Linux images. The BitBake and OE components combine together to form a reference build host, historically known as Poky. You can also build U-boot bootloader and Linux Kernel as well.


## Support for IoT-LAB boards

We provide a custom U-boot bootloader, Linux kernel and image for IoT-LAB A8 and RPI3b(+) nodes based on Yocto. You can view our Github repository [here](https://github.com/iot-lab/iot-lab-yocto). Due to hardware port limitation the Yocto version used for IoT-LAB A8 nodes is **Krogoth**. You can also find a newer **Thud** version dedicated to the support of RPI3b+ models (eg. thud_port branch). These images are intended for Linux nodes hosted on the IoT-LAB testbed. Indeed they take into account specificities such as read-only filesystem, IPv6 configuration and provide a default list of packages (eg. Opkg package manager). You can of course ask us to add packages or Linux kernel module support for your needs. You also have the possibility to build your own packages with our repository and install them on the nodes during the experiment.