---
title: Python与itchat之抓取所有微信好友的头像合成一张图
tags:
  - itchat
  - Python
  - 微信
  - 编程
id: 388
categories:
  - 代码
date: 2017-08-19 11:28:26
---

**0x00**

用到的第三方库为

*   itchat
*   pillow
*   numpy

**0x01**
代码如下：
'''python
    import itchat
    import os

    import PIL.Image as Image
    from os import listdir
    import math

    itchat.auto_login(hotReload=True)
    itchat.auto_login(enableCmdQR=2)

    friends = itchat.get_friends(update=True)

    #抓取的头像存在 heads 文件夹
    headsDir = 'heads'

    #试图创建 heads文件夹，如果文件夹存在，则不创建。
    try:
        os.mkdir(headsDir)
    except:
        pass

    num = 0
    print("正在抓取头像...")
    #抓取好友头像
    for i in friends:
        img = itchat.get_head_img(userName=i["UserName"])
        if str(img) != "b''":#判断是否为默认头像，如果是，则不抓取
            fileImage = open(headsDir + "/" + str(num) + ".jpg", 'wb')
            fileImage.write(img)
            fileImage.close()
            num += 1

    print("抓取完成，正在读取文件..")
    #读取头像文件
    pics = listdir(headsDir)

    #获取抓到的头像数量
    numPic = len(pics)
    #输出头像数量
    print("读取到的图片数量为:",numPic)

    #计算在 640x640 的画板上每张图片的边长（正方形)
    eachsize = int(math.sqrt(float(640 * 640) / numPic))

    #每边可容纳图片数量
    numline = int(640 / eachsize)

    print('每行/列图片数量为:',numline)

    #最终画板边长
    l = eachsize * numline
    print("抓图已经完成，请输入您想要生成的图片的大小")
    print("请输入正整数，输入1，则为",l ,"x",l,":")
    n = int(input(":"))
    print("将为您生成的图片大小是",l * n,"x",l * n)

    #新建一张 s * nxs * n 的空白图片
    toImage = Image.new('RGBA',(l * n,l * n))

    x=0
    y=0
    print("图片正在生成...")
    #在空白图片上写入图片
    for i in pics:
        try:
            img = Image.open(headsDir + "/" + i)
        except IOError:
            print("Error,打开图片失败")
        else:
            img = img.resize((eachsize * n,eachsize * n),Image.ANTIALIAS)#改变头像大小
            toImage.paste(img,(x * eachsize * n,y * eachsize * n))#将头像逐行打印到空白图片
            x += 1
            if x == numline:
                x = 0
                y += 1

    #保存写入的图片
    toImage.save(headsDir + '.jpg')
    print("完成。。\n正在发送给文件助手...")
    #发送给 文件传输助手。
    itchat.send_image(headsDir + '.jpg','filehelper')
    ```

参考：

*   [itchat](http://itchat.readthedocs.io/zh/latest/)
*   [【Python里itchat模块能实现什么有趣的东西？】崔斯特：](https://www.zhihu.com/question/59524525/answer/212541119?utm_source=com.miui.notes&amp;utm_medium=social)