---
layout: openbmc
title: OpenBMC Development
date: 2024-06-03 11:45:03
tags: openbmc
---
## 1. Setting up the system for the OpenBMC development

- Install the following dependencies

  ```bash
  sudo apt install git python3-distutils gcc g++ make file wget gawk diffstat bzip2 cpio chrpath zstd lz4 bzip2
  ```
- Download the source code

  ```bash
  git clone https://github.com/bcran/openbmc
  cd openbmc
  ```
- Choose your machine

  ```bash
  . setup comhpcalt
  ```
- start to buid the firmware

  ```bash
  bitbake obmc-phosphor-image
  ```
- Once the build is completed, the BMC image will be created and stored in this location `tmp/deploy/images/<platform>/`

  - `obmc-phosphor-image-<platform>-<datetime>.static.mtd` and `obmc-phosphor-image-<platform>-<datetime>.static.mtd.tar`
