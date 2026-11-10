# Task 4: Service User Creation with Home Directory

## Task
Create a user named `ravi` in `App Server 2` without a home directory.

## Why this matters
In response to the latest tool implementation at `xFusionCorp Industries`, the system admins require the creation of a service user account.
## Steps

### 1. SSH into App Server 2 as `steve`

```bash
thor@jump-host ~$ ssh steve@stapp02
```

Enter the password when prompted.

Confirm you're on the right server and user:

```bash
[steve@stapp02 ~]$ whoami
steve
[steve@stapp02 ~]$ hostname
stapp03
```
### 2. Create a user named "ravi" without a home directory.
```bash
[steve@stapp02 ~]$ sudo useradd -M ravi
```
The `-M` flag tells`useradd` not to create a home directory, even if `CREATE_HOME` is enabled in `/etc/login.defs`.

### 3. To verify it worked:
```bash
[steve@stapp02 ~]$ id ravi
uid=1001(ravi) gid=1001(ravi) groups=1001(ravi)
[steve@stapp02 ~]$ getent passwd ravi
ravi:x:1001:1001::/home/ravi:/bin/bash
[steve@stapp02 ~]$ ls -ld /home/ravi
ls: cannot access '/home/ravi': No such file or directory
```
- `id ravi` should show the new user and its group.
- `getent passwd ravi` should show an entry whose home field is `/home/ravi`.
- `ls -ld /home/ravi` should fail with “No such file  or directory”, confirming no home directory was created.