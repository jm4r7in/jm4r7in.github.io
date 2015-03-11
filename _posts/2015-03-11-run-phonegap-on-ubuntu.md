---
published: false
---

## Run Phonegap on Ubuntu

## 1. Install Git

	sudo apt-get install git

## 2. Install NodeJS

	sudo apt-get install node
    
bla bla

## 3. Install PhoneGap

	sudo npm install -g phonegap

## 4. Install Ant

	sudo apt-get install ant
    
## 5. Get the Android SDK

Download from :
	http://developer.android.com/sdk/index.html
Extract to /usr/local/android-sdk-linux
    sudo tar -xvf android-sdk_r24.0.2-linux.tgz -C /usr/local/

## 6. Get Java (JRE & JDK)

	sudo apt-get install openjdk-7-jre
	sudo apt-get install openjdk-7-jdk

## 7. Launch the Android SDK Manager

	cd /usr/local/android-sdk-linux
    sh android

## 8. In the Android SDK Manager

Open the Tools directory and select:
	Android SDK Tools
	Android SDK Platform-tools
	Android SDK Build-tools (highest version)

Open the first Android X.X folder (the latest version) and select:
	SDK Platform
	A system image for the emulator, such as ARM EABI v7a System Image

Install the packages.


## . Update your PATH

Open .profile for editing using the following command.
	gedit ~/.profile

Append the following lines to the end of the file. Do not put these inside any of the IF blocks.
	export ANDROID_HOME="/usr/local/android-sdk-linux/tools"
	export ANDROID_PLATFORM_TOOLS="/usr/local/android-sdk-linux/platform-tools"
	export PATH="$PATH:$ANDROID_HOME:$ANDROID_PLATFORM_TOOLS"
Save the file, log out, and log back in to apply the changes.

## . Install the necessary Android packages


## . Update C/C++


## . Update C/C++


Inspired by: 
- http://www.levibotelho.com/development/the-complete-guide-to-running-phonegap-on-ubuntu/
- https://steveyoung.wordpress.com/2014/10/22/updating-phonegap-app-to-cordova-3-5-1/






