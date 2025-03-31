---
title: Chmod and Chown Commands
date: 2025-03-31 13:41:10
categories: Linux
tags: Linux
---

## 1. Chmod

- chmod - means that Change Mode. It is a command that controls the users permission on the file or directory in Linux.
- File accessing permissions of Linux/Unix are divided into three levels: file owner(Owner), user group(Group), and other users(Other Users).

![file-permissions-rwx](/images/chmod_chown.assets/file-permissions-rwx.jpg)

- The permission of the file or directory can be changed only by the owner or the superuser, others can't. There are two types model followed to specify the permissions.

  - Octal Model and Symbolic Model

    ![rwx-standard-unix-permission-bits](/images/chmod_chown.assets/rwx-standard-unix-permission-bits.png)

- Octal File Permissions Table

  | Number | Permissions            | rwx  | Binary |
  | ------ | ---------------------- | ---- | ------ |
  | 7      | Read + Write + Execute | rwx  | 111    |
  | 6      | Read + Write           | rw-  | 110    |
  | 5      | Read + Execute         | r-x  | 101    |
  | 4      | Read-only              | r--  | 100    |
  | 3      | Write + Execute        | -wx  | 011    |
  | 2      | Write-only             | -w-  | 010    |
  | 1      | Execute-only           | --x  | 001    |
  | 0      | None                   | ---  | 000    |

  

```bash
touch sample.sh
ll
```

Output: `-rw-rw-r--  1 raman raman    0  三  31 14:07 sample.sh`. Here, the first character (-) means it is a file.

When you create a file using touch command by default the permissions will be 664(-rw-rw-r--).

Changing the permissions to all(user, group, others).

```bash
chmod -v 777 sample.sh
ll
```

Output: `-rwxrwxrwx  1 raman raman    0  三  31 14:11 sample.sh*`

```bash
mkdir sample
ll
```

Output: `drwxrwxr-x  2 raman raman 4096  三  31 14:26 sample/`. Here, the first character (d) means it is a directory.

When you create a file using touch command by default the permissions will be 775(drwxrwxr-x).

For changing permissions multiple files or directories,

```bash
chmod -vR 777 directory_path/* #for directories
chmod -vR 777 file_name/* #for files
```



## 2. Chown

- chown - means that Change Ownership. This command is used to change the owner of the file or the directory.

- chown requires the permission of superuser(root) to execute it.

  ```bash
  touch sample.sh
  ll
  ```

  Output: `-rw-rw-rw-   1 raman raman     0  三   8 00:35 testfile`

- Changing the ownership from raman to jenkins.

  ```bash
  sudo chown -v jenkins:jenkins sample.sh
  ll
  ```

  Output: `-rw-rw-rw-   1 jenkins jenkins     0  三   8 00:35 testfile`

- For changing permissions multiple files or directories,

  ```bash
  chown -vR username:usergroup directory_path/* #for directories
  chmod -vR username:usergroup file_name/* #for files
  ```
