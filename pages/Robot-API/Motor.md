# 电机控制

```{toctree}
:maxdepth: 1
:glob:
```

------
电机API用于控制TITA上面的八个电机并获取八个电机的状态

## 左侧四个电机数据
**功能概述：** 读取左侧四个电机状态信息。<br>
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

## 右侧四个电机数据
**功能概述：** 读取右侧四个电机状态信息。<br>
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

## 电机控制接口
**功能概述：** 能通过控制接口控制TITA的电机。<br>
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
float32 kp 未使用
float32 kd 未使用
position 位置 Velocity 速度 torque 力矩
````