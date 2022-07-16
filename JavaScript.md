```
	2019年6月11日08:29:32开始创建
```

# 目录

[TOC]

# JavaScript

## JavaScript的基本介绍

### JavaScript

```
	
	JavaScript是一种基于对象和事件驱动的、具有安全性能的脚本语言(描述性语言) 与HTML标记语言一起 与Web客户实现交互 
	
	实现 制作网页特效 交互 
	实现 表单验证
	
	减轻服务端负担 增加客户端(用户)体验  //运行在客户端 由浏览器执行
	
```

### JavaScript特点

```
	
	向HTML页面中添加交互行为
	脚本语言 语法和Java 90%类似
	解释性语言 边解释边执行 由浏览器执行
	
```

### JavaScript组成

```
	
	ECMAScript  编码遵循 ECMAScript(欧洲计算机制造商协会)标准 规定了所有的属性、方法、对象的标准
	DOM 文档对象模型
	BOM 浏览器对象模型
	
```

### JavaScript的基本结构(语法)

```
	
	<script type="text/javascript">
			JavaScript语句;
	</script>

	//type为	<script> 标签的属性 用于指定文本使用的语言类别为text/JavaScript
	//有的网页中用缺省 type="text/Javascript" 这种写法是正确的 因为HTML5中可省略type属性 HTML5默认为是text/Javascript
	//<script></script>可以包含在文档中的任何地方 只要保证这些代码在被使用前已读取并加载到内存即可
	//浏览器会检查JavaScript语句的语法 有错误将会在警告框中显示
	
```

### 网页中引用JavaScript的方式

```
	
	一、 直接在html代码中使用<script>标签
		//适用于特效代码量少 仅用于单个页面
	二、 外部JS文件 常用 利于 管理和维护
	 在html5 导入页面中
	  <script src = "js文件位置.js" type="text/javascript"></script>
	 在js中
	  外部JS文件不能包含<script>标签 直接写JavaScript代码
	  //适用于代码较多 复用性高
	三、 直接在HTML标签中(标签事件属性)
	  例
	   <input type="button" value="弹出消息框" onclick="javascript:alert('欢迎你');"/>
		
		//javascript: 不可少
	
	!!! //无论是使用<script>标签还是 引用.js文件 浏览器都会按照<script> 标签在页面出现的先后位置进行解析 如果把<script>标签放在<head>中 那么意味着必须等到全部JavaScript的代码全部被下载解析执行完成后 才开始呈现网页内容 对于JavaScript代码多的页面页面来说 出现页面时会出现明显的延迟(一片空白) 为了避免这个问题 -- 将<script>标签放在<body>中 并且放在页面内容的后面
	
```

## JavaScript的核心语法

### 注释

```
	
	单行注释 //
	多行注释 /**/
	
```

### 语法约定

```
	
	代码区分大小写
	分号结尾
	变量 对象 函数名称 和Java相同
	
```

### 变量

```
	
	JavaScript 是一种弱类型语言(没有明确的数据类型)		//变量的类型由付给变量的值决定
	
	JavaScript 区分大小写 变量名遵循java语言命名规范
	
	变量有作用域 全局变量和局部变量
	
```

#### 先声明变量在进行赋值

```

	var 变量名; 变量名 = 变量值; //var 为用于声明变量的关键字
	
```

#### 同时声明和赋值变量

```
	
	var 变量名 = 变量值;
	var 变量名1,变量名2 = 变量值;
	
```

#### 不声明直接赋值(不推荐 也不这么写)

```
	
	变量名 = 变量值
	
	//变量可以不经声明而直接使用 但很容易出错 也很难查找排错 不推荐使用

```

### 常用的输入/输出

#### 输出

```
	
	alert("提示信息");	//警告对话框  //其内容可以是一个变量的值 或 表达式的值 //其他类型的值需要强制转换成字符串类型
	//警告对话框是当前运行的网页弹出的,在对该对话框做出处理前 当前网页将不可用 后面的代码也不会被执行 只有进行处理后 当前网页才会继续显示后面的内容
	
```

#### 输入

```
	
	prompt("提示信息","输入框的默认信息");	//提示对话框 //等待用户输入数据 //没有关闭x
	//第一个参数 通常是提示信息 可选  
	//第二个参数出现在用户输入的文本框中且被选中 作为默认值使用(默认的输入文本) 可选 
    //可以省略第二个参数
	//可以将第二个参数的值设置为空字符串""
	//如果用户单击取消或直接关闭提示对话框 则该方法将返回null
	//如果用户单击确认 则该方法将会返回一个字符串型数据
	//后面的代码也不会被执行 只有进行处理后 当前网页才会继续显示后面的内容
	
```

