# 遥控器指令模块

```{toctree}
:maxdepth: 1
:glob:
```

------
​**功能描述**：用于解析接收机的数据，动态设置各个功能模块的参数。该节点可以通过修改配置文件，改变按键的映射关系。

## Basic Information

| Installation method | Supported platform[s]    |
| ------------------- | ------------------------ |
| Source              | Jetpack 6.0 , ros-humble |

------

## Subscribed

|       ROS Topic        |            Interface             |       Frame ID       |       Description        |
| :--------------------: | :------------------------------: | :------------------: | :----------------------: |
|         `/joy`         |     `sensor_msgs::msg::Joy`      |        `joy`         | 用于接收第三方遥控器节点 |
| `system/battery/left`  | `sensor_msgs::msg::BatteryState` | `left_battery_info`  |  遥控器显示左侧电池信息  |
| `system/battery/right` | `sensor_msgs::msg::BatteryState` | `right_battery_info` |  遥控器显示右侧电池信息  |

## Published

|        ROS Topic         |        Interface        | Frame ID |              Description               |
| :----------------------: | :---------------------: | :------: | :------------------------------------: |
| `command/teleop/command` | `sensor_msgs::msg::Joy` |  `joy`   | 发布改变按键顺序的消息到active_command |
|          `/joy`          | `sensor_msgs::msg::Joy` |  `joy`   |        发布数据到 Joy 消息接口         |

## Config

|     Param      |     Range      | Default |              Description               |
| :------------: | :------------: | :-----: | :------------------------------------: |
|  `DebugMode`   |  `true/false`  | `false` |              调试使用开关              |
|   `AxesSize`   |     `1-8`      |   `8`   |            被处理的按键数量            |
|   `MoveAxes`   | `a/b` \| `0-7` |  `a0`   |  对应消息中第一个数值，模拟量，前进轴  |
|   `TurnAxes`   | `a/b` \|`0-7`  |  `a1`   |  对应消息中第二个数值，模拟量，转向轴  |
|  `PitchAxes`   |  `a/b`\|`0-7`  |  `a2`   |  对应消息中第三个数值，模拟量，俯仰角  |
|   `RollAxes`   | `a/b` \|`0-7`  |  `a3`   |  对应消息中第四个数值，模拟量，滚动轴  |
|   `StandUp`    | `a/b` \|`0-7`  |  `b4`   | 对应消息中第五个数值，开关量，站立开关 |
| `HeightSwitch` | `a/b` \|`0-7`  |  `b5`   | 对应消息中第六个数值，开关量，高度调节 |
|  `JumpButton`  | `a/b` \|`0-7`  |  `b6`   | 对应消息中第七个数值，开关量，跳跃开关 |
| `SpeedButton`  | `a/b` \|`0-7`  |  `b7`   | 对应消息中第八个数值，开关量，速度调节 |
|   `AxesBias`   |    `浮点数`    | 0.0013  |        遥控器模拟量轴的死区范围        |

