```
	2019年3月4日16:25:56创建
```

# 目录

[TOC]

# Debug

## 报错首则-绝对不相信自己任何一个地方写对了,再对也要检查(死磕定律)

```
	
	遵循 ！！！！！ 编码规范 编码格式
	失败 + ∞*坚持 = 成功
	
	
	
	待处理
	会不会有jdk和jre指定错误的问题
	
```

```
	
	//基础模板
	
	问题:
		
		
	
	分析:
		
		
	
	解决:
		
		
		
		参考: 
	
```

## Maven

```
	
	问题:
		
		无法下载Maven库 报一些插件错误 
	
	分析:
		
		下载jar包失败 重新定义镜像地址
	
	解决:
		
		方法一、修改或添加maven镜像库 镜像库优先百度
		
            <!-- 阿里云仓库1 -->
            <mirror> 
                <id>alimaven</id> 
                <name>aliyun maven</name> 
                <url>http://central.maven.org/maven2</url> 
                <mirrorOf>central</mirrorOf> 
            </mirror>

            <!-- 阿里云仓库2 -->
            <mirror>
                <id>alimaven</id>
                <mirrorOf>central</mirrorOf>
                <name>aliyun maven</name>
                <url>http://maven.aliyun.com/nexus/content/repositories/central/</url>
            </mirror>

            <!-- maven官方镜像 -->
            <mirror>
                <id>mirrorId</id>
                <mirrorOf>central</mirrorOf>
                <name>Human Readable Name </name>
                <url>http://repo1.maven.org/maven2/</url>
            </mirror>

	
		方法二、 直接访问下载失败的地址 手动下载放入对应文件夹 或者 拷贝其它类库 (不推荐)
		
		参考: 
	
```

## SSM框架

```
	
	问题:
		
		org.springframework.web.util.NestedServletException: Handler processing failed; nested exception is java.lang.NoSuchMethodError: xx.xx.xx.xx.xxxHandler(Ljava/lang/Integer;)Ljava/lang/Object;
	
	分析:
		
		这个问题出现在Ajax请求处理器上 原因是返回的类型指定成了 基本类型 或者 包装类 而返回类型是JSON
	
	解决:
		
		将该处理器的返回值类型改为Object
		
		参考: 
	
```

```
	
	问题: 
		
		IOException parsing XML document from ServletContext resource [/WEB-INF/applicationContext.xml]初始化错误
		
		
	分析:
		
		监听器没有指定配置Spring配置文件
	
	解决:
		
		在监听器同级 添加指定Spring配置文件路径
		<context-param>
       		 <param-name>contextConfigLocation</param-name>
       		 <param-value>classpath:applicationContext.xml</param-value>
    	</context-param>
    	
		参考: https://blog.csdn.net/baidu_19473529/article/details/82904301
		
```

```

	问题:
		
		使用SpringMVC配置静态文件引用之后 图片 层叠样式表 js文件还是不能正常加载
	
	分析:
		
		可能是SpringMVC配置错误
	
	解决:
		
		确认SpringMVC配置文件是否成功加载(检查配置文件配置错误)
		
		参考: 
	
```

```

	问题:
		
		配置静态文件引用 出现/statics 变红
	
	分析:
		
		可能是因为没有正常配置 Web Resource Directory
	
	解决:
		
		尝试在项目配置中Web配置块重 检查Web Resource Directory是否指定错误 进行修复
		
		参考: 
	
```

```
	
	问题:
		
		org.springframework.core.convert.ConversionFailedException: Failed to convert from type [java.util.ArrayList<?>] to type [java.util.List<org.springframework.core.io.Resource>] for value '[/js/]'; nested exception is org.springframework.core.convert.ConverterNotFoundException: No converter found capable of converting from type [java.util.ArrayList<?>] to type [org.springframework.core.io.Resource]
	
	分析:
		
		加载静态资源和日期统一转换冲突
	
	解决:
		
		将加载静态资源注释掉,换为这个<mvc:default-servlet-handler />
		
		参考: 
	
```


	问题:
		
		org.springframework.beans.factory.BeanCreationException: Error creating bean with name '创建的接口实现类名' defined in file [某个类的绝对路径.class]: Initialization of bean failed; nested exception is org.springframework.beans.TypeMismatchException: Failed to convert property value of type 'java.lang.String' to required type 'java.lang.Class' for property 'mapperInterface'; nested exception is java.lang.IllegalArgumentException: Cannot find class [某个类的全限定包]
	
	分析:
		
		原因 是 包名 在之前被改动了 之后 idea没有及时编译 找不到真的文件包地址 导致错误
	
	解决:
		
		删掉classes包文件 让idea进行重新编译
		
		参考: 


