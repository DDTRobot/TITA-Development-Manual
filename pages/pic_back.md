# TITA Image Transmission Configuration

```{toctree}
:maxdepth: 1
:glob:
```

------
As we all know, TITA contains many yet-to-be-discovered capabilities. This chapter introduces TITA's image transmission function. You can connect it to our racing simulator and enjoy an exciting race with your friends, or use it in inspection scenarios to receive real-time visual feedback to the terminal through image streaming.

## How to Install TITA Image Transmission Package

```{note}
Note! The built-in OpenCV in TITA may cause software conflicts during installation. Please uninstall OpenCV before proceeding.
```

1. Follow the steps below strictly to install the image transmission package:
```bash
1. sudo apt update 
2. sudo apt remove --purge libopencv-dev  # Uninstall OpenCV
3. sudo apt autoremove
4. sudo apt install libopencv-dev=4.5.4+dfsg-9ubuntu4
```

2. Install the ROS package:
```bash
sudo apt install ./tita-ros2-20250311164048.deb
```

3. Modify `/lib/systemd/system/tita-bringup.service` and set `Environment="ROS_LOCALHOST_ONLY=1"` to `0`;  
Also set the following in the terminal:
```bash
export ROS_DOMAIN_ID=45
```

```{note}
After completing the above steps:  
Launch `index.html`, enter the local IP address in the TITA Broker IP field, leave the username and password blank.  
Once connected, you will see real-time image transmission. Audio customization is not supported in the current version.
```

To get the installation package and webpage, visit the link: https://pan.baidu.com/s/14xZ87vO32fzI3aSUFQnyOw?pwd=p552