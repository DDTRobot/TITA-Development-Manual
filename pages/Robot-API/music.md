# Audio

```{toctree}
:maxdepth: 1
:glob:
```

------
Control the robot to play audio and change the audio that needs to be played.

------
**Action：**`interaction/audio_play`<br>
**Msg Type：**`tita_interaction_msgs/action/AudioPlay`<br>
**Code Example：**`ros2 action send_goal /[namespace]/interaction/audio_play tita_interaction_msgs/action/AudioPlay '{url: "/tmp/gpt_2024-02-02-17-05-50.wav"}'`<br>
**how to change language：**
``` bash
vim /usr/share/tita_bringup/params/default_param.yaml
language value in interaction_manager：
0: Chinese
1: English
````