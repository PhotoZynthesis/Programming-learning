﻿# 我的编程学习笔记 [2.0版本已上线]

## 1. 说明

- 2.0 版本说明编辑中。


## 2. Logs

### 2018.4.4

这里将是我开始的地方，本项目将用于存放我于各种知识的学习笔记。

此README将用于：

* 记录每一次的变动
* 像日记一样，记录我脑中随时出现的想法

**今日正文**

大约半年前我创建了GitHub账号，然而到昨天才创建了第一个repository（就是现在这个）。了解了GitHub一些基本的操作，大致熟悉了一下GitHub desktop客户端，可以进行基本的项目更新了。

于是将几个月来学习JavaSE所写的笔记添加到了项目，并准备开工写这个README.md。了解到.md后缀的文件原来就是Markdown文本文件，尝试用一直使用的notepad++打开，发现并不能像[毛线论坛](https://bbs.craft.moe)发帖一样实时预览最终效果。接着便找了半天md编辑器，最终决定用Typora。

Markdown写出来的文本具有多级标题，段落，列表等记事本不具有的特性，目前看来更加美观和方便阅读。于是我有了第一个脑洞：将以前所有的Java笔记全转换为Markdown格式。由于我写的txt笔记中每一个大的知识点标题都是以 **数字+"."** 开头，就想着能不能利用刚学的知识，用Java中IO的方式，截取 **数字+"."** 开头的所在行，通过在截取到的字符串前面加上 **#** 转变为Markdown的大标题并重新写入md文件中。

### 2018.4.11

JavaSE学习进度已推进到了多线程，开工了Markdown语法学习笔记。

近期准备开工JavaSE学习笔记Markdown转化工作。

### 2018.5.29

开始学习html。

### 2018.9.21

前几日将整个项目进行了重构，现采用HTML的查阅页面。

- 点击HTML页面右侧边栏可以切换不同的笔记阅读
- HTML页面由 **Typora** 生成

- 目前存在的缺点：
  - 浏览时不能实时修改笔记内容
  - 添加一篇笔记的流程复杂，导出HTML后还需要对`index.html`进行更改
  - 右侧导航栏剩余空间即将用尽，需要尽快提供解决办法
  - 已知在部分电脑/浏览器上，文章的打开速度很慢
  - 页面样式太过简单

### 2019.5.25

经过多天研究改进，已将本项目升级到 2.0 版本。

版本特色：

- 不再依赖 Typora。
- 显示的 html 版本 markdown 样式已可以随意自定义。
- 右侧导航栏已可实现内容超出时上下滚动。
- 右侧导航栏现已支持一层文件夹。
- 不再需要手动生成 html/手动更改 index.html。
- index.html 及所有文章的 html 文件，根据 md 文件夹下的文件结构，使用 java 编写的脚本一键生成。

版本缺陷：

- 不支持 md 文件下的多级目录，目前只能生成根目录及一级目录下的 html 文件。
- 页面样式可能待改进。
- 距离完整静态博客尚缺少一些元素。

### 2019.6.18

- 一些小问题的优化。