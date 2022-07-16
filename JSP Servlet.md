```
	2019年6月19日14:59:08创建
```

# 目录

[TOC]

# JSP Servlet

## 动态网页开发基础

```
	
	实现真正与用户实现互动的网站	
	
	动态网页 关键在于 需要使用 应用服务端的服务端脚本语言  
	
	根据客户端的不同请求生成相应的HTML页面 再返回给客户端的浏览器作为响应
	动态网页是在服务器端运行的交互式网页 它们根据某种条件的变化而返回不同的内容
	
	例如 JSP(Java Server Pages)  //java脚本语言 服务端脚本语言
	
```

### 动态网页优势

```
	
	交互性 网页会根据 用户的 要求和选择 动态改变 和 显示内容
	自动更新 无须改变页面代码 自动生成新的页面 节省工作量
	随机性 不同时间 不同人访问统一网址时会产生不同的效果 (例 不同账户登录后看到的内容不同)
	
```

### 软件架构

#### B/S架构

```
	
	浏览器/服务器端
	
	只需要在客户端安装浏览器软件 就可以在Internet范围内实现系统的访问及信息共享 维护效率极大提高 极少受客户端应用限制
	
	浏览器
	B/S的界面没有C/S友好 
	在速度和安全性上需要花费巨大的设计成本
	与操作系统平台的关系最小化
	客户端0维护
	B/S采取交互是请求/响应模式 一旦数据信息发生变化 必须通过刷新页面才能看到更新的数据信息
	
```

##### 工作原理

```
	
	请求/响应 进行交互
	
	用户输入 → (输入数据) → 浏览器 → 向服务器发送请求(运行JSP等服务端程序 根据需求 与 数据库服务器交互) → 返回响应(HTML页面) → 浏览器(解释执行HTML文件)
	
```

#### C/S架构

```
	
	客户端/服务器端
	
	用户在本地安装 客户端软件 通过网络与服务端 相互通信
	需要安装专用的客户端 对应用软件做微小改动 客户端软件就需要进行升级 系统维护工作量大
	
	需要专门的客户端应用
	能充分发挥客户端处理能力 客户端响应快
	对客户端操作系统一般有限制
	客户端需要单独维护和升级
	
```

### 资源分类

#### 静态资源

```
	
	所有用户访问后,得到的结果都是一样的,称为静态资源,静态资源可以直接被浏览器解析
 
	HTML CSS JAVASCRIPT
	
```

#### 动态资源

```
	
	每个用户访问相同资源后,得到的结果可能不一样,称为动态资源
	动态资源被访问后,需要先转换为静态资源,再返回给浏览器
	
	SERVLET/JSP,PHP,ASP...
	
```

### 网络通信三要素

#### IP

```
	
	电子设备(计算机)在网络中的唯一标识
	
	//在投入正常运行的商业应用中 为了避免记忆复杂的IP地址 通常使用域名来代替
	
```

#### 端口

```
	
	应用程序在计算机中的唯一标识 	0~65536
	
```

#### 传输协议

```
	
	定了数据传输的规则
	
	  基础协议
		TCP 安全协议 三次握手 速度稍慢
		UDP 不安全协议 速度快
		
```

#### 常见协议

```
	
	https:// 带有安全套接的协议 传输是加密的
	ftp://	文件传输协议
	file:// 本地文件协议
	
```

### HTTP

```
	
	超文本传输协议(Hyper Text Transfer Protocol)
	
	//定义了 客户端和服务器端通信时 发送数据的格式
	//超文本 超越文本的功能 不仅可以传输文字还可以传输音频 图片等
	
```

#### 特点

```
	
	基于TCP/IP 的高级协议
	默认端口号 80
	基于请求/响应模式的  一次请求 对应 一次响应
	无状态的 每次请求之间相互独立 不能交互数据
	
```

#### 历史版本

```
	
	1.0 每一次请求响应都会建立新的连接
	1.1 复用连接
	
```

#### 请求行

```
	
	请求方式 请求URL 请求协议/版本
	GET / xx.html HTTP/1.1
		
```

#### 请求方式

```
	
	HTTP协议中有7种请求方式 常用的有2种
	
	GET 
	 //请求参数在请求行中 在url后
	 //请求的url长度有限制
	 //不太安全
	
	POST
	 //请求参数在请求体中
	 //请求的url长度没有限制
	 //相对安全
	
```

#### 请求头

```
	
	客户端浏览器告诉服务器一些信息
	
	常见的请求头 请求头值
	 User-Agent  
	 //浏览器告诉服务器,我访问你使用的浏览器版本信息
	 //可以在服务器端获取该头的信息，解决浏览器的兼容性问题
	 Referer URL
	 //告诉服务器 我(当前请求)从哪里来
	 //用作防盗链 统计工作
	
```

#### 请求空行

```
	
	就是用于分割POST请求的请求头 和请求体的
	
```

#### 请求体

```
	
	封装POST请求消息的请求参数的
	//字符串格式
	
```

### URL统一资源定位符

```
	
	统一资源定位符(Uniform Resource Locator) //网址
	
	组成部分 
	//http://localhost:80/xx.html
	//协议部分   主机IP:端口号   路径(项目资源地址)
 	
 	//路径 一般用来表示服务器上的一个目录或文件地址等 由零或多个 / 隔开的字符串表示 指定的资源可以是一个HTML页面 也可以是一个图像等服务器能提供的资源
 	
 	//第一个部分和第二部分之间用"://"隔开 第二部分和第三部分用"/"隔开 其中第一部分和第二部分是不可缺少的 第三部分有时可以省略 当第三部分省略是 大多数服务器会访问系统默认的欢迎页面
	
```

## 部署简单的Web应用

```
	
	动态网页需要发布到服务器 通过服务器运行的
	
```

### Web服务器软件

#### 服务器

```
	
	安装了服务器软件的计算机
	
```

#### 服务器软件	

```
	
	接收用户的请求  处理请求  做出响应
	在web服务器软件中 可以部署web项目 让用户通过浏览器来访问这些项目
	Web容器在服务器上运行时会监听特定端口 为从客户端发出的针对该端口的请求提供相应的处理服务
	JSP容器是Web容器或应用服务的一部分 用于对JSP页面的运行提供支持 下面的Tomcat服务器就属于
	
```

#### 常见的Java相关的Web服务器软件

```
	
	webLogic  oracle公司 大型的JavaEE服务器 支持所有的JavaEE规范 收费的
	webSphere  IBM公司 大型的JavaEE服务器 支持所有的JavaEE规范 收费的
	JBOSS  JBOSS公司的 大型的JavaEE服务器 支持所有的JavaEE规范 收费的
	Tomcat  Apache基金组织 中小型的JavaEE服务器 仅仅支持少量的JavaEE规范servlet/jsp 开源的 免费的
	
	JavaEE Java语言在企业级开发中使用的技术规范的综合 一共规定了13项大的规范
	
```

### Tomcat服务器

```
	
	免费开源Web容器  JSP/Servlet容器
	
	Apache Jakarta的开源核心项目
	
	//下载 http://tomcat.apache.org/
	
```

#### 安装&运行(大略)

```
	
	解压版 //可以做集成
	安装板 推荐
	//详细处理 度娘
	
	//可能遇到问题
	  黑窗口一闪而过
	  原因 没有正确配置JAVA_HOME环境变量
	
	//修改自身端口号
	  conf/server.xml
	  <Connector port="端口号" protocol="HTTP/1.1" connectionTimeout="20000" redirectPort="8445" />
	  //一般会将tomcat的默认端口号修改为80(http协议默认端口) 在访问时 就不用输入端口号
	
    //暴力强拆端口占用
      找到占用的端口号 找到对应的进程 杀死该进程
      //详细百度 
	
	
    运行
     安装目录下 bin > startup.bat 启动Tomcat shutdown.bat 停止Tomcat
    
```

#### Tomcat的目录结构

```
	
	bin //可执行文件
	conf //配置文件
	lib //依赖jar包
	logs //日志文件
	temp //临时文件
	webapps //存放web项目
	work //存放运行时的数据 //由JSP生成的Servlet放于此目录下
	
```

#### 项目结构

```
	
	动态项目结构 //通常情况下 在同一网站同时存在静态网页和动态网
	 项目的根目录
	 	 该目录下所有文件在客户端都可以访问(JSP/HTML等)
	 	 META-INF目录(相当于一个信息包 用于配置应用程序 扩展程序 类加载器)(目录下的资源不能被浏览器直接访问)
	     WEB-INF目录 (WEB-INF目录下的资源不能被浏览器直接访问)
	        web.xml (web项目的核心配置文件)(控制整个应用的行为方式和方法) //此文件必须保存在WEB-INF目录下 
	        classes目录 (放置字节码文件的目录)
	        lib目录 (放置依赖的jar包)
	//注意 在Tomcat运行中 Tomcat类加载器会优先加载classes目录 下的文件 然后再加载lib目录下的类  //!!!如果两个目录下存在同名的类 那么classes目录下的类具有优先权
	
	
```

#### 部署项目(相对于Tomcat)

##### 一

```
	
	直接将项目放到webapps目录下
	
	//简化部署  将项目打成一个war包 再将war包放置到webapps目录下  war包会自动解压缩
	
```

##### 二

```
	
	配置conf/server.xml文件
	在<Host>标签体中配置
	<Context docBase="D:\文件夹" path="/URL路径" />
	docBase 项目存放的路径
	path 虚拟目录(URL路径)
	
```

##### 三

```
	
	在conf\Catalina\localhost创建任意名称的xml文件 在文件中编写
	<Context docBase="D:\文件夹" />
	docBase 项目存放的路径
	虚拟目录 xml文件的名称
	
```