## MyBatis框架

```
	
	问题:
		
		单元测试出现问题java.lang.NoClassDefFoundError: Could not initialize class xxx包xxx类
	
	分析:
		
		这个问题大几率是因为 SQL语句映射文件 出错 #{//此处为空}|加了其它字符影响结构
	
	解决:
		
		如果映射文件过多 则根据取半方法(注释) 一半Mappers 下的Mapper 找到问题映射 进行规范性排除
		
		参考: 
	
```

## Mysql

```
	
	问题0: //也可能是问题1的问题
	
		字段类型 为char 不能插入数据
	
	解决:
	
		设置(数据库 数据表 字段)编码字符集为utf8mb4 可以正常插入
		在my.ini 文件设置mysql的文件字符集为utf8mb4
	
```

```
	
	问题1:
	
		当在DOS窗口显示MySQL数据库内容 中的信息时 中文内容可能会出现乱码 这是因为DOS窗口默认字符集为GBK格式 如果当前MySQL设置的默认编码格式为非GBK格式 则可能会产生乱码
	
	
	解决:
	
		出现这种情况时 可以在输出信息之前 执行以下语句
            SET NAMES gbk;
            这句话等同于执行了以下三条语句
            SET character_set_client=gbk;
            SET character_set_results=gbk;
            SET character_set_connection=gbk;
            
 		 //但是在此命令是临时的 在MySQL重新启动之后就会恢复默认设置(详细设置上网查阅资料)
	
```

```
	
	在创建字段时 给一个字段 主键约束 非空约束 ZEROFILL属性 将会报错  可能是 设置NOT NULL 属性重复//待考究
	
```

## Spring框架

```
	
	问题:
		
		在Spring框架 进行声明式事务管理的时候报错 Caused by: java.lang.IllegalArgumentException: warning no match for this type name: com.xxx.xxx.service [Xlint:invalidAbsoluteTypeName]
	
	分析:
		
		原因是切面表达式错误
	
	解决:
		
		检查切面表达式 方法或者包名 有没有写错 进行校正
		
		参考: https://blog.csdn.net/w605283073/article/details/82999927
	
```

## HTML5和CSS3

```
	
	问题:
		
		父边框塌陷 导致后面位置崩塌
	
	分析:
		
		实现"一行多列"布局,推荐使用float方式,并解决"父边框塌陷"问题(另外一个display:inline-block方式不推荐使用)
	
	解决:
		
		改为用float属性 多用float 少用或不用 display
		
		参考: 
	
```

```
	
	问题:
		
		有时无法加载jpg图片  图片格局就会崩掉 改变大小 布局混乱
	
	分析:
		
		图片没有起到大小的作用导致偏移
	
	解决:
		
		在img外面增加一层div 让div保持img高度达到 替代图片大小的作用
		
		参考: 
	
```

## JSP/Servlet

```
	
	问题:
		
		alert不出现内容
	
	分析:
		
		一、注意javscript中的代码 \n换行 要写成\\n 要不会导致显示内容消失 或 错误
		二、导入代码时 <script>属性设置错误
	
	解决:
		
		修复以上问题
		
		参考: 
	
```

```
	
	问题:
		
		空页面问题 
	
	分析:
		
		一、注意out.print("<script></script>");	 //要正确 写入javascript代码 闭合标签否则会导致页面为空
		二、页面地址错误 路径问题 提交页面(具体页面 问题) 页面地址问题(注意项目下地址)  可将鼠标移动到超链接 文字 查看跳转地址 进行判断
		三、出现其它问题 可以让Tomcat进入运行调试模式 之后放开Tomcat 调试处理(单步调试F8 一步调试等) 进行调试
		四、通过alert()方法将不确定的数据 以信息框的方式展示
		
	解决:
		
		修复以上问题
		
		参考: 
	
```

```
	
	问题:
		
		页面出现中文乱码
	
	分析:
		
		一、可能因为form表单提交方式为post 没有进行转码操作 或 将设置编码操作设置到 获取内容之后 造成情形(先获取数据 后 更改编码的状况 导致中文乱码)
		二、idea没有进行编码设置 项目编码为默认编码 导致弹框中文乱码 检查项目使用编码字符集、页面设置字符集是否一致
	
	解决:
		
	   将设置编码操作提前
        或尝试添加以下几条编码操作
        response.setCharacterEncoding("UTF-8");
        response.setContentType("text/html;charset=UTF-8");
        request.setCharacterEncoding("UTF-8");
		
		尝试File > Settings > Editor > Encoding > 设置编码为UTF-8
		 
		参考: 
	
```

