---
title: Remotely Accessing Office PC from Home PC Using Tailscale
date: 2025-12-31 11:24:26
categories: Remote Access
tags: Remote Access
---

## Purpose

In the embedded system working field often may need to use multiple PCs for development or debugging purpose. We often use AnyDesk for the remote desktop access. But for console remote access we must be in the same network or we need to use VPN to access the device console. In this article we're going to see how can we access Device-A from Device-B by different network using TailScale software at zero cost.

Let's consider this scenario, Device-A is running Ubuntu OS and it's located in your office. Device-B is running Mac OS and you will carry this whereever you go and often connected to different network.

## Setting Up a Remote Console Access System

### Device-A Running Ubuntu OS Connected to the Office Network

1. Install SSH server.

```sh
$ sudo apt update
$ sudo apt install openssh-server -y
$ sudo systemctl enable ssh
$ sudo systemctl start ssh
$ sudo systemctl status ssh
```

2. Install Tailscale.

```sh
$ curl -fsSL https://tailscale.com/install.sh | sh
$ sudo tailscale up
```

3. It will provide a link in the terminal. Open it in your browser, log in (using Google, Microsoft, or GitHub), and your Ubuntu machine is now part of your private network.

### Device-B Running Mac OS Connected to the Home or Coffee Shop Network

1. Install SSH server.

```sh
$ brew update
$ brew install openssh
```

2. Install Tailscale from the App Store. Open the app & Log in using the same account you used for Device-A.

3. Install Tailscale app on your Mac (in the top menu bar), you will see your Ubuntu machine listed with its own IP address (it usually starts with 100.x.y.z). Copy that IP address.

4. You can also manage devices connected to your Tailscale by clicking the below link,
   https://login.tailscale.com/admin/machines

<div style="display: flex; flex-direction: column; align-items: center;">
    <img src="/images/RemotelyAccessingOfficePCfromHomePC.assets/TailscaleWebManager.png" alt="TailscaleWebManager">
</div>
5. Connect via SSH: Now, from your MacBook terminal, simply type: ssh username@100.x.y.z (Replace username with your Ubuntu login and 100.x.y.z with the Tailscale IP you just copied).

<div style="display: flex; flex-direction: column; align-items: center;">
    <img src="/images/RemotelyAccessingOfficePCfromHomePC.assets/SSHConsole.png" alt="TailscaleWebManager">
</div>

## Setting Up a Remote Desktop Access System

You can also use the native Ubuntu Remote Desktop features, which can be combined with the Tailscale method for a full graphical remote experience.

### Device-A Running Ubuntu OS Connected to the Office Network

<div style="display: flex; flex-direction: column; align-items: center;">
    <img src="/images/RemotelyAccessingOfficePCfromHomePC.assets/UbuntuSharing-1.png" alt="TailscaleWebManager">
</div>
</br>

<div style="display: flex; flex-direction: column; align-items: center;">
    <img src="/images/RemotelyAccessingOfficePCfromHomePC.assets/UbuntuSharing-2.png" alt="TailscaleWebManager">
</div>

### Device-B Running Mac OS Connected to the Home Network

Install Windows App(previously it named as Windows Remote Desktop) in Device-B and enter Device-A's Tailscale IP. Just simply follow steps as I mentioned in the following screenshots so you will get into to desktop quickly.

<div style="display: flex; flex-direction: column; align-items: center;">
    <img src="/images/RemotelyAccessingOfficePCfromHomePC.assets/WindowsApp-1.png" alt="TailscaleWebManager">
</div>

</br>

<div style="display: flex; flex-direction: column; align-items: center;">
    <img src="/images/RemotelyAccessingOfficePCfromHomePC.assets/WindowsApp-2.png" alt="TailscaleWebManager">
</div>

</br>

<div style="display: flex; flex-direction: column; align-items: center;">
    <img src="/images/RemotelyAccessingOfficePCfromHomePC.assets/WindowsApp-3.png" alt="TailscaleWebManager">
</div>

</br>

<div style="display: flex; flex-direction: column; align-items: center;">
    <img src="/images/RemotelyAccessingOfficePCfromHomePC.assets/WindowsApp-4.png" alt="TailscaleWebManager">
</div>

</br>

<div style="display: flex; flex-direction: column; align-items: center;">
    <img src="/images/RemotelyAccessingOfficePCfromHomePC.assets/WindowsApp-5.png" alt="TailscaleWebManager">
</div>

</br>

<div style="display: flex; flex-direction: column; align-items: center;">
    <img src="/images/RemotelyAccessingOfficePCfromHomePC.assets/WindowsApp-6.png" alt="TailscaleWebManager">
</div>

</br>

<div style="display: flex; flex-direction: column; align-items: center;">
    <img src="/images/RemotelyAccessingOfficePCfromHomePC.assets/WindowsApp-7.png" alt="TailscaleWebManager">
</div>

</br>

<div style="display: flex; flex-direction: column; align-items: center;">
    <img src="/images/RemotelyAccessingOfficePCfromHomePC.assets/WindowsApp-8.png" alt="TailscaleWebManager">
</div>

</br>

<div style="display: flex; flex-direction: column; align-items: center;">
    <img src="/images/RemotelyAccessingOfficePCfromHomePC.assets/WindowsApp-9.png" alt="TailscaleWebManager">
</div>

</br>

<div style="display: flex; flex-direction: column; align-items: center;">
    <img src="/images/RemotelyAccessingOfficePCfromHomePC.assets/WindowsApp-10.png" alt="TailscaleWebManager">
</div>

## Reference

1. https://tailscale.com/
2. https://www.openssh.org/