#### 部署项目(相对于IEDA)

```
	
	将Tomcat 集成到IDEA中 并且创建JavaEE的项目 部署项目
	//编辑项目模块 将 指定lib库文件 指定classes文件 
	右键项目(根据项目结构设置) > Open Module Settings 
	
	--Paths--
	(自定义编译class目录)Use module compile output path 两个地方都设置到 项目结构的classes目录
	
	--Dependencies--
	//添加lib目录
	添加 > 1(JAR 或 目录) > 选择到 项目结构的lib目录 //后期注意添加 Tomcat的lib目录到里面
	
	//设置控制台编码  并 //编辑运行模块 //添加项目模块
	Run > Edit Configurations >Templates > Tomcat Server > Local 
	
	--Server--
	[Name]//项目名称
	[Application server]//Tomcat安装目录
	[After launch] //设置默认浏览器 [URL] //开启项目后自动打开的首页
	[VM options]//虚拟机参数 -Dfile.enciding=UTF-8 设置控制台 语言为UTF-8 //注意需要IDEA全体为UTF-8编码 //如果还没有中文则设置 根目录下>bin>idea.exe.vmoptions 内容下添加-Dfile.enciding=UTF-8 行 (注意高版本IDEA C盘用户文件下 也有此文件 也将其更改)
	[On frame deactivation]//如果项目内容发生改变 则采取的操作 //Update classes and resources更新项目不重启服务 ...
	[JRE] Java运行环境和版本
	
	--Deployment--
	添加Web项目模块 可添加多个 
	[Application context]//虚拟路径 每个项目模块需要不同

	
	//IDEA会为每一个tomcat部署的项目单独建立一份配置文件  C > 用户 > .IntelliJIdeaxxxx > system > tomcat > _itcast
	//工作空间项目  和  tomcat部署的web项目 //tomcat真正访问的是 tomcat部署的web项目 tomcat部署的web项目 对应着 工作空间项目  的web目录下的所有资源
	//断点调试 使用 小虫子 启动 //dubug 启动
	
```

#### 常见错误

```
	
	未启动Tomcat  //xx无法显示该网页
	未部署Web应用	//404
    URL输入错误 //404
    目录被引用 //注意META-INF WEB-INF下的目录文件不能被引用
	
```

#### 配置访问页面

```
	
	通过配置文件web.xml修改访问起始页 也可以设置起始访问为Servlet
	
	<web-app></web-app>标签中添加
	<welcome-file-list>
		<welcome-file>xxx.html</welcome-file>
		<welcome-file>xxx1.html</welcome-file>//如果第一个页面找不到 则找这个
	</welcome-file-list>
	
	<welcome-file> //用于指定某一具体页面
	<welcome-file-list> //元素可以包含 一个 或 多个<welcome-file>子元素 如果没有找到第一个元素中指定的文件 Web容器会尝试显示第二个 以此类推
	
	//这样设置了之后 用户进入到了项目路径后就会自动进入第一个起始页
	
```

## JSP简介(应用在服务端的 服务端脚本语言)

```
	
	JSP(Java Server Pages)  //实际上JSP是指在HTML中嵌入Java脚本语言 用户通过浏览器请求访问Web应用时 使用JSP进行处理和运行 然后将生成的页面返回客户端浏览器进行显示
	
```

### JSP工作(执行)过程

```
	
	Java脚本 > 嵌入 > JSP页面 //将Java脚本嵌入到
	JSP页面 > 翻译(.java) > 编译(.class) > 执行 > 应用服务器 
	应用服务器 <-交互-> 数据库服务器 
	应用服务器 > 返回页面信息 > 客户端(浏览器)
	
	Web容器处理JSP文件需要经过三个阶段
	翻译阶段 编译阶段 执行阶段
	客户端 > 请求 > 应用服务器 > JSP > 翻译(.java) > 编译(.class) > 执行 >应用服务 > 响应 > 客户端
	
	第一次请求之后 Web容器可以重用已经编译好的字节码文件(第二次请求之后)直接执行(执行效率提高)
	//如果对JSP文件进行了修改 Web容器会重新对JSP文件进行翻译和编译
	
```

### JSP页面元素

```
	
	静态内容	 HTML静态文本 CSS JavaScript
	  //这些内容将 原封不动 地做为动态生成HTML内容的静态部分
	
	
	指令  	  以<%@>开始 <%>结束 
	  //可以有多个
	  //通过设置内部的多个属性 定义整个页面的属性
	  //常用属性 
		language(指定JSP页面使用的脚本语言)[默认Java]
    	import(引用脚本语言用到的类文件)[无默认值]//如果要导入多个用,号隔开
    	contentType(指定MIME类型和JSP页面回应时所采用的字符编码方式)(页面和浏览器发送请求编码)[text/html;charset=UTF-8] [默认值text/html;charset=ISO-8859-1] //text/html表示页面以HTML页面的格式进行显示 charset=UTF-8表示 浏览器以UTF-8的编码方式显示内容
	
	
	小脚本		 <% Java代码 %> 
	  //可以包含任意的Java片段(可以直接写逻辑判断)
	  //不能在此里面定义方法
	  //jspservice()方法内容 定义的变量都是该方法的局部变量
	  //包含out等隐藏对象
	
	
	表达式 	 <%= Java表达式 %> 
	  //Web容器遇到表达式时 会先计算嵌入的表达式值或变量值 而后将计算结果输出到页面中
	  //在表达式中方法的后面不能有分号;
	  //如果表达式是调用一个方法(这个方法必须要有返回值)而不应是void  返回void方法是不能被调用的
	  
	  
	声明 	      <%! 方法/全局变量 %> 
	  //不能直接写逻辑 逻辑要写在方法里面
	  //不能在声明中使用out等隐藏对象(因为out等隐藏对象,是作用域jspservice方法中定义的)
	
	
	注释		  
	  <!-- 客户端可以看到 --> 
      <%-- 客户端无法看到 --%>
      在JSP脚本中注释 <% //单行注释 %> <% /*多行注释*/ %>
	
```

## JSP数据交互

### JSP内置对象

```
	
	JSP内置对象是Web容器创建的一组对象
	//不用声明和创建 就可以直接使用
	//就是由Web容器加载的一组 Servlet API的实例 这些实例由JSP规范进行了默认的初始化操作 可以直接在JSP中使用 
	//注意内置对象名称均是JSP的保留字 不得当作自定义变量名使用
	
```

#### 常见JSP内置对象

##### out对象(用于向客户端输出数据)

```
	
	//使用最频繁的对象 使用起来最简单的
	//需要用小脚本 隔离br换行时 注意不要遗漏{}括号
	
```

###### 常用方法

```
	
	print() //用于在页面中输出数据
	println() //用于在页面中输出数据 带换行
	
	//可以输出JS代码但是要注意 js标签和代码的正确书写 字符串转换'' 还有属性值用''包裹起来
	//注意out.print("<script></script>");	 //要正确 写入javascript代码 闭合标签
	否则会导致页面为空
	//导致页面为空 页面地址错误 路径问题 提交页面(具体页面 问题) 页面地址问题(注意项目下地址)
	
```

##### request(对象获取请求消息)(转发)

```
	
	主要用于处理客户端请求
	
	//包含了有关浏览器请求的信息
	客户端 > 请求 {[request对象 > 获取请求的信息使用 >]}
	//[]中为JSP页面  {}为服务器
	
```

###### 常用方法

```
	
	getParameter(String name) //返回值String  //根据表单组件名称获取提交数据
	getParameterValues(String name) //返回值String[] //获取表单组件对应多个值时的请求数据
	setCharacterEncoding(String charset) //无返回值 //指定每个请求的编码
	getRequestDispatche(String path) //返回值RequestDispatcher //返回一个java.servlet.RequestDispatcher对象(该对象的forward()方法用于转发请求)
	
```

###### 为什么会出现中文乱码问题

```
	
	常用字符集编码 ASCLL、ISO-8859-1、GB2313、GBK、Unicode、UTF-8 等
	Java在其内部使用Unicode字符集来表示字符 这样就存在Unicode字符集和本地字符集进行转换的过程 在Web应用中 通常都包括浏览器、Web服务器、Web应用服务器、数据库 等部分 每一部分都有可能使用不同的字符集 从而导致字符数据在各种不同的字符集之间转换时 出现乱码问题
	
```

###### 处理中文字符集(获取数据时解决中文乱码问题)

```
	
	在页面设置支持中文字符的字符集 UTF-8
	
	form表单 method post模式
	  //在接受包的地方 设置读取请求信息的字符编码为UTF-8
	  //request.setCharacterEncoding("UTF-8");
	
	--Tomcat8版本后 get的方法默认为UTF-8 不更改也行
	第一种 form表单 method get模式
	  //读取值时进行 字符编码  //此时setCharacterEncoding()方法是无效的
	  String xxx = request.getParameter("xxx");
	  xxx = new String(xxx.getBytes("ISO-8859-1"),"UTF-8");
	  //当获取多个参数时每个参数都要进行重新编码 操作繁琐 效率不高 推荐使用以下方法	
	第二种 form表单 method get模式
	  //在Tomcat目录结构\conf\server.xml中设置字符集
	  <Connector port="8080" protocol="HTTP/1.1">
	  connectionTimeout="20000" redirectPort="88430" [URIEncoding="UTF-8"] />
	  //如果在Tomcat中设置了字符集编码 则无须在JSP页面在进行重新编码处理
	
```

###### contentType 和 pageEncoding的区别

