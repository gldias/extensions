# **Robot Operating System Extension Concept**

For help on how to use an App Inventor extension, please see this [extensions guide](http://ai2.appinventor.mit.edu/reference/other/extensions.html).

## Notes
This documentatin is for an exntension that is currently a work in progress and not available for download at this time.

## Description
This extension will allow users to interact with a Robot Operating System (ROS) node. To start, this extension will allow the user to move a robot using the `twist` message.

## Functions Concept
![Connect to master URI](ROSBlocks/ConnectToMasterURI.png)

Connects the application to the ROS master node at the `URI` address.

![Twist](ROSBlocks/Twist.png)

Sends a `twist` message to the ROS master node. The arguments tell the robot how fast to move and turn in which dimension.

![Turn](ROSBlocks/Turn.png)

Sends a `twist` message to rotate the robot.

![Stop](ROSBlocks/StopRobot.png)

Sends a `twist` to tell the robot to stop moving in all directions.

![Move forward indefinitely](ROSBlocks/ForwardIndefinitely.png)

Sends a `twist` to tell the robot to move forward indefinitely. The arguments tell the robot how fast to move.

![Move backwards indefinitely](ROSBlocks/BackwardsIndefinitely.png)

Sends a `twist` to tell the robot to move backwards indefinitely. The arguments tell the robot how fast to move.

![Spin Clockwise](ROSBlocks/SpinClockwise.png)

Sends a `twist` to tell the robot to spin clockwise indefinitely. The arguments tell the robot how fast to spin.

![Spin Counter-Clockwise](ROSBlocks/SpinCounterClockwise.png)

Sends a `twist` to tell the robot to spin counter-clockwise indefinitely. The arguments tell the robot how fast to spin.

## Developer Documentation

More in-depth information for developers can be found [here](https://gldias.github.io/extensions/ROS/ROS_Devel).

## Download

A non-functioning extension file can be found [here](https://github.com/gldias/extensions/raw/gh-pages/ROS/ros_bridge.aix)

## Authors
This extension was originally created by George Colgrove (lead developer), Guilherme Lopes Dias, Ryan Connors, and Nathan Oesterle
