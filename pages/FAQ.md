## Frequently Asked Questions

### Unable to SSH into TITA host

Please check the following:

1. Ensure the network connection is working properly.  
2. Do not keep the flashing cable plugged into the DBG port when powering on. Otherwise, the system will enter flashing mode, and SSH login will not work. Unplug the cable and reboot the device.  
3. Some versions of Windows cannot recognize the USB network adapter. You may need to reinstall the driver.

### How to check the system firmware version?

In the terminal, enter:

```
uname -a
```

This will display system version information.

### ROS system is running, but the remote controller has no response?

1. You can use the following command to check joint states:  
   `ros2 topic echo /tita_namespace/joint_states`  
   If the joint state is shown as "offline", it indicates that the locomotion system is offline. This usually happens due to external forces (e.g., collisions or impacts) causing insufficient 48V power supply, making the motors unresponsive. In this case, reboot the robot.

### How to check the version of the ROS deb package?

In the terminal, enter:

```
apt info tita-ros2
```
