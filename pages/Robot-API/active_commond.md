# 主动指令模块
```{toctree}
:maxdepth: 1
:glob:
```
------
主动指令管理器，其中包含了用户的SDK输入和遥控器的输入。将遥控器的输入数值映射成机器人的实际输入。


## Subscribed

|         ROS Topic          |                    Interface                     | Frame ID |       Description       |
| :------------------------: | :----------------------------------------------: | :------: | :---------------------: |
|  `command/teleop/command`  |             `sensor_msgs::msg::Joy`              |  `joy`   |     遥控器输入指令      |
|   `command/user/command`   | `tita_locomotion_interfaces::msg::LocomotionCmd` |   `\`    | 用户的 SDK 控制指令输入 |
| `locomotion/body/fsm_mode` |             `std_msgs::msg::String`              |   `\`    |   机器人实际状态返回    |

## Published

|        ROS Topic         |                    Interface                     | Frame ID |       Description        |
| :----------------------: | :----------------------------------------------: | :------: | :----------------------: |
| `command/active/command` | `tita_locomotion_interfaces::msg::LocomotionCmd` |  `joy`   | 机器人外部输入的控制指令 |

## Config

|       Param       |      Range      | Default |                    Description                     |
| :---------------: | :-------------: | :-----: | :------------------------------------------------: |
|     `use_sdk`     |  `true/false`   | `false` |      是否使用SDK控制，True 表示遥控器解除控制      |
|  `sdk_max_speed`  |      `3.0`      |  `3.0`  |              机器的速度上限，3.0 m/s               |
| `turn_max_speed`  |      `6.0`      |  `6.0`  |              旋转速度上限，6.0 rad/s               |
| `pitch_max_pose`  |      `1.0`      |  `1.0`  |              机器人俯仰角上限 1.0 rad              |
| `height_max_pose` |      `1.0`      |  `1.0`  |        对应消息中第三个数值，模拟量，俯仰角        |
|    `pub_freq`     | `[100.0,170.0]` | `170.0` |                主动控制指令发布频率                |
| `speed_max_ratio` |   `(0.0,1.0]`   |  `1.0`  |        对应按键高速挡，3.0 * 1.0 = 3.0 m/s         |
| `speed_mid_ratio` |   `(0.0,1.0]`   |  `0.5`  |        对应按键高速挡，3.0 * 0.5 = 1.5 m/s         |
| `speed_min_ratio` |   `(0.0,1.0]`   | `0.15`  |       对应按键高速挡，3.0 * 0.15 = 0.45 m/s        |
|   `height_max`    |   `(0.0,0.3]`   |  `0.3`  | 对应遥控器最高高度挡位，轮轴与机身中心的距离 0.3 m |
|   `height_mid`    |   `(0.0,0.3]`   |  `0.2`  | 对应遥控器中间高度挡位，轮轴与机身中心的距离 0.2 m |
|   `height_min`    |   `(0.0,0.3]`   |  `0.1`  | 对应遥控器最低高度挡位，轮轴与机身中心的距离 0.1 m |


开发者仅需要使用用户指令实现机器人运动，以下对控制API的详细介绍。

## 控制API

**功能概述**

**Topic:**/tita_spacename/command/user/command 

**Message Type:** tita_locomotion_interfaces/msg/LocomotionCmd

**命令示例**：

```
ros2 topic pub /tita3231679/command/user/command tita_locomotion_interfaces/msg/LocomotionCmd "
{
  twist: {linear: {x: 0.0}, angular: {z: 0.5}},
  pose: {position: {z: 0.1}},
  fsm_mode: 'transform_up'
}"
```
**Notices:** 
- 每台机器人都有自己的命名空间，请根据实际情况修改命名空间。
- 不使用（保留为空）：pose.orientation.x, pose.orientation.y, pose.orientation.z, pose.orientation.w
- 机器人状态：fsm_mode，控制取值范围：'transform_up', 'transform_down', ‘jump’

**取值范围：**
inear x ±3.0
twist.angular.z ±6.0
height(position.z) min: 0.1 max: 0.3 mid: 0.2
pitch ±1.0
pub_freq: 100--170.0Hz

**相关示例程序：**
```
https://github.com/DDTRobot/TITA-SDK-ROS2.git
```