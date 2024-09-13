# Motor Control

```{toctree}
:maxdepth: 1
:glob:
```

------
The Motor API is used to control the eight motors on TITA and to obtain the status of the eight motors.

## Data from left side four motors
**Function Overview：** Read the status information of the four motors on the left side.<br>
**Topic：** `locomotion/motorgroupinput_left`<br>
**Msg Type1：** `tita_motion_msgs::msg::MotorGroupIn`<br>
**Msg Type1 Value：** <br>
`std_msgs/Header`<br>
`header`<br>
`MotorIn[4] motor_in`<br>
**Msg Type2：** `tita_motion_msgs::msg::MotorIn`<br>
**Msg Type2 Value：**<br>
std_msgs/Header<br>
header<br>
uint8 id<br>
float32 position<br>
float32 velocity<br>
float32 torque<br>

## Data from right side four motors
**Function Overview：** Read the status information of the four motors on the right side.<br>
**Topic：** `locomotion/motorgroupinput_right`<br>
**Msg Type1：** `tita_motion_msgs::msg::MotorGroupIn`<br>
**Msg Type1 Value：** <br>
`std_msgs/Header`<br>
`header`<br>
`MotorIn[4] motor_in`<br>
**Msg Type2：** `tita_motion_msgs::msg::MotorIn`<br>
**Msg Type2 Value：**<br>
std_msgs/Header<br>
header<br>
uint8 id<br>
float32 position<br>
float32 velocity<br>
float32 torque<br>

## Motor Control Interface
**Function Overview：** Control interface to control the motors of TITA.
<br>
**Topic：** `locomotion/motorgroupinput_right`<br>
**Msg Type1：** `tita_motion_msgs::msg::MotorGroupIn`<br>
**Msg Type1 Value：** <br>
`std_msgs/Header`<br>
`header`<br>
`MotorIn[4] motor_in`<br>
**Msg Type2：** `tita_motion_msgs::msg::MotorIn`<br>
**Msg Type2 Value：**<br>
std_msgs/Header<br>
header<br>
uint8 id<br>
float32 position<br>
float32 velocity<br>
float32 torque
````{note}
float32 kp (not used)
float32 kd (not used)
````