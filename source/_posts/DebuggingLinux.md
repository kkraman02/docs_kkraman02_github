---
title: Debugging Linux
date: 2025-01-20 10:42:12
comment: true
category: Linux
tag: Linux
---

Debugging Linux systems is addictive for many developers who know how to handle the following.

1. `dmesg`
2. `journalctl`

The difference between those features in Linux is,



## 1. dmesg

- **Purpose**: Displays the messages from the kernel ring buffer.

- **Scope**: Focuses exclusively on kernel messages, including hardware initialization, driver events, and kernel warnings/errors.

- **Usage**: Primarily used for debugging kernel-related issues.

- **Features**: 

  - Shows logs generated during boot and runtime from the kernel.
  - Does not include user-space application logs.
  - Limited to recent logs, as the kernel ring buffer overwrites old messages over time.
  - It requires root privileges for some operations.

- **Command**:

    ```bash
    sudo dmesg
    sudo dmesg | grep "error"  # Filter for specific messages
    sudo dmesg -T              # Display timestamps in human-readable format
    ```



## 2. journalctl

- **Purpose**:  A modern systemd-based logging tool for querying and managing logs from both the kernel and user-space applications.

- **Scope**: Covers all logs recorded by systemd-journald, including kernel messages, system events, and application logs.

- **Usage**: General-purpose log management and troubleshooting tool.

- **Features**: 

  - Centralized log collection for the entire system (both kernel and user-space).
  - Offers powerful filtering and querying options (e.g., by time, service, priority).
  - Logs are structured and stored in a binary format.
  - It may require root privileges for some operations.

- **Command**:

  ```bash
  journalctl                   		# View all logs
  journalctl -k                		# View only kernel logs
  journalctl -u <service>      		# Logs for a specific systemd service
  journalctl --since "1 hour ago"	# Logs from the last hour
  journalctl -p err            		# Filter logs by priority level (e.g., error)
  ```

