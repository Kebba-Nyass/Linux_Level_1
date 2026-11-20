# Task 8: Data Backup for Developer

## Why this matters
The jump host server hosts a directory named `/data`, serving as a repository for various developers non-confidential data. Developer `john` has requested a copy of their data stored in `/data/john`. The System Admin team has provided the following steps to fulfill this request:

## Task
a. Create a compressed archive named `john.tar.gz` of the `/data/john` directory.

b. Transfer the archive to the `/home` directory on the Jump Host Server.

## Steps

### 1. Confirm you're on the right server and user:

```bash
thor@jump-host ~$ whoami
thor
thor@jump-host ~$ hostname
jump-host
```
### 2. Creating a compressed archive
```bash
thor@jump-host ~$ cd /data/
thor@jump-host /data$ sudo tar -czf john.tar.gz -C /data john
thor@jump-host /data$ ls
john  john.tar.gz
```
### 3. Tansfering john.tar.gz to /home/ of the Jump Host Server.
```bash
thor@jump-host /data$ sudo cp john.tar.gz /home/
thor@jump-host /data$ cd /home/
thor@jump-host /home$ ls
ansible  john.tar.gz  thor
```