```
	2019年10月10日08:30:27创建
```

# 目录

[TOC]

# JSTL EL Ajax JSON

## EL表达式

### 为什么需要EL表达式

```
	
	在JSP中嵌入Java代码容易导致结构复杂 降低程序可读性 不利于维护
	访问结构比较复杂的数据时代码烦琐，且经常需要强制类型转换
	
	使用EL表达式可以简化开发
	
```

### 什么是EL表达式

```
	
	EL表达式的全称Expression Language 它是一种借鉴了JavaScript和Xpth的表达式语言 
	它定义了一系列的隐含对象和操作符 使开发人员能够很方便地访问页面的上下文 以及不同作用域内的对象
	//提供了在Java代码之外 访问和处理应用程序数据的功能 通常用于在某个作用域(pgae,request,session,application等)内取得属性值 或做简单的运算和判断
	//自动转换类型 使用EL得到某个数据时可以自动转换类型 类型限制宽松
	//使用简单 和JSP页面嵌套Java代码相比 EL表达式使用简单
	//但是不能实现逻辑控制
	
```

### EL的语法

```
	
	EL是JSP 2.0增加的技术规范 不需要导入
	
	${EL 表达式}    通过变量名取值 获取对象的属性值 获取集合元素 执行表达式
	主要有两个要素 $ 和 {} 缺一不可
	
	EL表达式通常由两部分组成 对象和属性
	//可以用.操作符访问对象的某个属性 ${对象.属性} 例 user对象的name属性  ${user.name} 也可调用getter/setter方法${user.getName()} 可以调用对象内的方法  
	//想要通过EL表达式获取对象属性的值，那么这个属性就必须有与之对应的get方法 没有经过准确验证 可以参考https://blog.csdn.net/hjc132/article/details/78288355
	//与点操作符类似 [] 操作符也可以访问对象的某个属性 ${user["name"]} ""必须引起来否则无作用 ''也可以 不能调用getter/setter方法 原因是因为去掉""双引号的会被当做变量处理
	//注意指定变量作用域的时候 一定要确定 否则可能会出现变量串位 使用变量时一定要指定变量作用域Scope
	//[]还提供了其他功能 
		当属性名中包含了特殊字符如"." 或 "-"等的情况下(常量) 点操作符不能用 只能用[]操作符
		[]可以使用变量实现动态访问 ${user[propertyName]} propertyName为另一个变量 改变其值可以动态访问user的不同属性
		访问数组 如果有一个对象名为array的数组(集合也行) 可以根据索引下标访问元素 ${array[0]} 注意!!!集合类型Map取值是靠key 而其它例如List集合可以根据下标取值 而且Map取值的时候还可能遇到key为数字 在EL表达式中${xx[1]}和${xx["1"]}、${xx['1']} 都能取到值 但是${xx.1}这样不行(编写错误) 而且在存入map集合中的元素的时候 key键 如果使用纯数值格式key 只能使用长整数型(Long)(注意写L确定下以后好辨别)其它整数类型取不出来值 所以建议Map集合使用String做key
	//注意!!!List集合 add()方法会有返回值true 
		
```

### 执行表达式

```
	
	EL表达式中 
	有六个关系操作符  三个逻辑操作符 Empty操作符 
	
	Empty是一个前缀操作符 用于检测一个变量是否为null或者为empty(如长度为0的字符串变量或集合变量)
	//例${empty a(不存在变量)} 结果为true   //${! empty a} 结果为false
	
```

| 关系操作符 |   说明   |            示例             | 结果  |
| :--------: | :------: | :-------------------------: | :---: |
|   ==/eq    |   等于   | ${23 == 5} 或 ${“a” == “b”} | false |
|   !=/ne    |  不等于  |         ${23 != 5}          | true  |
|    </lt    |   小于   |          ${23 < 5}          | false |
|    >/gt    |   大于   |          ${23 > 5}          | true  |
|   <=/le    | 小于等于 |         ${23 <= 5}          | false |
|   >=/ge    | 大于等于 |         ${23 >= 5}          | true  |

| 逻辑操作符 |  说明  |          示例          | 结果 |
| :--------: | :----: | :--------------------: | :--: |
|   &&/and   | 逻辑与 | ${A(true) && B(true)}  | true |
|  \|\|/or   | 逻辑或 | ${A(true) && B(false)} | true |
|   !/not    | 逻辑非 |      ${!A(false)}      | true |

### EL隐式对象

