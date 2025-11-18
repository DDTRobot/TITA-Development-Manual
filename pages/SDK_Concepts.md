# 应用开发
```{toctree}
:maxdepth: 1
:glob:
```
------




## SDK介绍

D1_sdk_ros2 是基于ROS2开发，将高层逻辑封装成ROS2节点，提供ROS2 API给用户使用，用户通过ROS2 topic 发送指令给机器人，完成机器人控制。

查看ros话题
```bash 
robot@tita:~$ ros2 topic list 
/d13043495/battery_info_broadcaster/battery/battery1 # 主机电池信息
/d13043495/battery_info_broadcaster/battery/battery2 # 从机电池信息
/d13043495/battery_info_broadcaster/transition_event
/d13043495/body/fsm_mode # 本体状态机
/d13043495/body/motors_status # 电机状态
/d13043495/command/cmd_key # 控制指令，状态机切换
/d13043495/command/cmd_pose # 控制指令，位姿
/d13043495/command/cmd_twist # 控制指令，速度
/d13043495/dynamic_joint_states
/d13043495/imu_sensor_broadcaster/imu # imu状态
/d13043495/imu_sensor_broadcaster/transition_event
/d13043495/joint_state_broadcaster/transition_event
/d13043495/joint_states # 关节信息 位置速度力据
/d13043495/joy # 遥控器stick值相关
/d13043495/robot_description 
/d13043495/y1v0h_rl_controller/transition_event
/parameter_events
/rosout
/tf
/tf_static
```
如果没有，将下文添加在~/.bashrc结尾后执行source ~/.bashrc再输入查看ros话题命令
```bash 
export ROS_LOCALHOST_ONLY=1
export ROS_DOMAIN_ID=42
source /opt/ros/humble/setup.bash

```

1. `command/manager/cmad_key`
2. Topic type: `std_msgs/msg/String`
机器人状态机切换：状态机包含以下：`transform_up` `idle` `transforn_down` `loco` `joint_pd` `car`
`rl_1` `rl_2` `rl_3`

示例：
```bash
source /opt/y1_ros2/setup.bash 

# 站立     
ros2 topic pub -1 /$ROBOT_NS/command/manager/cmd_key std_msgs/msg/String "data: 'transform_up'"     

# 趴下     
ros2 topic pub -1 /$ROBOT_NS/command/manager/cmd_key std_msgs/msg/String "data: 'transform_down'"    
 
# 平地   
ros2 topic pub -1 /$ROBOT_NS/command/manager/cmd_key std_msgs/msg/String "data: 'loco'"

# 策略1
ros2 topic pub -1 /$ROBOT_NS/command/manager/cmd_key std_msgs/msg/String "data: 'rl_1'"          

```


3. `command/manager/cmd_pose` 
Topic type: geometry_msgs/msg/PoseStamped
机器人头部位置姿态控制指令，目前仅仅为pitch（双轮足loco状态下）

```bash 
source /opt/y1_ros2/setup.bash 
ros2 topic pub -1 /$ROBOT_NS/command/manager/cmd_pose geometry_msgs/msg/PoseStamped "{         
    header: {             
        stamp: {                 
            sec: 0,   
            nanosec: 0}, 
        frame_id: 'world'
        },          
    pose: {             
        position: {x: 0.0, y: 0.0, z: 0.0}, # only valid in z，range in 0.1 to 0.3    
        orientation: {x: 0.0, y: 0.0, z: 0.0, w: 0.0}
        }
}"  

```
说明：通过四元数控制机器人头部姿态，目前仅双轮足loco状态下有效。



4. `command/manager/cmd_twist` 

Topic type: `geometry_msgs/msg/Twist`

机器人速度控制指令,包括linear, angular等, 仅和angular.z有效
```bash
source /opt/y1_ros2/namespace.sh
ros2 topic pub -1 /$ROBOT_NS/command/manager/cmd_twist geometry_msgs/msg/Twist "{         linear: {x: 0.2, y: 0.0, z: 0.0},          
    angular: {x: 0.0, y: 0.0, z: 0.0}}"    

```
说明：取值范围`linear.x`：-3.0 to 3.0、`angular.z`：-0.5 to 0.5




想了解如何获取关节数据、IMU数据，请查看[数据读取接口](Robot-API.md)