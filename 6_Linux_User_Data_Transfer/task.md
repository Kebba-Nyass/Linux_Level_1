# Task 6: Linux User Data Transfer

## Task
Locate all files (excluding directories) owned by user `ravi` within the `/home/usersdata` directory on `App Server 3`. Copy these files while preserving the directory structure to the `/beta` directory.

## Why this matters
Due to an accidental data mix-up, user data was unintentionally mingled on Nautilus `App Server 3` at the `/home/usersdata` location by the Nautilus production support team in Stratos DC. To rectify this, specific user data needs to be filtered and relocated. 
## Steps

### 1. SSH into App Server 3 as `banner`

```bash
thor@jump-host ~$ ssh banner@stapp03
```

Enter the password when prompted.

Confirm you're on the right server and user:

```bash
[banner@stapp03 ~]$ whoami
banner
[banner@stapp03 ~]$ hostname
stapp03
```
### 2. Locate and Copy /home/usersdata directory
```bash
[banner@stapp03 ~]$ sudo find /home/usersdata -type f -user ravi -exec cp --parents -p {} /beta/ \;
```
- `-type f -user ravi` matches only regular files owned by `ravi`, so directories are excluded.
- `cp --parents` recreates each file’s full source path under the destination, so a file at `/home/usersdata/wp-content/foo.php` lands at `/beta/home/usersdata/wp-content/foo.php`.
- `-p` keeps ownership, mode and timestamps where permissions allow. Run it with `sudo` so files `ravi` owns can be read and written to `/beta`.
  
### 3. To check the result, compare the two lists. They should show the same files  
```bash
[banner@stapp03 ~]$ sudo find /home/usersdata -type f -user ravi | wc -l
1880
[banner@stapp03 ~]$ sudo find /beta -type f | wc -l
1880
```