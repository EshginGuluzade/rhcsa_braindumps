## Question 1
Set cronjob for user eshgin to do /bin/echo guluzade at 14:23. 

### Solution
Note: We assume that user *eshgin* is already created
1. Open crontab file for user eshgin
``` bash
crontab -e -u eshgin
```
2. Paste this content to crontab file
``` bash
35 21 * * * /bin/echo guluzade
```

## Question 2
Note: We assume users *eshgin* and *tahir* are already created
Configure the permissions of /var/tmp/fstab </br>
Copy the file /etc/fstab to /var/tmp/fstab. </br>
Configure the permissions of /var/tmp/fstab so that: </br>
the file /var/tmp/fstab is owned by the root user. </br>
the file /var/tmp/fstab belongs to the group root. </br>
the file /var/tmp/fstab should not be executable by anyone. </br>
the user eshgin is able to read and write /var/tmp/fstab. </br>
the user tahir can neither write nor read /var/tmp/fstab. </br>
all other users (current or future) have the ability to read /var/tmp/fstab. </br>

### Solution
1. Copy file to /var/tmp
``` bash
cp /etc/fstab /var/tmp/fstab
```
2. Change user and group ownership to root
``` bash
chown root:root /var/tmp/fstab
```
3. Remove execute permission from all users
``` bash
chmod a-x /var/tmp/fstab
```
4. Give read and write permission to specific user *eshgin*
``` bash
setfacl -m u:eshgin:rw /var/tmp/fstab
```
5. Revoke all permissions from specific user *tahir*
``` bash
setfacl -m u:tahir:- /var/tmp/fstab
```
6. if you run `ls -l /var/tmp/fstab`, you should get following result
``` bash
-rw-rw-r--+ 1 root root 540 Nov  9 22:18 /var/tmp/fstab
```

## Question 3
Create the following users, groups, and group memberships: </br>
A group named admin. </br>
A user eshgin who belongs to admin as a secondary group </br>
A user tahir who also belongs to admin as a secondary group. </br>
A user nihad who does not have access to an interactive shell on the system, and who is not a member of adminu </br>
eshgin, tahir, and nihad should all have the password of rhcsa. </br>

### Solution
1. Create group *admin*
``` bash
groupadd admin
```
2. Create users *eshgin* and *tahir*
``` bash
useradd eshgin
useradd tahir
```
3. Add users *eshgin* anf *tahir* to admin group as a secondary group
``` bash
usermod -a -G admin eshgin
usermod -a -G admin tahir
```
4. Create user *nihad* with non-interactive shell
``` bash
useradd nihad -s /sbin/nologin
```
5. Set password 'rhcsa' for users *eshgin*, *tahir* and *nihad*
``` bash
for i in eshgin tahir nihad; do echo "rhcsa"| passwd $i --stdin; done
```
6. if you run `cat /etc/passwd | tail -3`, you should get similar result
``` bash
eshgin:x:1004:1006::/home/eshgin:/bin/bash
tahir:x:1005:1007::/home/tahir:/bin/bash
nihad:x:1006:1008::/home/nihad:/sbin/nologin
```
7. If you run `id eshgin && id tahir && id nihad`, you should get similar result
``` bash
uid=1004(eshgin) gid=1006(eshgin) groups=1006(eshgin),1005(admin)
uid=1005(tahir) gid=1007(tahir) groups=1007(tahir),1005(admin)
uid=1006(nihad) gid=1008(nihad) groups=1008(nihad
```

## Question 4
Create the following users, groups, and group memberships: </br>
A group named admin. </br>
A user eshgin who belongs to admin as a secondary group </br>
A user tahir who also belongs to admin as a secondary group. </br>
A user nihad who does not have access to an interactive shell on the system, and who is not a member of adminu </br>
eshgin, tahir, and nihad should all have the password of rhcsa. </br>

### Solution
