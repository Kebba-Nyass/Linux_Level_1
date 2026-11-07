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

### Step 4 :

### Verify

To check that the UID is free beforehand and that everything worked afterwards:

```bash
[banner@stapp03 ~]$ getent passwd 1325          # no output means the UID is free
anita:x:1325:1001::/var/www/anita:/bin/bash
[banner@stapp03 ~]$ id anita                    # should show uid=1325
uid=1325(anita) gid=1001(anita) groups=1001(anita)
[banner@stapp03 ~]$ getent passwd anita         # should show /var/www/anita as the home
anita:x:1325:1001::/var/www/anita:/bin/bash
```
--- 

# Task 2: Group Creation and User Assignment

## Task

a. Create a group named `nautilus_noc` across all App servers within the Stratos Datacenter.

b. Add the user jarod into the nautilus_admin_users group on all App servers. If the user doesn't exist, create it as well.

## Why this matters

The system admin team at `xFusionCorp Industries` has streamlined access management by implementing group-based access control.

## Steps

Creating the named `nautilus_noc` across all app servers.

### Step 1: Creating the group and adding the user in App Server 1

- SSH to `App Server 1` using user `tony's` login deatails.

```bash
thor@jump-host ~$ ssh tony@stapp01
```

put tony's password once it prompt for it.

- Create the group named `nautilus_noc`

```bash
[tony@stapp01 ~]$ sudo groupadd nautilus_noc
```

verify whether user `sonya` exist, if not we create it using.

```bash
[tony@stapp01 ~]$ id sonya
id: ‘sonya’: no such user
[tony@stapp01 ~]$ sudo useradd sonya
[tony@stapp01 ~]$ id sonya
uid=1001(sonya) gid=1002(sonya) groups=1002(sonya)
```

- Adding user `sonya` to the `nautilus_noc` in `App Sever 1`

```bash
[tony@stapp01 ~]$ sudo usermod -aG nautilus_noc sonya
[tony@stapp01 ~]$ id sonya
uid=1001(sonya) gid=1002(sonya) groups=1002(sonya),1001(nautilus_noc)
[tony@stapp01 ~]$ getent group nautilus_noc
nautilus_noc:x:1001:sonya
```

### Step 2: Creating the group and adding the user in App Server 2

- SSH to `App Server 2` using user `steve's` login deatails.

```bash
thor@jump-host ~$ ssh steve@stapp02
```

put steve's password once it prompt for it.

- Create the group named nautilus_noc

```bash
[steve@stapp02 ~]$ sudo groupadd nautilus_noc
```

verify whether user `sonya` exist, if not we create it using.

```bash
[steve@stapp02 ~]$ id sonya
id: ‘sonya’: no such user
[steve@stapp02 ~]$ sudo useradd sonya
[steve@stapp02 ~]$ id sonya
uid=1001(sonya) gid=1002(sonya) groups=1002(sonya)
```

- Adding user `sonya` to the `nautilus_noc` in `App Sever 2`

```bash
[steve@stapp02 ~]$ sudo usermod -aG nautilus_noc sonya
[steve@stapp02 ~]$ id sonya
uid=1001(sonya) gid=1002(sonya) groups=1002(sonya),1001(nautilus_noc)
[steve@stapp02 ~]$ getent group nautilus_noc
nautilus_noc:x:1001:sonya
```

### Step 3: Creating the group and adding the user in App Server 3

- SSH to `App Server 3` using user `banner's` login deatails.

```bash
thor@jump-host ~$ ssh banner@stapp03
```

put banner's password once it prompt for it.

- Create the group named `nautilus_noc`

```bash
[banner@stapp03 ~]$ sudo groupadd nautilus_noc
```

verify whether user `sonya` exist, if not we create it using.

```bash
[banner@stapp03 ~]$ id sonya
id: ‘sonya’: no such user
[banner@stapp03 ~]$ sudo useradd sonya
[banner@stapp03 ~]$ id sonya
uid=1001(sonya) gid=1002(sonya) groups=1002(sonya)
```

- Adding user `sonya` to the `nautilus_noc` in `App Sever 3`

```bash
[banner@stapp03 ~]$ sudo usermod -aG nautilus_noc sonya
[banner@stapp03 ~]$ id sonya
uid=1001(sonya) gid=1002(sonya) groups=1002(sonya),1001(nautilus_noc)
[banner@stapp03 ~]$ getent group nautilus_noc
nautilus_noc:x:1001:sonya
```
---

# Task 3: Linux User Setup with Non-Interactive Shell

## Task

Create a user named `ammar` with a non-interactive shell on **App Server 2** (hostname `stapp02`).

## Why this matters

To accommodate the backup agent tool's specifications, the system admin team at `xFusionCorp Industries` requires the creation of a user with a non-interactive shell. A non-interactive shell such as `/sbin/nologin` blocks interactive logins while still allowing the user to own files and run processes.

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

### 2. Create the user with a non-interactive shell

```bash
[steve@stapp02 ~]$ sudo useradd -s /sbin/nologin ammar
```

`sudo` prompts for banner's password. The `-s` flag sets the login shell.

### 3. Verify

```bash
grep ammar /etc/passwd
ammar:x:1001:1001::/home/ammar:/sbin/nologin
```

The last field, `/sbin/nologin`, confirms the shell.

Optionally, confirm login is blocked:

```bash
sudo su - ammar
# This account is currently not available.
```

## Key takeaways

- `useradd -s <shell>` sets the user's login shell.
- `/sbin/nologin` denies interactive login.
- `/etc/passwd` is the quickest place to verify a user's shell.
