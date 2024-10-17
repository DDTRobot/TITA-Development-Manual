# Quick Start
```{toctree}
:maxdepth: 1
:glob:
```
------
For novice users, we have provided a tailored Demo for the TITA Ubuntu system. This Demo allows you to control the robot to perform simple actions and become familiar with the development process, system framework, and functional features of the TITA system. Let's quickly get started with TITA!

TITA Demo in GitHub：https://github.com/DDTRobot/TITA-SDK-ROS2

## SDK Operation Steps

- First, we need to access the TITA system
```bash
ssh robot@192.168.42.1
password : apollo
```
- After entering the system, we need to create a folder for the code repository we want to clone and then enter it, as shown in the figure.
```bash
mkdir -p tita-sdk/src
cd tita-sdk/src
```
![sdk1](./../_static/sdk1.jpg)
- After entering the folder, we need to clone our SDK repository and then compile it.
```bash
git clone https://github.com/DDTRobot/TITA-SDK-ROS2.git
colcon build

Notice:During compilation, you may encounter the error "colcon command not found." In this case, you will need to install the colcon tool by running the command sudo apt install python3-colcon-common-extensions.

```
- After the compilation is complete, you will see the following printed information, as shown in the figure.

![sdk2](./../_static/sdk2.jpg)

- Once everything is ready, you first need to `source` the setup.bash in the SDK.
```bash
source install/setup.bash
```
- Finally, you can start executing the SDK! Welcome to the world of TITA!
```bash
ros2 launch tita_bringup sdk_launch.py
```