# 应用开发
```{toctree}
:maxdepth: 1
:glob:
```
------




## SDK介绍

D1_sdk_ros2 是基于ROS2开发，将高层逻辑封装成ROS2节点，提供ROS2 API给用户使用，用户通过ROS2 topic 发送指令给机器人，完成机器人控制。

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




### 非ROS层高层运动控制

本节介绍指导用户如何使用 D1_SDK 创建一个属于自己的高层应用例程程序。利用tita_robot.hpp 创建一个tita_robot对象，并调用相应的接口函数，实现机器人控制。实现机器人站立，例子如下 ：
```bash

#include <time.h>

#include <algorithm>
#include <chrono>
#include <iostream>
#include <map>
#include <memory>
#include <string>
#include <thread>

#include "tita_robot/tita_robot.hpp"

tita_robot robot(8);
void test_write()
{
  int example = 1;
  switch (example)
{  
   case 1:
    robot.set_motors_sdk(false);
    std::cout << "robot stand up" << std::endl;
    can_device::api_channel_input_t input;
    while (1)
    {
      robot.set_rc_input(input);
      robot.set_robot_stand(true);
      sleep(1);
    }
    break;
   case 2:
    while(1)
    {
      robot.set_robot_down(true);
      sleep(1);
    }

  default:
    break;
}

}
int main(int argc, char *argv[])
{
  (void)argc;
  (void)argv;
  test_write();
  return 0;
}
```
运动接口详细查阅[高层运动控制接口](./Robot-API.md)