### 数据类型(注意声明为var)

#### undefined(未定义类型)

```
	
	var 变量名; //变量没有初始值 将被赋予值undefined
	//只有一个值 undefined  
	//由值null派生而来 定义与null相等 //但是它们的 含义不同
	//含义 声明了变量但未对该变量赋值
	
```

#### null(空类型)(占位符)

```
	
	表示一个空值(什么都没有)
	
	//含义 该变量被赋予了一个空值
	//与undefined值相等
	
```

#### number(数值类型)

```
	
    //既可以表示32位的整数 又可以表示64位的浮点数
    
	var 变量名 = 23; //整数 
	
	var 变量名 = 23.0; //浮点数
	
	//有一个特殊值 NaN(Not a Number) 表示非数 它是number类型
	
```

#### boolean(布尔类型)(逻辑型数据)

```
	
	只有两个值	true 和 false
		
```

#### String(字符串的变量类型)

```
	
	一组被引号(单引号或双引号) 括起来的文本
	
	var 变量名 = "xxxxx"; var 变量名 = 'xxxxx';
	
	//JavaScript不对"字符"或"字符串"加以区别
	
```

### String对象(用于支持对字符串的处理)(JS内置对象)

#### 属性

```
		
	var str = "xxxx";
		
	str.length //获取String对象的长度 从1开始数

```

#### 方法

```
	
	//注意为索引位置
	
	charAt(index) //返回在指定位置的字符
	indexOf(str,index) //查找某个指定的字符串,在字符串中首次出现的位置 没找到返回-1 
	//其中index为可选整数参数 表示从第几个字符开始查找(索引位置)
	substring(index1,index2) //返回位于指定索引index1和index2之间的字符串 前要后不要
	split(str) //将字符串分割为字符串数组
	toLowerCase() //把字符串转化为小写
	toUpperCase() //把字符串传化为大写

```

### Array数组(储存一系列的值)(多个值的集合)(JS内置对象)

```
	
	var 数组名称 = new Array(数组中可存放元素总数);
	也可以用方括号 定义
	var 数组名称 = ["值1","值2","值3"];
	
	为数组元素赋值 
	var xArray = new Array("值1","值2","值3");
	//和Java差不多 数组名[下标] 取值赋值
	
```

#### 属性

```
	
	xArray.length //设置或返回数组中元素的数目
	
```

#### 方法

```
	
	join() //通过一个分隔符分割 把数组的所有元素放入一个字符串
	sort() //对数组排序
	push(必需值,可选值,可选值*n) //向数组末尾添加一个或更多元素 并返回新的长度
	
```

### Math(用于执行常用的数学任务)(JS内置对象)

```

	它是JavaScript的全局对象	不用创建(var)
	
```

#### 方法

```
	
	ceil() //对数进行上舍入 例 ceil(25.5) > 26	ceil(-25.5) > 25
	floor() //对数进行下舍入 
	round() //把数四舍五入 为做接近的数
	random() //返回0~1之间的随机数  //包括小数范围 //返回的数包含0不包含1
	
	例 返回整数范围为2~99的随机数
	Math.floor(Math.random()*98+2); //可能有100
	
```

### Date(用于操作日期和时间)(JS内置对象)

```
	
	var 日期实例 = new Date(参数)
	//日期实例 是储存Date对象的变量 可以省略 参数 省略代表当前日期和时间
	参数格式: MM DD,YYYY,HH:MM:SS
	
	
	var 对象名 = new Date(); //返回当前日期和时间
	var 对象名 = new Date("september 1,2019,6,09:06:08");
	
```

#### 方法

```
	
	getDate() //返回Date对象的一个月中的每一天 值介于1~31之间
	getDay() //返回Date对象的星期中的每一天 值介于0~6之间 //注意处理值
	0是星期日 6是星期六 月份+1 //其他都正常
	getHours() //返回Date对象的小时数 值介于0~23之间
	getMinutes() //返回Date对象的分钟数 值介于0~59之间
	getSeconds() //返回Date对象的秒数 值介于0~59之间
	getMonth() //返回Date对象的月份 值介于0~11之间
	getFullYear() //返回Date对象的年份 值为4位数
	getTime() //返回自某一时刻 以来的毫秒数

```

