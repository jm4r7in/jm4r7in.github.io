---
published: true
---

Inspired from:
- http://alexbachuk.com/deploying-meteor-application-part-2/
- https://gentlenode.com/journal/meteor-19-deploying-your-applications-in-a-snap-with-meteor-up-mup/41



## 1. Installing Meteor-Up

In your local app directory, run:
	sudo npm install -g mup
    sudo ln -s /usr/bin/nodejs /usr/bin/node
    sudo apt-get install sshpass
    
If you need to update MUP to the latest version in the future:
    npm update mup -g

## 2. Creating and Configuring a Meteor-Up Project

In your local app directory, run:
	mup init
    
Open mup.json and enter your credentials, host, username, password, nodeVersion should be 0.10.28 or greater

{
  // Server authentication info
  "servers": [
    {
      "host": "",
      "username": "",
      "password": ""
      // or pem file (ssh based authentication)
      //"pem": "~/.ssh/id_rsa"
    }
  ],

  // Install MongoDB in the server, does not destroy local MongoDB on future setup
  "setupMongo": true,

  // WARNING: Node.js is required! Only skip if you already have Node.js installed on server.
  "setupNode": true,

  // WARNING: If nodeVersion omitted will setup 0.10.33 by default. Do not use v, only version number.
  "nodeVersion": "0.10.33",

  // Install PhantomJS in the server
  "setupPhantom": true,

  // Application name (No spaces)
  "appName": "Idretis",

  // Location of app (local directory)
  "app": "/home/jerome/meteor/csm",

  // Configure environment
  "env": {
    "PORT": 3000,
    "UPSTART_UID": "meteoruser", // The user you want to run meteor as.
    "ROOT_URL": "http://app.idretis.com"
  },

  // Meteor Up checks if the app comes online just after the deployment
  // before mup checks that, it will wait for no. of seconds configured below
  "deployCheckWaitTime": 35
}

After all info is saved, run 
	mup setup
now the script will setup all required dependencies for the meteor app, like node, phantom and mongodb.

## 3. Deploying your Application

If everything went well, next command is 
	mup deploy
the script will upload your app to the server and convert the app into plain node.js application.

## 4. Installing and Configuring nginx

Just run:
	sudo apt-get install nginx

SSH to your server and 
	sudo nano /etc/nginx/sites-available/default
    
[CTRL+O] to save the file
    
The config file looks like this

server {
	listen *:80;
	server_name app.idetis.com;
    location / {
    	proxy_pass http://127.0.0.1:3000;
    	proxy_http_version 1.1;
    	proxy_set_header Upgrade $http_upgrade;
    	proxy_set_header Connection 'upgrade';
    	proxy_set_header X-Forwarded-For $remote_addr;
    }
}

In this case, nginx listens on port 80 for app.idretis.com and then proxies localhost:3000.

To restart nginx:
	/etc/init.d/nginx restart

## 5. Browsing Your Application Server Logs

To tail logs from the server, just run:
	mup logs -n1000
with the -n option, the tail command displays the last 1,000 lines
	mup logs -F
with the -F option, the tail command updates the display as new lines are added to the logs by another process

## 6. Reconfiguring and Restarting Your Application

When you’ve edited some of your environment variables in the configuration file, you can ask MUP to reconfigure and restart your application using the following command:
	mup reconfig

