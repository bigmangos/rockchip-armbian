# Armbian for Rockchip Boxes

Currently `Rock5b` firmware is supported, using [unifreq's](https://github.com/unifreq) enhanced version of `bootloader` and the [latest kernel](https://github.com/unifreq/linux-rock5b), The system is modified to dual partition, and related applications and services in [amlogic-s9xxx-armbian](https://github.com/ophub/amlogic-s9xxx-armbian) are added. Support installation and use in `TF/USB/eMMC/NVME`.

The latest version of the Armbian firmware can be downloaded in [Releases](https://github.com/ophub/rockchip-armbian/releases).

## Install to EMMC and update instructions

Write the IMG file to the USB/TF hard disk through software such as [Rufus](https://rufus.ie/) or [balenaEtcher](https://www.balena.io/etcher/). Insert the USB/TF hard disk into the device.

- ### Install Armbian to EMMC

If you need `NVME` or `USB` to boot, you must first flash the [spi bootloader](build-armbian/u-boot/rock5b).

Login in to armbian (default user: root, default password: 1234) → Upload the armbian image → input command:

```yaml
dd if=armbian.img  of=/dev/<your_device_name>  bs=1M conv=fsync
```

- ### Update Armbian Kernel

Login in to armbian → input command:

```yaml
# Run as root user (sudo -i)
# If no parameter is specified, it will update to the latest version.
armbian-update
```

If there is a set of kernel files in the current directory, it will be updated with the kernel in the current directory (The 4 kernel files required for the update are `header-xxx.tar.gz`, `boot-xxx.tar.gz`, `dtb-rockchip-xxx.tar.gz`, `modules-xxx.tar.gz`. Other kernel files are not required. If they exist at the same time, it will not affect the update. The system can accurately identify the required kernel files). If there is no kernel file in the current directory, it will query and download the latest kernel of the same series from the server for update. You can also query the [Optional Kernel](https://github.com/ophub/kernel/tree/main/pub/rock5b) version and update the specified version: `armbian-update 5.10.100`. The optional kernel supported by the device can be freely updated, such as from 5.10.100 kernel to 5.15.50 kernel.

- ### More instructions for use

To update all service scripts in the local system to the latest version, you can login in to armbian → input command:

```yaml
armbian-sync
```

For more services, please check the instructions in the [amlogic-s9xxx-armbian](https://github.com/ophub/amlogic-s9xxx-armbian) repository. In the use of Armbian, please refer to [armbian-docs](https://github.com/ophub/amlogic-s9xxx-armbian/tree/main/build-armbian/armbian-docs) for some common problems that may be encountered.

## Links

- [armbian](https://github.com/armbian/build)
- [Armbian for Amlogic](https://github.com/ophub/amlogic-s9xxx-armbian)
- [unifreq](https://github.com/unifreq)
- [kernel.org](https://kernel.org)

## License

The rockchip-armbian © OPHUB is licensed under [GPL-2.0](https://github.com/ophub/rockchip-armbian/blob/main/LICENSE)

