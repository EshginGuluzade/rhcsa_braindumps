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