### typeof运算符(检测变量的返回值)

```
	
	typeof根据返回值 判断变量的类型  语法typeof(变量或值)
	
	//返回值 undefined //为 变量声明后 未被赋值
	//返回值 String //为 用单引号或双引号声明的字符串
	//返回值 boolean //为 true或false
	//返回值 number //为 整数或浮点数
	//返回值 object //为 javascript中的是null类型 或 引用类型(对象、数组、函数)
	
```

### 运算符号

#### 算数运算符

```
	
	 +		  -		  *		  /		  %	 	 ++	 	 --
	//+ 运算符 有时候可能被解释为 拼接符
	
```

#### 赋值运算符

```
	
	=		 +=		-=
	
```

#### 比较运算符

```
	
	>		<		>=		<=		==		!=		===		!==
	
	//==表示等于 ===表示恒等(等值等型) !==表示不恒等(不等值或不等型)
	//==用于一般比较  ===用于严格比较  ==转化时可以转换数据类型 
	//===严格比较 只要数据类型不匹配 就返回false 
	
```

#### 逻辑运算符

```
	
	&&		||		!
	
```

#### 逻辑控制语句	

```
	
	//与Java相同
	if条件判断语句
	switch多分支语句
	for、while循环语句
	循环中断 语句break continue 也相同
	
```

##### for in

```
	
	//作用与Java中foreach语句相同  只是将 ":" 变成了 "in" //能更好地理解
	
```

## JavaScript函数

```
	
	类似于Java中的方法 是完成任务的代码语句块
	
	有两种 类型 系统函数 和 自定义函数
	
	//使用更简单 不用定义属于某个类 直接使用	
	
```

### 常用系统函数

```
	
	parseInt("字符串")  //将字符串转换为整形数字
	 //例 parseInt("23") 将字符串"23" 转换为整形值86
	//函数首先查看位置为0处的字符 判断他是否为一个有效数字 如果不是返回NaN(不再继续判断)
	//如果是有效数字将查看位置1处的字符 进行同样的测试 一直持续到有效数字为之 此时将该字符之前的字符串转换成数字
	
	parseFloat("字符串") //将字符串转换为浮点型数字
	 //例 parseFloat("23.33") 将字符串"23.33" 转换为浮点值23.33
	//处理方法与parseInt相似 第一个出现的小数点是有效字符 如果有第二个小数点 那么第二个小数点被看作无效
	
	isNaN() //用于检查其参数是否是非数字
	//通常用于检测parse两个方法的结果 以判断它们表示的是否是合法的数字 或 检测算数是错误(0作为除数等)
	
```

### 自定义函数(一般和事件联合使用)

```
	
	//需要先定义函数 之后才能调用函数
	
	funciton 函数名(参数1,参数2,...){
		//JavaScript 语句
		[return 返回值] //根据需求写
	}	
	//无参函数
	//有参函数
	//因为JavaScript是弱类型 所以它的参数也没有类型检查 和 限定
	//return语句用来 规定函数返回的值
	
	调用函数
		//函数调用一般和表单元素的事件一起使用 调用格式
		事件名="函数名()"
	
```

## 事件(使用频繁)(相对于浏览器页面来说window对象也有)

```
	
	onload //一个页面或一副图像完成加载
	onclick //鼠标单击某个对象
	onmouseover //鼠标光标移到某元素上
	onmouseout //鼠标光标从某元素移出
	onmousedown //鼠标按钮被按下
	onkeydown //某个键盘按键被按下
	onchange //域的内容被改变
	onscroll //捕捉页面垂直或水平的滚动
	
```

## JavaScript操作BOM对象

```
	
	BOM浏览器对象模型 Browser Object Model
	//提供了独立于内容的 可以与浏览器窗口进行互动的对象结构

```

### BOM可实现功能

```
	
	//弹出新的浏览器窗口
	//移动、关闭浏览器窗口以及调整窗口的大小
	//页面的前进、后退
	
```

### BOM层次结构

```
	
	Window --整个BOM的核心
	1↓
	history document location 
	2↓
	link form anchor
	2↓
	buttin checkbox text textarea radio select ...
	
```

### Window对象(全局对象在使用属性或方法时可以省略)

#### 常用属性

```
	
	history //有关客户访问过的URL的信息
	location //有关当前URL的信息
	screen //只读属性 包含有关客户端显示屏幕的信息 例screen.height //返回浏览器高度(px)
	
	调用语法window.属性名 = 属性值;
	例 跳转到XXX网站
	window.location = "XXXURL";
	
```