```
	
	EL提供了一系列可直接使用的隐式对象(无需声明) 按照途径可以分为 
	
	作用域访问对象 	//为了访问四个作用域内的变量和属性
		
		pageScope	//与page作用域相关联的Map对象
        requestScope	//与request作用域相关联的Map对象
        sessionScope	//与session作用域相关联的Map对象
        applicationScope	//与application(应用程序)作用域相关联的Map对象
        
        //当EL表达式访问某个变量时 
         指定查找的范围	${作用域Scope.变量名} //只在改变作用域下查找变量
         不指定查找范围	${变量名}	//会按照page > request > session > application 依次查找 找到即返回 找不到则返回null
		
	参数访问对象	//与页面输入参数有关的隐式对象 可以根据它获得用户的请求参数(from表单)
    	
    	param	//按照请求参数名称返回单一值的Map对象 ${param.xx} 等同于 request.getParameter("xx");
        paramValues	//按照请求参数名称返回String数组的Map对象(例多选按钮) ${paramValues.xx} 等同于 request.getparamValues("xx"); //${paramValues.xx}可以获取所有结果并遍历显示所有值
      
    JSP隐式对象	//它是JSP和EL的一个公共对象 通过pageContext可以访问其它八个JSP内置对象(request.response等)这也是EL表达式把它作为内置对象的主要原因
		
		pageContext //提供对页面信息和JSP内置对象的访问 如${pageContext.request.contextPath} 等价于<%=request.getContextPath()%>  也就是取出部署的应用程序名或者是当前的项目名称 可以用此实现动态绝对路径获取
	
```

## JSTL 标签库

### 为什么需要JSTL标签库

```
	
	EL表达式只能做到简化JSP编码 但不能进行逻辑判断和循环控制
	
	EL表达式封装了数据访问的功能 而 JSTL标签库封装了逻辑控制、循环控制、以及数据格式化等功能
	二者集合使用才能完整实现动态页面开发需求
	
```

### 什么是JSTL标签

```
	
	JSTL全称 Java Server Pages Standard Tag Library JSP标准标签库 包含了开发JSP页面时常用到的标准标签
	//可以不用嵌入Java代码就可以开发复杂的JSP页面的途径
	//可以编写各种动态功能
	
```

### 如何使用JSTL标签库

```
	
	引入JSTL的jar文件和标签库描述符文件  
	    //详细 https://blog.csdn.net/qq_32115439/article/details/54685786
		一般使用JSTL1.1以上版本,现在最新版是JSTL1.2.5
		在Apache Tomcat官网下载JSTL标签库(Taglibs)
		下载地址: http://tomcat.apache.org/download-taglibs.cgi
		
		下载页面有4个jar包:
    		Impl:   taglibs-standard-impl-1.2.5.jar    JSTL实现类库
    		Spec:   taglibs-standard-spec-1.2.5.jar    JSTL标准接口
    		EL:     taglibs-standard-jstlel-1.2.5.jar  JSTL1.0标签-EL相关
    		Compat: taglibs-standard-compat-1.2.5.jar  兼容版本

		从README得知: 
        	如果不使用JSTL1.0标签,可以忽略taglibs-standard-jstlel包,
        	README没有介绍taglibs-standard-compat包,估计应该是兼容以前版本标签库,
        	所以一般只需要 taglibs-standard-impl 和 taglibs-standard-spec 两个jar包
	
	在JSP页面添加taglib指令

        core 核心标签库 
        fmt  国际化标签 
        sql  数据库标签(废弃) 
        xml  XML标签(废弃)

		在JSP中引入 core fmt 标签库 
   			<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%>
    		<%@ taglib uri="http://java.sun.com/jsp/jstl/fmt" prefix="f"%>
			taglib通过uri属性引用 某个标签库的配置文件 JSP页面通过prefix属性指定的前缀就可以访问 相关标签库的标签功能
    
```

### JSTL标准(核心)标签库

```
	
	JSTL标准标签库
				
	核心标签库 //标签共13个，从功能上可以分为4类：表达式控制标签、流程控制标签、循环标签、URL操作标签
				
	通用标签(表达式控制标签)	条件标签(流程控制标签)	迭代标签(循环标签)	URL操作标签
	
	set						if					  forEach			import
	out						choose				  forTokens			 url
	remove					when									redirect
	catch					otherwise
	
```

#### 通用标签(在JSP设置、显示、删除变量)

