+++
title = 'Vocaloid 入门 - 安装与开始'
date = 2023-10-28T01:51:21+08:00
draft = true

tag = ['Vocaloid']
series = 'Vocaloid Introduction'
+++

> 唱出所想之歌

    Vocaloid, 是雅马哈公司开发的歌声模拟软件,很多虚拟歌姬都是基于Vocaloid引擎. 至于术力口则是日文的ボカロ

    本系列是基于**Vocaloid 4 FE Plus**编写

<!--more-->

## 获取Vocaloid Editor

    编辑器目前是更新到第六代(Vocaloid 6:AI), 但是用Vocaloid 4的用户多, 所以我们先获取Vocaloid 4

> 下载传送门: [myxxshare/v4plus (github.com)](https://github.com/myxxshare/v4plus)

    点进release下载附件即可

    但是仅仅下载Vocaloid Editor是无法启动, 必须要安装一个及以上的声库, 可以先去vocakey下载声库

<details>
  <summary>发电</summary>
  连连，我真的好爱你😍。可是我不敢说😭😭。无数个清晨，似是被什么遥远的呼唤打动，双眸定睛后，闪烁起异彩🤩。大概是有所领悟，出门，打开信箱，拿到信纸便逃也似地跑进房间🤤。小心地将那久别的寄信人名称纳入眼底，随之而来的，不可抑制一般的喜悦感几乎是震撼了自己。不禁有些恐慌，继而无端的恐慌转变成了更深邃的失望😢。我对自己还对这样一份残存的感情抱有期待而感到悲哀，为自己这样轻易地发生心境变化而懊恼。下一个瞬间几乎是想要杀死自己😭😭。再转一瞬竟衍生出了同情心，然后阖上双眼，想要忘却什么似的再度入眠。醒后，打开手机，动态中没有你的踪迹，手里被汗水儒湿的信封上写的也不是你😭😭😭😭。这个秋天，没有邀请函，也没有你。我狼狈地把信塞回信箱。趁着周遭无人。可是我不敢说😢。连连，我真的好爱你。😭😭😭😭😭😭 
  偷自BiliBili
</details>

> 新站传送门: [vocaloid4_library [VOCAKEY-愿你唱出心中的歌【内测版/共享版】] (imikufans.fun)](https://vocabeta.imikufans.fun/vocaloid4_library)

## 认识Vocaloid Editor主界面

    启动后应该如下图呈现

> 如果显示器分辨率过大,可以去调节DPI
> 
> <img src="https://s1.imagehub.cc/images/2023/10/28/783dc161db24ea6e92c2f950cc138707.png" title="" alt="783dc161db24ea6e92c2f950cc138707.png" data-align="center">

<img src="https://s1.imagehub.cc/images/2023/10/28/43fad1a093af44e199c55e08a6cf94ca.png" title="" alt="43fad1a093af44e199c55e08a6cf94ca.png" data-align="center">

> 图片可能不清晰, 但是大致应该能看清吧,,

    映入眼帘的主窗体包含着两个子窗体, 分别是**Track Editor**和**Musical Editor**, 我们一个一个介绍

### 菜单栏

#### View

<img title="" src="https://s1.imagehub.cc/images/2023/10/28/25db07d6465274078726f37dcf85b007.png" alt="25db07d6465274078726f37dcf85b007.png" data-align="center" width="328">

##### Phoneme Preferred Display 音素优先显示

    这个一般用于跨语种或者人造音等用处, 可通过<kbd>Ctrl + R</kbd>开启, 但是需要右键Note开启Phoneme Protect

<img src="https://s1.imagehub.cc/images/2023/10/28/5bae6fe46416fe91a3a42673ec298199.png" title="" alt="5bae6fe46416fe91a3a42673ec298199.png" data-align="center">

之后在**Vocaloid 跨语种教程**会有所讲述

##### Mixer 混音器

<img title="" src="https://s1.imagehub.cc/images/2023/10/28/8fe337f5ca1a745a1991d53ef4d0dfb8.png" alt="8fe337f5ca1a745a1991d53ef4d0dfb8.png" data-align="center" width="293">

    可以控制各个轨道的混音

#### Job 插件系统

<img title="" src="https://s1.imagehub.cc/images/2023/10/28/ac31643ea97927ec530c6e6e244d08a2.png" alt="ac31643ea97927ec530c6e6e244d08a2.png" data-align="center" width="384">

    如果用的是Vocaloid 4 FE Plus, 那么在`{安装目录}/JobPlugins`可找到大部分自带Job Plugin, 点击**Manage Job Plugins**添加插件后便可使用, 平时可以按下<kbd>Ctrl + J</kbd> 快捷召唤插件

#### Settings

<img src="https://s1.imagehub.cc/images/2023/10/28/0cc7b58daf9faf8b62e430880408c03e.png" title="" alt="0cc7b58daf9faf8b62e430880408c03e.png" data-align="center">

##### Preferences

    <img title="" src="https://s1.imagehub.cc/images/2023/10/28/7b24ab0512da074d69a306280a203992.png" alt="7b24ab0512da074d69a306280a203992.png" data-align="center" width="317">

    用于改变编辑器的偏好, 可以根据自己的情况调节

    不过**Audio Settings**调整要小心, 不然可能会导致引擎无法发声

<img title="" src="https://s1.imagehub.cc/images/2023/10/28/09b71274fcf67566b0bb47fb29297134.png" alt="09b71274fcf67566b0bb47fb29297134.png" data-align="center" width="435">

##### Singing Style

##### Singer Editor
