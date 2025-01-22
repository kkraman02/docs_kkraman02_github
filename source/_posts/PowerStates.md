---
title: CPU Power States
date: 2025-01-22 17:02:10
comment: true
category: CPU
tag: CPU
---

## Definition

CPU power states refer to the operating modes defined by the Advanced Configuration and Power Interface (ACPI) specification. These states control the power consumption of a system or its components, allowing it to conserve energy when idle or under low load conditions.

## Types of Power States

ACPI defines several power states for the **entire system** and individual **components**, such as CPUs. The two primary categories are:

### 1. System Power States (S-States)

| **State** | **Name**                 | **Description**                                              |
| --------- | ------------------------ | ------------------------------------------------------------ |
| **S0**    | Working                  | The system is fully operational. The CPU, memory, and peripherals are powered and active. |
| **S1**    | Sleep (Low Wake Latency) | A low-power state where the CPU halts but remains in a low-power mode. Memory is still powered for context. |
| **S2**    | Sleep (Deeper Sleep)     | Similar to S1, but with the CPU powered down completely, and only memory is retained. |
| **S3**    | Suspend-to-RAM           | Also known as "Standby" or "Sleep." The system stops almost all operations, saving the state to RAM. |
| **S4**    | Hibernate                | Known as "Suspend-to-Disk," the system saves its state to the disk and powers down almost entirely. |
| **S5**    | Soft Off                 | The system is fully powered down, but certain components like the BMC or wake-on-LAN (WOL) features remain active. |

### 2. CPU Power States (C-States)

| **State** | **Description**                                              |
| --------- | ------------------------------------------------------------ |
| **C0**    | Active state. The CPU is fully powered and executing instructions. |
| **C1**    | Halt state. The CPU is idle but can return to C0 almost immediately. |
| **C2**    | Stop-clock state. Some parts of the CPU are powered down for slightly lower power consumption. |
| **C3**    | Sleep state. The CPU stops all internal operations and requires more time to transition back to C0. |
| **C6**    | Deep power-down. The CPU core power is removed, and the state is saved externally (depends on architecture). |

### 3. Device Power States (D-States)

​	These states apply to individual devices (e.g., GPUs, storage, network adapters) and define their activity or power-saving modes:

| **State** | **Description**                                           |
| --------- | --------------------------------------------------------- |
| **D0**    | Fully on and operational.                                 |
| **D1**    | Low-power state with reduced functionality (optional).    |
| **D2**    | Deeper low-power state with more functionality reduction. |
| **D3**    | Powered off, except for wake-up circuitry (if available). |
