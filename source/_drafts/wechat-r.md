---
title: 基于itchat的Python微信机器人（一）
tags:
  - itchat
  - Python
  - 微信
  - 机器人
id: 356
categories:
  - 代码
date: 2017-08-14 20:06:59
---

## **0X00**
itchat 是一个开源的第三方微信Python库，提供了完整的微信接口。网上有人基于itchat创建了很多有趣的小程序。六月，我依葫芦画瓢，<del datetime="2017-08-14T11:53:18+00:00">抄</del>写了一个调用图灵机器人接口的微信聊天机器人。今天我看到知乎上有人在做 opensv-python的人脸识别，于是又捡起了我的微信机器人，<del datetime="2017-08-14T11:53:18+00:00">抄</del>加了这个功能。

用到的第三方库有：
* itchat ->(sudo) pip install itchat
* opencv-python ->(sudo) pip install opencv-python

## **0x01**
代码如下：
```python
    import requests
    import itchat
    import time
    from itchat.content import *
    import cv2
    import os
    from PIL import Image

    #构建图灵机器人消息回复
    def tuling(msg):
        url='http://www.tuling123.com/openapi/api'
        data={
        'key'   :'0bda0c8b640f432d96d13396856c5a4a',
        'info'  :msg,
        'userid':'hello-ffshine'
        }
        try:
            r=requests.post(url,data=data).json()
            return r.get('text')
        except:
            return
    #png转jpg
    def toJpg(msg):
        img=Image.open('./'+msg['FileName'])
        newImg= msg['FileName'][:-4] + '.jpg'
        img.save(newImg,format="jpeg")
        return os.getcwd() + '/' + newImg

    #构建简单的人像识别
    def humanFace(msg):
        faceData = '/home/ss/Desktop/opencv/data/3.xml'
        #photopath = os.getcwd() + msg['FileName']
        photopath = msg
        image = cv2.imread(photopath)
        #gray = cv2.cvtColor(image,cv2.COLOR_BGR2GRAY)
        face_casacade = cv2.CascadeClassifier(faceData)
        faces = face_casacade.detectMultiScale(image)
        color = (0,0,225)
        strokeWeight = 2
        a = '您发来的图片'+'共识别到'+str(len(faces))+'个人'
        for x,y,width,height in faces:
            cv2.rectangle(image,(x,y),(x + width,y +height),color,strokeWeight)
        cv2.imwrite(os.getcwd() + '/new.jpg',image)
        return a

    #回复好友
    @itchat.msg_register(itchat.content.TEXT)
    def frind_reply(msg):
        defaultReply='不好意思，我出错了！！'
        reply=tuling(msg['Text'])
        return reply or defaultReply

    #回复群聊
    @itchat.msg_register(TEXT,isGroupChat=True)
    def group_reply(msg):
        itchat.send(u'@'+msg['ActualNickName']+': '+tuling(msg['Content']),msg['FromUserName'])

    #处理好友发来的图片等信息
    @itchat.msg_register(PICTURE, RECORDING, ATTACHMENT, VIDEO)
    def download_files(msg):
        msg['Text'](msg['FileName'])
        a = humanFace(toJpg(msg))
        itchat.send_image('./new.jpg',msg['FromUserName'])
        return a
    #群友发来的图片
    @itchat.msg_register(PICTURE,isGroupChat=True)
    def download_group_files(msg):
        msg['Text'](msg['FileName'])
        a = humanFace(toJpg(msg))
        itchat.send_image('./new.jpg',msg['FromUserName'])
        return u'@'+msg['ActualNickName']+': '+a

    #有新好友申请，则自动同意加好友并录入消息
    @itchat.msg_register(FRIENDS)
    def add_friend(msg):
        itchat.add_friend(**msg['Text'])
        itchat.send_msg('你好，Nice to meet you',msg['RecommendInfo']['UserName'])

    #登录，并保持运行    
    #itchat.auto_login(hotReload=True)
    itchat.auto_login(enableCmdQR=2)
    itchat.run()
```
## **0x02**
参考资料

*   [itchat](http://itchat.readthedocs.io/zh/latest/)
*   [opencv github](https://github.com/opencv/opencv/)
*   [opencv-Python](http://opencv-python-tutroals.readthedocs.io/en/latest/)