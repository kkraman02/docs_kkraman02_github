---
title: Compressing &  Decompressing Files
date: 2024-06-23 01:27:22
---

Decompressing .tar.gz and .tar.xz files

```bash
sudo apt install tar
```

```bash
tar -xvf <file_name>.tar.gz
```

Decompressing .zst files

```bash
sudo apt install zstd
```

```bash
zst -d <file_name>.zst
```