+++
title = '搜索引擎 / 基础搜索'
date = 2025-01-07T23:57:59+08:00
draft = false
categories = ['计算机科学', '搜索引擎探索']
+++

## Preface

> 我真的, 好想写搜索引擎啊. 致三年前的自己.

首先, 这一系列是理论研究, 所以可能有些地方难以实现. 同时, 这系列文章也是为了能和BF联机写搜索引擎做教程文章.

关于搜索引擎, 最基础的部分就是全文检索. 而本文主要专注于全文搜索

## 原理解析

绝大多数的全文搜索引擎用的是索引. 也就是说, 像字典一样, 我需要通过一张表去寻找对应的文档. 但是索引分为正向索引与反向索引, 反向索引是效率高的一种索引方式

### 正向索引

```c#
public class Doc
{
    public string Word { get; set; }
    public int Times { get; set; }
    public List<int> Place { get; set; }
}
```

正向索引就是, 以`DocumentID`为索引, 每个文档中记录着每个字的信息, 例如说在哪里出现, 又在出现了几次.

使用正向索引的例子就是关系型数据库

正向索引的优势就是方便构建, 有新文档加入直接预处理加入到文档存储库里面即可, 但是若是要以`Word`为关键字的时候索引文档, 效率就不是很高了, 有时候在类似`MongoDB`等`NoSQL`中需要写个复杂的查询语句才能查到`DocumentID`, 并且效率低下.

非特定不使用

### 逆向索引

```c#
public class WordRecord
{
	public class ListsDef
    {
        public int DocId { get; set; }
        public int Times { get; set; }
       	public List<int> Positions { get; set; }
    }
    public int WordId { get; set; }
    public string Word { get; set; }
    public List<ListsDef> DocLists { get; set; }
}
```

反向索引就是, 以`Word`为索引, 去寻找包含这个`Word`的`Document`. 
