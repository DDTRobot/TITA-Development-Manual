# 数据读取接口

```{toctree}
:maxdepth: 1
:glob:

```

------


一、 获取关节位姿
```bash 
  /**
     * @brief Get the current joint positions in joint space.
     * @return std::vector<double>: current joint positions in radians.
     */
  std::vector<double> get_joint_q() const;
```
二、 获取关节速度
```bash
  /**
     * @brief Get the current joint velocities in joint space.
     * @return std::vector<double>: current joint velocities in radians per second.
     */
  std::vector<double> get_joint_v() const;
```
三、 获取关节力矩
```bash
  /**
     * @brief Get the current joint torques in joint space.
     * @return std::vector<double>: current joint torques in Newton meters.
     */
  std::vector<double> get_joint_t() const;
```
四、 获取关节状态
```bash
  /**
     * @brief Get the current joint status.
     * @note Joints status now is in bool value, true means the joint is online(TODO).
     * @return std::vector<uint16_t>: current joint status.
     */
  std::vector<uint16_t> get_joint_status() const;
```

五、 获取IMU四元数
```bash
  std::array<double, 4> get_imu_quaternion() const;  // x y z w

  /**
     * @brief Get the current imu acceleration of mcu.
     * @return std::array<double, 3>: current acceleration.
     */
```
六、 获取IMU加速度
```bash
  std::array<double, 3> get_imu_acceleration() const;

  /**
     * @brief Get the current imu angular velocity of mcu.
     * @return std::array<double, 3>: current angular velocity.
     */
```
七、 获取IMU角速度
```bash
  std::array<double, 3> get_imu_angular_velocity() const;