```
	
	<c:set>	<c:out>	<c:remove>
	
    <c:set> 设置指定范围内的变量值或属性 主要用于将变量存取于JSP范围中或JavaBean属性中
    	<c:set var="varible" value="value" scope="scope"/>
    	将value值存储到范围为scope的变量variable
    	scope属性对应变量作用域 可选值有page、request、session、application
    	//<c:set var="varible" scope="scope"/>把一个变量名为varible的变量存储在指定的scope范围内
    	
    	<c:set value="value" target="target" property="property" />
    	//<c:set target="target" property="property">value<c:set/> 可以达到同样效果
    	将value值设置到对象的属性中 相当于setter方法
    	target属性是操作的JavaBean对象 可以使用EL表达式来表示
    	property属性对应JavaBean对象的属性名
    	value属性时赋予JavaBean对象属性的值
    
    <c:out> 用于将计算的表达式结果输出显示 类似JSP中的<%= %> 但是功能更加强大 代码也更加简洁 方便页面维护 其语法格式分为指定默认值 和 不指定默认值两种形式
    	不指定默认值
    		<c:out value="value" />
    		value属性指 需要输出的表达式的运算结果 可以通过EL表达式获取
    	指定默认值
    		<c:out value="value" default="default"/>
    		default属性时value属性的值为空时输出的默认值
    	另外还有一个escapeXml属性 表示是否转换特殊字符 在输出诸如<、>、'、"、&在HTML和XML中具有特殊意义的字符时是否应该进行转义 true自动进行转义(默认值)
    	
    <c:remove> 用于移除指定作用域的指定变量 与<c:set>作用相反
    	var属性是待移除的变量的名称
    	scope属性是指移除的变量所在的范围 可选值有page、request、session、application 如果没有指定默认为page
    	
    <c:catch> 用于捕获异常
      <c:catch var="e"><%= 1/0 %></c:catch>   
      <p>${e.message}</p> //显示错误信息 算数异常
    
```

#### 条件标签(逻辑处理)

```
	
	<c:if> <c:choose> <c:when> <c:otherwise>
	
	<c:if> 实现Java中if语句的功能
		<c:if test="condition" var="varName" scope="scope">//省略主体内容</c:if>
		test属性是判断条件 condition可以用EL表达式表示 true执行内容 false不执行
		var属性定义变量 该变量存放判断的结果 该属性可以忽略
		scope值var定义变量的储存范围 可选值有page、request、session、application 可以忽略
	
	<c:choose> <c:when> <c:otherwise> 一起实现互斥条件的执行 类似于Java语言的if-else 语句 运行情况也和if-else语言一致
		<c:choose>是作为<c:when>和<c:otherwise>的父标签使用的 除了空白字符外,<c:choose>只能包含这两个标签
		<c:when>标签必须有个直接父类标签<c:choose> 而且必须在同一个父标签下的<c:otherwise>之前 可以有多个<c:when>标签
		<c:otherwise>必须有<c:choose>父标签 且必须是最后一个标签	
		//代码结构更加清晰 更利于维护和管理
		
		例
		<c:choose>
            <c:when test="${day == 1}">
                星期一
            </c:when>
            <c:when test="${day == 2}">
                星期二
            </c:when>
            <c:otherwise>
                休息日
            </c:otherwise>
   	    </c:choose>
	
```

#### 迭代标签库

```
	
	<c:forEach> <c:forTokens>
	
	<c:forEach></c:forEach> 实现对集合对象的遍历 实现循环语句
		遍历集合对象的成员
		<c:forEach var="varName" items="collectionName" varStatus="varStatusName" begin="beginIndex" end="endIndex" step="step">
			//省略主体内容
		</c:forEach>
		var属性是对当前成员的引用 如果当前循环到第一个成员 var就引用第一个成员 如果循环到第二个就是第一个成员类推  
		items指被迭代的集合对象
		varStatus属性用于存放var引用的成员的相关信息 如索引等 (.index 索引位置)(.count 是第几个)
		begin属性表示开始位置 默认为0 该属性可以省略
		end属性表示结束位置 该属性可以省略
		step表示循环的步长 默认为1 该属性可以忽略
		例
		<c:forEach items="userList" var="user" varStatus="status"><p>${user.name}</p></c:forEach>
		通过迭代标签遍历Map
		<c:forEach iems="map" var="entry">${entry.key}${entry.value}</c:forEach>
		
		指定语句的执行(迭代)次数
		 <c:forEach var="varName" varStatus="varStatusName" begin="start" end="end" step="step"></c:forEach>
		 var属性是对当前成员的引用 如果当前循环到第一个成员 var就引用第一个成员 如果循环到第二个就是第一个成员类推  
		 varStatus属性用于存放var引用的成员的相关信息 如索引等 (.index 索引位置)(.count 是第几个)(.first 第一个元素)(.last 最后一个元素)
		 begin属性表示开始位置 默认为0 该属性可以省略
		 end属性表示结束位置 该属性可以省略
		 step表示循环的步长 默认为1 该属性可以忽略
		 例
		 <c:forEach begin="1" end="5" step="2">
		 		<c:out value="*"></c:out> //结果为***
		 </c:forEach>
	
	<c:forTokens>分隔字符串
    <c:forTokens items="sdfa,fsad,fds" delims="," var="result">
        ${result}<br>
    </c:forTokens>
	
```

