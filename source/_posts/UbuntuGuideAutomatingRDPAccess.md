---
title: A Guide Automating Remote Desktop Access by Bypassing Keyring Prompts in Ubuntu
date: 2026-01-01 10:24:20
categories: Remote Access
tags: Remote Access
---

## Are You Getting Stuck With This Issue, Don't Know Why and How to Overcome?

<div style="display: flex; flex-direction: column; align-items: center;">
    <img src="/images/UbuntuGuideAutomatingRDPAccess.assets/PasswdKeys-1.png" alt="PasswdKeys-1">
</div>


Ubuntu stores your Remote Desktop (RDP) password in an encrypted "vault" called the Keyring. When Ubuntu boots up—especially if you have Automatic Login enabled—it logs you into the desktop, but it does not unlock your "vault" because you haven't typed your password yet. Since the vault is locked, the Remote Desktop service cannot "read" your RDP password. It essentially sits in a broken state, and the Windows App on your Mac gets a "Connection Refused" or "Internal Error" because the service isn't fully authorized yet.

## Let's Fix It Permanently

### Option A: Disable Automatic Login (Most Secure)

<div style="display: flex; flex-direction: column; align-items: center;">
    <img src="/images/UbuntuGuideAutomatingRDPAccess.assets/PasswdKeys-5.png" alt="PasswdKeys-1">
</div>

1. Go to Settings > Users.
2. Click Unlock (top right).
3. Toggle Automatic Login to OFF.

### Option B: Set a "Blank" Password for the Keyring (Most Convenient and Preferred One)

1. On Ubuntu, open the app called Passwords and Keys.

   <div style="display: flex; flex-direction: column; align-items: center;">
       <img src="/images/UbuntuGuideAutomatingRDPAccess.assets/PasswdKeys-2.png" alt="PasswdKeys-1">
   </div>

2. Right-click on the folder named **Default keyring** and **Login** (under "Passwords" on the left).

3. Select Change Password.

   <div style="display: flex; flex-direction: column; align-items: center;">
       <img src="/images/UbuntuGuideAutomatingRDPAccess.assets/PasswdKeys-3.png" alt="PasswdKeys-1">
   </div>

4. Enter your Current Password.

5. For the New Password, leave it completely blank and click Continue.

6. Confirm that you want to use "Unsafe Storage."

Try to connect again, this time you will definitely will get rid of that issue.
