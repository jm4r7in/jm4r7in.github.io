---
published: true
---


## Backup MongoDB on Ubuntu

http://stackoverflow.com/questions/30558625/what-is-the-easiest-to-backup-a-mongodb-deployed-with-mup/30559938

https://sheharyar.me/blog/regular-mongo-backups-using-cron/

http://www.codeproject.com/Tips/547759/Automating-backup-for-MongoDB-using-CRON-and-S-CMD


###Install s3cmd

Import S3tools signing key:
     wget -O- -q http://s3tools.org/repo/deb-all/stable/s3tools.key | sudo apt-key add -

Add the repo to sources.list: 
     sudo wget -O/etc/apt/sources.list.d/s3tools.list http://s3tools.org/repo/deb-all/stable/s3tools.list

Refresh package cache and install the newest s3cmd: 
     sudo apt-get update && sudo apt-get install s3cmd

