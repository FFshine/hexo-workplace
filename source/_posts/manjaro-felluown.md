---
title: manjaro 下第三方网易云音乐feeluown安装
id: 723
categories:
  - linux
date: 2017-10-14 19:21:35
tags:
---
### 2017/12更新

当网易云正式版更新后，完全可以即装即用。此文作废.


#### 以下原文:


<storng>手贱把系统换成arch linux系的manjaro了</storng>
网易云作为必不可少的软件，首先我考虑的是arch官方库里的netease-cloud-music,安装过程也很顺利。
<pre lang="bash">
$ sudo pacman -S netease-cloud-music
</pre>
很不幸的是，事情远没有那么简单。安装好了却怎么都打不开，在进程里也能查到网易云的进程。来来折腾了几回后，只能放弃之。。


通过某度发现了基于Python3的第三方网易云音乐[feeluown](https://github.com/cosven/FeelUOwn)。

根据作者提供的信息，通过pip运行（我的pip是Python3的pip）。
<pre lang="bash">
$ sudo pip install felluown
</pre>
按照作者的说的方法解决依赖。
<pre lang="bash">
$ feeluown-install-dev
</pre>
但因为作者用的的系统是debian系，用的是"apt-get"。所以返回的是"apt-get notfound"。

在作者的 [issues](https://github.com/cosven/FeelUOwn/issues/218) 中，得知在arch的软件仓库中有feeluown（不得不感叹AUR的强大)。

于是
<pre lang="bash">
$ yaourt -S feeluown
</pre>
但不幸的是 有一个依赖 "python-quamash"总是安装失败，导致编译失败。
我尝试着用pip安装这个python包
<pre lang="bash">
$ sudo pip install quamash
Requirement already satisfied: quamash in ./anaconda3/lib/python3.6/site-packages
</pre>
什么？？ quamash不是存在么？？
难道是anaconda自带的 软件用不了？？
好吧，修改 .bashrc文件，注释掉
<pre lang="bashrc">
#export PATH="/home/ss/anaconda3/bin:$PATH
</pre>
然后再用 yaourt编译安装Python-quamash。
<pre lang="bash">
$ yaourt -S python-quamash
</pre>
没有遇到错误。
然后
<pre lang='bash'>
$ yaourt -S felluown
</pre>
因为依赖解决了，所以也成功装上了。
点开feeluown图标。弹出的是一个黑色的框。只有几个控制按钮，最最重要的是，点遍全屏也找不到登录按钮，完全没法用。只能卸载
<pre lang="bash">
$ yaourt -R feeluown
</pre>

* * *

现在依赖问题解决了，何不回到开始用pip试试呢？
安装Python3的pip
```bash
$ sudo pacman -S python-pip
resolving dependencies...
looking for conflicting packages...

...
...
...

$ pip --version
pip 9.0.1 from /usr/lib/python3.6/site-packages (python 3.6)
```
然后回到第一步
<pre lang="bash">
$ sudo pip install feeluown
....
....
$ felluown
qt5ct: using qt5ct plugin
$ mkdir ~/.FeelUOwn
...
...
$ feeluown-genicon #生成图标
...
</pre>
<!--这个点屁事都要写一篇文章，是不是闲的蛋疼-->
<!--应该是吧-->