```
	
	contentType定义响应的资源类型 也可以包含JSP页面 和 响应内容的字符集 
	pageEncoding指定JSP文件的字符集及默认的contentType字符集
	
```

##### response(设置响应消息)(重定向)

```
	
	主要用于设置响应参数及取得响应流等(响应客户请求并向客户端输出)
	
	//设置响应参数以及获得响应流对象
	服务器> {从服务器中检索的信息 [response对象 > 响应的信息使用]} > 响应 > 客户端
	//[]中为JSP页面  {}为服务端
	
```

###### 常用方法

```
	
	addCookie(Cookie cookie) //向客户端添加Cookie
	setContentType(String type) //设置HTTP响应的contentType类型
	setCharacterEncoding(String charset) //设置响应所采用的字符编码类型
	sendRedirect(String location) //客户端将重新发送请求你到指定的URL //将请求重新定位到一个新的URL上 //重定向
	
```

##### 转发与重定向

###### 转发

```
	
	getRequestDispatche(String path).forward(request,response)
	转发主体  Web服务器
    请求次数  1次
    请求数据共享传递 可实现多个页面间请求参数的共享
    URL地址栏内容变化 不会发生变化 不会显示跳转后页面URL

		
	从程序运行的角度理解 即当客户端发送一个请求到服务器后 Web服务器在容器内部完成请求跳转 然后将最终的结果发送给浏览器 整个过程都是在容器内部完成的
	//而对应到客户端 无论服务器内部如何处理 作为浏览器都只是提交了一个请求 因而客户端的URL地址不会发生改变
	//转发可以在多个页面交互过程中实现请求数据的共享
	
```

###### 重定向

```
	
	respnse sendReditect()
	重定向主体 浏览器
	请求次数 2次
	请求数据共享传递 不能获得第一次请求数据
	URL地址栏内容变化  会发生改变 显示跳转后的URL地址
	
	
	客户端重新向服务器请求一个地址链接 由于是发送新的请求 因而上次请求中的数据将随之丢失 称为重定向 浏览器至少提交了两次请求
		
```

###### 重定向传值(查询字符串)

```
	
	如果需求在重定向的情况下将简单数据(值类型、字符串)传递至目标页面 可以使用查询字符串实现
	
	response.sendRedirect("xxx.jsp?参数名称="+参数值变量);
	//查询字符串以名值对方式储存数据 通过 ? 连接在URL地址后面 多个名值对可用 & 进行分割
	//如果需要传递复杂数据(对象、集合)需使用作用域
	
	取值还是request.getParameter("参数名称")
	
	
	超链接应用也经常用到查询字符串
	案例  在邮箱中有许多邮件 系统确定选择的邮件 在点击某一个邮件链接的同事 将这封邮件对应的编号传递给了系统 系统根据传递的邮件编号从数据库进行读取
	//<a href="xxx.jsp?邮件编号名称="+"01">第一封邮件</a>
	//<a href="xxx.jsp?邮件编号名称="+"02">第二封邮件</a>
	....
	
```

###### 区别

```
	
	都能实现页面的跳转 
	
	转发过程 Web服务器内部将一个request请求的处理权交给另外一个资源 属于同一个访问请求和响应过程 所以request对象的信息不会丢失
	转发是在服务器端发挥作用 通过RequestDispatcher对象的 forward()方法将提交信息在多个页面间进行传递
	转发是在服务器内部控制权的转移 客户端浏览器的地址栏不会显示出转向后的地址
	
	重定向 Web服务器向浏览器返回一个响应 浏览器接受此响应后再发送一个新的http请求到服务器 这属于两次不同的请求 则上一次请求的request信息将丢失
	重定向是在客户端发挥作用 通过请求新的地址实现页面转向  通过浏览器重新请求地址 在地址栏中可以显示转向后的地址
	
```

##### session 用于记录会话状态的相关信息

```
	
	浏览器与Web服务器之间是使用HTTP协议进行通信的 HTTP协议是一种基于请求/响应模式的无状态的访问协议 无状态指每一个HTTP请求都是独立的 服务不会保存以往的请求和会话记录 因此当一个客户端发送请求到Web服务器是 无论其是否第一次来访 服务器都会把它当做第一次来对待 
	
	//实际开发中 往往希望服务器能够识别已经访问过的客户端
	
	一个用户的活动会发生多次请求和响应 作为服务器而言 必须有一种机制来唯一标识 一个用户
同时记录该用户的信息 这就是会话跟踪机制 该机制可以保持每个用户的会话信息 为不同的用户保存自己的数据
	
```

###### session会话

```
	
	session 原意 指有始有终的一系列动作 在实际应用中通常翻译成会话
	
	//一个会话就是在 一段时间内 一个用户与Web服务器的一连串 相关的交互过程 它可以包含浏览器与服务器之间的多次请求、响应过程
	
	{浏览器 <- 交互(请求、响应) -> 服务器}  {}代表一个会话过程  交互可以有一个或多个
	
```

###### session会话机制

```
	
	会话机制是一种服务器机制
	当用户向服务器 发出第一次请求时 服务器会为该用户创建唯一的会话 会话将一直延续到用户访问结束
	服务器接收到客户端的请求时 服务器首先会判断是否已经创建了 与该客户端对应的会话 如果已经创建 就将该请求与此会话相关联 如果没有创建 则创建一个创建 此客户端之后发送的请求将关联到该会话
	
	服务器判断是否创建了相关会话 是通过唯一标识 sessionid 来实现的 如果在客户端请求中包含了一个sessionid 则说明在此之前已经为客户端创建了会话 服务器会根据这个sessionid将对应的会话对象读取出来 否则就会创建一个新的会话对象并生成一个sessionid 并将sessionid在本次响应的过程返回客户端保存
	
	sessionid 在客户端保存在cookie中 保存的sessionid的名称是JSESSIONID sessionid的值是由一串复杂字符串组成的 例 2A11D30C7B32329D7C8BF16DC598C509
	
	//同一个session对象sessionid相同
	
```

###### session对象

```
	
	session 对象允许用户访问会话的相关信息 以及绑定数据到会话(在服务器端使用类似与哈希表的结构来保存信息) 绑定到会话的数据可以在多次请求之间持续有效
	每个session对象都与一个浏览器窗口对应 重新开启一个浏览器窗口 可以重新创建一个session对象(不同版本浏览器可能有所差别)
	通过超链接打开的新窗口 新窗口的session与其父窗口的session相同
	
```

###### 会话失效

```
	
	会话也是有时效 的 使会话实效的方式有两种 
	//一 会话超时
	//二 手动调用方法设置失效
	
	
	会话超时是指 两次请求的时间间隔超过了服务器允许的最大时间间隔 会话的超时间隔 可以通过三种方式设置
	//一 通过session 对象的 setMaxInactiveInterval()方法设置 
	 <%
	 	session.setMaxInactiveInterval(600); //10分钟
	 %>
	//二 在项目的web.xml中设置代码段如下
	 <session-config>
	 	<session-timeout>10</session-timeout>  //单位分钟
	 	//如果设置为0或负数 表示永不超时
	 </session-config>
	//三 在应用服务器中设置 
	 在Tomcat目录/conf/web.xml 中找到<session-config>元素
	 其中<session-timeout>元素中的30就是默认的时间 单位是分钟 可以修改这个值
	 
	手动调用方法设置失效 
	 session.invalidate(); 主要用于用户注销的场合 
	 //如果只想清空会话中绑定的某个数据对象 则可以调用 session.removeAttribute(String key) 方法 将指定的对象 从会话中清除 而会话仍然有效
	
```

###### 常用方法

```
	
	getID()	//返回值String //获取sessionid
	setMaxInactiveInterval(int interval) //无返回值 //设定session的非活动时间 //秒
	getMaxInactiveInterval() //返回值int //获取session的有效非活动时间 以秒为单位
	invalidate() //无返回值 //设置session对象失效
	setAttribute(String key,Object value) //无返回值 //以key/value的形式将对象保存到session中
	getAttribute(String key) //返回值Object //通过key获取session中保存的对象
	//注意该方法取值 返回值是个Object需要进行转换
	removeAttribute(String key) //无返回值 //从session中删除指定的key对应的对象
	
```

###### 应用

```
	
	使用session对象实现权限控制 //用session对象储存一个 登录状态参数 如果直接进入页面状态参数没被赋值则 该用户没有进行登录过
	//注意不要直接 判断session对象为空 所有页面都会有个session对象 (误区)
	
```

##### application(类似于系统的全局变量 用于实现Web应用中的资源共享)

```
	
	实现用户之间的数据共享
	//统计网站访问次数
	//只能在一个Web应用程序中使用
	
```

###### 常用方法

```
	
	application实现用户之间的数据共享
	setAttribute(String key,Object value) //无返回值 //以key/value的形式保存对象值
	getAttribute(String key) //返回值Object //通过key获取对象值
	getRealPath(String path) //返回值String //返回相对路径的真实路径
	
```

###### 统计网站访问次数的案例

```
	
	--统计页面--
	<%
		Integer count = (Intege)application.getAttribute("count");
		if(count != null){
			count = 1 + count;
		}else{
			count = 1;
		}
		application.setAttribute("count",count);
	%>
	
	-显示页面-
	<%
		Integer i = (Integer)application.getAttribute("count");
		out.println("输出信息");
	%>
	
```

##### pageContext(page作用域访问对象)(了解)

###### 常用方法

```
	
	page作用域值本JSP页面的范围
	setAttribute(String key,Obejct value); //无返回值 //以key/value的形式保存对象值
	getAttribute(String key); //返回值Object //通过key获取对象值
	
```

