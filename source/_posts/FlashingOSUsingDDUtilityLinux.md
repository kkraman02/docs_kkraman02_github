---
title: Flashing OS Using DD Utility in Linux
date: 2024-06-23 01:06:14
category: Yocto
tag: Linux Commands
---

## 1. Formatting the USB stick

```bash
lsblk
```

```bash
sudo umount /dev/sdc1
```

```bash
sudo fdisk.vfat -F 32 -n USB_A /dev/sdc -I
```

## 2. Flashing the OS/Image file to the USB stick

```bash
sudo dd if=<file_name> of=/dev/sdc status=progress
```

```bash
sync
```

