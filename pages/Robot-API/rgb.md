# RGB灯效控制器

```{toctree}
:maxdepth: 1
:glob:
```
------
## Description
RGB灯效控制器用于控制整机所有可见RGB灯，包括TITA机器人前脸灯条、尾部灯条以及左右腿灯，能够实现任意部位任意灯珠的任意颜色。

由于本接口采用自定义消息，因此对此接口做详尽的说明。

其中前脸灯条由48个RGB灯珠组成，每个灯珠接受红色、绿色、蓝色和亮度共四个维度的共同控制，因此每个灯珠可以被uint32_t类型的数据控制，其中每个维度占据8位。整个灯条可以被含有48个元素的uint32_t类型的数组数据控制。

尾部灯条由36个RGB灯珠组成，每个灯珠接受红色、绿色、蓝色和亮度共四个维度的共同控制，因此每个灯珠可以被uint32_t类型的数据控制，其中每个维度占据8位。整个灯条可以被含有36个元素的uint32_t类型的数组数据控制。

左腿/右腿灯条分别由10个RGB灯珠组成，每个灯珠接受红色、绿色、蓝色共三个维度的共同控制，因此每个灯珠可以被uint32_t类型的数据控制，其中每个维度占据8位，剩余的八位数字无意义。整个灯条可以被含有10个元素的uint32_t类型的数组数据控制，左腿和右腿需要分开控制。

具体举例来说：
```
uint32_t head_rgb_light[48];
uint32_t tail_rgb_light[36];
uint32_t left_leg_rgb_light[10];
uint32_t right_leg_rgb_light[10];

head_rgb_light[0] = 0x12345678U;
tail_rgb_light[0] = 0x12345678U;
left_leg_rgb_light[0] = 0x12345678U;
right_leg_rgb_light[0] = 0x12345678U;

其中前脸灯条和尾部灯条的第一个灯被设置为0x12345678U, 
这意味着前脸灯和尾部灯的第一个灯的红色值为0x12U (18), 绿色值为0x34U (52), 
蓝色值为0x56U (86), 亮度值为0x78U (120)。具体灯效为上述混合后的效果。

左/右腿灯条的第一个灯被设置为0x12345678U,
这意味着左/右腿灯条的第一个灯的红色值为0x12U (18), 绿色值为0x34U (52),
蓝色值为0x56U (86), 0x78U这个值无意义。具体灯效为上述混合后的效果。
```

## Preparation

运行RGB灯效控制器模块：
```
ros2 run rgb_light_controller rgb_light_controller_node 
或者
ros2 launch rgb_light_controller rgb_light_controller_node.launch.py
```

## Usage
灯效控制器以服务的形式提供控制接口，用户有两种方法来实现控制。

**第一种是直接调用调试指令，实现单次控制：**
```
例如要控制前灯：
ros2 service call /system/light_control/head_light_control_srv tita_system_interfaces/srv/HeadLightControlSrv "{is_control: true, light_rgbl_value: [0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00]}"

或者想控制尾灯：
ros2 service call /system/light_control/tail_light_control_srv tita_system_interfaces/srv/TailLightControlSrv "{is_control: true, light_rgbl_value: [0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00]}" 

或者想控制左/右腿部灯：
ros2 service call /system/light_control/leg_light_control_srv tita_system_interfaces/srv/LegLightControlSrv "{is_control: false, target_leg_light: 1, light_rgbl_value: [0xff00ff00, 0xff00ff00, 0xff00ff00, 0xff00ff00, 0xff00ff00, 0xff00ff00, 0xff00ff00, 0xff00ff00, 0xff00ff00, 0xff00ff00]}"
其中target_leg_light为1表示左腿，2表示右腿

放弃控制请将is_control设置为false
```
**第二种是在程序构建Client向Service发送请求，实现更高效灵活的控制**

请不要为腿部灯条发送过高频率的请求，过高频率的请求可能会影响腿部电机通信。

## Basic Information

| Installation method | Supported platform[s]    |
| ------------------- | ------------------------ |
| Source              | Jetpack 6.0 , ros-humble |

------




