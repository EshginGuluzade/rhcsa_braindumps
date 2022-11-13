**NOTE:** All questions are performed in *CentOS Stream 9*

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
Resize the logical volume vo and its filesystem to 290 MB. </br>
Make sure that the filesystem contents remain intact. </br>
Note: Partitions are seldom exactly the same size requested, so a size within the range of 260 MB to 320 MiB is acceptable. 

### Solution

## Question 5
A YUM repository has been provided at http://serverdomain11.example.com/pub/x86_64/Server. </br>
Configure your system to use this location as a default repository. </br>

### Solution

## Question 6
SELinux must be running in the Enforcing mode. </br> 

### Solution
1. As a default you should get following result when you run this command `sestatus` </br>
``` bash
Current mode:                   enforcing
Mode from config file:          enforcing
```

## Question 7
Download the document from ftp://instructor.example.com/pub/testfile </br> 
find all lines containing [abcde] and redirect to /mnt/answer document </br>
then rearrange the order according the original content.</br>

### Solution
1. Let's create testfile first and copy below content to that file </br>
``` bash
vim testfile
```
Content: </br>
``` bash
a
ab
abc
abcd
abcde
aabcdee
qabcdtre
opabcdrtt
abcdtrefdg
abcdekllabcd
poljdjabcdhhe
jkoilabcdeeeee
ebacdgjhjabcdei
polkjabcdklklkap
```
2. Use grep to find lines containing `abcde` and redirect to /mnt/answer </br>
``` bash
grep abcde testfile > /mnt/answer
```

## Question 8
Create a volume group, and set the size is 500M </br> the size of single PE is 16M </br> 
Create logical volume named Iv0 in this volume group </br> 
set size is 20 PE, make it as ext3 file system, and mounted automatically under data </br>

### Solution
1. Let's create testfile first and copy below content to that file </br>
``` bash
vim testfile
```

## Question 9
Configure your web services </br> 
download from http://instructor.example.com/pub/serverX.html </br> 
And the services must be still running after system rebooting. </br>

### Solution
1. Install apache httpd </br>
``` bash
yum install httpd -y
```
2. Go to /var/www/html and install html page, then rename file to index.html</br>
``` bash
cd /var/www/html
curl -O https://httpd.apache.org/ABOUT_APACHE.html
mv ABOUT_APACHE.html index.html
```
3. Enable httpd and check status, it should be active and running </br>
``` bash
systemctl enable --now httpd
systemctl status httpd
```

## Question 10
Configure the FTP service in your system </br> 
allow remote access to anonymous login and download the program by this service </br> 
Service is still running after system rebooting </br>

### Solution
1. Install vsftpd service </br>
``` bash
yum install vsftpd -y
```
2. Set `anonymous_enable=YES` in /etc/vsftpd/vsftpd.conf </br>
``` bash
vim /etc/vsftpd/vsftpd.conf
```
3. You should get following result if you run this command `grep anonymous_enable /etc/vsftpd/vsftpd.conf` </br>
``` bash
anonymous_enable=YES
```
4. Enable httpd and check status, it should be active and running </br>` </br>
``` bash
systemctl enable --now vsftpd
systemctl status vsftpd
```
