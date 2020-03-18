# Notes for future ROS Extension Developers

## Overview
This is an extension to help add ROS functionality to an Android application, allowing the user to interact with a ROS node.

### Issues
There are some known areas that could use improvement. 

## ROS Extension Source Code
The source code for the Robot Operating System extension can be downloaded *here*. 

To use the files, download a fork of the [MIT App Inventor Project](https://github.com/mit-cml/appinventor-sources) and navigate to "*download_location*/appinventor/components/src/com". 
From there, you can either create your own package structure and change the `package` line at the top of each Java file or use the "com/rit/appinventor/components/runtime" already used in the files that were downloaded and place them in the runtime folder.

If you haven't already, don't forget to check out how to [use and create extensions](http://ai2.appinventor.mit.edu/reference/other/extensions.html) and [how to build a local version of MIT App Inventor](https://www.google.com/url?q=https://docs.google.com/document/d/1Xc9yt02x3BRoq5m1PJHBr81OOv69rEBy8LVG_84j9jc/pub&sa=D&ust=1580595462075000).

## Android Related Functions

### [Android Activity Lifecycle](https://developer.android.com/guide/components/activities/activity-lifecycle)
`ros_bridge(ComponentContainer container)`, `onDelete()`, `onResume()`, `onInitialize()`, and `onStop()` are functions to help control the lifecycle of the android application. 

`onDelete()`, `onResume()`, `onInitialize()`, and `onStop()` help to control the app as the user interacts with the phone and other applications. 
`OnStop()` is activated when the user navigates away from the application, `onResume()` is called when the user returns to the application that's been in the background, and `onDelete()` is called when the application is closed and removed from memory. `onInitialize()` is used when the application is first started by the user.

## ROS Functions
