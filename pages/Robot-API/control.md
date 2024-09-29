# Motion Control

```{toctree}
:maxdepth: 1
:glob:
```

------

TITA controls robot movement services and provides machine status data to users through a ROS2 plugin. This plugin offers the necessary API interfaces, converting control information into ROS message.

````{note}
First, you need to open the API calling interface
vim /usr/share/tita_bringup/params/default_param.yaml
change locomotion_manager's control_motion_mode value to 1
0: controller control moded
1: api control mode
2: autonomy control mode
````

## Stand
**Function Overview：** Enter the standing mode to control the standing posture.<br>
**Topic：**  `command/controller/lock`<br>
**MsgType：** `tita_motion_msgs/msg/ControllerCommandLock`<br>
**Code Example：** `ros2 topic pub /tita2303895/command/controller/lock tita_motion_msgs/msg/ControllerCommandLock "{lock_state: 2}" -1`

## Height
**Function Overview：** Control the robot's postural elevation through programming.<br>
**Topic：**  `locomotion/move_target/height`<br>
**MsgType：** `tita_motion_msgs/msg/Height`<br>
**Code Example：** `ros2 topic pub -r 30 /{ns}/locomotion/move_target/height tita_motion_msgs/msg/Height "{height: 0.2}"`<br>
**Value Range：** height：max 0.30 min 0.09
````{note}
Sending frequency ≥ 30 HZ.
````

## Pitch and Roll
**Function Overview：** Pitch and roll commands need to be sent simultaneously; Currently Control: linear.x forward and backward velocity, angular.z left and right turn velocity, linear.y roll angular velocity, angular.y pitch angular velocity; Not Used (set as empty): linear.z and angular.x.<br>
**Topic：**  `command/controller/api/move`<br>
**MsgType：** `geometry_msgs/msg/TwistStamped`<br>
**Code Example：** `ros2 topic pub /{ns}/command/controller/api/move geometry_msgs/msg/TwistStamped "{ twist: {linear: {x: 0.5, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 0.0}}}"`<br>
**Value Range：** <br>
linear x min : ±0.82. max ±1.52<br>
twist.angular.z min: ±0.42 max ±1.42<br>
height min: 0.09 max: 0.30<br>
linear.y: ±0.942(0.3 * PI)<br>
angular.y: ±0.2<br>
````{note}
Sending frequency ≥ 30 HZ.
````

## Jump
**Function Overview：** This API is used to control the robot's jumping action.<br>
**Topic：** `command/controller/jump`<br>
**Msg Type：** `tita_motion_msgs/msg/ControllerCommandJump`<br>
**Code Example：** `ros2 topic pub /{ns}/command/controller/jump tita_motion_msgs/msg/ControllerCommandJump "{jump_state: 2}" -1`<br>
**Value Range：**<br>
jump_state = JUMP (0x02)<br>
IDLE 0x00 /CHARGE 0x01 /JUMP 0x02

## Machine Status
**Function Overview：** This interface is for monitoring the current posture of the machine, allowing you to know whether the current machine status and feedback information match.<br>
**Topic：** `locomotion/locomotion_status`<br>
**Msg Type：** `tita_motion_msgs::msg::LocomotionStatus`<br>
**Code Example：** `ros2 topic echo /{ns}/locomotion/locomotion_status`<br>
**Value Range：**<br>
DIE = 0x00<br>
INIT = 0x01<br>
TRANSFORM_UP =0x02<br>
STAND = 0x03<br>
TRANSFORM_DOWN = 0x04<br>
CRASH = 0x05<br>
SUSPENDING = 0x06<br>
JUMP = 0x07