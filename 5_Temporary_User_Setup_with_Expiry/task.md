# Task 5: Temporary User Setup with Expiry

## Task
Create a user named `james` on `App` `Server 3` in Stratos Datacenter. Set the expiry date to `2027-03-28`, ensuring the user is created in lowercase as per standard protocol.

## Why this matters
As part of the temporary assignment to the `Nautilus` project, a developer named `james` requires access for a limited duration. To ensure smooth access management, a temporary user account with an expiry date is needed. 
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
### 2. Creating User 'james' with expiry date.

```bash
[banner@stapp03 ~]$ sudo useradd -m -s /bin/bash -e 2027-03-28 james
```
### 3. Verify

```bash
[banner@stapp03 ~]$ sudo chage -l james
Last password change                                    : Nov 16, 2026
Password expires                                        : never
Password inactive                                       : never
Account expires                                         : Mar 28, 2027
Minimum number of days between password change          : 0
Maximum number of days between password change          : 99999
Number of days of warning before password expires       : 7
```