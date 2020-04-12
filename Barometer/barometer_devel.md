# Notes for future Barometer Developers

## Overview
This is an extension to help an App Inventor user to easily create applications that measure the air pressure around their phone. 
This extension requires an air pressure sensor be present on the phone to work.

## Issues
No known issues

## Future Work
Other units could be added. 
Currently the pressure is reported only in MilliBars, other units that could be added are Atmospheres (AMT), Pounds Per Square Inch (PSI), as well as Pascals (Pa).

## Barometer Source Code
The source code for the Barometer extension can be downloaded [here](https://gldias.github.io/extensions/Barometer/barometer/SourceCode/BarometerSensor.java).

To use the files, download a fork of the [MIT App Inventor Project](https://github.com/mit-cml/appinventor-sources) and navigate to "*download_location*/appinventor/components/src/com".
From there, you can either create your own package structure and change the `package` line at the top of each Java file or use the "com/rit/appinventor/components/runtime" already used in the files that were downloaded and place them in the runtime folder.

## Android Related Functions

### [Android Activity Lifecycle](https://developer.android.com/guide/components/activities/activity-lifecycle)
`BarometerSensor(ComponentContainer container)`, `onDelete()`, `onResume()`, and `onStop()` are functions to help control the lifecycle of the android application.

`onDelete()`, `onResume()`, and `onStop()` help to control the app as the user interacts with the phone and other applications.
`OnStop()` is activated when the user navigates away from the application, `onResume()` is called when the user returns to the application that's been in the background, and `onDelete()` is called when the application is closed and removed from memory.