##### 对象的作用域(生命周期 / 访问范围的差异)

###### 作用域的分类(作用范围)

```
	
	page作用域  //对应的作用域访问对象 为 pageContext对象
	 //在一个页面范围内有效 
	
	request作用域 //对应的作用域访问对象 为 request对象 在一起
	 //在一个服务器请求访问范围内有效
	
	session作用域 //对应的作用域访问对象 为 session对象
	 //在一次会话范围内容有效
	
	application作用域 //对应的作用域访问对象 为 application对象
	 //在一个应用服务器范围内有效
	
```

###### 作用域的关系

```
	
	application作用域 对应整个代码块
	
	  session作用域 对应一个用户会话
	     request作用域 对应一次请求
	     
	        page作用域 对应一个JSP页面的运行 > 转发 > page作用域 > ......
	     
	     request作用域 对应一次请求
	     
	     ......
	  
	  session作用域 对应一个用户会话
	  
	  session作用域 对应一个用户会话
	
	  ......
	
```

### include指令

```
	
	实现在多个页面实现的访问权限控制 避免重复编码
	将共性的内容写入一个单独的文件中 然后通过include指令引用该文件
	
```

#### 具体语法

```
	
	<%@ include file="应用文件路径" %>
	 
	 //表示JSP编译时插入一个包含文本或代码的文件 这个包含的过程是静态的
	 //包含的文件可以是JSP页面 HTML网页 文本文件等 
	 //include指令只有一个file属性 表示被包含的文件路径
	 //注意应用文件路径 注意内容不要 与 导入页面 写重
	 
```

### Cookie

#### 什么是Cookie

```
	
	由Netscape 公司发明 最常用的跟踪用户会话的方式 
	是由Web服务端生成并发送给客户端浏览器 浏览器将其保存为一系列文本信息
	
```

#### Cookie作用

```
	
	追踪特定对象 如访问者访问次数 最后访问时间 路径 次数 等
	实现各种个性化服务 如针对不同的用户喜好 显示内容
	简化登录 有效期内
	统计网页浏览次数
	
	//注意 Cookie容易泄露信息 不要储存一些重要信息
	//session 被保存在Cookie中
	
```

#### Cookie使用

```
	
	//创建Cookie对象  //并且赋值
	//创建一行Cookie
	
	Cookie newCookie = new Cookie(String key,String value);
	
	//写入Cookie
	
	response.addCookie(newCookie);
	
	//读取Cookie //注意返回的是一个数组
	
	Cookie[] cookies = request.getCookies();

```

#### 常用方法

```
	
	setMaxAge(int time) //无返回值 //设置Cookie的有效期 以秒为单位
	 //一些设置 时间的可以 设置为 例 5*60 = 5分钟这样利于编写读取和理解
	 //设置有效期之后 Cookie会被从客户端清除
	
	setValue(String value) //无返回值 //在Cookie创建后 对Cookie进行赋值
	getName() //返回值String //获取Cookie的名称
	getValue() //返回值String //获取Cookie的值
	getMaxAge() //返回值int //获取Cookie的有效时间 以秒为单位
	
```

#### Cookie与Session的对比

```
	
	session 
	 在服务器端保存用户信息
	 session保存的类型是Object类型
	 随会话的结束而将其储存的数据销毁
	 保存重要的信息
	
	cookie
	 在客户端保存用户信息
	 cookie保存的是String类型
	 cookie可以长期保存在客户端
	 保存不重要的用户信息
	 
	区别为 在哪保存 保存什么样的类型 保存时间 保存一些什么样的数据

```

### 在Cookie中读取Session的问题

```
	
	如果是通过重定向查看sessionid 因为是两次请求 在第二次转换网页之前 服务以及对上一个请求做出了响应
	
	但如果是转发 他是一次请求 服务器端的处理 服务器没有对请求进行响应 所以 客户端没有写入Cookie 这是 只要通过浏览器再次访问页面(直接输入URL地址访问) 即可看到上次响应写入的cookie
	
```

## JSP访问数据库

```
	
	注意因为要使用数据库 所以就要使用JDBC jar包
	将对应数据库的驱动包 添加到项目的WEB-INF/lib目录下
	使用时根据先前的项目结构 lib设置 classes设置等 获取对应资源进行处理 在需要数据库的页面
	利用import导入要使用的类(进过简化Dao处理的) 进行相关操作
	
	//可以在项目下创建 resources文件夹 并在模块设置中 设置为 资源文件夹 便于管理
	
	分层实现
	数据访问层(DAO)
	表示层(JSP)
	 非空验证
	 提示错误信息并保留用户所填写的信息
	
```

## JNDI

### 什么是JNDI

```
	
	Java Naming and Directory Interface Java命名和目录接口
	//通过名称将资源与服务进行关联 
	//为开发人员提供了查找和访问各种命名和目录服务的通用API 通常可简单理解为 通过JNDI服务可以使用名字获取对应的资源(对象或服务)
	
```

### JNDI的作用与优点

```
	
	作用 在应用与Java对象或资源之间建立松耦合的逻辑关联
	//通俗的将就是 指定一个资源名称 将名称与某一资源或服务器相关
   
   	优点 
   		简化应用对于资源的配置及维护工作
   		可以在更大范围、不同应用间共享资源
   		
   	//使用application也能实现一些同样的功能 但是application对象只能在一个Web应用程序中使用 而JNDI发布的信息是对服务器上所有的Web程序都可见的
	
```

### JNDI应用

```
	
	实现在Tomcat中发布一条信息(资源)供所有的Web应用程序使用
	步骤一
	 修改Tomcat\conf\context.xml 文件
	 --context.xml-- //注意大小写!!!
	 <Context>
	 	<Environment name="参数1" value="参数2" type="参数3">
	 </Context>
	 //参数1  	JNDI查找的名称 	例HelloMsg
	 //参数2		资源的值(该值必须转成type属性指定的值)	例hello world
	 //参数3 		资源的类型   例java.lang.String
	 //<Environment>元素用于配置名的值 所配置的值作为环境条目资源对整个Web应用可见
	步骤二
	 使用lookup() 获取资源
	 --使用资源的编码位置--
	 //javax.naming.Context提供了查找JNDI的接口
	 Context context = new InitialContext(); //初始化Context对象
	 String helloMsg = (String)context.lookup("java:comp/env/HelloMsg"); //取出值
	 //javax.naming包下的Context接口表示命名上下文 由一组名称到对象的绑定组成
	 //lookup(String name) 根据名称检索指定对象
	 //其中java:comp/env/ 为固定前缀(为了避免JNDI命名空间中的资源名称互相冲突 避免可移植性问题)
	 ......使用helloMsg
	
```

### 连接池(Connection Pool) (注意!!!Tomcat版本)

```
	
	连接池设置问题 高版本tomcat内置的DBCP2和老版本的连接池不一样 7.0等老版本用的是DBCP
		
	maxActive 换为 maxTotal 重启Tomcat 解决问题
	maxWait 换为 maxWaitMillis 重启Tomcat 解决问题
	
```

#### 连接池作用

```
	
	传统数据库连接方式不足
	
			-->请求			-->操作(打开连接)!!!多次重复
	客户端 			服务器								数据库
			<--响应			<--结果(关闭连接)!!!多次重复
			
	//需要经常与数据库建立连接 在访问结束后必须关闭连接释放资源 耗费资源 容易引发异常
	//当并发访问数量较大时 执行速度受到极大影响
	//系统的安全性和稳定性相对较差
	
	//数据库连接池负责分配、管理、释放数据库连接 它允许应用程序重复使用一个现有的数据库连接 而不是重新建立一个 释放那些空闲时间超过最大空闲时间的数据库连接 以避免由于没有释放数据库连接而引起的数据库连接遗漏 它能明显的提高对数据库操作的性能
	
```

#### 连接池原理

```
	
	连接池中的连接
	
			-->请求			  		想要获得连接-->	 Connection1
	客户端 			服务器(应用程序)					Connection2	数据库
			<--响应                   <--返回一个连接	 Connection3
	
	//Connection1、2、3 组成的块称为 连接池
	//应用程序从连接池中获得连接
	//传统模式 数据库连接使用完毕需要将其关闭 释放资源
	//在连接池中关闭连接对象 不会真正的关闭连接 仅仅实现了断开应用程序与连接池之间的联系 将连接的使用权归还给连接池
	
	//数据库连接池在初始化时将创建一定数量的数据库连接并放到连接池中(由最小数据库连接数设定的)  连接池将确保至少有这么多的连接数量(无论是否被使用) 连接池的最大数据库连接数量限定了这个连接池能占有的最大连接数 当请求连接数超过最大连接数 请求加入等待队列 //等待时间超过预定时间 将返回空值(null) //系统对已经分配出去正在使用的连接只用作计数
	
```

#### DataSource(数据源)与连接池

```
	
	数据源在JDBC 2.0 引入的概念
	
	javax.sql.DataSource接口的实现类
	 //负责管理与数据库的连接
	 //有一组特性用于确定和描述它所表示的显示存在的数据源
	 //可以通过数据源直接获得数据库连接
	 //已连接池的形式对数据库连接进行管理
	 
	获取DataSource实例 原理指向
	 //DataSource对象由Web容器提供的 因此不能在程序中采用创建一个实例的方式生成DataSource对象 而需要通过JNDI来获取
	 //Tomcat支持将DataSource实现发布为JNDI资源
	 //Web应用通过JNDI获得DataSource引用
	 --Tomcat环境下--
	  Web应用(context.lookup("java:comp/env/jabc/s1"))
	  ↓
	  数据源JNDI名(jdbc/s1 | jdbc/s2)
	  ↓
	  数据源(DataSource实例1 | DataSouce实例2)
	 
```

