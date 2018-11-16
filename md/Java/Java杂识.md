# 一些Java杂识

[TOC]

## 1. BeanUtils

### 1.1 概述

BeanUtils工具由Apache软件基金组织编写，提供给我们使用，主要解决的问题是：把对象的属性数据封装到对象中。

**依赖于commons-loggin.jar，部分操作也会依赖于commons-collections.jar**，建议全部导入。

谷歌搜索即可下载。

JavaBean即标准的Java类，使用BeanUtils需要至少Bean满足以下条件：

- 类必须被public修饰
- 必须提供空参构造器
- 成员变量必须使用private修饰
- 提供公共的setter和getter方法

### 1.2 常用方法

|             方法              |               说明                |
| :---------------------------: | :-------------------------------: |
| populate(Object obj, Map map) | 将Map中的内容填充到传递的JavaBean |
|                               |                                   |
|                               |                                   |

说明：

- populate方法会对bean中存在的相关属性进行封装，若map中的键不存在于bean中，则该键不产生效果。



## 2. 项目设计

### 2.1 MVC架构

- M：

  Model，模型。

  完成具体的业务操作，如：查询数据库，封装对象。

- V：

  View，视图。

  展示数据。

- C：

  Controller，控制器。

  业务层，获取用户的输入、调用模型、将数据交给试图进行展示等。

- 优缺点：

  - 优点：

    1. 耦合性低，方便维护于协作开发。

    2. 重用性高。

  - 缺点：

    1. 使得项目的架构变得复杂，对开发人员的要求较高。

### 2.2 软件设计的三层架构

- 界面层（表示层/Web层）
  - 接收用户参数，封装数据，调用业务逻辑完成处理。
  - 转发JSP页面完成显示。
- 业务逻辑层（Service层）
  - 组合DAO层中简单的方法，形成复杂的业务逻辑。
- 数据访问层（DAO层）
  - Data Access Object
  - 定义了对数据/数据库基本的操作。



## 3. ThreadLocal

### 3.1 概述

- ThreadLocal是一个关于创建线程局部变量的类。
- 通常情况下，我们创建的变量是可以被任何一个线程访问并修改的。而使用ThreadLocal创建的变量只能被当前线程访问，其他线程则无法访问和修改。

### 3.2 使用

- 创建：

  ```java
  ThreadLocal<String> mStringThreadLocal = new ThreadLocal<>();
  ```

- set方法：

  ```java
  mStringThreadLocal.set("droidyue.com");
  ```

- get方法：

  ```java
  mStringThreadLocal.get();
  ```