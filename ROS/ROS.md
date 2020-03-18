# **Robot Operating System Extension**

For help on how to use an App Inventor extension, please see this [extensions guide](http://ai2.appinventor.mit.edu/reference/other/extensions.html).

## Download
You can download the Robot Operating System extension *here*.

## Description
This extension allows users to interact with a Robot Operating System (ROS) node. To start, this extension will allow the user to move a robot using the `twist` message.

## Properties

## Events

## Functions
`connectToMaster(String URI)`

Connects the application to the ROS master node at the `URI` address.

`twist(linearX, linearY, linearZ, angularX, angularY, angularZ)`

Sends a `twist` message to the ROS master node. The arguments tell the robot how much to move and turn in which dimension.

`turn()`

Sends a `twist` message to rotate the robot.

`stopRobot()`

Sends a `twist` to tell the robot to stop moving in all directions.

## Example App

You can use a *minimal App Inventor application* or a more *in-depth example App Inventor application* to see the ROS extension in action.

## Developer Documentation

More in-depth for developers can be found [here](https://gldias.github.io/extensions/ROS/ROS_Devel).

## Authors
This extension was originally created by George Colgrove (lead developer), Guilherme Lopes Dias, Ryan Connors, and Nathan Oesterle