#### 使用连接池实现数据库连接(注意!!!Tomcat版本)

```
	
	//注意不同的Web服务器配置数据源的方式不同
	
	//连接池设置问题 高版本tomcat内置的DBCP2和老版本的连接池不一样 7.0等老版本用的是DBCP
	  maxActive 换为 maxTotal 重启Tomcat 解决问题
	  maxWait 换为 maxWaitMillis 重启Tomcat 解决问题
	  
	步骤一 配置context.xml文件 //Tomcat的conf文件夹下
		--context.xml--
	 <Context>
	 	<Resource name="参数1" auth="参数2" type="参数3" maxActive="参数4" maxIdle="参数5" maxWait="参数6" username="参数7" password="参数8" driverClassName="参数9" url="参数10" />
	 </Context>
	 //参数1		指定Resource的JNDI名称  通常有/格式  例   jdbc/news
	 //参数2 		指定管理Resource的Manager  两个值待选 Container(表示由容器创建Resource) Application(表示由Web应用创建管理)
	 //参数3      指定Resource所属的Java类(类型)  例 javax.sql.DataSource //固定
	 //参数4  	指定连接池中处于 活动 状态的数据库连接的最大数目 (上班案例理解) 值例100
	 //参数5		指定连接池中处于 空闲 状态的数据库连接的最大数目 (上班案例理解) 值例20
取值为0表示不受限制
	 //参数6  	指定链接池中的连接处于空闲的最长时间 (上班案例理解) 值例10000
	 //参数7 		数据库连接用户名
	 //参数8 		数据库连接密码
	 //参数9		指定连接数据库的JDBC驱动程序
	 //参数10		数据库连接URL 值例 jdbc:mysql://localhost:3306/数据库名称?useUnicode=true&amp;characterEncoding=utf-8
	 //注意对于url中出现的"&" 要将其替换为对应的实体 "&amp;"
	
	步骤二 配置web.xml文件 //使用连接池Web项目的WEB-INF文件夹下 //与Context.xml指定的名称一致
		--web.xml--
	<resource-ref> 
		<description>对所引用资源的说明</description> //可省略项
        <res-ref-name>jdbc/news</res-ref-name> //指定JNDI的名字 与<Resource>元素中的name一致
        <res-type>javax.sql.DataSource</res-type> //指定引用资源的类名 与<Resource>元素中的type一致
        <res-auth>Container</res-auth> //指定管理所引用资源的Manager与<Resource>元素中的auth一致
    </resource-ref>
	
	步骤三 添加数据库驱动文件 //将数据库驱动的jar包 加入到Tomcat的lib中
	
	步骤四 进行代码编写 查找并获取数据源 //lookup()参数的写法
		--访问数据源的类--
		Context context = new InitialContext(); //创建Context对象
		DataSource dataSource = (DataSource)context.lookup("java:comp/env/jdbc/news"); //获取DataSource
		Connection connection = dataSource.getConnection; //获取Connection数据库连接对象
	......使用数据库连接对象 BasDao中使用 ....分层实现等等
	步骤五 程序结束数据库访问后 调用Connection的close()方法将Connection返回给数据库连接池让Connection恢复空闲状态
	
```

```
	
	还有一种配置数据源方式 只需要在WebRoot目录下的META-INF目录中创建一个context.xml文件 添加<Context>节点 然后在<Context>节点中添加<Resource>元素内容
	
```

#### 常见错误

```
	
	Cannot load JDBC driver class (SQLNestedException) 不能加载驱动类 注意添加jar包 如果还不行 把classes包中的东西都删除一遍
	
	Cannot create JDBC driver of class '' for connect URL 'null' (SQLNestedException) 由于连接路径为null 不能创建驱动 context.xml文件出现配置信息错误
	
	Name[xxxx] is not bound in this Context (NameNotFoundException) jdbc名称没有绑定到当前上下文  数据源名称与配置文件中的名称不一致 或者 lookup()中没有添加前缀jdbc:comp/env/
	
	注意利用数据库连接池 获取Connection对象  不能在IDEA的main方法内进行测试 需要在(Sevlet)Tomcat环境下进行
	
```

## 软件设计分层模式

```
	
	JSP开发分两层的弊端
	//展示逻辑与业务流程混合或者业务代码与数据访问混合
	//编码职责不清 修改时互相影响 难以扩展和重用
	
	分层模式是很多架构的基础 
	分层模式就是将解决方案的组件分隔到不同的层中 
	//每一层中的组件应保持内聚性 
	//每一层都应与其下面的各层保持松耦合
	
```

### 三层架构(影响力最大 最成熟)

```
	
	三层指 表示层 业务逻辑层 数据访问层
	
```

### 三层架构划分

```
	
				 表示层
		实 		↓
		体  		业务逻辑层
		类 		↓
		    	 数据访问层
	
	表示层  
		//与用户交互、收集数据、展示结果 
		//用户能够直接访问
		//为用户提供一种交互操作界面
		//一般以JSP文件、HTML文件为主
	 
	业务逻辑层 
		//根据业务需要控制执行过程(流程控制)、进行事务管理
		//提供对业务逻辑处理的封装
		//通过调用业务逻辑类的接口实现各种操作
		//业务逻辑类经常放在service包或biz包下 biz(business)的缩写 业务逻辑的意思
		
	数据访问层 
		//提供的业务无关的数据访问操作
		//实现对数据的保存和读取操作 
		//数据访问 可以访问关系数据库1、文本文件或者 XML文档等
		//通常放在dao包下 dao(Data Access Object) 数据访问对象的意思
		
```

### 三层架构层与层的关系

```
		
	各层直接的数据传递方向分为 请求 和 响应 两个方向

	 			--表示层--
	 	客户请求↓			↑响应数据	
	 		   --业务逻辑层--
	 	客户请求↓			↑响应数据	
	 		   --数据访问层--
	 	客户请求↓			↑响应数据	
	 	
	//三层架构 各层之间相互依赖 
	//表示层 依赖 业务逻辑层 
	//业务逻辑层 依赖 数据访问层
	//业务逻辑层的位置非常重要 起到数据转换中承上启下的作用 理想的分层式架构 应该是一个支持可抽取、可替换的"抽屉式"架构 所以对于支持可扩展的架构尤为关键(面向接口编程) 
	
    一 表示层根据用户操作 将请求提交给业务逻辑层
    二 业务逻辑层收到请求 对数据进行审核和处理 将请求通知数据访问层 或 直接将处理结果返回表示层
    三 数据库访问层收到业务逻辑层调用开始访问数据库
	四 数据访问层通过对数据库的访问得到请求结果 并把请求结果通知业务逻辑层
	五 业务逻辑层收到请求 对请求结果进行审核和处理 将请求通知表现层
	六 表示层接受请求结果 并把结果展示给用户
	 	
```

### 分层原则(分工明确,各司其职,职责清晰,无损替换(面向接口),复用代码,降低依赖程度)

```
		
	上层依赖 下层 依赖关系不跨层 
	 表示层 不能直接访问 数据库访问层
	 上层 调用 下层结果 取决于下层的实现
	下一次不能调用上一层
	下一层不依赖上一层
	 上层的改变不会影响下一层
	 下层的改变会影响上一次的到的结果
	在上一层中不能出现下一层的概念
	 
```

### 分层模式的弊端

```
	
	原本很直接的操作 现在要通过层层传递 势必造成性能的下降
    虽然分层架构可以降低层内变化的成本 但对于功能定义(接口定义)的变化非常敏感 功能定义的变动对于分层架构是致命的 修改起来难度非常大 所有 如果系统层内实现频繁变动(甚至整层替换)的可能性很大 而功能定义变动的可能性很小 就使用分层
	
```

### 新闻实例分层详概

```
	
	登陆部分(其他部分概括一样)
	
	实体类User //传输职责
	数据库工具类BaseDao //负责执行SQL(DML、DQL)语句 
	数据库连接类DatabaseUtil //负责关闭数据库连接 和 创建数据库连接(为了让事务在业务逻辑类实现 所以打开和关闭数据库连接必须放到业务逻辑层)
	数据库访问层UserDaoImpl //实现具体访问数据库的语句和方法
	数据库访问层接口 //隔离数据库实现
	业务逻辑层UserServiceImpl //负责处理数据和用户请求 控制事务 数据库对象开启和关闭 进行业务处理
	业务逻辑层接口UserServiceDao //隔离处理实现 实现无损替换
	显示层 //JSP/HTML等页面 导入上面java包 进行处理 实现显示
	
```

## JSP开发业务应用

### 实现数据分页显示(有分页page实现代码示例)

```
	
	数据量很大时,可能有几万、几十万甚至上百万条数据 受页面的限制 用户必须拖动页面才能浏览更多的数据,所以需要进行分页
	
```

#### 主要实现方式

```
	
	第一种 将所有查询结果 以集合等形式保存在内存中 翻页是从中取出一页所需的数据显示 、
	//有两个缺点 一是用户看到的可能是过期数据 二是如果数据量非常大 查询一次数据集会消耗很长时间 会占用大部分内存开销
	
	第二种 每次翻页只从数据库检索出本页所需的数据 但查询出的记录数相对较少 总体开销不大 配以连接池技术 可以达到比较高的效率
	
```

#### 实现步骤

