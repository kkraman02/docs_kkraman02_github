---
title: Mount and Unmount a .wic Yocto File in Ubuntu
date: 2025-02-17 11:00:00
comment: false
category: Yocto
tag: Linux Commands
---

When building a Yocto BSP for NXP products, the generated image file is in **.wic** format. Sharing this image with others can be a hassle because they need to flash it onto an SD card just to inspect its contents. Instead, we can mount the `.wic` file directly on our system without flashing.

## 1. Mounting a .wic File

### Step 1: Attach the .wic File as a Loop Device

Use `losetup` to associate the `.wic` file with a loop device.

```bash
sudo losetup -Pf my-image.wic
```

The `-P` option automatically detects partitions within the image.

### Step 2: Verify the Assigned Loop Device

Check which loop device (`/dev/loopX`) has been assigned:

```bash
sudo losetup -a
```

This will list all loop devices. If your `.wic` file has multiple partitions, they will be labeled as `/dev/loopXp1`, `/dev/loopXp2`, etc.

### Step 3: Identify Partitions in the .wic File

To see the partitions inside the `.wic` image, run:

```bash
sudo fdisk -l /dev/loopX
```

This will list partition details such as their sizes and offsets.

### Step 4: Mount the Partitions

Mount the partitions manually:

```bash
sudo mount /dev/loopXp1 /mnt/wic-rootfs
```

Change `/dev/loopXp1` to the actual partition you need to inspect.

------

## 2. Unmounting a .wic File

### Step 1: Find Mounted Partitions

Identify mounted partitions related to the `.wic` file:

```bash
mount | grep loop
```

### Step 2: Unmount Partitions

Unmount each mounted partition:

```bash
sudo umount /mnt/wic-rootfs
```

Or if multiple partitions were mounted, unmount them one by one.

### Step 3: Detach the Loop Device

Once all partitions are unmounted, remove the loop device association:

```bash
sudo losetup -d /dev/loopX
```

------

## 3. Verify Removal

Ensure the loop device is no longer active:

```bash
losetup -a
```

If `/dev/loopX` is no longer listed, the `.wic` file has been successfully detached.

------

Now you can inspect `.wic` files without needing to flash them onto an SD card!
