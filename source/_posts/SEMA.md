---
title: SEMA
date: 2025-04-14 15:00:00
categories: SEMA
tags: SEMA
---

# 1. Introduction

Are you curious to know about what is SEMA, and how it is actually works, built? Then, here you are.



# 2. Story About the SEMA

SEMA - Smart Embedded Management Agent. It is originally developed by referring the PICMG EAPI. The agent can work with Windows as well as with Linux operating systems. By its name defines it is an agent of EC and the user to manage your board.



# 3. SEMA on Linux Host Environment

It is a combined kernel driver and user-space library/toolset for ADLINK boards.

**Kernel Modules:** A multi-function device (MFD) driver (`adl-ec` core) that spawns several platform sub-devices (watchdog, board information, non-volatile memory, backlight, voltage monitor, hardware monitor, I²C, GPIO). These drivers communicate with the board’s embedded controller (EC) via ACPI EC ports (I/O ports 0x66/0x62) to perform low-level operations.

**User-Space Library (`libsema.so`):** A C library exposing a standardized EAPI (Embedded API) interface (`eapi.h`) for applications. It wraps direct sysfs reads/writes or custom char-device ioctls to interface with the kernel drivers. This allows tasks like reading board information, controlling watchdog timers, accessing storage areas, reading voltages, controlling fans, etc.

**Utilities:** `semautil` (a command-line tool defined in `app/main.c`) processes user commands to call EAPI functions, and `wdogtest` (in `watchdogtest/watchdog-test.c`) demonstrates Linux’s generic watchdog interface usage for testing.
