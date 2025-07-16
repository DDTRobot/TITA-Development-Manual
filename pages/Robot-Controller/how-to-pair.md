# 遥控手柄配对指南

```{toctree}
:maxdepth: 1
:glob:
```

------
（在机器人上执行此操作）最新的机器人系统现在配备了内置的遥控配对软件，有两种快速配对遥控器的方法。
```{note}
对于较旧的系统版本，使用 `sudo apt install crsf-app` 安装遥控器配对软件
或者您也可以联系FAE获取遥控器配对软件的安装包。
```
## 方法一
1. 使用`sudo dpkg -i crsf-app`（如果已经包含或已安装，请跳过此步骤。）
```{note}
如果没有安装 `crsf-app` 可以通过以下指令
`sudo apt-get install crsf-app.` 
```
2. 执行指令`crsf-app -bind`，可以观察到返回：
![f9](../../_static/flash9.jpg) 
3. 遥控器开机后 右边按键向左推进入界面后 按键依次进入Tools ->ExpressLRS-> bind模式，进行配对接收机.
 ![controller2](../../_static/controller2.JPEG)
 ![controller3](../../_static/controller3.JPEG) 
4. 配对完成返回pair success
![controller4](../../_static/controller4.jpg) 

## 方法二
1. 首先，您需要一根双头Type-C数据线，如下所示：
![flash11](../../_static/flash11.jpg)
2. 将数据线连接到机器人上的EXT端口和遥控器上的数据端口，如下所示：
![flash12](../../_static/flash12.jpg)
![flash13](../../_static/flash13.jpg)
```{note}
机器人和控制器必须处于开启状态。
```
3. 遥控器和机器人连接后，遥控器会出现`Select mode`的界面，并选择第三个选项`USB Serial`
![flash16](../../_static/flash16.jpg)
4. 耐心等待配对。如果配对成功，机器人的电池信息将显示在遥控器界面的右上角。
![flash15](../../_static/flash15.jpg)