# TITA-Interface

```{toctree}
:maxdepth: 1
:glob:
```

------

<p align="center"><strong>tita_locomotion_interfaces</strong></p>


​**机器人运动控制相关的自定义消息接口。**

## LocomotionCmd.msg

|         Type          |    Name    |       Description        |
| :-------------------: | :--------: | :----------------------: |
|   `std_msgs/Header`   |  `header`  |     ROS2 标准消息头      |
|       `string`        | `fsm_mode` |        机器人状态        |
| `geometry_msgs/Pose`  |   `pose`   | 机器人躯干的姿态控制信息 |
| `geometry_msgs/Twist` |  `twist`   | 机器人底盘的速度控制信息 |

---

<p align="center"><strong>tita_perception_interfaces</strong></p>

​**机器人感知相关的自定义接口。**


## BoundingBox.msg

|       Type        |   Name   |       Description        |
| :---------------: | :------: | :----------------------: |
| `std_msgs/Header` | `header` |     ROS2 标准消息头      |
|     `float64`     | `x_min`  | Bounding box 中 x 最小值 |
|     `float64`     | `y_min`  | Bounding box 中 y 最小值 |
|     `float64`     | `x_max`  | Bounding box 中 x 最大值 |
|     `float64`     | `y_max`  | Bounding box 中 y 最大值 |
|     `string`      | `label`  |         识别 ID          |

## BoundingBox.msg

|       Type        |   Name   |          Description           |
| :---------------: | :------: | :----------------------------: |
| `std_msgs/Header` | `header` |        ROS2 标准消息头         |
|  `BoundingBox[]`  | `boxes`  | 由 Bounding box 消息组成的数组 |

## ObjectDetection.srv

|        Type         |   Name   |   Description    |
| :-----------------: | :------: | :--------------: |
| `sensor_msgs/Image` | `image`  | 请求发送一张图片 |
| `BoundingBoxArray`  | `result` |  返回识别的结果  |


---
<p align="center"><strong>tita_system_interfaces</strong></p>

​	**机器人系统控制相关的自定义消息接口。**



## FanModeSetSrv.srv

|         Type          |    Name    |       Description        |
| :-------------------: | :--------: | :----------------------: |
|   `std_msgs/Byte`   |  `fan_mode`  |     风扇模式      |
| `bool` |  `success`   | 返回的结果 |

风扇模式取值：

| fan_mode | Description |
| :--: | :---------: |
|  0   |  自动档位   |
|  1   |  关闭风扇   |
|  2   |  风速1档   |
|  3   |  风速2档   |
|  4   |  风速3档   |
|  5   |  风速4档   |

## HeadLightControlSrv.srv

|         Type          |    Name    |       Description        |
| :-------------------: | :--------: | :----------------------: |
|   `bool`   |  `is_control`  |     采取控制      |
|   `uint32[48]`   |  `light_rgbl_value`  |     灯珠RGBL值      |
| `bool` |  `success`   | 返回的结果 |

采取控制取值：

| is_control | Description |
| :--: | :---------: |
|  false   |  放弃控制   |
|  true   |  采取控制   |

灯珠RGBL值取值：

| light_rgbl_value | Description |
| :--: | :---------: |
|  uint32[0]   |  第一个灯珠的RGBL取值   |
|  uint32[1]   |  第二个灯珠的RGBL取值   |
|  uint32[2]   |  第三个灯珠的RGBL取值   |
|  uint32[...]   |  省略   |
|  uint32[45]   |  第四十五个灯珠的RGBL取值   |
|  uint32[46]   |  第四十六个灯珠的RGBL取值   |
|  uint32[47]   |  第四十七个灯珠的RGBL取值   |

假设`uint32[0] = 0x12345678`, 则第一个灯珠的RGBL取值的具体含义为：

| uint32[0] | Description |
| :--: | :---------: |
|  0x12   |  第一个灯珠的`Red`取值为`0x12`,`Red`取值范围为`0x00~0xFF`  |
|  0x34   |  第一个灯珠的`Green`取值`0x34`,`Green`取值范围为`0x00~0xFF`  |
|  0x56   |  第一个灯珠的`Blue`取值为`0x56`,`Blue`的取值范围为`0x00~0xFF`  |
|  0x78   |  第一个灯珠的`Lightness`取值为`0x78`,`Lightness`取值范围为`0x00~0xFF`  |

