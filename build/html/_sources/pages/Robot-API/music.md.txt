# 音效

```{toctree}
:maxdepth: 1
:glob:
```

------
控制机器人播放音频的能力和改变需要播放的音频

------
**Action：**`interaction/audio_play`<br>
**Msg Type：**`tita_interaction_msgs/action/AudioPlay`<br>
**命令示例：**`ros2 action send_goal /[namespace]/interaction/audio_play tita_interaction_msgs/action/AudioPlay '{url: "/tmp/gpt_2024-02-02-17-05-50.wav"}'`<br>
**更换语言方法如下：**
``` bash
vim /usr/share/tita_bringup/params/default_param.yaml
interaction_manager中的language 字段意义如下：
0: Chinese
1: English
````