#### 常用方法

```
	
	prompt(输入对话框,用来提示用户输入一些信息) //显示可提示用户输入的对话框 //只有关闭和确定按钮
	
	alert(警告对话框的消息) //显示带有一个提示信息和一个确认按钮的警示窗 //警告对话框是当前运行的网页弹出的,在对该对话框做出处理前 当前网页将不可用 后面的代码也不会被执行 只有进行处理后 当前网页才会继续显示后面的内容
	
	confirm("对话框中显示的纯文本") //显示(弹出)一个带有提示信息、确认和取消按钮的对话框 //在用户做出应答之前 不会执行下一条语句 点击取消按钮返回 false 确认按钮返回true //常用于确定操作
	
	//三个方法之间的区别
	prompt() 两个参数 点击取消按钮 返回null 点击确定则返回 用户输入的值 常用于收集用户关于特定问题而反馈的信息
	alert() 一个参数 仅显示警告对话框的消息 无返回值 不能对脚本产生任何改变
	confirm() 一个参数 确认对话框 显示提示对话框的消息 点击取消按钮返回 false 确认按钮返回true //常用于确定操作
	
```

```
	
	close() //关闭浏览器
	
	open() //打开一个新的浏览器窗口 加载给定URL所指定的文档
	
	语法window.open("弹出窗口的URL"，"窗口名称","窗口特征");
	
	窗口特征
	height、width //创建文档显示区的高度、宽度 以像素计
	left、top //出现窗口的X坐标 Y坐标 以像素计
	toolbar = yes | no | 1 | 0 是否显示浏览器工具栏 默认yes
	scrollbars = yes | no | 1 | 0 是否显示滚动条 默认yes
	location = yes | no | 1 | 0 是否显示地址地段 默认yes
	status = yes | no | 1 | 0 是否添加状态栏 默认yes
	menubar = yes | no | 1 | 0 是否显示菜单栏 默认yes
	resizable = yes | no | 1 | 0 是否可调节尺寸 默认yes
	titlebar = yes | no | 1 | 0 是否显示标题栏 默认yes
	fullscreen = yes | no | 1 | 0 会否使用全屏模式显示浏览器 默认是no
	//处于全屏模式的窗口必须同时处于剧院模式
	
```

#### 定时函数

```
	
	setTimeout("调用的函数",等待的毫秒) //在指定的毫秒数后 调用函数 或 计算表达式 //延时函数 //会返回一个函数ID
	
	setInterval("调用的函数",等待的毫秒) //安装指定的周期(以毫秒计)  调用函数 或 表达式
	//如果要多次调用 使用周期定时函数 或者在方法中自身调用setTimeout() //周期函数 //会返回一个函数ID
	
	clearTimeout(对应定时函数方法返回的ID值) //清除Timeout函数 
	clearInterval(对应定时函数方法返回的ID值) //清除Interval函数
	
```

### history对象

```
	
	常用方法
	back() //加载history 对象列表的前一个URL
	forward() //记载history 对象列表的下一个URL
	go() //记载history 对象列表的某一个具体URL
	
	history.back() 等价 history.go(-1)  //浏览器中的 后退
	history.forward() 等价 history.go(1) //浏览器中的 前进
	
```

### location对象

#### 常用属性

```
	
	host //设置 或 返回主机名 和当前URL的端口号
	hostname //设置 或 返回当前URL的主机名
	href //设置 或 返回完整的URL //实现跳转功能
	//也可以省略href直接使用location="URL"跳转页面	//之前使用超链接的href属性实现页面跳转但是这种方法跳转的是固定页面 二使用location.href可以动态改变连接的页面
	
```

#### 常用方法

```
	
	reload() //重新加载当前文档 //相当于刷新本页
	replace() //用新的文档替换当前文档
	
```

## JavaScript操作DOM对象(操作样式、节点、标签内容)

```

	DOM文档对象模型 Document Object Model
	//按节点关系找到页面元素 然后操作
	
```

### DOM可实现功能

```
	
	可以让网页真正动起来 动态增加 修改 删除数据
	
```

### Document对象(它是Windows对象的一部分也代表了整个HTML文档)

#### 常用属性

```
	
	referrer //返回载入当前文档的URL //外部网页 访问到本网页  返回的是外部网页的URL //如果不是通过超链接访问的 则referrer的值为null //可实现限制 从指定页面进入
	!!!如果当前文档不是通过超级链接访问的，则为 null 所以先进入 首页 再 在地址栏访问限制页面 是不成立的
	
	URL //返回当前文档的URL
	
	语法
    document.referrer  //可以判断页面是否是连接进入 
    document.URL
	
```

