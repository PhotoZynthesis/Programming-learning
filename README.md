﻿# 我的编程学习笔记

### 2018.4.4

这里将是我开始的地方，本项目将用于存放我于各种知识的学习笔记。

此README将用于：

* 记录每一次的变动
* 像日记一样，记录我脑中随时出现的想法

**今日正文**

大约半年前我创建了GitHub账号，然而到昨天才创建了第一个repository（就是现在这个）。了解了GitHub一些基本的操作，大致熟悉了一下GitHub desktop客户端，可以进行基本的项目更新了。

于是将几个月来学习JavaSE所写的笔记添加到了项目，并准备开工写这个README.md。了解到.md后缀的文件原来就是Markdown文本文件，尝试用一直使用的notepad++打开，发现并不能像[毛线论坛](https://bbs.craft.moe)发帖一样实时预览最终效果。接着便找了半天md编辑器，最终决定用Typora。

Markdown写出来的文本具有多级标题，段落，列表等记事本不具有的特性，目前看来更加美观和方便阅读。于是我有了第一个脑洞：将以前所有的Java笔记全转换为Markdown格式。由于我写的txt笔记中每一个大的知识点标题都是以 **数字+"."** 开头，就想着能不能利用刚学的知识，用Java中IO的方式，截取 **数字+"."** 开头的所在行，通过在截取到的字符串前面加上 **#** 转变为Markdown的大标题并重新写入md文件中。