# 机械臂配置使用教程
```{toctree}
:maxdepth: 1
:glob:
```
------

## MCU Board
上层SOC和下层MCU通过CANBUS实现通信。此方法通过上层计算好 `set_tilt`通过CANBUS发送到下层，实现一定的底盘稳定控制。
![arm1](../_static/arm1.png)

## SOC Board
目前粗略适配了三种机械臂，**Airbot** 、**RM_65** 以及 **Piper** ，目前 Airbot无法直接安装在 Ubuntu22.04上，适配较为麻烦，其他两种适配较为简单
||  aibot | RM_65 | Piper |
|-------|-------|-------|---------|
| ros api | ros1/noetic | ros1/noetic<br>ros2/humble | ros1/noetic<br>ros2/humble |

配置的仓库地址：

- Airbot on TITA: https://github.com/DDTRobot/airbot_on_tita
- airbot joy: https://github.com/DDTRobot/airbot_joy

## AIRBOT（求之）
### 配置
Airbot原生在ubuntu20.04下支持, 且提供支持ros1, 因此在NX上安装docker, 安装docker教程如下[Docker在ARM安装](docker_on_arm.md), 如果后续系统默认带有docker, 则无需安装  

### Docker镜像
- Airbot官方提供镜像配置
以下两个为Airbot提供原生的docker镜像链接和网盘链接，可选择其中一个下载docker：
1. https://repo.ddt.dev/static/manipulator/airbot/image/arm-control.tar
2. https://pan.baidu.com/s/1FHfqTxuFpB5MVb9BkKS9kA?pwd=ddt1 提取码: ddt1

安装好docker后，通过如下命令安装：
```bash
docker image load -i ./arm-control.tar
```
- 默认此镜像内带有ros-noetic，通过类似如下的命令来进入docker
```bash
docker run -it --rm --name airbot --privileged --cap-add=SYS_PTRACE -v $HOME/.ssh:/root/.ssh --network=host -v ~/manipulator:/workspace --workdir /workspace registry.qiuzhi.tech/airbot-play/arm-control:2.9.0 /bin/bash
```
```{note}
需要额外安装ros2-humble 以及ros1_bridge
- ros2-humble安装: https://blog.csdn.net/m0_62353836/article/details/129730981
- ros1-bridge安装: https://zhuanlan.zhihu.com/p/651809579
```
- 在docker内，需要配置一下环境变量
```bash
1. echo 'export ROS_DOMAIN_ID=69' >> ~/.bashrc # 取决与你的tita的实际domain_id
2. echo 'export RMW_IMPLEMENTATION=rmw_cyclonedds_cpp' >> ~/.bashrc
3. echo 'export ROS1_PATH=/opt/ros/noetic/setup.bash' >> ~/.bashrc
4. echo 'export ROS2_PATH=~/ros2_humble/install/setup.bash' >> ~/.bashrc
5. echo 'export ROS_BRIDGE=~/ros1_bridge/install/setup.bash' >> ~/.bashrc #取决与你的ros2及bridge实际安装位置
```
```{note}
以上配置如果后续NX镜像自带, 则无需额外配置
```

## 启动
### 硬件配置

**TITA机器人** x1
**电源板** x1
**TypeC 连接线** x1
**Airbot** x1
**夹爪** x1
**夹爪连接线** x1

将以上硬件连接起来，如图所示：
![arm2](../_static/arm2.png)
### 软件配置
- 通过ssh进入TITA机器人
```bash
ssh robot@192.168.42.1 # wire connected to host, if use wifi, check your tita ip address 
```
- 新建一个工作目录，拉取机械臂相关代码，编译及启动（可遵循以下指令，一步步执行）
```bash
cd 
mkdir manipulator && cd manipulator
git clone http://git.ddt.dev:9281/lkx8421/manipulator_ws.git
cd airbot_ws
chmod +x *.bash
./docker_run.bash
# in docker container
source /opt/ros/noetic/setup.bash
catkin_make
./can_up.bash # success if print "can1 up success"
./ros_run.bash # launch ros_interface of airbot
# if in terminal print such as : 
# terminate called after throwing an instance of 'std::runtime_error'
# what():  AIRBOT Play needs to be calibrated. Please run airbot_auto_set_zero or airbot_set_zero
# please kill with `Ctrl+C` and run with `airbot_set_zero -m can1` to set arm to zero position
# more information of airbot please refer to https://discover-robotics.github.io/docs/latest/AIRBOT-Play/tutorials/env/
```
```{note}
配置完以上步骤后，机械臂类似 '喀嗒'声响, 正常启动成功, 在正常编译好程序后, 可以在`host`内`./one_start.bash`启动
```
- 可以使用机器人遥控器控制机械臂
```{note}
使用机器人操控机械臂时，遥控器无法控制机器人。
```
使用以下指令更改遥控器控制权限
```bash
mkdir -p airbot_joy/src && cd airbot_joy/src
git clone https://git.ddt.dev:9281/rbt/manipulator/aibot_joy
cd ..
colcon build 
source install/setup.bash
ros2 launch airbot_joy airbot_joy.launch.py
```
- 遥控器上更改操控模式
1. 按一下遥控器上方小屏幕右侧按钮进入菜单
2. 选择并单击第二项模式（user-sdk模式，选择成功会在前方显示 “ * ”）
3. 左摇杆控制机械臂末端XY轴，右摇杆控制Z轴，右下按钮单击复位机械臂
4. 注意底盘和臂的控制是解耦的，非sdk模式目前直接控制底盘，而sdk模式则只操作机械臂

### 关闭机械臂
1. 机器连接电脑，并在电脑新建终端
2.使用ssh 进入机器人
3.先输入指令停止机械臂：`docker exec airbot pkill -SIGINT -f "roslaunch ros_interface airbot_arm.launch"`
4.关闭`docker` : `docker stop airbot`
```{note}
如果需要重新启动机械臂，可重新按照 `one_start`来执行即可。
```