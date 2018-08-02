---
layout: post
title: Ubuntu下录制屏幕，并转换为gif图片格式
date: 2018-08-02 15:50:24.000000000 +09:00
---

## 录制屏幕
```
sudo add-apt-repository ppa:maarten-baert/simplescreenrecorder
sudo apt update
sudo apt install simplescreenrecorder
```

启动simplescreenrecorder就可以录制屏幕了。

## 将录像文件转换为图片
```
ffmpeg -i video.mp4  -r 5 'frames/frame-%03d.jpg'
```

亲测可用