其余灯珠取值含义同理

## TailLightControlSrv.srv

|         Type          |    Name    |       Description        |
| :-------------------: | :--------: | :----------------------: |
|   `bool`   |  `is_control`  |     采取控制      |
|   `uint32[36]`   |  `light_rgbl_value`  |     灯珠RGBL值      |
| `bool` |  `success`   | 返回的结果 |

采取控制取值：

| is_control | Description |
| :--: | :---------: |
|  `false`   |  放弃控制   |
|  `true`   |  采取控制   |

灯珠RGBL值取值：

| light_rgbl_value | Description |
| :--: | :---------: |
|  `uint32[0]`   |  第一个灯珠的RGBL取值   |
|  `uint32[1]`   |  第二个灯珠的RGBL取值   |
|  `uint32[2]`   |  第三个灯珠的RGBL取值   |
|  `uint32[...]`   |  省略   |
|  `uint32[33]`   |  第三十三个灯珠的RGBL取值   |
|  `uint32[34]`   |  第三十四个灯珠的RGBL取值   |
|  `uint32[35]`   |  第三十五个灯珠的RGBL取值   |

假设`uint32[0] = 0x12345678`, 则第一个灯珠的RGBL取值的具体含义为：

| uint32[0] | Description |
| :--: | :---------: |
|  `0x12`   |  第一个灯珠的`Red`取值为`0x12`,`Red`取值范围为`0x00~0xFF`  |
|  `0x34`   |  第一个灯珠的`Green`取值`0x34`,`Green`取值范围为`0x00~0xFF` |
|  `0x56`   |  第一个灯珠的`Blue`取值为`0x56`,`Blue`的取值范围为`0x00~0xFF`  |
|  `0x78`   |  第一个灯珠的`Lightness`取值为`0x78`,`Lightness`取值范围为`0x00~0xFF`  |

其余灯珠取值含义同理

## LegLightControlSrv.srv

|         Type          |    Name    |       Description        |
| :-------------------: | :--------: | :----------------------: |
|   `bool`   |  `is_control`  |     采取控制      |
|   `uint8`   |  `target_leg_light`  |     目标腿灯      |
|   `uint32[10]`   |  `light_rgbl_value`  |     灯珠RGBL值      |
| `bool` |  `success`   | 返回的结果 |

采取控制取值：

| is_control | Description |
| :--: | :---------: |
|  `false`  |  放弃控制   |
|  `true`   |  采取控制   |

目标腿灯取值：

| target_leg_light | Description |
| :--: | :---------: |
|  1   |  左腿灯   |
|  2   |  右腿灯   |

灯珠RGBL值取值：

| light_rgbl_value | Description |
| :--: | :---------: |
|  `uint32[0]`   |  第一个灯珠的RGBL取值   |
|  `uint32[1]`   |  第二个灯珠的RGBL取值   |
|  `uint32[2]`   |  第三个灯珠的RGBL取值   |
|  `uint32[...]`   |  省略   |
|  `uint32[7]`   |  第七个灯珠的RGBL取值   |
|  `uint32[8]`   |  第八个灯珠的RGBL取值   |
|  `uint32[9]`   |  第九个灯珠的RGBL取值   |

假设`uint32[0] = 0x12345678`, 则第一个灯珠的RGBL取值的具体含义为：

| uint32[0] | Description |
| :--: | :---------: |
|  `0x12`   |  取值无意义，仅占符位  |
|  `0x34`   |  第一个灯珠的`Red`取值为`0x12`,`Red`取值范围为`0x00~0xFF`  |
|  `0x56`   |  第二个灯珠的`Green`取值`0x34`,`Green`取值范围为`0x00~0xFF`  |
|  `0x78`   |  第三个灯珠的`Blue`取值为`0x56`,`Blue`的取值范围为`0x00~0xFF`  |

其余灯珠取值含义同理


