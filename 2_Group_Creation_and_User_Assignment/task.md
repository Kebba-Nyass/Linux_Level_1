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