```
	
	确定每页显示的数据数量[pageSize]
	计算显示的页数(当前页数)[currPageNo]
	获取总记录数[totalCount]
	数据总共分了多少页[totalPageCount]
	
	Limit核心公式 (当前页数-1)*每页显示数量[起始行偏移量],每页显示数量[每页获取个数]
	
	//注意对数据进行合法性判断
	
	将有关分页的数据封装到Page类
	public class Page {

        private int currPageNo = 1; // 当前页码
        private int pageSize = 15;    // 页面大小，即每页显示记录数
        private int totalCount;          // 记录总数
        private int totalPageCount; // 总页数
        List<News> newsList;         // 每页新闻集合

        // 省略getter/setter方法 //必要数据合法性验证 //和根据变量值进行 页面边界控制
	}
	
	根据已确认的当前页码设置参数
	<%  
  		 <a href="pageControl.jsp?pageIndex=1">首页</a>
 	     <a href="pageControl.jsp?pageIndex=<%=pageIndex - 1%>">上一页</a>
 	     <a href="pageControl.jsp?pageIndex=<%=pageIndex + 1%>">下一页</a>
  	     <a href="pageControl.jsp?pageIndex=<%=totalPages%>">末页</a>
	%>

```

### 实现文件上传(有文件上传实现代码示例)

```
	
	使用Commons-FileUpload组件实现 可以极大地简化开发编码工作量
	
	Commons是Apache开放源代码组织的Java子项目 该项目主要涉及 开发中要用的常用模块 文件上传 命令行处理 数据库连接池等  FileUpload 就是其中一个用于处理HTTP文件上传的子项目 
	//使用简单 能够全程控制上传内容 能够对上传文件大小、类型 进行控制 能够获得全部上传文件的信息(包括文件名称、类型、大小等)方便操作
	
	//首先要获取Commons-FileUpload组件 详细操作进行百度
	http://commons.apache.org/fileupload下载Commons-FileUpload组件
		类库：commons-fileupload-1.2.2.jar
		API文档：commons-fileupload-1.2.2\site\apidocs 
	http://commons.apache.org/io下载Commons-IO组件
		类库：commons-io-2.4.jar
		API文档：commons-io-2.4\docs
		
```

#### Commons-FileUpload组件的API

```
	
	ServletFileUpload类的常用方法  主要用于文件上传操作
	
	public void setSizeMax (long  sizeMax) //设置请求信息实体内容的最大允许的字节数
	public  List  parseRequest (HttpServletRequest  req) //解析form表单中的每个字符的数据，返回一个FileItem对象集合
	public static final boolean isMultipartContent(HttpServletRequest req) //判断请求信息中的内容 是否是multipart/form-data类型
	public  void  setHeaderEncoding (String  encoding) //设置转换时所使用的字符集编码
    
    
   FileItem接口的常用方法 用于封装单个表单字段元素的数据

    public  boolean  isFormField() //判断FileItem对象封装的数据类型（普通表单字段返回true，文件表单字段返回false）
 	public  String  getName() //获得文件上传字段中的文件名（普通表单字段返回null）
	public  String  getFieldName() //返回表单字段元素的name属性值
	public  void  write() //将FileItem对象中保存的主体内容保存到指定的文件中
	public  String  getString() //将FileItem对象中保存的主体内容以一个字符串返回。其重载方法public  String  getString(String encoding)中的参数用指定的字符集编码方式
	public  long  getSize() //返回单个上传文件的字节数


	FileItemFactory接口  	实现类 DiskFileItemFactory

	public void  setSizeThreshold(int sizeThreshold) //设置内存缓冲区的大小
	public void  setRepositoryPath(String path) //设置临时文件存放的目录
    
```

#### 实现步骤

```
	
	首先实现文件上传 需要在form表单属性中添加enctype属性 用于设置表单提交数据的编码方式
	由于文件传到服务器是与一般文本类型的编码方式不同 需要使用multipart/form-data的编码方式
	<form enctype="multipart/form-data" method="post"><form>
	//上传文件是form标签的method属性取值必须为"post",不能为"get"
	
	//表单的enctype属性有一下三个值
	application/x-www-form-urlencoded 是其默认值 该属性主要用于处理少量文本数据的传递 在向服务器发送大量的文件包含非ASCII字符的文本或二进制数据时效率很低
	multipart/form-data 上传二进制数据 只有使用了multipart/form-data才能完整地传递文件数据 进行上传操作
	text/plain 主要用于向服务器传递大量文本数据 比较适用于电子邮件的应用
	
	第二部 使用File控件(input表单元素 文件域)
	<form enctype="multipart/form-data" method="post"><input type='file' name='afile'></input><form>
	
	环境准备
	在项目中引入commons-fileupload-1.2.2.jar和commons-io-2.4.jar文件
	并且将commons-fileupload组件使用的类库导入到JSP 
	<%@ page import="org.apche.commons.fileupload.*" %>
	
	编写上传文件处理页的实现步骤
		创建FileItemFactory对象
		创建ServletFileUpload对象	
			通过构造方法：ServletFileUpload( 利用FileItemFactory实例化 )
		解析form表单提交的所有表单元素数据
		//调用ServletFileUpload对象的parseRequest() 将表单中字段解析成FileItem对象的集合
		//通过迭代一次处理每个FileItem对象 根据表单字段(getName()获取表单name值)进行判断
			如果是普通表单元素
				获取该元素的名和值使用
			如果是文件数据
				获取文件名的等参数
				保存文件数据到服务器
				//通过File的构造方法构建一个指定路径名和文件名的文件 并通过FileItem对象的write()方法将上传文件的内容保存到文件中
	
```

#### 控制文件上传(使服务器更安全 避免服务器被破坏 节约服务器空间)

```
	
	控制上传文件类型
	//利用Arrays类的asList()方法 创建固定长度的集合(允许文件类型的集合) 然后通过集合的contains()方法匹配上传文件的扩展名来判断文件类型是否在允许范围内
	
	控制文件上传大小
		/*
			File tempPatchFile = new File("//缓存路径");
			if(!tempPatchFile.exists()) //判断文件或目录是否存在
				tempPatchFile.mkdirs(); //串讲指定的目录包括所有必须但不存在的父目录
			if(isMultipart){
				DiskFileItemFactory factory = new DiskFileItemFactory();
				factory.setSizeThreshold(4096); //设置缓冲区大小4kb
				factory.setRepository(tempPatchFile); //设置临时文件目录路径
				ServletFileUpload upload = new ServletFileUpload(factory);
                 // 设置一个完整请求的最大限制
                 upload.setSizeMax(1024 * 30); 
                 try { 
                     // ……省略上传代码
                 } catch (FileUploadBase.SizeLimitExceededException ex) {
         	        out.print("上传失败，文件太大，全部文件的最大限制是：" +
             	    upload.getSizeMax() + "bytes!");
                 }
			}
		*/

```

## Servlet基础

```
	
	JSP技术是基于Servlet技术实现的
	//是一个符合特定规范的Java程序 是一个基于Java技术的Web组件 运行在服务端 由Servlet容器管理 用于处理客户端请求并做出响应(主要用于生成动态的内容 可以接受和处理请求 动态生成HTML内容对客户端进行响应)
	
	//就是一个接口 定义了Java类被浏览器访问到(tomcat识别)的规则
	
```

### Servlet容器

```
	
	Servlet容器也称为Servlet引擎 是Web服务器或应用程序服务器的一部分,用于在发送的请求和响应之上提供网络服务,管理和运行Servlet/JSP的容器也称为Web容器
	
```

### Servlet与JSP的关系 和 区别

```
	
	它们都可以在页面上动态显示数据 
	在访问JSP页面的时候 将JSP翻译成JAVA源代码 解释了JSP的技术根源 (在运行JSP后 Tomcat安装目录的work\Catalina\localhost\store\org\apche\jsp下会生成一个xxx_jsp.java) 即JSP在运行时会被Web容器翻译为一个Servlet 动态响应内容是通过运行Servlet类产生的 //是动态交互技术的关键组件 也是JSP的技术基础
	JSP是为了简化Servlet的开发而产生的 避免了编写复杂的输出方法 更加适用于 开发 带有页面内容 的表示层组件现在的Java Web应用开发中 JSP和Servlet分别扮演着不同的角色
	//JSP可以看成是运行时的Servlet
	
	区别
	JSP页面在HTML元素中嵌入Java脚本diamante 和 JSP标记 比传统Servlet技术开发表示层更加容易 JSP的部署也更加简单JSP容器(Servlet容器)会对扩展名是.jsp的URL统一配置 将其转换为Servlet为客户端服务器 无需为每一个JSP文件配置URL映射
	JSP页面 HTML元素与Java脚本混合的语法 对于请求处理过程中 编写流程控制代码、数据访问代码等是不利的 难以模块化开发以及重用 此时更适合采用传统Java类的形式进行开发 故而使用Servlet在服务器解析和执行浏览器的请求 充当客户端和其它层之间的中间层角色更加合适
	
	//合并以上 Servlet和JSP各有所长 
	JSP可以方便的开发表示层组件(只负责 表示层)
	Servlet适合编写流程控制代码(负责 流程控制和业务逻辑处理 当做页面控制器)
	在开发Web应用时 可以针对两者的特点结合使用 合理分工 提高代码重用
	
```

### Servlet生命周期

