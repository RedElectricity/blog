+++
title = "Jujutsu Kaisen Phantom Parade - Unpack log"
date = 2024-06-24T01:24:32
draft = false
categories = ['Reverse', '呪術廻戦']
image = "feature_images/jujutsuphanpara_dump.png"
+++

{{< rawhtml >}}
<center>进来前先大声喊: <audio controls src="/audio/jjk_para.ogg"></audio></center>
{{< /rawhtml >}}

> 本文将会持续更新

> 本文仅供学习使用, 请勿用于各种非个人的行为或者商业性行为
> For further detail, contact my email.

## 前言

至于我为什么会开始逆向Jujutsu Kaisen Phantom Parade, 原因还是里面的Live2D过于好看(虎子和五条是不错的)

真是百变虎子, 衣服挺多的

~~再也不解包日服游戏了~~

## 解包过程

### 分析游戏的整体

首先, 我们要分两个部分: 电脑版(DMM)和手机版

总的来说, 他们都是使用il2cpp编译的(~~废话, 现在哪里有游戏还是用mono~~)

- 电脑版: 直接从DMM上获取即可, 但是这条路基本上是死的. 为什么呢? 只要你把游戏的逻辑文件 `GameAssembly.dll` 拖到 `Detect it easy` 便可得知游戏是用的 `HyperTech Crackproof` (我看到这个基本上就知道要转战了), 现在网上也没有对于这个壳的脱壳方法. 并且我的电脑没法用 `KsDumper`
- 手机版: 这个是真好解包, 用 `GameGuardian` 加上[脚本](https://gameguardian.net/forum/files/file/2769-hidden-global-metadatadat-searcher/)直接可以dump出未加密的 `global-metadata.dat` 和 `libil2cpp.so`. 从文件来看, 解包apk中只有 `global-metadata.dat` 是加密的.

因此, 为了方便(~~偷懒~~), 我们选择使用手机版+模拟器进行.

#### 关于octo

根据网络上仅有的几个解包教程, octo包很有可能是cyberagent自己搞的资源管理类包, 并且跟cyberagent有关的公司和工作室有使用这个包.

其中在octo文件夹里面左翻右翻其中就有个叫 `octocacheevai` 的文件, 根据先辈的遗产[Nire的解包](https://github.com/190nm/rein-kuro), 这个文件用于存储在v1文件夹下资源的目录以及其名称, 描述的protobuf如下

```protobuf
syntax = "proto3";

message Database {
    int32 revision = 1;
    repeated Data assetBundleList = 2;
    repeated string _tagname = 3;
    repeated Data resourceList = 4;
    string urlFormat = 5;
}

message Data {
    int32 id = 1; //id={0}
    string filepath = 2;
    string name = 3; //name={1}
    int32 size = 4; //size={2}
    uint32 crc = 5; //crc={3}
    repeated int32 tags = 6; //tags=[{4}]
    int32 priority = 7;
    repeated int32 deps = 8; //deps=[{5}]
    State state = 9; //state={6}?
    string md5 = 10; //md5={7}
    string objectName = 11; //objectName={8}
    uint64 generation = 12; //generation={9}
	enum State {
		NONE = 0;
		ADD = 1;
		UPDATE = 2;
		LATEST = 3;
		DELETE = 4;
	}
}
```

### 提取密钥

~~你以为dump出 `global-metadata.dat` 等有用吗? 不, 这并没有什么用. 我们将采取一种最方便的办法, dump内存.~~

注意到先辈遗产中的代码片段

```python
    # All currently known magic numbers to try
    en = ("st4q3c7p1ibgwdhm", "LvAUtf+tnz")
    jp = ("p4nohhrnijynw45m", "LvAUtf+tnz")
    encbt = ("p4nohhrnijynw45m", "LvAUtf+tnz")
    jpcbt = ("ezj749zwskuskg46", "LvAUtf+tnz")
```

注意到IV其实是不变的(~~这对于所有使用了octo的游戏IV都是不变的~~), 启动Nire, 在 `GameGuardian` 中用IV搜一搜, 得到内存范围再dump出内存片段.

注意到IV附近的内容, 其中有一段是我们的Key, 按葫芦画瓢便可以得到Jujutsu Kaisen Phantom Parade的密钥

> 这是什么呢?
>
> U2FsdGVkX18IhwXLCGzYEBKTdqrPt91MVF3avXiuaKJN5cQME2qOEmsCKnybO1+k7I2GKXBbCoLUIwVMmN80wQ==
>
> Hint: AeS Key:Game Domain

获得到密钥之后你就可以使用[Nire的解包](https://github.com/190nm/rein-kuro)解密资源清单到下一步.

### 关于 `Criware` 的密钥

最简单也最方便的办法: 全自动的 [lico-n/ZygiskUnityCriwareKeylogger: Extracts CriWare encryption keys for Unity games via Zygisk.](https://github.com/lico-n/ZygiskUnityCriwareKeylogger)

### 解密资源

~~你以为解密一个资源清单有什么用吗? 哈哈其实资源也是加密的~~

资源总的来说分两种: 一种是 `Asset Bundle` 一种是资源文件(存储语音和视频)

我们的主要目的是提取 `Asset Bundle` , 资源文件大部分是使用 `Criware` 加密

~~正当你以为前面先辈的遗产有用, 正当你以为dump出 `global-metadata.dat` 等有用. 其实都错了.~~

当你拖进IDA找到对应的解密函数时其实根本就找不出先辈找出来的那几个函数, 因此我们便可以判断不是和Nire等一样的加密.

注意到程序调用了`FastAES`, 其实资源文件的加密是AES

> ~~TMD花了我几天时间, 我还以为加密方法没变. 我都快哭晕在IDA里了~~

### End of this section

其实到这里大部分解包的基础就已经完成, 接下来是对解包出来的 `.unity3d` 进行加工.

## 资源的运用

> 本人已完成最基础的解包器的编写, 需要的可以带上GitHub ID+证明有阅读C#代码的能力发送邮件来. 为了避免被橄榄, 仓库是Private的.

### 关于处理未下载的资源

在前文的Protofile中有定义字段

```protobuf
string urlFormat = 5;
```

而在提取之后, 我们得到这个字段对应的值

```json
{"UrlFormat":"https://asset-cdn.jujutsuphanpara.jp/{o}"}
```

其中很明显是字符串插值, 其中变量`o`经过我的测试之后对应的字段是

```protobuf
string md5 = 10; //md5={7}
```

放到浏览器中便可以下载, 但是特别注意的是资源服务器是锁IP的, 需要日区IP才可以下载.

### 资源中人物的使用技术栈

每个人物都有对应的战斗骨骼, 出勤小人骨骼, 动态立绘以及动态卡面.

其中使用到了`Criware` `Live2D` `Spine`.

都是日厂游戏老套路了, 如果下面看不懂可以选择另寻教程.

#### 关于解决动态卡面等`Criware`加密过后的视频

可以使用第三方的工具`CRID(.usm)Demux Tool`(搜一下就能得到)解密.

使用以下Powershell脚本

```powershell
$usms = Get-ChildItem -Filter "*.usm"

foreach ($item in $usms) {
	.\crid_mod.exe $item -a f8a0f8f8 -b 001bcd62 -v -x
	Remove-Item $item
}
```

#### 关于解决动态立绘等`Live2D`预处理过后的`Live2D`模型

解包过后在`live2d`文件夹下会出现两个目录, `model`和`motion`. 其实前辈写过一个`UnityLive2DExtractor`, 但是年久失修.

其实最重要的是提取到`moc3`文件, 这个文件对应着package中的名叫`moc`的`MonoBehaviour`, 以Raw方式提出出来, 剔除掉前面的几个字节到`MOC3`这个魔数开始便是可以正常使用的`moc3`文件.

然后模型贴图则是package为数不多的`Texture2D`.

关于每个角色对应的`motion`文件, 则在`motion`文件夹中, 其中每个角色可能对应不止一个motion package(例如说虎杖的motion就有normal和baseball, 对应着两套皮肤不同的motion).

当然直接提出来的motion是不能用的, 应为是unity特有记录动画的格式, 并且每个部分对于的path也是一串乱码. 但这并非是乱码, 这是每个model的部分的full path经过crc编码后得到的产物, 所以要先使用, 你需要读取`moc3`文件中的每一个

```
Parts/...
Parameters/...
```

再带回去替换. 但是要注意的是, 有一部分的crc可能没有, 跳过去就好了.

正常的话应该是这样

![Normal Live2D](/live2d_normal.png)

#### 关于解决`Spine`的骨骼

这个是最好解决的, 找到每个角色对于的骨骼(自己翻, 我忘了). 打开package里面搜索`*.skel`和`*.atlas`, 这两个是骨骼的定义文件以及贴图定义文件, 以Raw模式导出, 不需要改文件头就能使用. 另外还需要找到package中唯一的贴图文件.

应为package是Spine预处理过的, 所以需要解包贴图(软件内).

![Normal Spine](/spine_normal.png)

### 关于提取台词

台词文件位于`adv/script`中, 每一个stage都对应一个package, 并且package里面的script文件层次很简明, 自己写个脚本提取就好了.

## End of File

至此, Jujutsu Kaisen Phantom Parade已经大体上解包完成. 本人正是抱着对虎杖的喜爱才终于突破困难在短短几天之内dump出来. 最后再放张虎杖礼服的插画.

![Yuji](/yuji.png)

