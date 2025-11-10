# 底层运动控制 
```{toctree}
:maxdepth: 1
:glob:
```
------

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

tita_robot robot(8);



void test_write()
{

    robot.set_motors_sdk(true);
    while (1)
    {
      std::cout << "=================================" << std::endl;
      std::vector<double> t = {0.0, 0.0, 0.0, 1.0, 0.0, 0.0, 0.0, 0.0};
      robot.set_joint_torque(t);
      sleep(1);
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

#### 运动接口
##### 设置电机力矩
```bash
 /**
     * @brief Set the target joint feed-forward torques.
     * @param t the target joint feed-forward torques.
     * @return return true if the target is set successfully.
     */
  bool set_target_joint_t(const std::vector<double> & t);
```

#### 设置电机PD控制
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