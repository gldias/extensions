# **Robot Operating System Extension**

For help on how to use an App Inventor extension, please see this [extensions guide](http://ai2.appinventor.mit.edu/reference/other/extensions.html).

## Download
You can download the Robot Operating System extension *here*.

## Description
This extension allows users to interact with a Robot Operating System (ROS) node. To start, this extension will allow the user to move a robot using the `twist` message.

## Properties

## Events

## Functions
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

## Example App

You can use a *minimal App Inventor application* or a more *in-depth example App Inventor application* to see the ROS extension in action.

## Developer Documentation

More in-depth for developers can be found [here](https://gldias.github.io/extensions/ROS/ROS_Devel).

## Authors
This extension was originally created by George Colgrove (lead developer), Guilherme Lopes Dias, Ryan Connors, and Nathan Oesterle