```
	
	实例化 Servlet容器创建Servlet实例
	
		Servlet不能独立执行 必须被部署到Servlet容器中 由容器实例化和调用Servlet的方法 Servlet容器在Servlet的声明周期内管理Servlet Servlet会查找内存中是否存在该Servlet实例 如果不存在 就创建一个Servlet实例 如果存在该Servlet实例 就直接从内存中取该实例响应请求
	
	初始化 该容器调用init(ServletConfig)方法 只被调用一次
	
		Servlet实例化之后 将会调用init()方法进行初始化 目的是让Servlet对象在处理客户端请求前完成一些准备或资源预加载工作 例如 建立JDBC连接 或是建立对其它资源的引用 对于每一个Servlet实例 init()方法只被调用一次
		
	服务   如果请求Servlet 则容器调用service()方法  反复调用
	
		Servlet初始化之后 就处于能响应请求的就绪状态 调用service()方法会根据GET或POST请求转调doGet() doPost()方法
	
	销毁   销毁实例之前调用destroy()方法 执行一次
	
		容器判断Servlet是否应当被释放是(容器关闭或需要回收资源) 容器就会调用Servlet的destroy()方法 该方法指明那些资源可以被系统回收 而不是直接回收实例

```

### Servlet 体系结构

```
	
	接口 
	
		Servlet     ServletConfig
	
	抽象类
	
		GenericServlet
			继承↑
		HTTPServlet
	
	请求响应相关接口
	
	ServletRequest请求 	ServletResonse响应
    继承↑
	HttpServletRequest请求 	HttpServletResonse响应
	
```

### Servlet API

```
		
	Servlet 实际上就是按照Servlet规范编写的一个Java类
		
	Servlet API主要包含在两个包内
		
	javax.servlet 包含Servlet ServletRequest ServletResponse ServletConfig ServletContext接口及抽象类GenericServlet
	jacax.servlet.http 包中的类和接口是用于支持HTTP协议的Servlet API
		
```

#### Servlet接口(定义了所有Servlet需要实现的方法)

|                           方法名称                           |                           功能描述                           |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
|         abstract void  init (ServletConfig  config)          | 由Servlet 容器调用，用于完成Servlet对象在处理客户请求前的初始化工作 |
| abstract void  service (ServletRequest  req,ServletResponse  res) |           由Servlet容器调用，用来处理客户端的请求            |
|                  abstract void  destroy ()                   |        由Servlet容器调用，释放Servlet对象所使用的资源        |
|         abstract ServletConfig getServletConfig ( )          | 返回ServletConfig对象，该对象包含此Servlet 的初始化和启动参数。返回的ServletConfig对象是传递给init() 方法的对象 |
|              abstract String  getServletInfo()               | 返回有关Servlet的信息，比如作者、版本和版权。返回的字符串是纯文本，而不是任何种类的标记(如 HTML、XML等) |

#### GenericServlet抽象类 (提供了Servlet与ServletConfig接口方法的默认实现 service()方法除外)

|                     方法名称                     |                           功能描述                           |
| :----------------------------------------------: | :----------------------------------------------------------: |
|   public  void  init (ServletConfig  config )    | 对Servlet接口中init()方法的实现，对ServletConfig实例进行了保存。此方法还有一个无参的重载方法，可用于子类中重写 |
| public  String  getInitParameter (String  name ) |           返回web.xml中名称为name的初始化参数的值            |
|    public  ServletContext getServletContext()    |                 返回ServletContext对象的引用                 |

```
	
	通常只需要重写不带 参数的init() 方法 如果重写init(ServletConfig config)方法 则应包含super.init(config)代码
	如果要编写一个通用的Servlet 只要继承自GenericServlet类 实现Servlet方法即可
	
```

#### HttpServlet抽象类

```
	
	大多数的网络应用是通过HTTP协议访问服务器资源的 因此我们编写的Servlet大多也是应用于处理HTTP协议的请求和响应 抽象类HTTPServlet继承自GenericServlet类 提供了HTTP相关的实现 支持对HTTP的Post Get等请求方式进行差异化处理 开发中如果需要编写Servlet主要就是继承HttpServlet抽象类
	
```

|                           方法名称                           |                           功能描述                           |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
| public  void service ( ServletRequest  req, ServletResponse  res ) | 对GenericServlet类中service()方法的实现，将请求分发给protected  voidservice (HttpServletRequest  req,HttpServletResponse  res ) |
| protected  void  service (HttpServletRequest req,HttpServletResponse  res ) |     接收HTTP请求，并将它们分发给此类中定义的doXXX()方法      |
| protected  void  doXXX(HttpServletRequest  req,HttpServletResponse  res ) | 根据请求方式的不同分别调用的相应处理方法，如doGet()、doPost()等    //所以在使用的时候 只需要重写 这两个方法就行 doGet()、doPost() |

#### ServletConfig接口

```
	
	Servlet 容器使用ServletConfig接口的实例 在Servlet初始化期间向其传递配置信息 
	一个Servlet只有一个ServletConfig对象
	
```

|                 方法名称                 |                  功能描述                   |
| :--------------------------------------: | :-----------------------------------------: |
| String  getInitParameter (String  name ) | 获取web.xml中设置的以name命名的初始化参数值 |
|   ServletContext  getServletContext( )   |         返回Servlet的上下文对象引用         |

#### ServletContext接口(获取Web应用上下文,与Servlet容器进行通信)

```

	JSP内置对象 application 就是 ServletContext的实例
	ServletContext对象呗Servlet容器中所有的Servlet共享
	可以用来获取服务器信息
	
```

|                   **方法名称**                    |                           功能描述                           |
| :-----------------------------------------------: | :----------------------------------------------------------: |
|     String  getInitParameter (String  name )      | 获取名为name的系统范围的初始化参数值，系统范围的初始化参数可在部署描述符中使用<context-param>元素定义 |
| void  setAttribute (String name,  Object object ) |                     设置名称为name的属性                     |
|       Object  getAttribute (String  name )        |                     获取名称为name的属性                     |
|           void  log ( String message )            |                       记录一般日志信息                       |
|        String  getRealPath (String  path )        |                 返回参数所代表目录的真实路径                 |

#### ServletRequest接口(获取客户端请求的数据)

|                      方法名称                       |           功能描述           |
| :-------------------------------------------------: | :--------------------------: |
|          Object getAttribute(String name)           |    获取名称为name的属性值    |
|    void setAttribute(String name,Object object)     | 在请求中保存名称为name的属性 |
|          void removeAttribute(String name)          |  清除请求中名字为name的属性  |
|            String getCharacterEncoding()            |  返回请求体所使用的字符编码  |
|     void setCharacterEncoding (String charset)      |     设置请求体的字符编码     |
|          String getParameter(String name)           |     返回指定请求参数的值     |
|      String[] getParameterValues(String name)       |   返回指定请求参数的全部值   |
| RequestDispatcher getRequestDispatcher(String path) |  返回指向指定路径的请求分发  |

#### HttpServletRequest接口

```
	
	除了继承ServletRequest接口中的方法 还增加了一些用于读取HTTP请求信息的方法
	
```

|            方法名称            |                           功能描述                           |
| :----------------------------: | :----------------------------------------------------------: |
|    String  getContextPath()    | 返回请求URI中表示请求上下文的路径，上下文路径是请求URI的开始部分 |
|    Cookie[ ]  getCookies()     |          返回客户端在此次请求中发送的所有cookie对象          |
|    HttpSession getSession()    | 返回和此次请求相关联的session，如果没有给客户端分配session，则创建一个新的session |
|       String getMethod()       |       返回此次请求所使用的HTTP方法的名字，如GET、POST        |
| String getHeader(String  name) |                     返回指定的请求头信息                     |

#### ServletResponse接口(设置响应参数和向客户端发送响应数据)

|                  方法名称                  |                           功能描述                           |
| :----------------------------------------: | :----------------------------------------------------------: |
|          PrintWriter getWriter()           |          返回PrintWriter对象，用于向客户端发送文本           |
|       String getCharacterEncoding()        |            返回在响应中发送的正文所使用的字符编码            |
| void setCharacterEncoding(String charset ) |                      设置响应的字符编码                      |
|      void setContentType(String type)      | 设置发送到客户端的响应的内容类型，此时响应的状态属于尚未提交 |

#### HttpServletResponse接口

```
	
	除了继承ServletResponse接口中的方法,还增加了适用于HTTP响应的新方法
	
```

|                   方法名称                   |                          功能描述                          |
| :------------------------------------------: | :--------------------------------------------------------: |
|        void addCookie(Cookie  cookie)        | 增加一个cookie到响应中，这个方法可多次调用，设置多个cookie |
| void  addHeader( String name,String  value ) |     将一个名称为name，值为value的响应报头添加到响应中      |
|         void  encodeURL(String  url)         |           使用sessionID对用于重定向的URL进行编码           |
|     void  sendRedirect(String  location)     |  发送一个临时的重定向响应到客户端，以便客户端访问新的URL   |

### Servlet的应用

