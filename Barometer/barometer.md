# **Barometer Extension**

For help on how to use an App Inventor extension, please see this [extensions guide](http://ai2.appinventor.mit.edu/reference/other/extensions.html).

## Download
You can download the barometer extension [here](https://gldias.github.io/extensions/Barometer/barometer.aix).

## Description
This extension measures atmospheric pressure and returns the data to your phone to be displayed however you would like. This requires a device with a pressure sensor.

## Properties
![Is Barometer Available Block](BarometerBlocksImages/barometerAvailable.JPG)

Indicates whether the sensor is available.

![Is Barometer Enabled Block](BarometerBlocksImages/barometerEnabled.JPG)

Indicates whether the sensor is enabled.

![Set Barometer Enabled Block](BarometerBlocksImages/setBarometerEnabled.JPG)

Sets the barometer sensor `Enabled` flag to provided boolean value (true or false).

![Get Barometer Millibar Block](BarometerBlocksImages/barometerMbar.JPG)

Gets the pressure level data in millibars.

## Events
![Barometer Changed Block](BarometerBlocksImages/barometerChanged.JPG)

This event is triggered when the atmospheric pressure changes. For continuous reading, this block would be used to encompass any additional logic that requires the barometer.

## Example App

You can use this [example App Inventor application](https://gldias.github.io/extensions/Barometer/BarometerDemo.aia) to see the barometer extension in action.