#### URL操作标签

```
	
	在URL后加参数
    <c:param> 嵌套在<c:import>、<c:url>、<c:redirect>,为这些标签所用URL附加参数
	
	实现include功能
    <c:import url="/index.jsp" var="p" scope="page"></c:import>
    输出: ${p}
    
    URL重写
    <c:url value="/index.jsp" context="${pageContext.request.contextPath}" var="eurl" scope="page"></c:url>
    <a href="${eurl}">xxx</a>
    
    请求重定向
    <c:redirect url="/index.jsp" context="${pageContext.request.contextPath}"></c:redirect>
	
```

### JSTL国际化标签库

```
	
	格式化日期       
    <fmt:formatDate value="<%=new Date()%>" pattern="yyyy/MM/dd hh:mm:ss" var="date" scope="request" />
    ${requestScope.date} //2019/10/14 04:58:45

格式化数字       
    <fmt:formatNumber value="3.1415926" pattern="0000.00000000000" var="num1" scope="request" />
    <fmt:formatNumber value="3.1415926" pattern="####.###########" var="num2" scope="request" />
    ${requestScope.num1}<br> //0003.14159260000
    ${requestScope.num2}<br> //结果好像没变 3.1415926
	
```

## Ajax异步请求

### 为什么需要Ajax

```
	
		无刷新 不刷新整个页面，只刷新局部
        无刷新的好处
            只更新部分页面，有效利用带宽
            提供连续的用户体验
            提供类似C/S的交互效果，操作更方便
	
```

### 什么是Ajax

```
	
	Ajax(Asynchronous JavaScript and XML) 并不是一种全新技术 而是由JavaScript XML CSS等几种现有技术整合而成
	
	
```

### Ajax执行流程

```
	
	用户界面触发事件调用JavaScript 
	通过 Ajax引擎 XMLHttpRequest对象异步发送请求到服务器 
	服务器返回XML JSON 或 HTML等格式的数据
	然后利用返回的数据使用DOM和CSS技术局部更新用户界面
	
	-----------------------------浏览器		    		---------服务器
	         >JavaScript> 			   >HTTP请求>   
	用户界面				Ajax引擎							处理请求
			<DOM+CSS< 				 <XML/JSON/HTML数据<
	
```

### 传统Web开发技术和Ajax技术有什么区别

```
	
	无论使用哪种开发技术 流程都是先由客户端发送HTTP请求 然后有服务器对请求生成响应
	但还是 存在三条差异
	 
	差异1 发送请求方式不同
	传统Web应用通过浏览器发送请求 而Ajax技术则是 通过JavaScript的XMLHTTPRequest对象
	
	差异2 服务器响应不同
	传统Web应用 响应回来的是一个完整的页面  而Ajax技术则是 只响应需要的数据
	
	差异3 客户端处理的响应方式不同
	传统Web应用 浏览器会等待服务器响应完后重新刷新整个页面 而Ajax技术浏览器不再空闲等待请求响应 而是通过JavaScript动态更新页面中需要更新的部分 不对用户其它操作进行影响
	
```

### XMLHttpRequest

```
	
	这个对象可以在不刷新当前页面的情况下 向服务端发送异步请求 并接受服务器端的响应结果 实现无刷新技术
	
	虽然它叫XMLHttpRequest但它也可以接受JSON或HTML等格式的文档数据
	整个Ajax技术的核心
	提供异步发送请求的能力
	
```

#### 创建XMLHttpRequest对象

