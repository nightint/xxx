# Akeana SDK layer for OpenEmbedded/Yocto

[**Description**](#Description)

[**Prerequisites**](#Prerequisites)

[**Dependencies**](#Dependencies)

[**Build targets**](#Build-targets)

[**Build artifacts**](#Build-artifacts)

[**Running in QEMU**](#Running-in-QEMU)

[**FAQ**](#FAQ)

<a name="Description"></a>
# Description

The Akeana SDK uses the OpenEmbedded/Yocto framework to build customizable images including:
* bootloader binaries (OpenSBI, U-Boot, U-Boot SPL)
* Device Tree Binary (DTB);
* Linux kernel images
* ramdisk root filesystem

<a name="Prerequisites"></a>
# Prerequisites

* [Docker](https://docs.docker.com/engine/install/)

* [kas](https://kas.readthedocs.io/en/latest/userguide.html#dependencies-installation)

<a name="Dependencies"></a>
# Dependencies

This layer depends on:
* https://git.yoctoproject.org/git/poky
* https://github.com/unnecessary-abstraction/meta-linux-mainline

<a name="Build-targets"></a>
# Build targets

This layer provides a customizable image based on Ubuntu 24.04.1 LTS (Noble Numbat) for FPGA and QEMU.

To build an image use the following command:
```
kas-container build ./meta-akeana/kas/shasta-ubuntu-${MACHINE}.yml
```
where `MACHINE` can be:
- `fpga`
- `qemu`

To include additional packages in the image add the package name(s) to `APT_EXTRA_PACKAGES` in kas/apt-extra.yml and use the following command:
```
kas-container build ./meta-akeana/kas/shasta-ubuntu-${MACHINE}.yml:meta-akeana/kas/apt-extra.yml
```

<a name="Build-artifacts"></a>
# Build artifacts

Build artifacts maybe found in:
`$BUILDDIR/tmp/deploy/images/shasta-${MACHINE}/fw_payload.elf`

<a name="Running-in-QEMU"></a>
# Running in QEMU

To run the OpenEmbedded/Yocto framework provided wrapper for QEMU use the following command:

```
kas-container shell meta-akeana/kas/shasta-ubuntu-qemu.yml -c "runqemu nographic slirp"
```

<a name="FAQ"></a>
# FAQ

Q1 : Where are the Devicetree Memory bindings?

A : For FPGA they are in `recipes-bsp/device-tree/files/shasta-fpga.dts` and for QEMU they are in `recipes-bsp/device-tree/files/shasta-fpga.dts`.

Q2 : Where are the Devicetree RISC-V CPU Bindings?

A : They are in recipes-bsp/device-tree/files/soc.dtsi b/recipes-bsp/device-tree/files/soc.dtsi`.
