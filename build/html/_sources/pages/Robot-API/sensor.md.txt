# 传感器状态信息

```{toctree}
:maxdepth: 1
:glob:
```

------

查看所有传感器状态，反馈所有传感器如异常，未初始化等等。

------

**Topic：** `system/sensor_status`<br>
**Msg Type：** `tita_system_msgs::msg::SensorStatus`<br>
**命令示例：** `ros2 topic echo /[namespace]/system/sensor_status`<br>
### 字段描述
- `header`：用于更高级别的带时间戳的数据类型的标准元数据。此字段用于传递时间戳和坐标帧信息。<br>
- `infrared_status`：红外传感器的状态。<br>
- `ultrasonic_status`：超声波传感器的状态。<br>
- `camera_status`：摄像头的状态。<br>
- `left_motor_status`：左侧电机的状态。这是左侧电机组中每个电机的状态列表。<br>
- `right_motor_status`：右侧电机的状态。这是右侧电机组中每个电机的状态列表。<br>
- `temperature_humidity_status`：温度和湿度传感器的状态。<br>
- `controller_status`：控制器的状态。<br>
- `locomotion_status`：运动系统的状态。
### 状态代码
消息中的状态字段使用以下状态代码：<br>
- `UNINITIALIZED = 0`：传感器或系统未初始化。<br>
- `OK = 1`：传感器或系统正常工作。<br>
- `ERROR = 2`：传感器或系统遇到错误。<br>
- `OFFLINE = 3`：传感器或系统离线。<br>
`locomotion_status`字段使用不同的状态代码。<br>
- `DIE = 0x00`：运动系统已停止。<br>
- `INIT = 0x01`：运动系统正在初始化。<br>
- `TRANSFORM_UP = 0x02`：运动系统正在向上变形。<br>
- `STAND = 0x03`：运动系统正在站立。<br>
- `TRANSFORM_DOWN = 0x04`：运动系统正在向下变形。<br>
- `CRASH = 0x05`：运动系统已崩溃。<br>
- `SUSPENDING = 0x06`：运动系统正在暂停。<br>
- `JUMP = 0x07`：运动系统正在跳跃。<br>
- `UNINITIALIZED_STATUS = 0x08`：运动系统未初始化。<br>