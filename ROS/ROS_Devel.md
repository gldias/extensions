# Notes for future ROS Extension Developers

## Notes

This page is meant for developers or people who are interested in contributing to the development of the ROS extension for MIT App Inventor. If you are only interested in the extension, the documentation for that can be found [here](https://gldias.github.io/extensions/ROS/ROS)

## Overview
This is an extension to help add ROS functionality to an Android application, allowing the user to interact with a ROS node.

### Issues

The current issues that block the ROS libraries from being added to AppInventor is that the compiler only use dx in dex mode which only allow that total amount of function in the libraries to add up to under 64k methods however the ROS library plus it’s dependencies push it over that limit, which either require multi-dex or d8 which both appear to work with AppInventor. The PR to add d8 to AppInventor is located here. A full document outlining the issue is located here.
	
The next issue is there is conflict in libraries so we had to use guava 14 since AppInventor already used it instead of using what we currently know guave 12 that works already which could cause issues once the last library that currently is our main blocker has been resolved.

The main trouble library is the apache_xmlrpc_client-0.3.6 library which contains a resource file that when dx or d8 process it strips out of the library so when the code is executed it can’t find it and breaks. Once the build process is updated to repackage these resource files it would work as expected. 

### Future Work

A file for the extension that has the skeleton code for the extension has been created. That file contains the defined blocks for the extension, documentation for those blocks can be found [here](https://gldias.github.io/extensions/ROS/ROS). It's reccomended that if you want to contribute to the development of this extension to read through the documentation for ROS as well as ROSjava, both of which can be found below. It is also reccomended that you setup a ROS simulator of some kind. The one that we reccomend using is Gazebo alongside GzWeb and links to those can also be found below.

## ROS Extension Source Code
The current source code for the Robot Operating System extension can be found [here](https://gldias.github.io/extensions/ROS/ros_bridge.java). 

To use the files, download a fork of the [MIT App Inventor Project](https://github.com/mit-cml/appinventor-sources) and navigate to "*download_location*/appinventor/components/src/com". 
From there, you can either create your own package structure and change the `package` line at the top of each Java file or use the "com/rit/appinventor/components/runtime" already used in the files that were downloaded and place them in the runtime folder.

If you haven't already, don't forget to check out how to [use and create extensions](http://ai2.appinventor.mit.edu/reference/other/extensions.html) and [how to build a local version of MIT App Inventor](https://www.google.com/url?q=https://docs.google.com/document/d/1Xc9yt02x3BRoq5m1PJHBr81OOv69rEBy8LVG_84j9jc/pub&sa=D&ust=1580595462075000).

## Android Related Functions

### [Android Activity Lifecycle](https://developer.android.com/guide/components/activities/activity-lifecycle)
`ros_bridge(ComponentContainer container)`, `onDelete()`, `onResume()`, `onInitialize()`, and `onStop()` are functions to help control the lifecycle of the android application. 

`onDelete()`, `onResume()`, `onInitialize()`, and `onStop()` help to control the app as the user interacts with the phone and other applications. 
`OnStop()` is activated when the user navigates away from the application, `onResume()` is called when the user returns to the application that's been in the background, and `onDelete()` is called when the application is closed and removed from memory. `onInitialize()` is used when the application is first started by the user.

## ROS Specific Functions 

### Publisher Nodes

Publishers in ROS are used to send commands to the robots in order to be executed. The `ROSJava` library saves you a lot of time in writing these by providing the skeleton for the nodes in the form of the `AbstractNodeMain` class. This class implements the `NodeMain` interface that provides you with all the node methods for you to fill in. The main method you should focus on is the `onStart()` method provided by the interface. This method is where you should include the loop that tells the robot what to do. Make sure when writing these to provide the correct message type and that you have said message type in your project or else the publisher node won’t work. A good example of what a publisher node looks like can be found [here](http://rosjava.github.io/rosjava_core/0.1.6/getting_started.html).

## Useful Resources

[ROS Documentation](http://wiki.ros.org/Documentation)

[ROSJava Documentation](http://wiki.ros.org/rosjava)

[How to setup gazebo with ROS](http://gazebosim.org/tutorials?tut=ros_overview)

[GzWeb Tutorial](http://gazebosim.org/tutorials?tut=gzweb_install&cat=gzweb)