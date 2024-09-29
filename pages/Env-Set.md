# Environment Configuration
----
This section describes how to configure the secondary development compilation environment.

- After inserting the Debug data cable into the DBG port, connect it to the computer.
- After completing the wiring, open the command terminal and enter `ssh root@192.168.55.1` to log in.
- Configure the WIFI connection either through the command line；
```{note}
If use command line, you can enter this command
nmcli dev wifi connect <wifi name> password <password>
If connected Success will return like this:
Device 'wlan0' successfully activated with 'a43402c8-b98d-443a-be61-e19484882a65'.
```
- Once the WIFI connection is successful, use the docker pull command to download the Ubuntu docker
`docker pullregistry.cn-hangzhou.aliyuncs.com/ddt_robot/nvidia-ubuntu`
- After the download is complete, proceed with the environmental configuration. You can open the two configuration files `/lib/systemd/system/tita-vision.service` and `/lib/systemd/system/tita-bringup.service`, and modify the two variables `Environment="ROS_LOCALHOST_ONLY=0"`；
- After the environment is configured, restart the Docker to compile your developed ROS2 code inside the Docker.
```{note}
The Type-C cable included with the robot is a flashing cable, which will automatically enter recovery mode when connected to the robot, hence it cannot be used as a debug cable. For debugging purposes, please use another USB Type-C cable.
```