```
	
	问题:
		
		Servlet页面跳转到JSP页面 样式等无法正常显示
	
	分析:
		
		在servlet中转发时css和图片的路径变成相对于这个servlet的相对路径而非相对于web项目的路径了
	
	解决:
		
		<link rel="stylesheet" href="${pageContext.request.contextPath }/css/main.css" type="text/css" />
		
		参考: https://www.cnblogs.com/zshibo/p/8011491.html 
	
```

## Idea

```
	
	问题:
		
		问题未知  写入文件错误啥的
	
	分析:
		
		有报错可能和文件没有写入权限 有关
	
	解决:
		
		暂无 科学重启
		
		参考: 
	
```

```
	
	问题:
		
		单元测试时 需要通过传统方式获取数据库连接 不能通过数据源方式获取   
	
	分析:
		
		因为数据源配置在Tomcat环境中 不能为测试环境所用
	
	解决:
		
		在控制台上显示数据 要使用JDBC连接数据库 或者 不用单元测试
		
		参考: 
	
```

```
	
	问题:
		
		idea不进行 编译
	
	分析:
		
		可能错误 JSP中导入类 地址错误
	
	解决:
		
		ctrl + F9 进行IDEA编译
		重新导入jar包
		清除idea缓存等
		直接删掉classes文件夹 让它重新读取编译整个文件(优先检查代码)
		
		参考: 
	
```

```
	
	问题:
		
		编译Java程序出现 Error:java: 无效的源发行版 
	
	分析:
		
		jdk指定的 版本错误 将其调成正确的就好
	
	解决:
		
		调整idea指定jdk版本
		
		参考: https://www.cnblogs.com/dongling/p/8670852.html
	
```

## JavaScript

```
	
	问题:
		
		无法使用表单的onsumbit onreset事件
	
	分析:
		
		猪蠢 form表单 form表单 你写 button input 干屁
	
	解决:
		
		把事件从 button inout 移动到 form 表单上面去 
		
		参考:
	
```

## IDEA集成Tomcat

```
	
	问题:
		
		Tomcat控制台中文乱码问题
	
	分析:
		
		
	
	解决:
		
		打开"运行/调试配置"中"编辑配置..."
		在Server选项卡"虚拟机选项"中添加以下参数: -Dfile.encoding=UTF-8
		
		参考: 
	
```

```
	
	问题:
		
		[localhost-startStop-1] org.apache.tomcat.dbcp.dbcp2.BasicDataSourceFactory.getObjectInstance Name = news Property maxWait is not used in DBCP2 , use maxWaitMillis instead. maxWaitMillis default value is -1. You have set value of "10000" for "maxWait" property, which is being ignored.
	
	分析:
		
		连接池设置问题 原因 高版本tomcat内置的DBCP2和老版本的连接池不一样 7.0等老版本用的是DBCP 一些设置不一样所以出现这个问题
	
	解决:
		
		将maxWait 换为 maxWaitMillis 重启Tomcat 解决问题
		
		参考: https://blog.csdn.net/vr_jia/article/details/74530389
	
```

```
	
	问题:
		
		[localhost-startStop-1] org.apache.tomcat.dbcp.dbcp2.BasicDataSourceFactory.getObjectInstance Name = news Property maxActive is not used in DBCP2, use maxTotal instead. maxTotal default value is 8. You have set value of "100" for "maxActive" property, which is being ignored.
	
	分析:
		
		连接池设置问题 原因 高版本tomcat内置的DBCP2和老版本的连接池不一样 7.0等老版本用的是DBCP 一些设置不一样所以出现这个问题
	
	解决:
		
		maxActive 换为 maxTotal 重启Tomcat 解决问题
		
		参考: https://blog.csdn.net/vr_jia/article/details/74530389
	
```

```
	
	问题:
		
		警告 [RMI TCP Connection(4)-127.0.0.1] org.apache.tomcat.util.descriptor.web.WebXml.setVersion Unknown version string [4.0]. Default version will be used.
	
	分析:
		
		 当前Tomcat8.5不支持Web4.0版本
	
	解决:
		
		要么降低Web版本,要么提高Tomcat版本
		
		//降低Web版本
		在项目文件中的web.xml
   		 <web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
   		      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
   		      xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
   		      http://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd"
   		      version="3.1"><!--将web版本4.0修改为3.1，注意上一行约束文件也要修改-->
    	</web-app>
    
		参考: https://blog.csdn.net/qq_32483145/article/details/80292463
	
```

## @include导入外部代码

```
	
	问题:
		
		使用include出现乱码乱字符号
	
	分析:
		
		HTML和被include引入的HTML文件的编码不统一造成
	
	解决:
		
		给导入代码的页面 或者 include导入的HTML文件 添加pageEncoding="UTF-8"  设置和导入页面相同编码
		
		参考: http://www.divcss5.com/html/h764.shtml 
	
```