#### 常用方法

```
	
	getElementById() //返回拥有指定id的第一个对象的引用 //对象的id唯一的元素
	getElementsByName() //返回带有指定名称的对象的集合 //相同name属性的元素
	getElementsByTagName() //返回带有指定标签名的对象的集合 //相同的元素
	
	write() //向文档写文本、HTML表达式或JavaScript代码
	
	innerHTML 几乎是所有HTML元素都有的属性 它是一个字符串 用来设置 或 获取 该对象开始标签和结束标签之间的HTML
	
```

### DOM层次结构

```
	
	DOM
	1↓
	DOM Core  	HTML-DOM 	CSS-DOM
	
```

### 节点解释 和 节点之间的关系

```
	
	浏览器把HTML文档的元素转换成节点对象 所有节点组成了一个树状结构

	DOM是以树状结构组织的HTML文档 
	DOM规定 
	整个文档是一个文档节点 每个HTML标签是一个元素节点 包含在HTML元素中的文本是文本节点
	
	每个HTML属性时一个属性节点 注释属于注释节点
	
	节点树中 顶部节点被称为根 
	
	根节点 父节点 子节点 兄弟节点
	
	//关系层 间对照图
	document 文档
	html标签  根节点
	根据标签间嵌套关系 父节点 子节点 兄弟节点
	
```

### 根据层次关系访问节点

```
	
	//都会忽略文档结构
	getElementById() //返回拥有指定id的第一个对象的引用 //对象的id唯一的元素
	getElementsByName() //返回带有指定名称的对象的集合 //相同name属性的元素
	getElementsByTagName() //返回带有指定标签名的对象的集合 //相同的元素
	
```

```
	
	parentNode		//返回节点的父节点
	childNodes 		//返回子节点集合 childNodes[i]取元素
	firstChild		//返回节点的第一个子节点
	lastChild		//返回节点的最后一个子节点
	nextSibling 	//下一个节点
	previousSibling	//上一个节点
	
	//浏览器解析代码时 把<ul>中的空行也认为是一个子节点 所以可能会因 空行 或 换行 导致无法准确访问到节点的情况  
	//通常出现该问题的浏览器FireFox
	
	
```

```
	
	element属性
	
	firstElementChild //返回节点的第一个子节点
	lastElementChild //返回节点的最后一个子节点
	nextElementSibling //下一个节点
	previousElementSibling //上一个节点
	
	//通常两个写法一起用(注意先写Element属性)
	
	//节点1 在 节点2上面 互相为兄弟节点
	
	节点 = 节点1.nextElementSibling || 节点1.nextSibling
	
```

### 操作节点

#### 节点信息

```
	
	nodeName		//节点名称
	nodeValue 		//节点值
	nodeType		//节点类型
	
	//节点类型 返回对应的值 根据值 判断 节点类型
	
	元素element 	1
	属性attr	  	2
	文本text		3
	注释comments  8
	文档document  9
	
```

#### 操作节点属性(HTML-DOM)

```
	
	getAttribute("属性名") //获取 属性名 的属性值 //如果属性不存在 则返回null
	setAttribute("属性名","属性值") //更改设置 属性名的 属性值
	
```

#### 创建和插入节点(HTML-DOM)

```
	
	createElement("标签名") //创建一个标签名的新元素节点 对应document对象
	A.appendChild(B) //把节点B追加到节点A的后面 对应A节点
	insertBefore(A,B) //把A节点插入到B节点之前
	
	cloneNode(参数) //复制某个指定的节点 
	//其中参数为布尔值 true 则复制该节点及该节点的所有子节点 false 只复制该节点和其属性
	 
```

#### 删除替换节点(HTML-DOM)

```
	
	删除节点的父节点.removeChild(节点名称)  //删除指定的节点
	替换节点的父节点.replaceChild(新节点,旧节点)属性attr //用新节点替换旧节点
	
```

#### 操作节点样式(CSS-DOM)	

##### style属性

```
	
	HTML元素.style.样式属性="值";
	
	//例 HTML元素.style.样式属性名称 = "值";
	
	//在JavaScript 如果样式属性名称中带有 - 号则要省去 - 并且 - 后首字母大写
	//样式属性名称 将-字符去掉 例 text-Align >>> textAlign //-后第一个字母大写
	
```

