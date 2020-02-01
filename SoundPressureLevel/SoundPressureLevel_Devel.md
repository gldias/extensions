# Notes for future SPL Extension Developers

## Overview
This is an extension to help add Sound Pressure Level Meter functionality to an application, allowing the user to measure the intensity of background sound in decibels.
This extension will report unweighted, A-Weighted, and C-Weighted decibels over a user selected time interval which is 200 milliseconds (ms) by default.
A-Weighted and C-Weighted decibels are calculated by performing a Fast Fourier Transformation (FFT) on the sound data over time, weighing the resulting frequency bins [according to these formulas](https://en.wikipedia.org/wiki/A-weighting#Function_realisation_of_some_common_weightings), and performing an inverse FFT and then convert sound data to pascals then decibels.

### Issues
There are some known areas improvement. 

* Applications work well while they are in the foreground and in active use, however there are some issues when multitasking with the `SPL.aia` built as an APK. 
The Android operating system seems to believe that when the application is put into the background that it frequently closes.
It's suspected that this is likely an issue with the extension's implementation of the Android Activity Lifecycle. 
More information provided below.

* There are accuracy issues when using two different devices next to each other. 
This is likely due to different microphones having different sensitivities. 
However, higher Android API levels do [provide a value for microphone sensitivity](https://developer.android.com/reference/android/media/MicrophoneInfo.html#getSensitivity()) which may be useful.

## SPL Extension Source Code
The source code for the Sound Pressure Level extension can be downloaded [here](https://gldias.github.io/extensions/SoundPressureLevel/SourceCode/SoundPressureLevel.java). 
SoundPressureLevel.java also relies upon [Complex.java](https://gldias.github.io/extensions/SoundPressureLevel/SourceCode/Complex.java) and [FFT.java](https://gldias.github.io/extensions/SoundPressureLevel/SourceCode/FFT.java).
Complex.java and FFT.java are courtesy of Robert Sedgewick and Kevin Wayne of Princeton's Computer Science Department. 
Links to the location of the original files can be found in the respective Java files.

To use the files, download a fork of the [MIT App Inventor Project](https://github.com/mit-cml/appinventor-sources) and navigate to "*download_location*/appinventor/components/src/com". 
From there, you can either create your own package structure and change the `package` line at the top of each Java file or use the "com/rit/appinventor/components/runtime" already used in the files that were downloaded and place them in the runtime folder.

If you haven't already, don't forget to check out how to [use and create extensions](http://ai2.appinventor.mit.edu/reference/other/extensions.html) and [how to build a local version of MIT App Inventor](https://www.google.com/url?q=https://docs.google.com/document/d/1Xc9yt02x3BRoq5m1PJHBr81OOv69rEBy8LVG_84j9jc/pub&sa=D&ust=1580595462075000).

## Android Related Functions

### [Android Activity Lifecycle](https://developer.android.com/guide/components/activities/activity-lifecycle)
`SoundPressureLevel(ComponentContainer container)`, `onDelete()`, `onResume()`, and `onStop()` are functions to help control the lifecycle of the android application. 

`SoundPressureLevel(ComponentContainer container)` is what starts the application, and a second thread that drives the application. 
In this thread, the extension checks to see if the android permission allows for recording sound, if the user wants to be analyzing sound data, and analyzes the sound to measure the intensity if allowed.
The time delay between sound measurements is currently 200ms by default, however that number can be temporarily changed by the user before creating the app through MIT App Inventor or while running the app by giving the `ListenIntervalMilliseconds(int milliSeconds)` block a new value.

`onDelete()`, `onResume()`, and `onStop()` help to control the app as the user interacts with the phone and other applications. 
`OnStop()` is activated when the user navigates away from the application, `onResume()` is called when the user returns to the application that's been in the background, and `onDelete()` is called when the application is closed and removed from memory.

This area could use some work. Currently, when the application is put into the background a warning can pop-up saying that "SPLApp keeps stopping" and newer versions of Android report that the application frequently crashes. However, the user can put the app in the background by navigating to another app then navigate back to the application without a noticeable problem.

## SPL Functions
### `updateSoundPressureLevel(Pair<Complex[], Integer> tuple)`
`updateSoundPressureLevel(Pair<Complex[], Integer> tuple)` is where the majority of the calculations happen or are triggered. 
To start, there is some commented out code to generate a 1000Hz signal. 
That consistent signal can help with debugging by removing the changing background noise the phone picks up.  
After data structure creation, the first largest possible power of 2 (2^1, 2^2, 2^3, etc) amount of sound data will be taken to be used to find the intensity of. 
This is required because we perform an FFT on the sound data, and FFT requires a power of 2 amount of data.  
Performing an FFT takes the sound data over time, and returns sound data over frequency.
That is represented by an array of shorts, where the short is the intensity and each index is a bin for a set of frequencies.
Then each value to in the frequency bins are multiplied by weighting coefficients, to weigh the sound according to A and C weighting equations.  
From here, both A and C weighed data is separate but they go through the same process.
After the weighing, each version of the weighed sound has an Inverse FFT performed on it to transform the sound over frequency to sound over time again.
After we have sound over time, the shorts that represent voltage are converted to doubles that represent sound pressure in pascals.
A Root-Mean-Square is then performed on the sound data in pascals, to find an average of the sound data in line with what the human ear perceives.
That mean in pascals is then converted to decibels and an event is trigger to send the value is sent to the UI to be shown to the user.

After the weighted sound pressure levels are calculated, the unweighted sound pressure level is calculated.
To calculate that, the unedited sound data is converted from shorts that represent voltage is converted to pascals.
Those pascal values are then averaged using the Root Mean Square, which is then used to calculate the number of decibels over time.
An event is then triggered to send the unweighted sound pressure level in decibels to the UI to display the user.

### `convertMicVoltageToPressure(Complex[] soundData)`
It's believed that most smartphone microphones are accurate until about 100db, which would be represented by a short's max value (32,767).
To convert the shorts to pressure, we need to divide by the short value per pascals. 
100dB is equivalent to 2 pascals, so 1 pascal is a short of 16383.5.
So dividing each short in the array by shorts per pascal, 16383.5, will make each resulting double the number of pascals at that moment measured.

### `calcRootMeanSquare(double[] soundData, int numSamples)`
This function takes the square of each number in the array, and totals it.
That total is then divided by the number of data samples that were added, then that resulting value has the square root taken of it.
This provides an average of all the data passed to it.
When an RMS is taken on sound data in pascals, it's result represents how the human ear reacts to sound.

### `calcFFTLength(int len)`
This function determines the largest amount of data an FFT can be performed on.
An FFT requires a power of 2 (2^1, 2^2, 2^3, etc) amount of information to be passed in.
Java does not have the innate ability to work with base 2 logarithms, so the first line uses logarithmic division to convert from base 10 numbers to base 2.
That number is then floored to round down, then the floored number is used as a base 2 exponent to find the largest power of 2 that's less than `len`.

### `analyzeSoundData()`
This function uses Android API to read sound data from the phone's microphone, which is an array of shorts, and the length of the sound data recorded.
The shorts gathered are then converted to Complex numbers so we can later perform an FFT on it.
The array of Complex numbers and length returned are then packaged up into a `Pair` to be able to return them both and later use both values.

### `startListening()`
After checking to see if the user has granted permission to record and that the recorder object (a reference to the microphone) exists, the state is checked.
If the recorder state is uninitialized then a new reference to the microphone is created, to guarantee the existence of a valid reference. 
Once the reference is guaranteed, we check to see if the microphone is not in the recording state and start recording if so. 
A private variable is then set to reflect this known state.

### `stopListening()`
After checking to see if the user has granted permission to record and that the recorder object (a reference to the microphone) exists, the state is checked.
If the recorder state is uninitialized then a new reference to the microphone is created, to guarantee the existence of a valid reference. 
Once the reference is guaranteed, we check to see if the microphone is in the recording state and stop recording if so. 
A private variable is then set to reflect this known state.

### `Available()`
This is a method that can be accessed through MIT App Inventor.

It creates a new reference to the microphone and tried to record with it.
If the new reference is able to record then the app has permission to use the microphone and a microphone exists to listen with.
If the new reference is not able to record, then the app is not able to use the microphone. 
This could be could be due to the permission to record audio not being granted or there being no microphone available to use on the phone.

### `SoundPressureLevelUpdated(double decibels, double aWeightedDecibels, double cWeightedDecibels)`
This is an event available to use in MIT App Inventor. 

This fires every time there is an update from the `updateSoundPressureLevel(Pair<Complex[], Integer> tuple)`, giving the user access to the newly calculated decibel reading.
This reading is in unweighted decibels.

### `ListenIntervalMilliseconds(int milliSeconds)`
This is a method that can be accessed through MIT App Inventor.

This function sets the variable that controls the amount of time in milliseconds the thread in `updateSoundPressureLevel(Pair<Complex[], Integer> tuple)` waits while listening for sound.
The longer this time is, the more sound data will be recorded and analyzed for its intensity.
However that also means the measurement will also be updated less often.
If this number is smaller, the time listening for sound is short so there will be less sound data per loop.
However that means the measurement will be updated more often.

### `checkPermissions()`
This function checks the Android package manager for the permission to record audio.
Once it sees whether or not it has permission, it then checks the applications internal knowledge of its ability to record to see if it's recently changed.
If the information from the operating system and internal values differ, then the internal values will be updated.
A boolean representing whether or not permission is granted is then returned.
