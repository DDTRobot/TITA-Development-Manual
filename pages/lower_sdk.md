# 底层运动控制 
```{toctree}
:maxdepth: 1
:glob:
```
------

一、应用示例

本节介绍指导用户如何使用 D1_SDK 创建一个属于自己的底层运动控制程序。利用tita_robot.hpp 创建一个tita_robot对象，并调用相应的接口函数，实现机器人控制。实现机器人站立，例子如下 ：

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

int main(){
    // 创建机器人实例（如果需要使用vcan，可传入参数）
  tita_robot robot(8); 
    
  std::cout << "Tita Robot测试程序启动" << std::endl;
  robot.set_motors_sdk(true);
  for (int i = 0; i < 10; ++i) {
            // 等待100ms
      std::vector<double> t = {0.0, 0.0, 0.0, 1.0, 0.0, 0.0, 0.0, 0.0};
      robot.set_target_joint_t(t);

      std::this_thread::sleep_for(std::chrono::milliseconds(100));
        }

  std::cout << "测试程序结束" << std::endl;
  return 0;


```

创建CMakeLists.txt文件
```bash
cmake_minimum_required(VERSION 3.10)
project(lower_sdk_example)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_compile_options(-Wall -Wextra -Wpedantic)
set(LOWER_SDK "/opt/y1_ros2/")

include_directories(
    ${LOWER_SDK}/include
)

link_directories(
    ${LOWER_SDK}/lib  
)

add_executable(lower_sdk_example lower_sdk_example.cpp)

target_link_libraries(lower_sdk_example
    tita_robot  
    pthread     
)
```

二、运动控制接口
（1） 设置电机力矩
```bash
 /**
     * @brief Set the target joint feed-forward torques.
     * @param t the target joint feed-forward torques.
     * @return return true if the target is set successfully.
     */
  bool set_target_joint_t(const std::vector<double> & t);
```

（2）设置电机PD控制
```bash
  /**
     * @brief MIT control method. Set the target joint positions, velocities, kp, kd and feed-forward torques of the
     motors.
     * @param q the target joint positions in radians.
     * @param v the target joint velocities in radians per second.
     * @param kp the target joint proportional gains.
     * @param kd the target joint derivative gains.
     * @param t the target joint feed-forward torques.
     *
     * @return return true if the target is set successfully
     */
  bool set_target_joint_mit(
    const std::vector<double> & q, const std::vector<double> & v, const std::vector<double> & kp,
    const std::vector<double> & kd, const std::vector<double> & t);
```