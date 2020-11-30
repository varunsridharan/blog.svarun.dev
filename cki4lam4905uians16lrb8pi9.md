## Simple MySQL Backup Script In Shell Script

This post will be relatively short compared to my other posts and may not be informative as my other posts too. I am writing this blog just to share a script that I have been using for years to take the backup of ***MYSQL*** database.


## Requirements

Please make sure you have installed `MySQL` & `mysqldump` program if you are running this script from a remote server. 

if you are using it on the same server then no additional programs need to be installed. 


## Script
```shell
#!/bin/sh

# SQL Export File Name
FILE=db.`date +"%Y%m%d-%H%M%S"`.sql

# Database Server Host Name
DBSERVER="localhost"  

# Database Name
DATABASE=""

# Database User Name
USER=""

# Database User Password
PASS=""

# Backup Script
mkdir /root/backup/mysql/

cd /root/backup/mysql/ 

mysqldump --opt --user=${USER} --password=${PASS} --host=${DBSERVER} ${DATABASE} > ${FILE}

echo "SQL Backup ${FILE} was created:"
```

## Feedback

I have been using this for years now and have never faced any issues to date and this script runs mostly via CRON in my server which triggers this script every day.

I have tested and actually used this script with a database that is over 1GB in-size too. never faced issues in exporting it.


---

%%[blog-footer]