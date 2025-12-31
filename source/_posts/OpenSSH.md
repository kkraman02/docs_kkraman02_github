---
title: SSH (Secured Shell)
date: 2025-03-26 21:14:30
categories: Remote Access
tags: Remote Access
---

## Definition

SSH is stands for Secured Shell. It is a network protocol that is used to send the commands in a secure way to the host from the client.



## On the SSH Server

For Debian-based system:

```bash
sudo apt update
sudo apt install openssh-server -y
sudo systemctl enable ssh
sudo systemctl start ssh
sudo systemctl status ssh
```



## On the SSH Client

```bash
sudo apt update
sudo apt install openssh-client -y
```



##  Test SSH Connection from Client

```bash
ssh username@server_ip_address
```



## Transferring the files over SCP (Secured Copy Protocol)

Copy file from local to remote.

```bash
scp /path/to/local/file username@remote_host:/path/to/remote/destination
# Ex: scp myfile.txt user@192.168.1.100:/home/user/
```

Copy file from remote to local.

```bash
scp username@remote_host:/path/to/remote/file /path/to/local/destination
# Ex: scp user@192.168.1.100:/home/user/myfile.txt ./
```



## Transferring the files over rsync (Remote Sync)

Copy file from local to remote.

```bash
rsync -avz /path/to/local/file username@remote_host:/path/to/remote/destination
# Ex: rsync -avz myfile.txt user@192.168.1.100:/home/user/
```

Copy file from remote to local.

```bash
rsync -avz username@remote_host:/path/to/remote/file /path/to/local/destination
# Ex: rsync -avz user@192.168.1.100:/home/user/myfile.txt ./
```

**Options Breakdown**

- `-a`: archive mode (preserves permissions, symbolic links, etc.)
- `-v`: verbose
- `-z`: compress file data during the transfer
