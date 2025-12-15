# 语音播报控制器

```{toctree}
:maxdepth: 1
:glob:
```
------
## Description
语音播报控制器提供给用户一个语音播报功能，用户可以调用这个功能来播放一段语音。

## 示例
```bash
import rclpy 
from rclpy.node import Node
import os
from tita_system_interfaces.srv import PlayAudioSystemPrompts
import asyncio 
import time 
tita_namespace ='tita'
unique_id_file ='/proc/device-tree/serial-number'
try:
    with open(unique_id_file, 'r') as file:
        unique_id = file.read().strip()
        unique_id = unique_id.replace('\x00', '')[6:]
        tita_namespace = 'tita'+unique_id
except FileNotFoundError:
        tita_namespace='tita'
except Exception as e:
        tita_namespace='tita'

class PlayAudio(Node):
    def __init__(self):
        super().__init__('playAudio_node')
        self.play_client = self.create_client(PlayAudioSystemPrompts,f'/{tita_namespace}/system/audio_control/play_audio_system_prompts')
        while not self.play_client.wait_for_service(timeout_sec=5.0):
                self.get_logger().info('服务不可用，正在等待服务端启动...')



    def send_request(self, audio_file_name):
        # 创建服务请求
        from std_msgs.msg import String
        request = PlayAudioSystemPrompts.Request()

        request.audio_file_name = String(data=audio_file_name)  # 设置请求参数

        # 异步发送请求
        future = self.play_client.call_async(request)
        future.add_done_callback(self.callback)

    def callback(self, future):
        try:
            response = future.result()
            if response.success:
                self.get_logger().info('服务调用成功，音频播放完成！')
            else:
                self.get_logger().info('服务调用失败，音频播放未完成。')
        except Exception as e:
            self.get_logger().error(f'服务调用过程中发生错误: {e}')


    audio_file_name='user/audio/6.mp3'    #播放音频文件  
    self.send_request(audio_file_name1)

def main(args=None):
        rclpy.init(args=args)
        node = PlayAudio()

        try:
                rclpy.spin(node)
        except KeyboardInterrupt:
                pass
        finally:
        # 关闭 ROS 2 节点
                node.destroy_node()
                rclpy.shutdown()
if __name__ == '__main__':
    main()
```

注意：
1. 自定义音频文件存放路径为：/opt/tita/sound/
2. 音频文件命名格式为：xxx.mp3
3. 加权限：`sudo chown -R robot:robot /opt/tita/sound/`