# Ubuntu System Flashing Process
```{toctree}
:maxdepth: 1
:glob:
```

------
## Precautions
1.  Please read the usage instructions and flashing documentation carefully. Starting the flashing process implies that you have read the following instructions. Any consequences that arise are the responsibility of the customer.
2. Flashing the system is an irreversible process; once the Ubuntu system is successfully installed, it is not possible to flash back to the original Yocto system.
3. The current version of the flash is a preliminary version intended for system replacement, with a limited number of built-in functional APIs as follows: ToF data, motion control functions; for future updates on other functional APIs, please pay attention to the official website of Moonshot Robotics.

## Preparation Work
Hardware Preparation: The flashing cable that comes with TITA (with logo A facing outwards, insert into the DBG port, plug in the cable before powering on); an Ubuntu system computer.
This operation requires downloading the flashing package to the computer (a Linux system is required), creating a new folder, and extracting the flashing package into the newly created folder.
```bash
0. sudo apt install abootimg binfmt-support binutils cpio cpp device-tree-compiler dosfstools
        lbzip2 libxml2-utils nfs-kernel-server openssl python3-yaml qemu-user-static
        sshpass udev uuid-runtime whois rsync zstd lz4 (in your computer system which to flash the robot)
1. Download apollo-ubuntu-${date}.tar （Download the system software package corresponding to the date）
2. mkdir apollo-ubuntu（You can create a folder at any location in your computer's system）
3. tar -xf apollo-ubuntu-${date}.tar -C apollo-ubuntu （Extract the system software package into the newly created folder）
```

## Begin the flashing process.
Navigate into the folder you just created.
1. cd  apollo-ubuntu
2. sudo ./flash_robot.sh
Attention! Some Ubuntu systems may lack the sshpass and nfs-kernel-server plugins. If either is missing, install the one that is not present.
![f1](.././_static/flash1.JPEG)
![f2](.././_static/flash2.JPEG)

## Termination Indicator
When the flashing is complete, you should see the following information:
```{bash}
1. Flash is successful
2. Reboot device
3. Cleaning up...
4. Log is saved to Linux_for_Tegra/initrdlog/flash_3-1_0_20240821-140503.log
``` 
And by entering the command `lsusb`, you can see this information.
![f3](.././_static/flash3.JPEG)

## Connect TITA Robot System
You can use a USB 3.0 USB-Type C cable to insert into the "DBG" interface and use SSH commands to enter the robot system (Note! The Type C cable included with the package is for flashing and should not be used as a debugging cable).
```bash
ssh robot@192.168.42.1
password: apollo
```

## How to connect WIFI
After flashing, you will need to download ROS packages and other dependencies, so you must first connect the robot to the network. Here is a tutorial on how to connect to the local WIFI:

1. First, run sudo vim /etc/wpa_supplicant/wpa_supplicant-nl80211-wlan0.conf
2. Modify the configuration to include your network's SSID and password, like so: ssid="WIFI name"; psk="Password"
3. After making the changes, reboot the system with reboot
4. Once the robot restarts, it will automatically connect to the WIFI network you configured in the previous steps.
![f8](.././_static/flash8.jpeg)

## Install Dependencies
In the new system, to ensure that the ROS2 packages can run properly, you need to install the following dependencies:
#### Install g2o
Execute the following steps in the robot system:
1. `sudo wget http://webdav:qwVNGwbCzjKRWFx0@61.145.190.130:10088/cdFile/ubuntu_deb/g2o-1.2.23-Linux.deb`
2. `sudo dpkg -i g2o-1.2.23-Linux.deb`
#### Install ROS Dependencies
1. Open Terminal and input：`ssh robot@192.168.42.1`，Password: `apollo`, connect Robot
2. Download ROS2 package：`sudo wget  http://webdav:qwVNGwbCzjKRWFx0@61.145.190.130:10088/cdFile/ros2_deb/tita-ros2-20241017000618.deb`
3. Execute `sudo apt-get update` to update the package sources.
4. Execute `sudo dpkg -i tita-ros2-20241017000618.deb`. This installation will not succeed, but it will inform the system of the dependencies needed.
5. Execute `sudo apt install -f` to download the required dependencies.
Run the installation command again with `sudo dpkg -i tita-ros2-20241017000618.deb`. If successful, the installation is complete.
7. If you find it troublesome to copy each command separately, you can create a bash script from the following code and run it:
```{bash} 
#!/bin/bash

# download deb
sudo wget http://webdav:qwVNGwbCzjKRWFx0@61.145.190.130:10088/cdFile/ros2_deb/tita-ros2-20241017000618.deb

# update package source
sudo apt-get update

# Attempt to install the .deb package (this will not succeed yet)
sudo dpkg -i tita-ros2-20241017000618.deb

# Install the dependencies needed for the .deb package
sudo apt install -f

# Retry installing the .deb package
sudo dpkg -i tita-ros2-20241017000618.deb
```

