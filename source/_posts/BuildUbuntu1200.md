---
title: Build Ubuntu OS for LEC-MTK-1200
comment: true
category: MTK-1200
tag: MTK-1200
---
## Download Ubuntu OS Images and Boot Firmware
Visit https://ubuntu.com/download/mediatek-genio and download the following two archives to your host PC:

> - The Ubuntu OS image (Desktop or Server) of your choice. The following steps apply to both Ubuntu Desktop and Ubuntu Server.
> - The boot firmware for your Genio EVK

Extract the Ubuntu image first, and then extract the boot firmware into the same directory. On Ubuntu host PC this can be done with the following commands:

```bash
cd ~/Downloads
```

```bash
tar -xJvf genio-classic-desktop-2204-x01-20231005-133.tar.xz
```

```bash
tar -xzvf ubuntu-boot-firmware-genio-1200-evk-v23.1.3.tar.gz
```

```bash
mkdir ubuntu_adlink_mtk
```

Copy the following files from the Yocto image to the ubuntu_adlink_mtk.

- bl2.img

- bootassets.vfat
- fip-mt8195.bin -> rename it as fip.bin
- lk.bin
- u-boot-env.bin
- u-boot-initial-env-lec-mtk-i1200-ufs-2022.10+gitAUTOINC+c58839fb0a-r0 -> rename it as u-boot-initial-env

Copy the following files from baoshan-classic-desktop-xxxx to ubuntu_adlink_mtk

- ubuntu.img

- ubuntu.json

- firmware.vfat



## Unzip the Firmware File

Create a mount point (directory):

```bash
sudo mkdir /mnt/vfat
```

Mount the .vfat file:

```bash
sudo mount -o loop firmware.vfat /mnt/vfat
```

This will mount the `.vfat` image to the `/mnt/vfat` directory, allowing you to view and modify its contents.

Create a directory called `lec-mtk-i1200-ufs` under `/mnt/vfat/FIRMWARE/mediatek/`.

Put all the Yocto device tree files (`/build/tmp/deploy/images/lec-mtk-1200-ufs/devicetree/`) into this directory (`/mnt/vfat/FIRMWARE/mediatek/lec-mtk-i1200-ufs/`).

Also, the `lec-mtk-i1200-ufs--5.15.42+git0+a46a21ed7e-r0-lec-mtk-i1200-ufs-20241015034349.dtb` file and rename it as `lec-mtk-i1200-ufs.dtb`.

## Repack (Unmount) the `.vfat` file:

After modifying the files in the mounted directory, unmount the image and repack it.

Unmount the `.vfat` file:

```bash
sudo umount /mnt/vfat
```

