# WIFI 便携式应用
```{toctree}
:maxdepth: 1
:glob:
```
------

## 安装部署
```
sudo apt install network-manager
git clone https://github.com/DDTRobot/config_of_documents.git
cd config_of_documents
sudo chmod +x install.sh
sudo ./install.sh
#Power off and restart
```
```{note}
开启ap热点模式
wifi名：TITAxxxxxxx
密码：12345678
ip地址：10.42.0.1 
```

## 使用指令

1、开启ap热点模式
```
 sudo wifi-app -ap_on
```
![wifi_ap_of](../_static/wif-app_ap_on.png)

2、连接wifi
```{warning}
若已经开启ap热点模式，想要连外部 wifi模块需要关掉ap模式:sudo wifi-app -ap_off
```
```
sudo wifi-app -on
```
![wifi_on](../_static/wifi_on.png)
(1) ctrl+c #enter
(2) 输入wifi名 #enter
(3) 密码 #enter
![wifi_app](../_static/wifi_app.png)


3、若想机器人开机默认开启ap模式
```
cd config_of_documents
cp wifi-app.service /etc/systemd/system/
systemctl daemon-reload
systemctl enable wifi-app.service
systemctl restart wifi-app.service
```