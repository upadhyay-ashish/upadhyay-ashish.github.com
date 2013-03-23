---
layout: post
title: Setting up RHODES with an Android Emulator 
category: posts
---

+ Installing Ruby. Please follow the sequence of commands given below to install ruby on ubuntu using RVM.


		sudo apt-get install git  
		sudo apt-get install curl  
		bash -s stable &lt;  $ rvm pkg install zlib  
		rvm pkg install openssl  
		rvm install ruby-1.8.7-p334  
		rvm alias create default ruby-1.8.7-p334



+ Download Android-sdk for linux  
		[Android SDK Download](http://dl.google.com/android/android-sdk_r16-linux.tgz)

+ Download Android-ndk for linux  
		[Android NDK Download](http://dl.google.com/android/ndk/android-ndk-r7-linux-x86.tar.bz2)

+ Extract both the zip files in two different folder's.

+ Java is needed to be installed in the system.If not then download the Java SDK zip files from  
		[Java SDK 7 Download](http://www.oracle.com/technetwork/java/javase/downloads/jdk-7u2-download-1377129.html)

+ Open the terminal and install the rhodes gem.
		<code> gem install rhodes  </code>	
the installation of the gem will take time as the size of the gem is &lt; 50 MB

+ After the gem installation ,type
		<code>rhodes-setup</code>
at the terminal .The screen should come up something like this :
![Alt pik](http://2.bp.blogspot.com/-uM0CgKEDFsw/TzZMJ6ijPmI/AAAAAAAAACE/q4_DxHJpnmE/s1600/Screenshot+at+2012-02-11+16:28:15.png)

	Now type in the directories where you extracted the

		Java SDK    
		Android SDK    
		Android NDK   

+ Setting up the environment is complete.

__Now we will generate a demo application using rhodes to test the emulator.__

+ Setting up Android SDK to host an emulator of a specific android version.

+ Go to the directory where you extracted the sdk .Then go into the tools folder in the sdk and click on a file name **"android"**.A window opens up : 3. Click on the checkbox Android 3.0 , this selects all the checkboxes in this group.Now click on install wait for a few minutes.

4. Now open your terminal and generate a new rhodes application.  
		
		rhogen app Demo 
		cd Demo 5. 

	Edit the built.yml file in any text editor to change the android version to 3.0 instead of default 2.1 and add an emulator name.  
  
6. Now go back to the terminal and type 
		
		rake run:android 

7. The android emulator will show up in a few minutes and load the rhomobile application .   
Now we can go forward designing the mobile application.
