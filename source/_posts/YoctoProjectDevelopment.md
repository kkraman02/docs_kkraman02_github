---
title: Yocto Project Development
date: 2026-02-28 21:00:40
categories: Yocto
tags: Yocto
---

## 1. Bitbake

Bitbake is the build engine. It reads instructions(recipes) and builds a full Linux system from source. It's commoly used in the Yocto project to create custom Linux distributions. Bitbake processes recipes, which specify how to fetch, configure, compile, and package software components, enabling reproducible and customizable builds.

## 2. Terminlology

Terminology in the Yocto Project can be a little confusing. These definitions should help you along the way:

- **OpenEmbedded**: Build system and community
- **The Yocto Project**: Umbrella project and community
- **Metadata**: Files containing information about how to build an image
- **Recipe**: File with instructions to build one or more packages
- **Layer**: Directory containing grouped metadata (start with “meta-”)
- **Board support package (BSP)**: Layer that defines how to build for board (usually maintained by vendor)
- **Distribution**: Specific implementation of Linux (kernel version, rootfs, etc.)
- **Machine**: Defines the architecture, pins, buses, BSP, etc.
- **Image**: Output of build process (bootable and executable Linux OS)

## 3. Block Diagram

![Components of Yocto](/images/YoctoProjectDevelopment.assets/YoctoBlockDiagram.png)

## 4. Must to Know Commands

### 4.1 Basic Yocto Build Setup and Commands

You must setup the build environment before building it.

```
source oe-init-build-env
```

Build an image.

```
bitbake <image-name>
```

Remove just only build ouput(artifacts).

```
bitbake -c clean <recipe-name>
```

Remove build output + sstate cache

```
bitbake -c cleansstate <recipe-name>
```

Remove build output + sstate cache + downloaded source code

```
bitbake -c cleanall <recipe-name>
```

Compiling the recipe.

```
bitbake -c complile <recipe-name>
```

Configuring the recipe.

```
bitbake -c configure <recipe-name>
```

List layers used in your current build environment.

```
bitbake-layers show-layers
```

Add new layer to you current build environment.

```
bitbake-layers add-layer <layer-name>
```

### 4.2 Package Management

List available recipes and it's version.

```
bitbake -s
```

### 4.3 Troubleshooting and Debugging

Bitbake server stuck issue.

```
pkill -f "bitbake.*server" || true
rm -f ./bitbake.lock ./cache/bitbake.lock
```

Show environment variables used for the recipe.

```
bitbake -e <recipe-name>
```

Generates dependency graph.

```
bitbake -g <recipe-name>
```

Start modifying a recipe in workspace

```
devtool modify <recipe>
```

Build a recipe from workspace

```
devtool build <recipe-name>
```

Show the status of the modified recipes

```
devtool status
```

Finalize modification into a layers

```
devtool finish <recipe-name> <layer-name>
```

wic create <wks-file> --image-name <image>