```
	
	创建Servlet 一个xxxServlet名称 java类
		//继承HTTPServlet
		//重写doPost()或doGet()方法
		//编写业务处理逻辑(创建out对象 进行页面输出 调用业务逻辑层处理业务等等)
		
	部署Servlet
		//编译Servlet到/WEB-INF/classes目录
		//编辑部署描述文件web.xml  
		<servlet> <!-- 将Servlet全类名(包名+类名)映射到一个内部名称 -->
	        <servlet-name>xxxServlet</servlet-name>
	        <servlet-class>web.位置包.xxxServlet</servlet-class>
	    </servlet>
	
	    <servlet-mapping> <!-- 将某个URL映射到Servlet的内部名称 -->
	        <servlet-name>xxxServlet</servlet-name>
	        <url-pattern>/xxxServlet</url-pattern> <!-- 先找它 根据它得到servlet-name 之后 向(servlet)中找<servlet-name> -->
	    </servlet-mapping>
		
	启动Tomcat 访问Servlet
		表单提交(action) 超链接(href) 提交路径 指向web.xml文件中<url-pattern>元素所指定的URL 即可访问对应的Servlet
	
	//<servlet>元素可以包含多个子元素  <servlet-name> <servlet-class> <load-on-startup>
	//<servlet-name>指定Servlet的名字 这个名字在同一个Web应用中必须唯一
	//<load-on-startup> 有时需要指定在容器启动时Servlet的加载次序 可以在<servlet>元素中增加该元素 //该元素的值必须是整数 如果为负数或没有指定这个元素 容器将在客户端首次访问Servlet时进行加载 如果为整数或0容器在启动时根据值的顺序加载Servlet 且值越小加载优先级越高
	//<servlet-class>指定Servlet1完全限定名
	//<servlet-mapping>元素在Servlet和URL之间定义映射 包含两个子元素<servlet-name>和<url-pattern>
	//<url-pattern>元素指定Servlet的URL 注意 该路径是相对于Web应用程序的路径
	//常用<url-pattern>设置方法
		<url-pattern>/xxx</url-pattern> //精确匹配
		<url-pattern>/xxx/*</url-pattern> //路径匹配 如果没有请求匹配 对/***/路径的所有请求将由该Servlet进行处理
		<url-pattern>*.xxx</url-pattern> //如果没有精确匹配和路径匹配 则所有针对.xxx扩展名的请求将由该Servlet处理
	
	**/当Servlet容器接收到一个请求时 对请求的路径和Servlet映射的路径进行匹配 进而调用具体Servlet类的相关方法
	
```

#### Servlet的应用处理流程

```
	
	浏览器 发送请求 到Web服务器的Servlet(根据请求访问业务逻辑层 或 直接返回结果)[编译/运行] 选择表示层 > JSP 响应回浏览器 浏览器接收显示
	
```

#### 创建Servlet (Servlet示例)

```
	
	public class XxxServlet extends HttpServlet{
		public void doGet(HttpServletRequest request,HttpServletResponse response) throws ServletException,IOException{
			response.setContentType("text/html;charset=UTF-8"); //设置响应编码
			PrintWriter out = response.getWriter(); //注意这里是通过response对象获取的要先设置编码 之后在获取此对象 要不然设置编码无用 出现乱码问题
			String contextPath = request.getContextPath(); //可以通过此方法获取当前Web应用的上下文路径 对于经由浏览器请求的URL 使用应用上下文路径进行约束 可以避免使用 相对路径时 可能发生的路径解析错误 例如location.href 转发 重定向 地址等可以将它进行地址拼合 对于转发方法使用的URL可以直接以/开始表示当前应用的根路径
			//省略逻辑处理
			out.print("<h1>测试内容</h1>");
			out.flush(); //刷新流
			out.close(); //关闭流
			
		}
		public void doPost(HttpServletRequest request,HttpServletResponse response) throws ServletException,IOException{
			request.setCharacterEncoding("UTF-8"); //设置post提交方式 请求编码
			this.doGet(request,respnse);
		}
	}
	
```

#### 初始化参数及访问应用上下文

```
	
	初始化参数 //只能被该Servlet访问
	
	定义Servlet的初始化参数时 使用<init-param>元素
	<init-param>元素是<servlet>元素的子元素 它包含<param-name>元素定义初始化参数的元素和<param-value>元素
	<param-name>元素定义初始化参数的名字 <param-value>指定初始化参数的值
	
	//初始化参数在Servlet的初始化环节被加载 可通过ServletConfig实例的getInitParameter(String name)方法进行访问  
	String initParam = getInitParameter(String name);//通过GenericServlet定义的getInitParameter(String name)方法获取初始化参数  较为简洁
	getServletConfig().getInitParameter(String name) //完整写法
	
```

```
	
	上下文参数访问
	
	<web-app>
		<context-param>
			<param-name>上下文参数名称</param-name>
			<param-value>上下文参数值</param-value>
		</context-param>
	</web-app>
	
	<context-param>元素声明Web应用的全局范围参数 包括<param-name>和<param-value>元素
	<param-name>指定上下文参数名称 <param-value>指定上下文参数的值
	
	//上下文 参数可以通过ServletContext对象的getInitParameter(String name)方法获取
	String contextParam = this.getServletContext().getInitParameter("上下文参数名称");
	
```

## 一些实现处理

### 实现将用户填写过的信息保留在注册页面中(用户填写信息处理错误)并且返回错误信息

```
	
	例
	 --判断验证页面--
	 //判断出 用户输入 出现失误后 记录出错信息 
	 <%
	 	String errMsg = "";//错误提示信息
	 	if(出错条件1){
	 		errMsg = "对应返回提示信息";
	 		request.setAttribute("errMsg",errMsg); //利用request保存错误信息
	 		request.getRequestDispatcher("输入信息页面").forward(request, response);
	 	}else if(出错条件2){
	 		errMsg = "对应返回提示信息";
	 		request.setAttribute("errMsg",errMsg); //利用request保存错误信息
	 		request.getRequestDispatcher("输入信息页面").forward(request, response);
	 	}.......
	 	//成功跳转到某个页面......
	 	//如果需要提示成功信息 可以利用
	 	out.println("<script>alert('您已成功操作');location.href='成功后跳转的页面URL;'</script>")
	 %>
	 

	 --输入信息页面--
	 <h1 style="color=red;"><!--错误信息显示框 -->
	 	<%= request.getAttribute("errMsg")==null? "": request.getAttribute("errMsg")  %>
	 </h1>
	 <input type="text" name="userName" id="userName" value='<%= request.getParameter("userName") == null ? "":request.getParameter("userName") %>'><!-- 如果错误过一次就会有requset对象值 返回信息 如果第一次进就为null -->
	 .......//其它代码	 
	 
```

### 使用过滤器处理中文乱码

```
	
	详细参考 
	
	https://blog.csdn.net/fukua2017/article/details/80724783
	
	在web.xml中配置过滤器信息
	
        <web-app>
          <filter>
              <filter-name>EncodeFilter</filter-name>
              <filter-class>cn.jbit.demo.web.EncodeFilter</filter-class>
              <init-param>
                <param-name>encode</param-name>
                <param-value>UTF-8</param-value>
              </init-param>	  
          </filter>
          <filter-mapping>
              <filter-name>EncodeFilter</filter-name> 
              <url-pattern>/*</url-pattern>  	   	  
          </filter-mapping>
        </web-app>


	编写自定义类EncodeFilter
	
	public class EncodeFilter implements Filter {
	private String encode = null;
	public void destroy() {	encode = null;    }
	// 对所有页面设置字符集编码
	public void doFilter(ServletRequest request, ServletResponse  response, FilterChain chain) throws Exception {
		if (null == request.getCharacterEncoding()) {
			request.setCharacterEncoding(encode);
		}
		chain.doFilter(request, response);
	}
	public void init(FilterConfig filterConfig) throws ServletException {
		String encode = filterConfig.getInitParameter("encode");
		if (this.encode == null) {
			this.encode = encode; // 查找配置文件中欲设的字符集编码
		}
	}
}

```

## 啊这无处安放的技术(好像可以放到Java中 暂时搁着吧)

```
	
	public ResultSet executeQueryOnly(String prepareSql, Object... params){
        
    }
	//Object... params 可变长参数 
	//在调用此方法时 此形参位置可以传入若干个实参 在此方法中 params当做数组使用
	//!!!注意一个方法中只能有一个这样的形参(可变长参数) 且只能放在参数列表的最后
	
	-------------------------------------------------------------------------
		
	为了分离页面中的HTML代码和Java代码 解决在维护和修改上的困难 我们将一些负责完成业务逻辑 数据显示等操作的代码通过一些类来封装 这样只需几行代码调用类中的方法 就可以实现所需的功能 能够提升代码复用 还能使数据显示 和 业务逻辑分开 这就是JavaBean的实质
		
	JavaBean 是Java中可跨平台重用的组件 通常用于封装做业务逻辑、数据操作(业务处理JavaBean和 数据处理JavaBean) 本质上就是一个Java类 只是要遵循一定编码约定的Java类 
	1.是一个public修饰的共有类 
	2.所有属性由private修饰 
	3.通过public修饰的setter/getter方法访问属性 
	4.提供public修饰的无参构造方法
	封装数据的JavaBean通常对应 着数据库中的一张数据表(或视图),JavaBean的属性与表(视图)中的字段一一对应 一个封装数据的 JavaBean 通常会有一个封装业务处理的JavaBean与之对应
	
	-------------------------------------------------------------------------
	
	Sun推荐的属性命名规则为xxx的属性对应setXxx()方法
	一般情况下 Java的属性变量都以小写字母开始 如name,count等 但也存在 特殊的情况(一些特定意义的大写英文缩略词XML、URL等) JavaBean 也允许使用大写字母开头的属性变量名 但是必须满足"变量的前两个字母要么全部大写 要么全部小写的要求" 符合要求的(IDcode、ID)这样的属性变量名是合法的 而(iDCode、iD)是非法变量名  在有些情况下 非法的变量名再以属性名 第一个字母大写的方式命名getter/setter方法 会导致找不到属性错误
	解决方法如下
	 如果属性名的第二个字母大写 那么该属性名直接用作getter/setter方法中 get/set后部分 大小写不变(属性名uName > getuName/setuName)
	 如果前两个字母大写 属性名直接用作getter/setter方法 get/set后部分 (属性名URL > getURL/setURL)
	 如果首字母大写 则属性名直接用作getter/setter方法 get/set后部分(属性名Name 方法getName/setName 这是最不符合规范的情况 很容易发生错误 因为通过getter/setter方法得到的默认属性名是name)
		
```

























