---
title: "Jujutsu Kaisen Phantom Parade - Unpack log"
draft: false
_build:
  render: never
  list: never
  publishResources: false
---

> 本文将会持续更新

> 本文仅供学习使用, 请勿用于各种非个人的行为或者商业性行为
> 😭先辈的遗产真是节省了我大部分时间

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

### 解密资源

~~你以为解密一个资源清单有什么用吗? 哈哈其实资源也是加密的~~

资源总的来说分两种: 一种是 `Asset Bundle` 一种是资源文件(存储语音和视频)

我们的主要目的是提取 `Asset Bundle` , 资源文件大部分是使用 `Criware` 加密

~~正当你以为前面先辈的遗产有用, 正当你以为dump出 `global-metadata.dat` 等有用. 其实都错了.~~

当你拖进IDA找到对应的解密函数时其实根本就找不出先辈找出来的那几个函数, 因此我们便可以判断不是和Nire等一样的加密.

注意到程序调用了`FastAES`和另一位[先辈的遗产](https://github.com/sainz1407/Jujutsu-Kaisen-Phantom-Parade), 其实资源文件的加密是AES

> ~~TMD花了我几天时间, 我还以为没变. 还是先辈拯救了我~~

### EOF 1

其实到这里大部分解包的基础就已经完成, 接下来是对解包出来的 `.unity3d` 进行加工.

## 资源的运用

> ERROR: 本Section正在施工中...
