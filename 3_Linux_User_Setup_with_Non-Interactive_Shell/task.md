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
