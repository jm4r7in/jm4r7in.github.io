---
published: true
---



## Backup MongoDB on Ubuntu

http://stackoverflow.com/questions/30558625/what-is-the-easiest-to-backup-a-mongodb-deployed-with-mup/30559938

https://sheharyar.me/blog/regular-mongo-backups-using-cron/

http://www.codeproject.com/Tips/547759/Automating-backup-for-MongoDB-using-CRON-and-S-CMD


### wput

	sudo apt-get install wput
    

### Script

    mongo_backup.sh
    

  #!/bin/bash
  
  MONGO_DATABASE="appDBName"
  APP_NAME="appName"

  MONGO_HOST="127.0.0.1"
  MONGO_PORT="27017"
  TIMESTAMP=`date +%F-%H%M`
  MONGODUMP_PATH="/usr/bin/mongodump"
  BACKUPS_DIR="/home/meteoruser/backups/$APP_NAME"
  BACKUP_NAME="$APP_NAME-$TIMESTAMP"
  
  # mongo admin --eval "printjson(db.fsyncLock())"
  # $MONGODUMP_PATH -h $MONGO_HOST:$MONGO_PORT -d $MONGO_DATABASE
  $MONGODUMP_PATH -d $MONGO_DATABASE
  # mongo admin --eval "printjson(db.fsyncUnlock())"
  
  tar -zcvf $BACKUP_NAME.tgz dump
  rm -rf dump
  
  wput $BACKUP_NAME.tgz ftp://login:password@ftp.domain.com/backups/


	chmod +x mongo_backup.sh
	bash mongo_backup.sh


	sudo su
	crontab -e


	00 00 * * * /bin/bash /home/username/scripts/mongo_backup.sh
    

###Install s3cmd

from : 
[http://s3tools.org/repositories](http://s3tools.org/repositories)

Import S3tools signing key:

     wget -O- -q http://s3tools.org/repo/deb-all/stable/s3tools.key | sudo apt-key add -

Add the repo to sources.list: 

     sudo wget -O/etc/apt/sources.list.d/s3tools.list http://s3tools.org/repo/deb-all/stable/s3tools.list

Refresh package cache and install the newest s3cmd: 

     sudo apt-get update && sudo apt-get install s3cmd
