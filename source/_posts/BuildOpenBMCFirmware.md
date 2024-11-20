---
title: Building OpenBMC Firmware
date: 2024-07-04 11:48:50
---

## 1. Setting up the Yocto build environment

```bash
sudo apt install git python3-distutils gcc g++ make file wget gawk diffstat bzip2 cpio chrpath zstd lz4 bzip2
```

### 1.1 Fork the upstream OpenBMC repo to yours

https://github.com/openbmc/openbmc -> https://github.com/kkraman02/openbmc

- Pull the forked repo in your Ubuntu system.

```bash
git clone -v https://github.com/kkraman02/openbmc
```

```bash
cd openbmc
```

- Check the available branches remote and local 

```bash
git branch -all
```



## 2. Build OpenBMC Firmware for the AST-2500 EVB board

```bash
. setup evb-ast2500
```

```bash
bitbake obmc-phosphor-image
```

- Once, the build is completed you can see the image in the following path `/openbmc/build/evb-ast2500/tmp/deploy/images/evb-ast2500`

- Check the file size

```bash
ls -lh obmc-phosphor-image-evb-ast2500*
```







## 3. Build OpenBMC Firmware for the ADLINK board

```bash
git checkout -b development
```

```bash
git push -u origin development
```

```
mkdir meta-adlink
```

```bash
cp -rv meta-aspeed/* meta-adlink/
```