```
	
	在老版本的IE浏览器(IE5和IE6)中创建XMLHttpRequest对象的方式与较新版本的IE(IE 7及以上)及其他大部分浏览器中的创建方式 是不同的
	
	老版本IE(IE5和IE6)
	XMLHttpRequest = new ActiveXObject("Microsoft.XMLHTTP");
	
	新版本IE和其他大部分刘拉你(推荐使用)
	XMLHttpRequest = new XMLHttpRequest();
	
```

#### XMLHttpRequest常用方法(熟悉常用方法即可)

|                             方法                             |           说明           |
| :----------------------------------------------------------: | :----------------------: |
| open(String method,String url,boolean async,String user,String password) |   创建一个新的HTTP请求   |
|                      send(String data)                       |    发送请求到服务器端    |
|                           abort()                            |       取消当前请求       |
|         setRequestHeader(String header,String value)         | 设置请求的某个HTTP头信息 |
|               getResponseHeader(String header)               | 获取响应的指定HTTP头信息 |
|                    getAllResponseHeader()                    | 获取响应的所有HTTP头信息 |

```
	
	open(String method,String url,boolean async,String user,String password)
	
	method 设置Http请求方法 如POST GET等 对大小写不敏感
	url 请求的URL地址
	async 可选 指定此请求是否为异步方法 默认为true
	user 可选如果服务器需要验证 此处需要指定用户名 否则 会弹出 验证窗口
	password 可选 验证信息中的密码 如果用户名为空 此指将被省略
	
```

```
	
	send(String data)
	
	data 字符串类型 通过此请求发送的数据 此参数值 取决于open方法中的method参数 如果method值为 POST 可以指定该参数 如果method值 为GET 该参数为null
	
```

```
	
	setRequestHeader(String header,String value)
	
	header 要指定的HTTP头名称
	value 要指定的HTTP头名称所对应的值
	
```

#### XMLHttpRequest常用属性

```
	
	事件
		onreadystatechange //指定回调函数
	
	常用属性
		readyState XMLHttpRequest状态信息
			0-未初始化 1-开始发送请求 2-请求发送完成 3-开始读取响应 4-读取响应结果
		
		status 返回当前请求的HTTP状态码
			200-正确返回 404-找不到访问对象
	
		statusText 返回当前请求的响应行状态
		
		responseText 以文本形式获取响应值
		
		responseXml 以XML形式获取响应值 并且解析成DOM对象返回
	
	
```

### (传统方式)

#### 使用Ajax发送GET请求及处理响应

```
	
	使用文本框的onBlur事件 或者其它 事件 根据需求 判断
    使用Ajax技术实现异步交互
        创建XMLHttpRequest对象
        通过XMLHttpRequest对象设置请求信息
        向服务器发送请求
        创建回调函数，根据响应状态动态更新页面
        编写服务器端处理客户端请求
	
```

```
	
	//1.创建XMLHttpRequest对象
	if(window.XMLHttpRequest){ //返回值为true时说明是新版本IE或其他浏览器
		xmlHttpRequest = new XMLHttpRequest();
	}else{ //返回值为false时说明是老版本IE浏览器(IE 5 和 IE 6)
		xmlHtppRequest = new ActiveXObject("Mincrosoft.XMLHTTP");
	}
	
	//2.设置回调函数 
	//监听服务器的响应状态并作出相应处理
	xmlHttpRequest.onreadystatechange = callBack;
	
	//3.初始化XMLHttpRequest组件
	//open()方法根据 提交方式有不同 当前为get方式 所以需要将发送的数据附加在URL路径后面
	var url = "xxxServlet?参数="+代表参数值的变量值; //可以动态拼合 url地址  //了解这里可以传参
	xmlHttpRequest.open("GET",url,true);
	
	//4.发送请求
	//调用open()方法 参数为要发送到服务端的数据 因为采用Get方式请求时 参数只能附加到URL路径 所以这里为null
如果send()方法不设置值 在不同的浏览器下可能存在不兼容问题 例如 在IE中能够运行 但在Firefox却不能 所以最好设为null
	xmlHttpRequest.send(null);
	
	
	//回调函数callBack()中处理服务器响应的关键代码
	//直到步骤3请求发送过程就结束了 但是想要知道这个请求是否发送成功 服务器是否成功返回数据 则需要在步骤二设置的回调函数中判断 
	//使用status属性判断当前请求的HTTP状态码 如果状态为"4" 状态码为"200" 表示成功接收到服务端发送的数据 这时就可以使用XMLHttpRequest对象的responseText属性去获取服务器端返回的文本格式数据
	
	function callBack(){
		if(xmlHttpRequest.readyState == 4 && xmlHttpRequest.status == 200){
			var data = xmlHttpRequest.responseText;
			if(data.trim() = "true"){
				$("#nameDiv").html("结果为true的情况");
			}else{
				$("#nameDiv").html("结果为false的情况");
			}
		}
	}
	
	
	执行处理检查功能的Servlet
	
	public class XXXServlet extends HttpServlet{
		public void doGet(HttpServletRequest request, HttpServletResponse response) throwsServletException,IOException{
			String xxx = request.getParameter("参数名");
			boolean xxxx = false; //记录处理答案
			if(//省略判断条件){
				xxxx = true;
			}else{
				xxxx = false;
			}
			response.setContentType("text/html;charset=UTF-8");
			PrintWriter out = response.getWriter();
			out.print(xxxx-);
			out.flush();
			out.close();
		}
		//省略doPost()方法 -修改字符集编码 -调用doGet方法
	}
	
```