##### className属性

```
	
	HTML元素.className="样式名称"   //给元素设置.class 名称
	
```

#### 获取元素的样式(CSS-DOM)

```
	
	HTML元素.style.样式属性;
	//只能获取内联样式的属性值 不能获取内部样式表或外部样式表中的属性值
	
	
   --微软 为每个元素提供了 currentStyle对象 包含了所有元素的style对象的特性 和任何未被覆盖的CSS规则的style特性 
	
	HTML元素.currentStyle.样式属性;
	//currentStyle是只读的
	//只局限于IE浏览器 其他浏览器无法获取样式的属性值
	
	
	
   --DOM提供了getComputedStyle()方法 有两个参数

	document.defaultView.getComputedStyle(元素,null).样式属性名称
	
	//虽然这个方法时DOM提供的 但是IE 浏览器不支持 而 Firefox、opera、safari、chrome浏览器是支持的 IE浏览器还是要用currentStyle获取样式的属性值
	
```

#### 获取元素位置

```
	
	offsetLeft 		//返回当前元素左边界到它上级元素的左边界的距离,只读属性
	offsetTop		//返回当前元素上边界到它上级元素的上边界的距离,只读属性
	offsetHeight	//返回元素的高度
	offsetWidth		//返回元素的宽度
	offsetParent	//返回元素的偏移容器 即对最近的动态定位的包含元素的引用
	scrollTop		//返回匹配元素的滚动条的垂直位置
	scrollLeft 		//返回匹配元素的滚动条的水平位置
	clientWidth		//返回元素的可见宽度
	clientHeight	//返回元素的可见高度
	
	document.documentElement.scrollTop; //标准浏览器
	document.body.scrollTop; //Chrome浏览器只认识
	
	//两种写法在同一个浏览器使用只会有一个值生效 例 当第一个方法取到值后另一个就始终为0
	//所以最好两种方法 || 者写
	
	//实现随鼠标滚动的广告图片 
	<script>
		//滚动距离....
		window.onload=获取图片的原位置函数;//收集原信息
		window.onscroll=更改图片位置的函数;//根据滚动距离进行更改 //onscroll 捕捉页面垂直或水平的滚动
	</script>
	
```

## JavaScript 对象及面向对象(前端内容 仅做了解 省略跳过部分内容)

```
	
	对象是包含相关属性和方法的集合体
	面向对象仅仅是一个概念或编程思想 通过做原型的方式实现面向对象编程
	
```

### 自定义对象

```
	
	自定义对象 通过 添加属性和方法  //基于Object对象的方式创建对象
	
	var 对象名称 = new Object();
	 例
	 var xxx = new Object();
	 xxx.name = "xxxx"; //设置属性
	 xxx.jump = function(){ alert('xxx');//一些方法操作 }  调用xxx.jump();
	 
	//使用字面量赋值方式创建对象
	
	var 对象名称={
        xxx:"xxx",
        xxx:"xxx",
        xxx:function(){//操作}  调用相同
	}
	
```

```

	可以使用  Chrome调试工具和alert()方法两种方式 调试程序

```

## Chrome开发者工具

```
	
	Elements 查看编辑当前页面的HTML和CSS元素
	Console 用于显示脚本中所输出的调试信息,或运行测试脚本等
	Sources 用于查看和调试当前页面所加载的脚本的源文件
	Network 用于查看HTTP请求的详细信息、如请求头、响应头及返回内容等
	TimeLine 用于查看脚本执行时间、页面元素渲染时间等信息
	Profiles 用于查看CPU执行时间与内存占用等信息
	Resource 用于查看当前页面所请求的资源文件 如HTML、CSS样式文件等
	Audits 用于优化前端页面 加速网页加载速度等
	
```

### 语法错误排除

```
	
	打开网页F12进入调试界面
	进入Sources模块
	选中Pause On Caught Exceptions(圆圈中间2竖) //发送错误自动暂停功能
	在此模块下 按F5 显示代码错误 //会显示错误图标
	
```

### 逻辑错误排除

```
	
	打开网页F12进入调试界面
	进入Sources模块
	设置断点 (在Breakpoints选项会看到设置断点的代码)
	
	右边 的调试栏 分别代表
	停止 断点调试
	单步调试 不进入函数体内部
	单步调试 进入函数体内部
	禁用所有的断点 不做任何调试
	
```

## alert()方法

```
	
	通过alert()方法将不确定的数据 以信息框的方式展示

```
