# Ubuntu系统刷机教程
```{toctree}
:maxdepth: 1
:glob:
```

------
## 注意事项
1. 请仔细阅读使用须知即刷机文档。如开始进行刷机，即视为已阅读下述须知。产生的相应后果由客户自行负责。
2. 该系统的刷机是不可逆的过程，即刷机成功换成ubuntu系统后无法再刷回原来的Yocto系统。
3. 目前刷机的版本为先行版本，仅用于系统更换，内置功能API较少如下：ToF数据、运动控制功能；后续请关注本末科技官网（）其他功能API的更新。

## 准备工作
硬件准备：TITA随包装的刷机线（标志A朝外插入DBG口，先插线再上电）；Ubuntu系统电脑
此操作需要将刷机包下载至电脑（必须Linux系统）中，并创建新的文件夹，将刷机包解压至新建的文件夹中。

0. 
```bash
sudo apt install abootimg binfmt-support binutils cpio cpp device-tree-compiler dosfstools
        lbzip2 libxml2-utils nfs-kernel-server openssl python3-yaml qemu-user-static
        sshpass udev uuid-runtime whois rsync zstd lz4
        (全部复制，这是NVIDIA刷机所需要的依赖，请首先将以上依赖安装在刷机的电脑中，而不是机器人)
```
1. Download apollo-ubuntu-${date}.tar （下载对应日期的系统软件包；目前最新系统包可找我司FAE同事获取)
2. mkdir apollo-ubuntu（可在电脑系统的任意位置创建文件夹）
3. tar -xf apollo-ubuntu-${date}.tar -C apollo-ubuntu （解压系统软件包至新建文件夹中）

## 开始刷机
进入刚刚创建的文件夹
1. cd  apollo-ubuntu
2. sudo ./flash_robot.sh
注意！部分Ubuntu中可能缺少sshpass和nfs-kernel-server两个插件，缺哪个装哪个
![f1](.././_static/flash1.JPEG)
![f2](.././_static/flash2.JPEG)

## 结束标志
刷机完成时可以看到以下信息
```{bash}
1. Flash is successful
2. Reboot device
3. Cleaning up...
4. Log is saved to Linux_for_Tegra/initrdlog/flash_3-1_0_20240821-140503.log
``` 
并且输入指令`lsusb`能看到这个信息
![f3](.././_static/flash3.JPEG)

## Connect TITA Robot System
可以使用USB3.0的USB-TypeC线插入标志为“DBG”接口使用SSH指令进入机器人系统（注意！随包装的TypeC线为刷机线，不可作为调试线使用）
```bash
ssh robot@192.168.42.1
password: apollo
```

## 如何连接WIFI
刷机过后需要下载ROS包和其他依赖，所以需要先将机器人连接网络，以下是连接当前所在地的WIFI教程：
1.首先 `sudo vim /etc/wpa_supplicant/wpa_supplicant-nl80211-wlan0.conf`
2.修改图中，ssid= "WIFI name"; psk="PassWord"
3.修改完后reboot
4.当机器人重启后会自动连接上述步骤所设置的WIFI
![f8](.././_static/flash8.jpeg)

## 安装依赖
在目前的新系统中为了确保ROS2包能正常运行，所以需要安装以下的依赖：
<!-- #### 安装g2o
在机器人系统中执行以下步骤：
1. `sudo wget http://webdav:qwVNGwbCzjKRWFx0@61.145.190.130:10088/cdFile/ubuntu_deb/g2o-1.2.23-Linux.deb`
2. `sudo dpkg -i g2o-1.2.23-Linux.deb` -->
#### 安装ROS依赖
1. 打开终端输入指令：`ssh robot@192.168.42.1`，Password: `apollo`, 进入机器
2. 下载ROS2包：`sudo wget  http://webdav:qwVNGwbCzjKRWFx0@61.145.190.130:10088/cdFile/ros2_deb/tita-ros2-20241218101915.deb`（版本号以实际情况而定）
3. 执行 `sudo apt-get update`，更新源
4. 执行`sudo dpkg -i tita-ros2-20241218101915.deb`，此次安装是不会成功的，目的是让系统知道需要装什么依赖
5. 执行`sudo apt install -f`，下载包中所需依赖
6. 再执行一次安装指令`sudo dpkg -i tita-ros2-20241218101915.deb`，成功安装即可。
7. 如果嫌上面一条条复制麻烦，可以将下面代码生成bash脚本运行
```{bash} 
#!/bin/bash

# 下载deb包
sudo wget  http://webdav:qwVNGwbCzjKRWFx0@61.145.190.130:10088/cdFile/ros2_deb/tita-ros2-20250515153729.deb

# 更新APT源
sudo apt-get update

# 尝试安装deb包，让系统识别依赖
sudo dpkg -i tita-ros2-20250515153729.deb

# 安装deb包所需依赖
sudo apt install -f

# 再次安装deb包
sudo dpkg -i tita-ros2-20250515153729.deb
```

## 设置ROS2环境
若第一次刷机后，使用ros2指令比如使用`ros2 topic list`或者 `ros2 service list` 会出现没有topic或者service的情况。这时我们需要设置环境，设置ROS2环境需要对两个文件做操作，分别是 `~/.bashrc`；`tita-bringup.service`。
####  1. ~/.bashrc
- 输入:`sudo vim ~/.bashrc`
- 进入~/.bashrc后在最后的位置添加两个字段
```bash
export ROS_DOMAIN_ID=42
source /opt/ros/humble/setup.bash
```
- 保存退出后需要 `source ~/.bashrc`
![f5](.././_static/flash5.JPEG)
#### 2. tita-bringip.service
- 输入 `sudo vim /usr/lib/systemd/system/tita-bringup.service`
- 确保`ROS_DOMAIN_ID=42`,并将`ROS_LOCALHOST_ONLY=1`改成`ROS_LOCALHOST_ONLY=0`，如图
- 修改完成保存退出
![f4](.././_static/flash4.JPEG)
#### 3. 自检
- 如果以上操作都完成后可以执行 `sudo systemctl restart tita-bringup.service`
- 让ROS2服务重启后可以输入 `ros2 topic list`查看是否能print机器里的ros2 topic，如图
![f7](.././_static/flash7.jpeg)

## 网络配置
```bash
sudo apt install network-manager
```
2. 安装完依赖后需要克隆AutoNetworkManager的仓
` git clone http://git.ddt.dev:9281/wuyunzhou/AutoNetworkManager.git`
3. 通过AutoNetworkManager的脚本安装
```bash
cd AutoNetworkManager
chmod 777 install.sh
sudo ./install.sh
```
完成以上步骤后，通过`ifconfig`能看到eth0自动分配IP 192.168.19.97，并且可以ping TITA Tower上默认IP 192.168.19.97。

## 如何配对遥控器
（在机器人上执行此操作）最新的机器人系统现在配备了内置的遥控配对软件，有两种快速配对遥控器的方法。
```{note}
对于较旧的系统版本，您可以联系FAE获取远程控制配对软件的安装包。
```
相应教程可跳转[遥控器配对指南](./Robot-Controller/how-to-pair.md)
## 如何在Ubuntu系统中升级运控和电机
```bash
1. 首先安装OTA应用程序
sudo apt-get install motor-upgrade
Ps.注意电脑中是否安装python3-pip
2. 升级运控板&电机程序指令
otafifth_demo -f $BIN_PATH
3. 升级完成后可查询运控版本
can-app -Version
Ps. 请注意！为保证升级正常,请先确定机器人运行正常(8个电机都通讯正常),并将机器调为趴下状态。
```