## Setting up the ROS2 environment
If after the first flash you use ROS2 commands such as `ros2 topic list` or `ros2 service list` and there are no topics or services showing up, we need to set up the environment. Setting up the ROS2 environment requires manipulation of three files, which are `~/.bashrc`, `local_setup.bash`, and `tita-bringup.service`.
####  1. ~/.bashrc
- Enter the following command: `sudo vim ~/.bashrc`
- After opening the `~/.bashrc` file, add the following two lines at the end:
```bash
export ROS_DOMAIN_ID=42
source /opt/ros/humble/setup.bash
```
- After saving and exiting, you need to: `source ~/.bashrc`
![f5](.././_static/flash5.JPEG)
#### 2. tita-bringip.service
- enter `sudo vim /usr/lib/systemd/system/tita-bringup.service`
- Ensure that `ROS_DOMAIN_ID=42`, and change `ROS_LOCALHOST_ONLY=1` to `ROS_LOCALHOST_ONLY=0`, as shown in the figure.
- After making the changes, save and exit.
![f4](.././_static/flash4.JPEG)
#### 3. local_setup.bash
- Enter the command: `sudo vim /opt/ros/humble/local_setup.bash`
- Add the field `export ROS_DOMAIN_ID=42` at the end of the file.
- After setting up, save and exit, then execute `source local_setup.bash`.
![f6](.././_static/flash6.jpeg)
#### 4. selfcheck
- If all the above operations are completed, you can execute `sudo systemctl restart tita-bringup.service`.
- After restarting the ROS2 service, you can enter `ros2 topic list` to check if the ROS2 topics on the machine are being printed, as shown in the figure.
![f7](.././_static/flash7.jpeg)

## Network Configuration
This network configuration is for the network allocation of the TITA Tower accessory, allowing you to assign a unique IP for use with the TITA Tower in coordination with the robot.
1. Install Dependencies
```bash
sudo apt install network-manager
sudo apt install systemd-networkd
```
2. After installing the dependencies, you need to clone the AutoNetworkManager repository:
` git clone http://git.ddt.dev:9281/wuyunzhou/AutoNetworkManager.git`
3. Install through the script provided by AutoNetworkManager.
```bash
cd AutoNetworkManager
chmod 777 install.sh
./install.sh
```
After completing the above steps, you should be able to see that eth0 has been automatically assigned an IP of `192.168.19.97` using the `ifconfig` command, and you should be able to ping the default IP of the TITA Tower, which is `192.168.19.97`.


## How to pair Controller
（Perform this operation in the robot）
1. Use git clone to clone the remote control pairing script git clone 
`git clone http://git.ddt.dev:9281/wuyunzhou/crsf-app.git`
2. `cd crsf-app`
3. `chmod 777 install_ubuntu.sh`
4. `sudo ./install_ubuntu.sh`
5. Execute the command `crsf-app -bind`, you can observe the return：   
```{bash}
root@apollo-nx:~# crsf-app -bind   
正在检查串口通讯状态...   
uart connect success   
正在进入配对模式...  
 bind mode success   
请打开遥控器,左长按右侧按键进入TOOLS->ExpressLRS->[Bind],手动搜索配对
```
![f9](.././_static/flash9.png)
6. After powering on the remote control, push the button on the right side to the left to enter the interface, then press the buttons in sequence to go to `Tools -> ExpressLRS -> bind mode` for pairing the receiver.
 ![controller2](./../_static/controller2.JPEG)
 ![controller3](.././_static/controller3.JPEG)
7. Pairing completed, return "pair success"
![controller4](.././_static/controller4.PNG)
## How to upgrade motion control and motors in the Ubuntu system
1. Perform the following operations first in the robotic system
```bash
sudo git clone git@git.ddt.dev:wuyunzhou/motor_upgrade.git /usr
sudo cp /usr/motor_upgrade/ota_lib/*.so /usr/lib
sudo cp /usr/motor_upgrade/ota_lib/otafifth_demo /usr/bin
sudo pip install pycryptodome
sudo pip install crcmod
```
2. After completing the aforementioned steps, you need to run the upgrade script.
```bash
cd ~/motor-patch/
chmod 777 run.sh
sudo ./run.sh
```
3.After the upgrade is complete, restart the machine by powering it down and then back up.
