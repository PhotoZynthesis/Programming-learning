# JavaSE学习笔记

## 目录：

[TOC]

## 1. 概述

### 1.1 Java的起源和特征

**Java 编程语言**最初是由**Sun公司**开发的，该公司由 **James gosling** 于 1995 年创立 。

随着 Java 的发展进步和它的广泛流行， Java 做出了很多调整从而适应不同类型的平台。例如： J2EE 是为企业级应用程序设计的， J2ME 是为移动应用程序设计的。 

Java的特征有：面向对象性，平台独立性，简单性，安全性，体系结构中立性，便捷性，稳健性，多线程，易于理解，高性能，分布式，动态性。

### 1.2 JDK环境变量

- Windows：
  1. Java_Home：新建变量`Java_Home`，内容为jdk的目录。
  2. Path：在`path`变量中增加`%JAVA_HOME\bin%`。
  3. classpath：新建变量`CLASSPATH`，内容为`.;%Java_Home%\bin;%Java_Home%\lib\dt.jar;%Java_Home%\lib\tools.jar`。

- Linux：

  编辑`/etc/profile`文件，在末尾加入：

  ```
  export JAVA_HOME=(JDK安装目录)
  export JRE_HOME=${JAVA_HOME}/jre
  export CLASSPATH=.:${JAVA_HOME}/lib/tools.jar:${JRE_HOME}/lib/dt.jar
  export PATH=${JAVA_HOME}/bin:${JAVA_HOME}/jre/bin:$PATH
  ```

- 相关解释：

  1. JAVA_HOME指JDK的目录，很多需要JDK的程序会默认去取这个环境变量。
  2. 将JDK中的bin目录添加到Path环境变量，就可以在任意目录下执行bin中的可执行程序，例如`javac.exe`和`java.exe`。
  3. CLASSPATH的设置，可以使得在任意位置访问指定class文件。CLASSPATH中有多个项，系统将从左到右寻找class文件。



## 2. Java基础知识&语法

### 2.1 关键字与标识符

- 关键字：被Java语言赋予特定含义的单词，一些软件中会高亮显示。

  - Java的关键字有：

  ```
  abstract,assert,boolean,break,byte,case,catch,char,class,const（保留关键字）,continue,default,do,double,else,enum,extends,final,finally,float,for,goto（保留关键字）,if,implements,import,instanceof,int,interface,long,native,new,package,private,protected,public,return,short,static,strictfp,super,switch,synchronized,this,throws,transient,try,void,volatile,while
  ```

  - 注意事项：
    1. 关键字为全部小写。
    2. 不能作为标识符名。

- 标识符：给类、接口、方法（函数）、变量等起名字的字符序列。

  - 组成规则：

    由大小写的英文字母、数字、`$`和`_`组成。

  - 命名规则：

    - 包：全部小写，例如`com.zxy`。
    - 类/接口：首字母大写，例如`Student`。
    - 方法（函数）/变量：首字母小写，后续单词首字母大写，例如`indexOfElement`。
    - 常量：全部大写，例如`STUDENT_MAX_AGE`。

  - 注意事项：

    1. 标识符不能是关键字。
    2. 不能以数字开头。
    3. 区分大小写。

### 2.2 注释

注释就是对程序进行解释说明的文字，能提高代码的可阅读性。

- 单行注释：

  ```
  // 注释内容
  ```

- 多行注释：

  ```
  /*
  	注释内容
  */
  ```

- 文档注释：

  ```java
  /**
  	这方法天下第一，非常的🐮🍺。
  	@author 作者
  	@version 版本
  	@param a 参数说明
  	@return b 返回值说明
  	@throws NullPointerException 可能抛出的异常说明
  */
  ```

### 2.3 常量&变量&进制

- 常量：程序执行过程中，其值不发生改变的量。

  具体分为如下几类：

  - 整数常量：`12`，`23`。
  - 小数常量：`12.345`。
  - 字符常量：`a`，`A`。
  - 字符串常量：`"Hello!"`。
  - 布尔常量：`true`，`false`。
  - 空常量：`null`。
  - 自定义常量：final修饰。

- 变量：程序执行过程中，其值在某个范围内可以发生改变的量。

  定义格式：

  ```
  数据类型 变量名 = 初始化值;
  数据类型 变量名;
  变量名 = 初始化值;
  ```

- 进制相关：

  - 二进制：以`0b`开头。
  - 八进制：以`0`开头。
  - 十进制：默认就是十进制。
  - 十六进制：以`0x`开头。

### 2.4 数据类型

Java是强类型的语言，针对每种数据提供了对应的数据类型。

- 基本数据类型：

  分为如下八种：

  |  名称   |  占用字节  |                         备注                         |
  | :-----: | :--------: | :--------------------------------------------------: |
  |  byte   |     1      |       0000 0000 包含这8个bit（位），-128 ~ 127       |
  |  short  |     2      |                    -32768 ~ 32767                    |
  |   int   |     4      |               -2147483648 ~ 2147483647               |
  |  long   |     8      |                    -2^63 ~ 2^63-1                    |
  |  float  |     4      |         1bit符号位，8bit指数位，23bit尾数位          |
  | double  |     8      |         1bit符号位，11bit指数位，52bit尾数位         |
  |  char   |     2      |          由于默认采用Unicode编码，故为2字节          |
  | boolean | 1（未定4） | 实际占用字节数未明确规定，编译后可能转成int所以未定4 |

  注意事项：

  1. 关于float和double的具体精度：

     符号位、指数位和尾数位表示一个数的公式：`符号位 1.尾数位 * 2^指数位`，类似十进制科学计数法。

     吉祥物：`0b1.11111111111111111111111 x 10(2)^1000(8)`。

     **指数位决定了大小范围**，因为指数越大，能表示的数就越大。

     **尾数位（小数位）决定了精度**，因为后面的小数越多，精度越高。

     所以对于float，其有23bit小数位，2^23=8,388,608。其最多能有7位有效数字，但只有6位能保证绝对精确。

     同理对于float，其最多有16位有效数字，但只能保证15位绝对精确。

     **然而这些目前并没有卵用，精确计算小数用BigDecimal。**

  2. 关于char：

     占用字节数取决于编码，而Java语言采用Unicode作为默认编码，故默认char占用2字节。

  3. 关于boolean：

     Java并没有明确说明boolean占用多少个字节。

     一说具体取决于JVM，而部分JVM的boolean编译后会变成int。

     所以暂定有1或4个字节两种说法。

- 引用数据类型：

  Java有5种引用类型：类、接口、数组、枚举、标注。