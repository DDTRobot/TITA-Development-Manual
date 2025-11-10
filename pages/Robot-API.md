# 高层运动接口

```{toctree}
:maxdepth: 1
:glob:

```

------

#### 获取状态时间检测
```bash 


  /**
     * @brief Get the current states update timeout.
     * @return bool: if current states not update, return true.
     */
  bool data_timeout() const;
```
#### 获取关节位姿
```bash 
  /**
     * @brief Get the current joint positions in joint space.
     * @return std::vector<double>: current joint positions in radians.
     */
  std::vector<double> get_joint_q() const;
```
#### 获取关节速度
```bash
  /**
     * @brief Get the current joint velocities in joint space.
     * @return std::vector<double>: current joint velocities in radians per second.
     */
  std::vector<double> get_joint_v() const;
```
#### 获取关节力矩
```bash
  /**
     * @brief Get the current joint torques in joint space.
     * @return std::vector<double>: current joint torques in Newton meters.
     */
  std::vector<double> get_joint_t() const;
```
#### 获取关节状态
```bash
  /**
     * @brief Get the current joint status.
     * @note Joints status now is in bool value, true means the joint is online(TODO).
     * @return std::vector<uint16_t>: current joint status.
     */
  std::vector<uint16_t> get_joint_status() const;
```
#### 获取机器人状态
```bash
  /**
     * @brief Get the current robot loco status.
     * @return robot_status_t: current robot status.
     */
  std::string get_robot_status() const;

```
#### 获取IMU四元数
```bash
  std::array<double, 4> get_imu_quaternion() const;  // x y z w

  /**
     * @brief Get the current imu acceleration of mcu.
     * @return std::array<double, 3>: current acceleration.
     */
```
#### 获取IMU加速度
```bash
  std::array<double, 3> get_imu_acceleration() const;

  /**
     * @brief Get the current imu angular velocity of mcu.
     * @return std::array<double, 3>: current angular velocity.
     */
```
#### 设置IMU角速度
```bash
  std::array<double, 3> get_imu_angular_velocity() const;
```
#### 设置控制模式
```bash
  // /**
  //  * @brief Set mcu board control mode, maybe remove in the future.
  //  * @param mode the target mcu mode, option: READY_WAITING AUTO_LOCOMOTION FORCE_DIRECT.
  //  *
  //  * @return return true if the target is set successfully
  //  */
  // bool set_board_mode(ready_next_t mode);
  /**
     * @brief Set mcu board can direct drive motors, default is auto_locomotion(use mcu control).
     * @param if_sdk true means use control motors sdk, false means use mcu control.
     *
     * @return return true if the target is set successfully
     */

 bool set_motors_sdk(bool if_sdk);

 ```

 #### 设置RC输入
```bash
  /**
     * @brief Set rc input to mcu. Only used in board mode is AUTO_LOCOMOTION.
     * @param forward the target forward.
     * @param yaw the target yaw.
     * @param pitch the target pitch.
     * @param roll the target roll.
     * @param height the target height.
     * @param split the target split.
     * @param tilt the target tilt.
     * @param forward_accel the target forward acceleration.
     * @param yaw_accel the target yaw acceleration.
     * @return return true if the target is set successfully
     */
  bool set_rc_input(can_device::api_channel_input_t input);
  /**
     * @brief Set rc input to mcu. Only used in board mode is AUTO_LOCOMOTION.
     * @param stand true if stand.
     * @return return true if the target is set successfully
     
     */
```
#### 站立
```bash
  bool set_robot_stand(bool stand);

  /**
     * @brief Set rc input to mcu. Only used in board mode is AUTO_LOCOMOTION.
     * @param jump true to start robot charge, then false change to start jump.
     * @return return true if the target is set successfully
     */
```
#### 软急停

```bash
  bool set_robot_stop();
  
```
#### 趴下
```bash
  bool set_robot_down(bool down);
```
