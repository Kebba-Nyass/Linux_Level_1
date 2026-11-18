# Task 7: Secure Root SSH Access

## Task
Your task is to disable direct SSH root login on all app servers (`stapp01`, `stapp02` and `stapp03`) within the `Stratos Datacenter`. Make sure the change is applied to the running SSH service on each server.

## Why this matters
Following security audits, the `xFusionCorp Industries` security team has rolled out new protocols, including the restriction of direct root SSH login.
## Steps

### 1. SSH into App Server 1 as `tony`

```bash
thor@jump-host ~$ ssh tony@stapp01
```
Enter the password when prompted.

Confirm you're on the right server and user:

```bash
[tony@stapp01 ~]$ whoami
tony
[tony@stapp01 ~]$ hostname
stapp01
```
Confirm from sshd_config file the Permission for ssh root login
```bash
[tony@stapp01 ~]$ sudo cat /etc/ssh/sshd_config
# Example of overriding settings on a per-user basis
#Match User anoncvs
#       X11Forwarding no
#       AllowTcpForwarding no
#       PermitTTY no
#       ForceCommand cvs server
PermitRootLogin yes
```
Editing the sshd_config file to deny ssh root login
```bash
[tony@stapp01 ~]$ sudo vi /etc/ssh/sshd_config
PermitRootLogin no
[tony@stapp01 ~]$ sudo cat /etc/ssh/sshd_config
# Example of overriding settings on a per-user basis
#Match User anoncvs
#       X11Forwarding no
#       AllowTcpForwarding no
#       PermitTTY no
#       ForceCommand cvs server
PermitRootLogin no
```
Validate the config
```bash
[tony@stapp01 ~]$ sudo sshd -t 
```
Apply it to the running service
```bash
[tony@stapp01 ~]$ sudo systemctl restart sshd
```
Verify the effective setting
```bash
[tony@stapp01 ~]$ sudo sshd -T | grep -i permitrootlogin    # expect: permitrootlogin no
permitrootlogin no
```


### 2. SSH into App Server 2 as `steve`

```bash
thor@jump-host ~$ ssh steve@stapp02
```
Enter the password when prompted.

Confirm you're on the right server and user:

```bash
[steve@stapp02 ~]$ whoami
steve
[steve@stapp02 ~]$ hostname
stapp02
```
Confirm from sshd_config file the Permission for ssh root login
```bash
[steve@stapp02 ~]$ sudo cat /etc/ssh/sshd_config
# Example of overriding settings on a per-user basis
#Match User anoncvs
#       X11Forwarding no
#       AllowTcpForwarding no
#       PermitTTY no
#       ForceCommand cvs server
PermitRootLogin yes
```
Editing the sshd_config file to deny ssh root login
```bash
[steve@stapp02 ~]$ sudo vi /etc/ssh/sshd_config
PermitRootLogin no
[steve@stapp02 ~]$ sudo cat /etc/ssh/sshd_config
# Example of overriding settings on a per-user basis
#Match User anoncvs
#       X11Forwarding no
#       AllowTcpForwarding no
#       PermitTTY no
#       ForceCommand cvs server
PermitRootLogin no
```
Validate the config
```bash
[steve@stapp02 ~]$ sudo sshd -t 
```
Apply it to the running service
```bash
[steve@stapp02 ~]$ sudo systemctl restart sshd
```
Verify the effective setting
```bash
[steve@stapp02 ~]$ sudo sshd -T | grep -i permitrootlogin    # expect: permitrootlogin no
permitrootlogin no
```


### 3. SSH into App Server 3 as `banner`

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
Confirm from sshd_config file the Permission for ssh root login
```bash
[banner@stapp03 ~]$ sudo cat /etc/ssh/sshd_config
# Example of overriding settings on a per-user basis
#Match User anoncvs
#       X11Forwarding no
#       AllowTcpForwarding no
#       PermitTTY no
#       ForceCommand cvs server
PermitRootLogin yes
```
Editing the sshd_config file to deny ssh root login
```bash
[banner@stapp03 ~]$ sudo vi /etc/ssh/sshd_config
PermitRootLogin no
[banner@stapp03 ~]$ sudo cat /etc/ssh/sshd_config
# Example of overriding settings on a per-user basis
#Match User anoncvs
#       X11Forwarding no
#       AllowTcpForwarding no
#       PermitTTY no
#       ForceCommand cvs server
PermitRootLogin no
```
Validate the config
```bash
[banner@stapp03 ~]$ sudo sshd -t 
```
Apply it to the running service
```bash
[banner@stapp03 ~]$ sudo systemctl restart sshd
```
Verify the effective setting
```bash
[banner@stapp03 ~]$ sudo sshd -T | grep -i permitrootlogin    # expect: permitrootlogin no
permitrootlogin no
```