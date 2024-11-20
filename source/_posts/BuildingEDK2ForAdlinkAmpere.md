---
title: Building EDK2 for Adlink Ampere
date: 2024-10-16 08:40:44
tags: EDK2
category: EDK2
---

## Setup the Build Environment

1. Check Cross-Compiler Installation

    ```bash
    sudo apt update && sudo apt upgrade -y
    sudo apt install gcc-aarch64-linux-gnu
    ```

2. Specify the Correct GCC Toolchain

   You may need to explicitly tell the build system to use the correct cross-compiler. Set the `GCC5_AARCH64_PREFIX` environment variable to point to the AArch64 GCC compiler:

   ```bash
   echo "export GCC5_AARCH64_PREFIX=aarch64-linux-gnu-" >> ~/.bashrc
   source ~/.bashrc
   ```



## Obtaining Source Code

1. Create a new folder (directory) on your local development machine for use as your workspace. This example uses /work/git/tianocore, modify as appropriate for your needs.

   ```bash
   echo 'export WORKSPACE=/media/raman/development/tianocore' >> ~/.bashrc
   mkdir -p $WORKSPACE
   cd $WORKSPACE
   ```

2. Into that folder, clone:

   - [edk2](https://github.com/tianocore/edk2)

   - [edk2-platforms](https://github.com/tianocore/edk2-platforms)

   - [edk2-non-osi](https://github.com/tianocore/edk2-non-osi) (if building platforms that need it)

   ```bash
   git clone https://github.com/tianocore/edk2.git
   cd edk2
   git submodule update --init
   cd ..
   git clone https://github.com/tianocore/edk2-platforms.git
   cd edk2-platforms
   git submodule update --init
   cd ..
   git clone https://github.com/tianocore/edk2-non-osi.git
   git clone git@github.com:ADLINK/edk2_aadp.git
   cd edk2_aadp
   git submodule update --init
   git clone git@github.com:ADLINK/edk2_adlink-ampere-altra.git
   ```

3. Set up a **PACKAGES_PATH** to point to the locations of these three repositories:

   ```bash
   echo 'export PACKAGES_PATH=$PWD/edk2:$PWD/edk2-platforms:$PWD/edk2-non-osi:$PWD/edk2_aadp:$PWD/edk2_adlink-ampere-altra:$PWD/edk2_aadp/edk2-platforms:$PWD/edk2_aadp/adlink-platforms:$PWD/edk2_aadp/OpenPlatformPkg:$PWD/edk2-platforms/Features/Intel/Debugging:$PWD/edk2_aadp/edk2-platforms/Features/Intel:$PWD/edk2_aadp/edk2' >> ~/.bashrc
   
   # echo 'export PACKAGES_PATH=$PWD/edk2:$PWD/edk2-platforms:$PWD/edk2-non-osi' >> ~/.bashrc
   source ~/.bashrc
   ```

4. Build the environment

   ```bash
   . edk2/edksetup.sh
   ```

5. Build BaseTools

   ```bash
   make -C edk2/BaseTools TOOLCHAIN=GCC5
   ```



## Building the UEFI image

Copy the ManageabilityPkg files into the right directory.

```bash
cp -rfv /media/raman/development/tianocore/edk2-platforms/Features/ManageabilityPkg /media/raman/development/tianocore/edk2-platforms/
```

Building EDK2 FD with the following command:

```bash
cd edk2-platforms
build -a AARCH64 -t GCC5 -b RELEASE -D SECURE_BOOT_ENABLE -p Platform/Ampere/ComHpcAltPkg/ComHpcAlt.dsc
# build -a AARCH64 -t GCC5 -b RELEASE -D SECURE_BOOT_ENABLE -p Platform/Ampere/JadePkg/Jade.dsc
# cd edk2-platforms && build -a AARCH64 -t GCC5 -b RELEASE -D SECURE_BOOT_ENABLE -p Platform/Ampere/JadePkg/ComHpcAlt.dsc
```

**Notes**: Please refer to [LinuxBoot.md](https://github.com/AmpereComputing/edk2-ampere-tools/blob/master/LinuxBoot.md) for building EDK2+LinuxBoot FD.

The resulting image will be at

```bash
edk2-platforms/Build/Jade/RELEASE_GCC5/FV/BL33_JADE_UEFI.fd
```

We will be using edk2-platforms/BUILDS/jade_tianocore_atf for the final artifacts.

```bash
cd edk2-platforms
mkdir -p BUILDS/jade_tianocore_atf
```



## Signing the Image

You need to download and install `cert_create` and `fiptool` from Arm Trusted Firmware.

```bash
cd ..
git clone --depth 1 https://github.com/ARM-software/arm-trusted-firmware.git
cd arm-trusted-firmware
make -C tools/cert_create
make -C tools/fiptool
```

Set up your $PATH to include cert_create and fiptool from above.

Perform the following to sign the image:

```bash
cd edk2-platforms
sudo apt install arm-trusted-firmware-tools
cert_create -n --ntfw-nvctr 0 --key-alg rsa --nt-fw-key edk2-platforms/Platform/Ampere/JadePkg/TestKeys/Dbb_AmpereTest.priv.pem --nt-fw-cert BUILDS/jade_tianocore_atf/jade_tianocore.fd.crt --nt-fw /media/raman/development/tianocore/Build/Jade/RELEASE_GCC5/FV/BL33_JADE_UEFI.fd
fiptool create --nt-fw-cert /media/raman/development/tianocore/edk2-platforms/BUILDS/jade_tianocore_atf/jade_tianocore.fd.crt --nt-fw /media/raman/development/tianocore/Build/Jade/RELEASE_GCC5/FV/BL33_JADE_UEFI.fd /media/raman/development/tianocore/edk2-platforms/BUILDS/jade_tianocore_atf/jade_tianocore.fip.signed
```



## Integrating Board Setting and Ampere's Arm Trusted Firmware (ATF)

You need to obtain Ampere ATF image and Board Setting file compatible with this vesion of Ampere EDK2 in order to build a final firmware image.

Contact [developer@amperecomputing.com](mailto:developer@amperecomputing.com) for information.

```bash
git clone https://github.com/ADLINK/AmpereAltra-ATF-SCP
git cp /media/raman/development/tianocore/AmpereAltra-ATF-SCP/atf/* /media/raman/development/tianocore/edk2-platforms/BUILDS/jade_tianocore_atf
git cp /media/raman/development/tianocore/AmpereAltra-ATF-SCP/board_settings/* /media/raman/development/tianocore/edk2-platforms/BUILDS/jade_tianocore_atf
git cp /media/raman/development/tianocore/AmpereAltra-ATF-SCP/scp/* /media/raman/development/tianocore/edk2-platforms/BUILDS/jade_tianocore_atf
```



## Build integrated UEFI + Board Setting + ATF image

Generating the final image with the following commands:

```bash
dd bs=1024 count=2048 if=/dev/zero | tr "\000" "\377" > BUILDS/jade_tianocore_atf/jade_tianocore_atf.img
dd bs=1024 conv=notrunc if=BUILDS/jade_tianocore_atf/altra_atf_signed_2.10.20221028.slim of=BUILDS/jade_tianocore_atf/jade_tianocore_atf.img
dd bs=1024 seek=1984 conv=notrunc if=BUILDS/jade_tianocore_atf/jade_board_setting_2.10.20221028.bin of=BUILDS/jade_tianocore_atf/jade_tianocore_atf.img
dd bs=1024 seek=2048 if=BUILDS/jade_tianocore_atf/jade_tianocore.fip.signed of=BUILDS/jade_tianocore_atf/jade_tianocore_atf.img
```

Build Tianocore Capsule.

```bash
build -a AARCH64 -t GCC5 -b RELEASE -p Platform/Ampere/JadePkg/JadeCapsule.dsc -D UEFI_ATF_IMAGE=BUILDS/jade_tianocore_atf/altra_atf_signed_2.10.20221028.slim -D SCP_IMAGE=BUILDS/jade_tianocore_atf/altra_scp_signed_2.10.20221028.slim
cp /media/raman/development/tianocore/Build/Jade/RELEASE_GCC5/FV/JADEUEFIATFFIRMWAREUPDATECAPSULEFMPPKCS7.Cap BUILDS/jade_tianocore_atf/jade_tianocore_atf.cap
cp /media/raman/development/tianocore/Build/Jade/RELEASE_GCC5/FV/JADESCPFIRMWAREUPDATECAPSULEFMPPKCS7.Cap BUILDS/jade_tianocore_atf/jade_scp.cap
```



## Bonus Tip(Automate the build using script)

You can automate the build using the script file from the edk2-ampere-tools.

```bash
sudo apt install efitools gnu-efi
cd /media/raman/development/tianocore/edk2-ampere-tools/efitools
make
cd ~/media/raman/development/tianocore/edk2-ampere-tools
./edk2-build.sh -b RELEASE Jade --atf-image /media/raman/development/tianocore/edk2-platforms/BUILDS/jade_tianocore_atf/altra_atf_signed_2.10.20221028.slim
```