#### 使用Ajax发送POST请求及处理响应(GET与POST方式实现Ajax的区别)

```
	
	POST方式的实现根GET方式类似 基本步骤相同
	区别在
	
	GET与POST方式实现Ajax的区别
		初始化XMLHTTPRequest对象
		GET
			//指定 XMLHttpRequest对象的open()方法中的method参数为"GET"
			xmlHttpRequest.open("GET",url,true);
		POST
			//指定 XMLHttpRequest对象的open()方法中的method参数为"POST"
			xmlHttpRequest.open("POST",url,true); //这里的URL不能传参数
			//指定 XMLHttpRequest对象要请求的HTTP头信息 该HTTP请求头信息为固定写法
			xmlHttpRequest.setRequestHeader("Content-Type","application/x-www-form-urlencoded");
		发送请求
		GET
			//指定 XMLHttpRequest对象的send()方法中的data参数为"null"
			xmlHttpRequest.send(null);
		POST
			//可以指定 XMLHttpRequest对象的send()方法中的data参数的值(data就是个参数字符串 opr=1&k='某某') 即该请求需要携带的具体数据(请求参数) 多个用&连接
			//!!!但是不能在URL中传递参数 要在send()方法加
			xmlHttpRequest.send("opr=1&k=某某");
	
```

### (jQuery方式)

```
	
		使用方式 实现Ajax的不足
	步骤繁琐
	方法、属性、常用值、较多不好记忆
	处理繁杂结构的响应数据(XML格式) 比较繁琐
	还具有浏览器兼容问题
	
	jQuery将Ajax相关操作都进行了封装
	
```

#### $.ajax()方法

```
	
	$.ajax()方法 可以通过发送HTTP请求加载远程数据 是jQuery 最底层 的实现 具有 较高灵活性
	
	语法 $.ajax([settings]);
	
	//特殊请求百度
	
	参数 			类型 			说明
	url 		String		 发送请求的地址 默认为当前页地址
	type		String 		请求方式(POST或GET 默认为GET) 1.9.0 之后的版本可以使用method代替type GETH和POST
    data 		PlainObject或String或Array 	   发送到服务器的数据
    dataType	String  	预期服务器返回的数据类型 可用类型有XML、HTML、Script、JSON、JSONP、Text
    timeout 	Number		设置请求超时时间
    global 		Boolean		默认为true 表示是否触发全局Ajax事件
    beforeSend  	 function(jqXHR.jqxhr,PlainObject settings)	发送请求前调用的函数 可用于设置请求头等 返回false将终止请求 参数jqxhr可选是XMLHttpRequest的超集    参数settings可选当前ajax()方法的setting对象
	success 		 function(任意类型 result,String textStatus,jqXHR jqxhr)  	请求成功后调用的函数	参数result可选由服务器返回的数据 textStatus可选描述请求状态的字符串 jqxhr可选
	error			function(jqXHR jqxhr,Stirng textStatus,String errorThrown) 	请求失败时被调用的函数  参数jqxhr可选 textStatus可选错误信息 errorThrown可选 文本描述的HTTP状态			
  	complete	    function(jqXHR jqxhr,Stirng textStatus) 	请求完成后调用的函数(请求成功或失败都调用)	参数jqxhr可选 textStatus可选描述请求状态的字符串
	
```

#### $.ajax()方法实现 用户名验证功能 示例