## 字符串对比错误

```
	
	问题:
		
		魔法错误 true == true  等于false
	
	分析:
		
		实例问题 ajax 问题 在进行javascript == “true” 对比字符串的时候 可能遇到 值相同但是 结果返回false 问题可能是 那个字符串加了空格
	
	解决:
		
		加了空格  ！！！！！ 管它谁加的直接trim()
		
		参考: 
	
```

## jQuery

```
	
	问题:
		
		出现操作不了值的情况 而且你傻不拉几的 用了innerHtml()
	
	分析:
		
		你属性用错了 javaScript 和 jQuery 别混行吗！！
	
	解决:
		
		注意html()方法和val()方法你 不要 用错!!! 不要用错!!!!!!  不要用错!!!!!!!
		
		参考: 
	
```

```
	
	问题:
		
		jQuery对比值时不正确
	
	分析:
		
		jQuery 可能不支持 区间判断 例如   1 < 被判断值 < 2
	
	解决:
		
		换成  1 < 被判断值 && 被判断值 < 2
		
		参考: 
	
```

## 重装问题

```
	
	问题:
		
		装机时 安装不了驱动
	
	分析:
	
		
	
	解决:
		
		进入设备管理器 安装基本驱动程序  更新驱动程序  
		浏览我的计算机	 以查找驱动程序软件 让我从计算机上的可用驱动程序列表中选取 卸载本机的微软驱动
		
		参考: 
	
```

## C

```
	
	//基础模板
	
	问题:
		
		语法错误 缺少; 在类型的前面
	
	分析:
		
		
	
	解决:
		
		C 语言语法规定 变量要定义在 当前代码块 的最前面
		
		参考: 
	
```

```
	
	//基础模板
	
	问题:
		
		warning C4996 scanf ... may be unsafe
		scanf 可能是不安全的 建议使用scanf_s
	
	分析:
		
		scanf c 语言提供的
		scanf_s 是VS编译器提供的 //不建议使用 整个更正 只有VS可以识别 无可移植性
	
	解决:
		
		代码导入部分 #pragma warning(disable:4996)
		或 #define _CRT_SECURE_NO_WARNINGS 1 //加源文件的第一行
		屏蔽警告
		
		//通过 VS2022\Common7\IDE\VC\VCProjectItems
将 #define _CRT_SECURE_NO_WARNINGS 1 添加到默认代码块 newc++file.cpp
		
		
		参考: 
	
```

```
	
	//基础模板
	
	问题:
		
		输出 莫名其妙的d 字符等等
	
	分析:
		
		
	
	解决:
		
		printf("d",2) 函数%d 少写了%
		printf("%d",2)
		
		参考: 
	
```

## GitHub

```
	
	//基础模板
	
	问题:
		
		vs2022 连接 github 连接不上
		浏览器 DNS_PROBE_FINISHED_NXDOMAIN
	
	分析:
		
		
	
	解决:
		
		使用steamcommunity 302 成功进入
		
		参考: 
	
```

```
	
	//基础模板
	
	问题:
		
		vs2022 推送到github上 一直没有成功
	
	分析:
		
		这个真的是 犯得sb错误 硬是没有找到问题 但其实根本没有问题 就是自己不注意 消息队列一直是空的 没填导致无法上传 一直没发现还在找bug
	
	解决:
		
		填 消息队列的东西 上传什么得写吧? 
		
		参考: 
	
```



## 其它不分类问题

```
	
	问题:
		
		u盘不能正确导入 有图标不是u盘本身问题
	
	分析:
	
		
	
	解决:
		
		进入设置下的 设备 在蓝牙和其他设备中删除不能正常显示的u的名字 重新插入u盘
		
		参考: 
	
```

```
	
	问题:
		
		安装notepad++软件导致lol不能开启 注意安装的版本 可能和软件支持的计算机位数有关 32位 64位
	
	分析:
	
		程序安装成32位了 安装成64位
	
	解决:
		
		重新安装notepad++ 注重版本
		
		参考: 
	
```

```
	
	问题:
		
		DesktopMgr64.exe 损坏的映像
		InkImgExio64.dll 没有被指定在Windows 上运行 或者它包含错误 请尝试使用原始安装介质重新安装程序 错误状态0xc000012f
	
	分析:
		
		软件安装的dll 在更新系统时可能不会被自动注册
	
	解决:
		
		卸载有关桌面美化的东西 有需要重装即可
		
		参考: https://www.zhihu.com/question/60209458
	
```

