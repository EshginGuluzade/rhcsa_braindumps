## Question 1
Set cronjob for user eshgin to do /bin/echo guluzade at 14:23. 

### Solution
1. Open crontab file for user eshgin
``` bash
crontab -e -u eshgin
```
2. Paste this content to crontab file
``` bash
35 21 * * * /bin/echo guluzade
```

## Question 1
Configure the permissions of /var/tmp/fstab 
Copy the file /etc/fstab to /var/tmp/fstab. 
Configure the permissions of /var/tmp/fstab so that: 
the file /var/tmp/fstab is owned by the root user. 
the file /var/tmp/fstab belongs to the group root. 
the file /var/tmp/fstab should not be executable by anyone. 
the user eshgin is able to read and write /var/tmp/fstab. 
the user tahir can neither write nor read /var/tmp/fstab. 
all other users (current or future) have the ability to read /var/tmp/fstab. 


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
