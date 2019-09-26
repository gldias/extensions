# **Sound Pressure Level Extension**

For help on how to use an App Inventor extension, please see this [extensions guide](http://ai2.appinventor.mit.edu/reference/other/extensions.html).

## Download
You can download the sound pressure level extension [here](https://gldias.github.io/extensions/SoundPressureLevel/SoundPressureLevel.aix).

## Description
This extension measures the sound pressure level and returns the data to your phone to be displayed however you would like. This data is shown in decibels, which is the standard unit used to measure the intensity of a sound. With this data you can build applications that measure and display sound around the device, or even to use sound as a way to control some other component of the application!

Currently, permission to use the microphone needs to be given before using the app. To do this, navigate through the device's settings to the 'MIT AI2 Companion' app or custom built Sound Pressure Level app, find where permissions are listed and toggle the microphone permission to the 'on' position.

## Properties
![Is Sound Pressure Available Block](SPLBlocksImages/splAvailable.JPG)

Indicates whether or not there is a microphone available to measure sound pressure.

![Is Sound Pressure Enabled Block](SPLBlocksImages/splEnabled.JPG)

Indicates whether or not the microphone is measuring sound pressure.

![Set Sound Pressure Enabled Block](SPLBlocksImages/setSPLEnabled.JPG)

Sets the sensor's `Enabled` flag to the provided boolean value (true or false). This can be used to stop or restart measurements.

![Get Sound Pressure Level Block](SPLBlocksImages/splData.JPG)

Gets the sound pressure level data in decibels.

## Events
![Sound Pressure Level Changed Block](SPLBlocksImages/splChanged.JPG)

This event is triggered when the sound level changes. For continuous reading, this block would be used to encompass any additional logic that requires continuous sound measurements.
## Example App

You can use this [example App Inventor application](https://gldias.github.io/extensions/SoundPressureLevel/SoundPressureLevelDemo.aia) to see the sound pressure level extension in action.
