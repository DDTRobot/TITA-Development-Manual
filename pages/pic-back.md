# TITA 图传功能配置
```{toctree}
:maxdepth: 1
:glob:
```


------
众所周知，TITA蕴含了许多仍未发现的能力，这章节是讲述了TITA的图传功能，你可以让它接入我们的赛车模拟器与好兄弟一起来一场酣畅淋漓的竞速，也可以在巡检场景中通过图传实时获取信息反馈给终端。

## 如何安装TITA图传包
```{note}
注意！TITA自带的Opencv在安装时会造成软件冲突，需要卸载 Opencv 后再进行安装
```
1. 需要严格按照以下步骤进行安装图传包
```bash
1. sudo apt update 
2. sudo apt remove --purge libopencv-dev //卸载OpenCV
3. sudo apt autoremove
4. sudo apt install libopencv-dev=4.5.4+dfsg-9ubuntu4
```

2. 安装ROS包
```bash
sudo apt install ./tita-ros2-20250311164048.deb
```

3. 设置修改 /lib/systemd/system/tita-bringup.service 并设置Environment="ROS_LOCALHOST_ONLY=1" 为 0；
并在终端设置对应的 export ROS_DOMAIN_ID=45
```bash
sudo apt install ./tita-ros2-20250311164048.deb
```
```{note}
完成以上步骤后；
启动index.html , 在 TITA Broker IP 窗口输入局域网IP地址，用户名密码为空
连接可看到实时图传，当前版本自定义音频暂不开放。
```

获取安装包和网页可以跳转该链接：https://pan.baidu.com/s/14xZ87vO32fzI3aSUFQnyOw?pwd=p552