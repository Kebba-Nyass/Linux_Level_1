# Linux Level 1

# Task 1: Custom Apache User Setup

## Task

a. Create a user named `anita` on `App server 3` within the Stratos Datacenter.

b. Assign a unique UID `1325` and designate the home directory as `/var/www/anita`.

## Why this matters

In response to heightened security concerns, the `xFusionCorp Industries` security team has opted for custom Apache users for their web applications. Each user is tailored specifically for an application, enhancing security measures. The task is to create a custom Apache user according to the outlined specifications:

## Steps

### Step 1

`SSH` in to `App Server 3` using the credentials of user `banner`.

```bash
thor@jump-host ~$ ssh banner@stapp03
```

Confirm whether we are login with the right user and the right server.

```bash
[banner@stapp03 ~]$ whoami
banner
[banner@stapp03 ~]$ hostname
stapp03
```

### Step 2

Create the user named `anita`.

```bash
[banner@stapp03 ~]$ sudo useradd anita
```

### Step 3

Assigning a unique UID of `1325` and designate the home directory as `/var/www/anita`.

Since user `anita` already exist we only need to modify the account instead.

```bash
[banner@stapp03 ~]$ sudo usermod -u 1325 -d /var/www/anita -m anita
```

- `usermod` modifies the properties of the user.
- `-u 1325` sets the UID. useradd refuses to reuse an existing UID unless you pass `-o`, so it stays unique.
- `-d /var/www/anita` sets the home directory.
- `-m` creates the directory if it doesn’t exist. Without it, useradd only records the path.

### Step 4 : Verify
To check that the UID is free beforehand and that everything worked afterwards:
```bash
[banner@stapp03 ~]$ getent passwd 1325          # no output means the UID is free
anita:x:1325:1001::/var/www/anita:/bin/bash
[banner@stapp03 ~]$ id anita                    # should show uid=1325
uid=1325(anita) gid=1001(anita) groups=1001(anita)
[banner@stapp03 ~]$ getent passwd anita         # should show /var/www/anita as the home
anita:x:1325:1001::/var/www/anita:/bin/bash