```
	
	//这里""也可使用''  !!!注意不要忘了 ,号  
	//全局在<script></script>内 并且已经导入jQuery 库包
	//参数列表 参数列表需要包含在一对 括号{}之间 每个参数以 "参数名":"参数值" 的方式书写 如果有多个参数 用 ,号隔开  该语法为JSON语法
	
	$.ajax({
		"url"		:  "userServlet",	       //要提交的URL路径
		"type"		:  "GET",		          //要发送请求的方式
		"data"		:  "name="+name(变量),     //要发送到服务器的数据
		"dataType"   :  "text",				  //指定返回的数据格式
		"success"    :  callBack,			  //响应成功后要执行的代码
		"error"		:  function(){		      //请求失败要执行的代码
			alert("验证出现错误,请稍后再试 或者与管理员联系");
		}  
		
		//可以利用 beforeSend success error  complete 编写function()方法 添加业务公共 提升用户体验 例如请求时间长 可以在提交前 显示一条提示信息  或者利用jQuery的show() hide()等方法显示提示等待信息框  禁用提交按钮防止用户重复操作 之后利用complete参数特点 恢复状态km
		
	});
	//响应成功时的回调函数
	function callBack(data){ //入参表示响应结果
		if(data == "true"){
			//相关提示
		}else{
			//相关提示
		}
	}
	
```

#### Ajax交互扩展

```
	
	除了$.ajax()方法之外Jquery还提供了 其他多种更简单的 Ajax实现方法 $.get() $.post() $.getJSON() 对象.load() 等方法
	
```

##### $.get()

```
	
	语法
		$.get(url,[,data][,success][,dataType]);
		//参数解释参考 $.ajax()方法
	例
		$.get("xxxServlet","name="+name,callBack); //发送请求
		//省略回调函数代码
	
```

##### $.post()

```
	
	语法
		$.post(url,[,data][,success][,dataType]);
		//参数解释参考 $.ajax()方法
	例
		$.post("xxxServlet","name="+name,callBack); //发送请求
		//省略回调函数代码
	
	
```

##### $.getJSON()

```
	
	语法
		$.getJSON(url,[,data][,success]);
		//参数解释参考 $.ajax()方法
		//注意$.getJSON()方法只能以GET方式发送请求
	例
		$.getJSON("xxxServlet","name="+name,callBack); //发送请求
		//省略回调函数代码
	
	
```

##### 使用Ajax直接加载页面内容

```
	
	在前面的Ajax实现中 复杂结构的响应数据 由服务器通过JSON格式发送 客户端接收后再由JavaScript提取数据 并构建HTML文档结构进行展示	//数据规范 扩展性好
	除此之外还可以在服务器端直接产生HTML格式的响应结果 客户端可以直接将响应结果直接嵌套在现有页面中 //使用方便 局限性强
		
	//具体显示方式就是 dataType 设置为html 在Servlet拼合好HTML文档内容 之后返回   之后回调函数直接使用data进行显示
	
```

##### 对象.load()方法

```

/参数解释参考 $.ajax()方法	
	对于Ajax请求直接加载HTML内容到当前页面的使用场景 jQuery也提供了一个.load()方法作为简单实现
	//注意!!!!!!
	//.load()不是全局函数，而是针对与选择器匹配的元素执行
	//包含匿名回调函数，自动将返回值设置为匹配元素的HTML内容
	//load默认使用SET方式提交 如果提供了对象形式的数据 则自动转为POST方式

	语法
		$(selector).load(url[,data][,complete]);
		//参数解释参考 $.ajax()方法
	
	//此方法还可以仅加载远程文档的某个部分 通过修改url的语法可以实现 详细百度 		  https://www.w3school.com.cn/jquery/ajax_load.asp
	
```

### 使用jQuery解析表单数据

```
	
	需要发送表单数据时，提取表单元素的值并构造成合适的数据格式是件很烦琐的事
	
	使用jQuery提供的方法简化处理
 	.serializeArray()	$.param()
 	//手动创建submit提交按钮(button) 并且在调用事件的时候触发Ajax相关方法
		
	.serializeArray()会从一组表单元素中检测有效控件 将其序列化成由name 和value两个属性构成的JSON对象的数组
	有效控件的规则 有
	没有被禁用
	必须有name属性
    选中的checkbox或radio
    触发提交事件的submit按钮
    file元素不会被序列化
	//在此结果基础上 进行表单验证等
	
	//如果要发送到服务器还需要进一步将数据序列化成请求字符串的形式 可以通过$.param()方法实现 
	序列化的结果举例  nid=元素的值$cauthor=元素的值$cip=元素的值
	
	//jQuery还添加了.serialize()
	.serialize()内部使用$.param()对.serializeArray()做了一个简单包装。不需要中间环节时，可以更简便地完成表单数据的序列化
	
	参考 https://www.w3school.com.cn/jquery/ajax_serializearray.asp
	//多选框那种 它会生成同样name的name属性名 和 不同value值的 Json对象数组

```

