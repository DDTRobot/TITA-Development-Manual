# 控制

```{toctree}
:maxdepth: 1
:glob:
```

------

TITA控制以ROS2 plugin形式让客户端能控制机器人运动服务，并且向客户提供机器状态数据，此插件提供必要的API接口，将控制信息转换成ROS消息格式向外发布。

````{note}
首先要打开API调用接口
vim /usr/share/tita_bringup/params/default_param.yaml
将 locomotion_manager中的control_motion_mode 字段改为 1
0: controller control moded
1: api control mode
2: autonomy control mode
````

## 站立
**功能概述：** 进入站立模式，控制站立姿态。<br>
**Topic：**  `command/controller/lock`<br>
**MsgType：** `tita_motion_msgs/msg/ControllerCommandLock`<br>
**命令示例：** `ros2 topic pub /tita2303895/command/controller/lock tita_motion_msgs/msg/ControllerCommandLock "{lock_state: 2}" -1`

## 高度
**功能概述：** 控制机器人的站立高度。<br>
**Topic：**  `locomotion/move_target/height`<br>
**MsgType：** `tita_motion_msgs/msg/Height`<br>
**命令示例：** `ros2 topic pub -r 30 /{ns}/locomotion/move_target/height tita_motion_msgs/msg/Height "{height: 0.2}"`<br>
**取值范围：** height：max 0.30 min 0.09
````{note}
发送频率需大于30hz即可
````

## 移动、转向
**功能概述：** linear.x 前进后退速度、 angular.z 左转右转速度 、linear.y roll角速度 、angular.y pitch角速度；不使用（保留为空）：linear.z和angular.x。<br>
**Topic：**  `command/controller/api/move`<br>
**MsgType：** `geometry_msgs/msg/TwistStamped`<br>
**命令示例：** `ros2 topic pub /{ns}/command/controller/api/move geometry_msgs/msg/TwistStamped "{ twist: {linear: {x: 0.5, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 0.0}}}"`<br>
**取值范围：** <br>
linear x min : ±0.82. max ±1.52<br>
twist.angular.z min: ±0.42 max ±1.42<br>
height min: 0.09 max: 0.30<br>
linear.y: ±0.942(0.3 * PI)<br>
angular.y: ±0.2<br>
````{note}
发送频率需大于30hz即可
````

## 跳跃
**功能概述：** 该API用于控制机器跳跃<br>
**Topic：** `command/controller/jump`<br>
**Msg Type：** `tita_motion_msgs/msg/ControllerCommandJump`<br>
**命令示例：** `ros2 topic pub /{ns}/command/controller/jump tita_motion_msgs/msg/ControllerCommandJump "{jump_state: 2}" -1`<br>
**取值范围：**<br>
jump_state = JUMP (0x02)<br>
IDLE 0x00 /CHARGE 0x01 /JUMP 0x02

## 机器状态
**功能概述：** 该接口是监控机器目前姿态情况，能知道目前机器状态与反馈信息是否相符<br>
**Topic：** `locomotion/locomotion_status`<br>
**Msg Type：** `tita_motion_msgs::msg::LocomotionStatus`<br>
**命令示例：** `ros2 topic echo /{ns}/locomotion/locomotion_status`<br>
**取值范围：**<br>
DIE = 0x00<br>
INIT = 0x01<br>
TRANSFORM_UP =0x02<br>
STAND = 0x03<br>
TRANSFORM_DOWN = 0x04<br>
CRASH = 0x05<br>
SUSPENDING = 0x06<br>
JUMP = 0x07