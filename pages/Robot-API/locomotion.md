# 运动控制模块

```{toctree}
:maxdepth: 1
:glob:
```
------

​
机器人运动控制管理。主要分为以下4个模块:

- **device**：硬件bridge, 目前处理遥控器下发mcu, 读取mcu的motors及imu sensor信息．
- **libraries**：第三方库, ．
- **locomotion_bringup**：机器人运动控制启动文件．
- **locomotion_msgs**: 机器人运动控制消息定义, 目前仅为调试信息。
- **tita_controllers**：继承于ros2_control框架中`controller_interface`，处理`hardware_interface`数据并得到控制指令发送到`hardware_interface`。
- **tita_description**：机器人描述文件存放位置。
- **tita_webots_ros2**：存放机器人仿真环境的位置, 托管在`git@git.ddt.dev:rbt/alg/tita_webots_ros2.git`

## Basic Information

| Installation method | Supported platform[s]    |
| ------------------- | ------------------------ |
| Source              | Jetpack 6.0 , ros-humble |

------

## Subscribed
1. `/${tita_ns}/command/manager/cmd_key` (TODO: 现在不好使)
Topic type: `std_msgs/msg/String`
机器人状态机切换: 状态机包含: `transform_up`, `transform_down`, `balance`, `jump`, `idle`
    ``` bash
    ros2 topic pub -1 /${tita_ns}/command/manager/cmd_key std_msgs/msg/String "data: 'idle'"
    ```

2. `/${tita_ns}/command/manager/cmd_pose`    
Topic type: `geometry_msgs/msg/PoseStamped`
机器人头部位置姿态控制指令,包括调节高度,调节劈叉,`roll`, `pitch`等
    ``` bash
    ros2 topic pub -1 /${tita_ns}/command/manager/cmd_pose geometry_msgs/msg/PoseStamped "{
        header: {
            stamp: {
                sec: 0, 
                nanosec: 0}, 
            frame_id: 'world'}, 
        pose: 
        {
            position: {x: 0.0, y: 0.0, z: 0.1}, # only valid in z , range in 0.1 to 0.3
            orientation: {x: 0.0, y: 0.0, z: 0.0, w: 1.0}
        }
        }"
    ```

3. `/${tita_ns}/command/manager/cmd_twist` 
Topic type: `geometry_msgs/msg/Twist`
机器人速度控制指令,包括`linear（线速度）`, `angular（角速度）`等, 仅`linear.x（前进后退，取正负数值）`和`angular.z（左转右转，取正负数值）`有效
    ``` bash
    ros2 topic pub -1 /${tita_ns}/command/manager/cmd_twist geometry_msgs/msg/Twist "{
        linear: {x: 0.1, y: 0.0, z: 0.0}, 
        angular: {x: 0.0, y: 0.0, z: 0.1}}"
    ```

## Published
1. `/${tita_ns}/joint_states`
Topic type: `sensor_msgs/msg/JointState`
打印机器人关节信息, 包含`position`, `velocity`, `effort`

    ``` bash
    # ros2 topic echo /${tita_ns}/joint_states
    header:
    stamp:
        sec: 1728640435
        nanosec: 207354406
    frame_id: ''
    name:
    - joint_left_leg_1
    - joint_left_leg_2
    - joint_left_leg_3
    - joint_left_leg_4
    - joint_right_leg_1
    - joint_right_leg_2
    - joint_right_leg_3
    - joint_right_leg_4
    position:
    - 0.44081687927246094
    - 1.0672786235809326
    - -2.6032021045684814
    - 2.209383249282837
    - -0.5037123560905457
    - 1.1171343326568604
    - -2.625253915786743
    - 0.26672905683517456
    velocity:
    - -0.0
    - 0.010471980087459087
    - -0.0
    - 0.0
    - 0.0
    - -0.0
    - -0.0
    - -0.0
    effort:
    - -0.0
    - 0.030666524544358253
    - -0.0
    - -0.02499999850988388
    - 0.0
    - -0.0
    - -0.0
    - 0.016919462010264397
    ---
    ```

1. `/${tita_ns}/imu_sensor_broadcaster/imu`
Topic type: `sensor_msgs/msg/Imu`
打印机器人imu sensor信息, 包含`orientation`, `angular_velocity`, `linear_acceleration`

    ``` bash
    # ros2 topic echo /${tita_ns}/imu_sensor_broadcaster/imu
    header:
    stamp:
        sec: 1728640659
        nanosec: 77332444
    frame_id: imu
    orientation:
    x: -0.004162624944001436
    y: 0.0013127117417752743
    z: -0.12123985588550568
    w: 0.9927361011505127
    orientation_covariance:
    - 0.0
    - 0.0
    - 0.0
    - 0.0
    - 0.0
    - 0.0
    - 0.0
    - 0.0
    - 0.0
    angular_velocity:
    x: -0.009841999970376492
    y: -0.004255999810993671
    z: -0.004788000136613846
    angular_velocity_covariance:
    - 0.0
    - 0.0
    - 0.0
    - 0.0
    - 0.0
    - 0.0
    - 0.0
    - 0.0
    - 0.0
    linear_acceleration:
    x: 0.0
    y: -0.08621344715356827
    z: 9.785225868225098
    linear_acceleration_covariance:
    - 0.0
    - 0.0
    - 0.0
    - 0.0
    - 0.0
    - 0.0
    - 0.0
    - 0.0
    - 0.0
    ---
    ```

