# Servlet & Tomcat

[TOC]

## 1. web服务器软件概述

- **服务器与服务器软件的区别**：
  - 服务器：安装了服务器软件的计算机。
  - 服务器软件：接收用户的请求，处理请求并做出响应。
- **常见的Java相关的web服务器软件**：
  - WebLogic：Oracle公司的大型JavaEE服务器，支持所有JavaEE规范，收费。
  - WebSphere：IBM公司的大型JavaEE服务器，支持所有JavaEE规范，收费。
  - JBOSS：JBOSS公司的大型JavaEE服务器，支持所有JavaEE规范，收费。
  - Tomcat：Apache基金组织的中小型JavaEE服务器，支持部分JavaEE规范，如Servlet、JSP，开源、免费。



## 2. Tomcat的安装与访问

### 2.1 Windows下安装/启动步骤

1. 官方网站下载，地址：[http://tomcat.apache.org/](http://tomcat.apache.org/) 
2. 安装与卸载：
   - 安装：解压下载得到的压缩包即可。
   - 卸载：删除目录即可卸载。
3. 启动与关闭：
   - 启动：运行`bin`下的startup.bat或startup.sh
   - 关闭：
     - 运行shutdown.bat或shutdown.sh
     - ctrl + c
     - 点击`x` 

### 2.2 访问

在浏览器输入：

```
// 默认端口号
http://localhost:8080

// 使用80端口号（可以省略端口号）
http://localhost

// 访问webapps目录下的项目
http://localhost/demoProject
```

### 2.3 常见问题

- 启动时窗口直接闪退
  - 检查JAVA_HOME环境变量
- 启动报错：端口号被占用
  - 关闭占用端口号的Process：
    1. `netstat -ano`查看占用端口号的Process ID
    2. 任务管理器找到Process并关闭
  - 修改自身端口号：
    1. 找到conf/server.xml
    2. 打开并找到`Connector`标签，修改端口（推荐修改为80，这样可以省略端口号）。



## 3. Tomcat项目的部署

- **Tomcat目录下**：

  直接将项目文件夹放在webapps目录下即可。

  说明：

  1. 虚拟路径名为**项目文件夹**的名称。
  2. 可以将项目文件夹压缩为**war**包（zip）并放置在webapps目录下，会**自动**解压/删除。

- **其他路径**：

  - 修改`conf/server.xml`文件

    在`Host`标签体中新增：

    ```xml
    <Context docBase="<项目文件夹目录...>" path="/<虚拟路径...>" />
    ```

  - 在`conf/Catalina/localhost`新增任意名称xml文件

    内容：

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <Context docBase="<项目文件夹目录...>" />
    ```

    - xml文件名即为虚拟目录。



## 4. IntelliJ IDEA中使用Tomcat

### 4.1 新建Tomcat项目

遵循以下步骤：

1. 新建`Java Enterprise`项目，并在右侧勾选`Web Application`，同时设置Tomcat为Application Server；

2. 进入后，项目目录应如下所示：

   > -> src
   >
   > -> web
   >
   > ​	-> WEB-INF
   >
   > ​		-> classes
   >
   > ​		-> lib
   >
   > ​		-> web.xml
   >
   > ​	-> index.jsp

   需要在`WEB-INF`下新建`classes`和`lib`文件夹，分别用于存放生成的字节码文件和库。

3. 将classes文件夹设置为字节码文件输出地址，将lib文件夹设置为jar库，按照如下方式：

   > File -> Project Structure -> Modules -> Paths/Dependencies

### 4.2 常见问题

- 没有Tomcat类库

  > File -> Project Structure -> Modules -> Dependencies
  >
  > 在右侧+号添加即可

- 没有Tomcat运行环境

  > Run -> Edit Configurations
  >
  > 添加Tomcat即可，注意设置好端口号等项目



## 5. Servlet概述/入门/配置

### 5.1 概述

- Servlet是两个单词`server`和`applet`的缩写。
- Servlet是运行在服务器端的小程序。
- Servlet是JavaEE中的一个接口，定义了Java类被浏览器访问的规则。

### 5.2 Servlet体系结构

- **Servlet**：接口

  - **GenericServlet**：抽象类

    只抽象Servlet中的service()方法，对其他方法都做了默认空实现。

    - **HttpServlet**：抽象类

      包含doGet()/doPost()等方法。

### 5.3 入门&配置

按照以下流程创建Servlet：

1. 使用IDE新建**JavaEE项目**。

2. 自定义类实现Servlet接口。

3. 实现接口中的方法。

4. 配置Servlet，有如下几种方式：

   - 修改`WEB-INF`目录下的`web.xml`文件：

     ```xml
     <!-- 在根标签中增加如下内容 -->
     <servlet>
         <!-- 自定义的名称 -->
     	<servlet-name>demoName</servlet-name>
         <!-- Servlet主类完整类名 -->
         <servlet-class>io.github.photozynthesis.DemoMainClass</servlet-class>
     </servlet>
     
     <servlet-mapping>
         <!-- 与上方一致 -->
     	<servlet-name>demoName</servlet-name>
         <!-- 虚拟路径 -->
         <url-pattern>/demo</url-pattern>
     </servlet-mapping>
     ```

     说明：

     ​	系统在收到请求后，会解析请求URL，获取访问Servlet的虚拟路径。之后到web.xml

     文件中查找是否有对应的< url-pattern >标签体内容，若有，则找到对应类执行对应方法。

   - 使用注释配置，**需要Servlet 3.0及以上**：

     在主类上加上`@WebServlet`注解：

     ```java
     // urlPatterns是必选属性，所以只定义该属性的时候可以只写一个双引号及中间的内容
     @WebServlet(name="AnnotationServlet" urlPatterns="/demoUrl")
     public class MyServlet implements Servlet{
         ...
     }
     ```



## 6. Servlet生命周期

Servlet的生命周期方法如下：

- 被创建：init()

  - 只执行一次

  - 默认情况下，第一次访问时，Servlet被创建

  - 可以在`web.xml`中指定创建时机：

    ```xml
    <servlet>
    	...
        <!-- 为负数时将在第一次访问时创建，为0或正整数时服务器启动即创建 -->
        <load-on-startup>5</load-on-startup>
    </servlet>
    ```

- 提供服务：service()

  - 每次访问Servlet时，该方法都会被调用

- 被销毁：destroy()

  - **服务器正常关闭**时，会销毁Servlet
  - 在Servlet销毁前执行，一般用于释放资源



## 7. Servlet：Request & Response

### 7.0 HTTP协议入门

- **HttpRequest格式**：

![](C:\Users\Photo\Documents\Github\Programming-learning\md\Java\JavaEE\httpProtocol.jpg)

- **HttpResponse格式**：

  > <协议版本...> <响应状态码...> <状态码描述...>
  >
  > <头部字段名称...>:<值...>
  >
  > <头部字段名称...>:<值...>
  >
  > ...
  >
  >
  >
  > 响应体...

- **Http响应状态码概述**：

  | 分类 |                      说明                      |
  | :--: | :--------------------------------------------: |
  | 1xx  |  信息，服务器收到请求，需要请求者继续执行操作  |
  | 2xx  |           成功，操作被成功接收并处理           |
  | 3xx  |       重定向，需要进一步的操作以完成请求       |
  | 4xx  |   客户端错误，请求包含语法错误或无法完成请求   |
  | 5xx  | 服务器错误，服务器在处理请求的过程中发生了错误 |

  常用：

  - 200：OK，请求成功。一般用于GET与POST请求
  - 302：Found，临时移动（重定向）。与301类似。但资源只是临时被移动。客户端应继续使用原有URI
  - 304：Not Modified，未修改（访问缓存）。所请求的资源未修改，服务器返回此状态码时，不会返回任何资源。客户端通常会缓存访问过的资源，通过提供一个头信息指出客户端希望只返回在指定日期之后修改的资源
  - 404：Not Found，服务器无法根据客户端的请求找到资源（网页）。通过此代码，网站设计人员可设置"您所请求的资源无法找到"的个性页面
  - 405：Method Not Allowed，（没有doGet/doPost方法）客户端请求中的方法被禁止
  - 500：Internal Server Error，服务器内部错误，无法完成请求

- **示例文本**：

  ```http
  POST /sample.Jsp HTTP/1.1
  Accept:image/gif.image/jpeg,*/*
  Accept-Language:zh-cn
  Connection:Keep-Alive
  Host:localhost
  User-Agent:Mozila/4.0(compatible;MSIE5.01;Window NT5.0)
  Accept-Encoding:gzip,deflate
  
  username=jinqiao&password=1234
  ```

  ```http
  HTTP/1.1 200 OK
  Server: bfe/1.0.8.18
  Date: Thu, 03 Nov 2016 08:30:43 GMT
  Content-Type: text/html
  Content-Length: 277
  Last-Modified: Mon, 13 Jun 2016 02:50:03 GMT
  Connection: Keep-Alive
  ETag: "575e1f5b-115"
  Cache-Control: private, no-cache, no-store, proxy-revalidate, no-transform
  Pragma: no-cache
  Accept-Ranges: bytes
  
  <html>
  	...
  </html>
  ```

### 7.1 请求：Request

Servlet中的service()、doGet()、doPost()等方法会自动传递参数Request和Response。

注意事项：

> 获取请求参数时可能会出现乱码，具体如下：
>
> - GET：Tomcat 8 已经解决乱码问题。
>
> - POST：内容为中文时可能会出现乱码，因为Tomcat的默认编码方式为ISO-8859-1，解决方法如下：
>
>   获取参数前：request.setCharacterEncoding("UTF-8")

- **Request对象体系结构**：

  interface **ServletRequest** 

  ​	| > interface **HttpServletRequest** 

  ​		| > class(Tomcat) org.apache.catalina.connector.RequestFacade

- **Request功能**：

  #### 7.1.1 获取请求行数据

  |               方法               |                        说明                        |
  | :------------------------------: | :------------------------------------------------: |
  |      String **getMethod**()      |                 获取请求方式：GET                  |
  |   String **getContextPath**()    |              获取虚拟目录：/demoWork               |
  |   String **getServletPath**()    |           获取Servlet路径：/demoServlet            |
  |   String **getQueryString**()    |       获取GET方式的请求参数：id=demo&psw=123       |
  |    String **getRequestURI**()    |         获取请求URI：/demoWork/demoServlet         |
  | StringBuffer **getRequestURL**() | 获取请求URL：http://localhost/demoWork/demoServlet |
  |     String **getProtocol**()     |               获取协议版本：HTTP/1.1               |
  |    String **getRemoteAddr**()    |                  获取客户机IP地址                  |

  #### 7.1.2 获取请求头数据

  |                     方法                     |              说明              |
  | :------------------------------------------: | :----------------------------: |
  |      String **getHeader**(String name)       | 通过请求头字段的名称获取对应值 |
  | Enumeration<**String**> **getHeaderNames**() |   获取请求头中所有字段的名称   |

  #### 7.1.3 获取请求体数据

  |                  方法                   |      说明      |
  | :-------------------------------------: | :------------: |
  |     BufferedReader **getReader**()      | 获取字符输入流 |
  | ServletInputStream **getInputStream**() | 获取字节输入流 |

  **说明**：

  1. 只有POST方式的请求才会有请求体。
  2. 需要先获取流对象后再从流对象中获取数据。

  #### 7.1.4 获取请求参数（GET/POST通用）

  |                      方法                       |                         说明                         |
  | :---------------------------------------------: | :--------------------------------------------------: |
  |      String **getParameter**(String name)       |                  根据参数名称获取值                  |
  |  String[] **getParameterValues**(String name)   | 根据参数名称获取值的数组，一般用于有**多个值**的参数 |
  | Enumeration<**String**> **getParameterNames**() |                获取所有请求的参数名称                |
  |   Map<String, String[]> **getParameterMap**()   |                获取所有参数的Map集合                 |

  #### 7.1.5 请求转发

  一种服务器内部的资源跳转方式，使用同一个Request和Response，客户端地址栏不发生改变。

  使用步骤：

  1. 通过Request对象获取转发器对象，方法：RequestDispatcher getRequestDispatcher(String path)

  2. 使用得到的RequestDispatcher进行转发，方法：forward(ServletRequest request, ServletResponse, response)

     ```java
     RequestDicpatcher dispatcher = request.getRequestDispatcher("/demoServlet2");
     dispatcher.forward(request, response);
     ```

  #### 7.1.6 共享数据

  Request可以设置共享数据，可在多个Servlet的一次请求中共享数据。

  |                      方法                      |       说明       |
  | :--------------------------------------------: | :--------------: |
  | void **setAttribute**(String name, Object obj) |   存储共享数据   |
  |      Object **getAttribute**(String name)      |   通过键获取值   |
  |     void **removeAttribute**(String name)      | 通过键移除键值对 |

  #### 7.1.7 获取ServletContext

  - ServletContext **getServletContext**()

    也可以在Servlet内部用`this.getServletContext()`，获得的ServletContext是同一个。

    关于ServletContext的说明，见下文。

### 7.2 响应：Response

Servlet中的service()、doGet()、doPost()等方法会自动传递参数Request和Response。

- **重要功能**：

  #### 7.2.1 设置响应行

  |            方法            |               说明                |
  | :------------------------: | :-------------------------------: |
  | void **setStatus**(int sc) | 设置状态码（HttpServletResponse） |

  #### 7.2.2 设置响应头

  |                     方法                      |               说明                |
  | :-------------------------------------------: | :-------------------------------: |
  | void **setHeader**(String name, String value) | 设置响应头（HttpServletResponse） |

  **常用**：

  - 

  #### 7.2.3 设置响应体

  |                   方法                    |               说明                |
  | :---------------------------------------: | :-------------------------------: |
  |        PrintWriter **getWriter**()        | 获取字符输出流（ServletResponse） |
  | ServletOutputStream **getOutputStream**() | 获取字节输出流（ServletResponse） |

  #### 7.2.4 发送重定向

  |                  方法                  |                             说明                             |
  | :------------------------------------: | :----------------------------------------------------------: |
  | void **sendRedirect**(String location) | 用给定地址向客户端发送重定向响应，并清除缓存（HttpServletResponse） |

  - **重定向概述**：

    重定向是一种资源跳转方式。

    不同于请求转发，重定向具有如下特点：

    - 地址栏发生变化（请求转发不发生变化）
    - 可以访问其他站点的资源（请求转发只能跳转到服务器内部资源）
    - 重定向一共是两次请求（请求转发是一次）

  - **使用示例**：

    ```java
    // 设置状态码后设置响应头
    response.setStatus(302);
    response.setHeader("location", "/demoLocation/demoServlet");
    
    // 简略写法，效果完全相同
    response.sendRedirect("/demoLocation/demoServlet");
    ```



## 8. Servlet：ServletContext

- **概述**：

  代表整个Web应用，可以和Servlet容器进行通信。

  ServletContext是一个全局的储存信息的空间，服务器开始，其就存在，服务器关闭，其才释放。

- **获取方式**：

  - 通过Request对象：

    ```java
    request.getServletContext();
    ```

  - 通过HttpServlet：

    ```java
    this.getServletContext();
    ```

  说明：

  ​	两种方式获得的ServletContext是同一个。

- **功能**：

  - **获取MIME类型**：

    |                方法                 |      说明      |
    | :---------------------------------: | :------------: |
    | String **getMimeType**(String file) | 获取MIME的类型 |

    MIME类型是在互联网通信过程中定义的一种文件数据类型。

    获取的String具有如下格式：

    ​	<大类型...>/<小类型...>，举例：

    ​	text/html、image/jpeg

  - **共享数据**：

    |                       方法                       |         说明         |
    | :----------------------------------------------: | :------------------: |
    | void **setAttribute**(String name, Object value) |     设置共享数据     |
    |       Object **getAttribute**(String name)       | 根据键获取共享数据值 |
    |      void **removeAttribute**(String name)       |  根据键移除共享数据  |

    ServletContext的共享数据作用于整个服务器。

  - **获取真实路径**：

    |                方法                 |                    说明                    |
    | :---------------------------------: | :----------------------------------------: |
    | String **getRealPath**(String path) | 通过文件的虚拟路径获取其在硬盘上的完整路径 |