### 使用JSON传递数据

```
	
	$.ajax({
		"url"		:  "userServlet",	       //要提交的URL路径
		"type"		:  "GET",		          //要发送请求的方式
		"data"		:  "name="+name(变量),     //要发送到服务器的数据
		"dataType"   :  "json",				  //指定返回的数据格式
		"success"    :  callBack,			  //响应成功后要执行的代码
	});
	function(data){ //data为响应回来的数据
		在这里利用Json和字符串的拼合 等等根据需求拼写元素或修改内容 进行动态显示
	}
	
	//Servlet类 
	//省略其他内容 只简单描述 拼装JSON数组格式的响应内容
	//为了避免内容的双引号导致JSON解析(格式)错误 使用String replace("\"","&quot;") 进行转义处理 
	利用StringBuffer.append() 拼合一个JSON数组 
	最后利用out.print(StringBuffer); //发送响应结果 //注意刷新流和关闭流
	
```

### 使用FastJSON简介

```
	
	随着JSON的广泛使用，在服务器端生成JSON字符串成了一件麻烦的工作，效率低且易出错
	FastJSON
        一个性能很好的、Java实现的JSON解析器和生成器
            将Java对象序列化成JSON字符串
            将JSON字符串反序列化得到Java对象
    https://github.com/alibaba/fastjson/releases
    
    //详细实现可以优先 参考百度

	入口类：com.alibaba.fastjson.JSON

	public static String toJSONString(Object object) 	//将Java对象序列化成JSON字符串
	public static String toJSONString(Object object,boolean prettyFormat)  //pretyFormat为true时生成带格式的JSON字符串
	public static String toJSONString(Object object,SerializerFeature features) //可以通过参数features 指定更多序列化规则
    public static String toJSONStringWithDateFormat(Object object,String dateFormat,SerializerFeature features) //可以通过参数dataFormat指定日期类型的输出格式


	枚举类型 SerializerFeature 定义了多种序列化属性
	QuoteFieldNames  //为字段名加双引号，默认即使用
	WriteMapNullValue //输出值为null的字段，默认不输出
	WriteNullListAsEmpty //将值为null的List字段输出为[ ]
	WriteNullStringAsEmpty //将值为null的String字段输出为""
    WriteNullNumberAsZero //将值为null的数值字段输出为0
 	WriteNullBooleanAsFalse //将值为null的Boolean字段输出为false
	SkipTransientField //忽略transient字段，默认即忽略
	PrettyFormat //格式化JSON字符串，默认不格式化
	
	使用示例
		// 包含值为 null 的字段，数值为 null  输出0，String 为 null 输出“”
		String strJSON = JSON.toJSONString(javaObject,SerializerFeature.WriteMapNullValue,SerializerFeature.WriteNullNumberAsZero,SerializerFeature.WriteNullStringAsEmpty);
	
	

```

## JSON数据格式

```
	
	在前面的Ajax实现中 服务器响应内容是一些 含义简单的文本 对于更多应用而言是远远不够的
	需要用到结构化数据表示方式
	
```

### 什么是JSON

```
	
	JSON(JavaScript Object Notation)
	//一种轻量级的数据交换格式
	//采用独立于语言的文本格式
	//通常用于在客户端和服务器之间传递数据
	JSON的优点
	//轻量级交互语言
	//结构简单
	//易于解析
	
```

### 定义JSON对象

```
	
	语法
	var JSON对象 = {"name":value,"name":value,......};
	value可以是String Number boolean null 对象 数组
	name 必须为字符串
	
	例
	var parson = {"name":"张三","age":30,"spouse":null}; //对象
	
```

### 定义JSON数组

```
	
	语法
	var JSON数组 = [value,value,.......];  //取值和数组取值差不多 也可以用 $JSON数组.each()配合this进行遍历
	
	例
	var countryArray = ["中国","美国","俄罗斯"]; //字符串数组
	var personArray = [{"name":"张三","age":30},{"name":"李四","age":40}]; //对象数组
	
```














