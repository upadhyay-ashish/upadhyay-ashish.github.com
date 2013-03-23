---           
layout: post
title: Creating a native iOS application !
date: 2012-06-13 14:17:34 UTC
updated: 2012-06-13 14:17:34 UTC
comments: false
categories: ios app html5 native ios app Phonegap apple application natiive ios app ios html phonegap app ios native application
---

### Installing XCode on the system

*   Download and install `XCode` from the App Center alongwith the `Developer Tools`

### Download the Phonegap SDK

*   Download and unzip the Phonegap SDK.
*   Now navigate to the `iOS directory` in the extracted source and run the `Cordova-1.7.0.dmg` and install it.

### Creating a XCode Project

Run `XCode` and create a new Project

Select the template 

*   `Cordova-based Application`

This will create the a new project and include the neccesary Phonegap API Files.

### Changing the default compiler

*   Click on the application name and select `BUILD SETTINGS` tab in the center pane
*   Change the compiler in the `BUILD OPTIONS` from `APPLE LLVM COMPILER` to `LLVM GCC`

### Build and Run the Project

*   Click on the left top of the XCode window selecting the default device as iPad/iPhone Now run the Project. This would invoke the simulator and run the application on it.
*   Once the application runs a error will Popup stating the `index.html` is not found. Close the simulator and return back to the XCode project window.

### Include `www` folder in the project to start with application development

*   Right click the project name and select `Show in Finder`
*   Drag the `www` folder from the `Finder` to the `Project`
*   A window pop's up , select to create references to the files.

### Again `BUILD &amp; RUN` 

*   Now again build and run the project in an iPad/iPhone simulatore
*   This time it would show up the `index.html` which is located in the `www` folder. Also it would show up the `Dialog` stating that Phonegap was successfully integrated in the application

### Download JQuery Mobile bundle

Download the latest build of JQuery Mobile from  Unzip the contents and add the files in the `www` folder categorizing the folders as 

*   `javascripts`
*   `stylesheets`
*   `images'

### Including the JQuery mobile in the application

*   Open `index.html` and create references to the javascript and css files located in the `www` folder using the html tags

#### Add a few lines of HTML to the index page and use the JQuery classes and the Phonegap api function calls to implement the features of the native application as desired 


### * not tested though

*   Once the application is complete or for on Device testing a `Apple's Developer License` is required to sign the applications.
*   After signing it , push the application to `PhoneGap Build` .
*   Download the build package and deploy to th Device.  