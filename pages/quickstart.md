# Quick Start
```{toctree}
:maxdepth: 1
:glob:
```
------
针对一些新手用户我们提供了为TITA Ubuntu系统量身打造的Demo，该Demo是通过ROS2控制机器人进行简单动作并熟悉TITA系统的开发流程、系统框架、功能特点等。接下来就让我们快速上手TITA！

这是TITA Demo在github上的仓连接：https://github.com/DDTRobot/TITA-SDK-ROS2

## SDK操作步骤

- 首先我们要进入TITA的系统中
```bash
ssh robot@192.168.42.1
password : apollo
```
- 进入系统后我们为需要克隆的代码仓建一个文件夹并进入,如图
```bash
mkdir -p tita-sdk/src
cd tita-sdk/src
```
![sdk1](./../_static/sdk1.jpg)
- 进入文件夹后需要将我们SDK的仓克隆下来并编译
```bash
git clone https://github.com/DDTRobot/TITA-SDK-ROS2.git
colcon build

Notice:在执行编译时可能会出现 colcon commond not found，我们就需要安装一下 colcon 工具，执行 sudo apt install python3-colcon-common-extensions

```
- 编译完成后会有以下打印信息，如图
![sdk2](./../_static/sdk2.jpg)

- 一切准备好后，我们先要`source` SDK中的setup.bash
```bash
source install/setup.bash
```
- 最后我们就可以开始执行SDK啦！欢迎来到TITA的世界！
```bash
ros2 launch tita_bringup sdk_launch.py
```