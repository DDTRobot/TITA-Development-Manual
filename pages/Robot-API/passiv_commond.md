# 被动指令模块

```{toctree}
:maxdepth: 1
:glob:
```

------



​	被动指令模块，用于接收传感器的信息，将其转化为对用户主动输入控制指令的限制。使机器人的输入指令受到环境信息的影响，进而起到保护机器人的作用。

## Basic Information

| Installation method | Supported platform[s]    |
| ------------------- | ------------------------ |
| Source              | Jetpack 6.0 , ros-humble |

------

## Subscribed

|              ROS Topic              |        Interface         | Frame ID |   Description    |
| :---------------------------------: | :----------------------: | :------: | :--------------: |
| `perception/obstacle/distance_data` | `std_msgs::msg::Float64` |   `/`    | 识别到的障碍距离 |

## Published

|         ROS Topic         |                    Interface                     |   Frame ID    |           Description            |
| :-----------------------: | :----------------------------------------------: | :-----------: | :------------------------------: |
| `command/passive/command` | `tita_locomotion_interfaces::msg::LocomotionCmd` | `passive_joy` | 用于描述当前机器人的运动能力上限 |



