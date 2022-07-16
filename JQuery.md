```
	2019年9月14日14:00:58创建
```

# 目录

[TOC]

# JQuery

### JQuery基本介绍(官网http://jquery.com)

#### 什么是JQuery

```

	jQuery由美国人John Resig于2006年创建
	jQuery是目前最流行的JavaScript程序库，它是对JavaScript对象和函数的封装
	它的设计思想是write less,do more

```

#### JQuery库文件

```
	
	JQuery库 分开发版 和 发布版
	JQuery xx.js (开发版) 约286kb 完整无压缩版本，主要用于测试、学习、开发
	JQuery xx.min.js (发布版) 约94.8kb 经过工具压缩或经过服务器开始Gzip压缩主要用于发布产品和项目
	
	版本号为2.开头的库不提供对 IE6-IE8的支持 即无法解决这三个版本中的兼容性问题
	版本号为1.开头的可以支持所有版本IE 以及目前流行的浏览器(主下)
	
```

#### 在页面引入JQuery

```
	
	JQuery不需要安装 只需要在相关HTML文档中引入库
	<script src="js/jquery-xx.js" type="text/javascript"></script>
	
	在一个页面中使用多个库文件 变量冲突
	 //使用jQuery.noConflict()方法解决对变量$的jQuery控制权 释放对$的控制
	在一个页面中使用一个库文件 则不需要noConflict()方法
	
```

#### 其它JavaScript程序库

```
	
	Bootstrap 22%	Zepto 6%	Ext 5%	YUI 5%

```

#### JQuery能做什么(JQuery能做的JavaScript也都能做，但使用JQuery能大幅提高开发效率) 优势

```
	
	(样式操作、内容及Value值操作、节点操作、节点属性操作、节点遍历、CSS-DOM操作)
	访问和操作DOM元素
	控制页面样式
	对页面事件进行处理
	扩展新的JQuery插件
	与Ajax技术完美结合
	
	轻量级，压缩后只有100KB左右
    强大的选择器
    出色的DOM封装
    可靠的事件处理机制
    出色的浏览器兼容性(能使页面在各浏览器中保持统一的显示效果,即不存在与浏览器兼容性问题) 单纯使用JavaScript编写代码 需要保证各个浏览器的显示结果一致这对一些开发经验尚浅的人难度大,出现失误容易失去潜在用户
    使用隐式迭代简化编程
    丰富的插件支持
    
    !!! JQuery 只是JavaScript的程序库,相当于JavaScript的一个子集 所以它并不能完全取代JavaScript
	
```

### JQuery代码规范(风格)

```
	
	良好代码风格使代码具有可读性 如果统一JQuery代码的编码风格 则日后代码的维护非常有利
    
    //$ 在JQuery程序中 使用最多的是美元符号"$" 无论是页面元素的选择器 还是功能函数的前缀 都必须使用该符号 它是JQuery程序的标志 即$(document).ready() = jQuery(document).ready()
    //链式操作 在对DOM元素进行多个操作时 为了避免过度使用临时变量或不必要的重复代码在大多数jQuery代码采用了链式编程模式 它可以对一个对象进行多重操作 并将操作结果返回给该对象 以便于将返回结果应用于该对象的下一次操作
    例$("xxx").css("//css样式").addClass
    //隐式迭代 例为所有li标签设置css样式 $("li").css({//css样式}); 如果在传统JavaScript写法中将每个li添加需要getElementsByTagName() 获取li标签集合 然后for循环一个一个设置 而jQuery获取一个集合后会默认遍历所有元素
    //添加注释 
    开发阶段 为代码添加注释 可以增加代码的可读性 能让人很容易读懂的代码,便于后期维护
    维护阶段 建议吧关键的模块形成开发文档,便于后期维护,即便后期删除代码注释,也不影响后期维护
    产品正式发布 删除注释 减少文件大小 加快下载速度 提高用户体验 
	
```

### JQuery语法

```
	
	//在实际开发中 通常个需要在页面加载后 立即使用 JavaScript执行一些初始化工作,这通常涉及DOM元素的访问和操作,因此必须确保这些DOM元素已经加载完成,否则将得不到这些DOM对象
	//一般的做法是在$(document).ready()方法中执行这些工作
	
	$(document).ready(function() {
        //执行代码
	});
	
	类似于
	 
	window.onload(function() {
        //执行代码
	});
	
	//注意不要遗忘;
	//ready()方法类似于传统JS(JavaScript)中的onload方法 是JQuery中载入事件的方法 都意味着在页面加载完成时,执行事件
	//可以在功能实现上互换 但存在区别
			

				onload()										
	执行时机  必须等网页所有内容加载完毕(包括图片、Flash、视频等) 
	编写个数  同一页面不能同时编写多个 多个结果只会显示一次
	简化写法 无

				ready()
	执行时机  网页中所有DAO文档结构回执完毕即刻执行(与DOM关联的内容、图片等并没有加载完)
	编写个数  同一页面能同时编写多个
简化写法  
	$(document).ready(function() {    简化   $(function() {
		//执行代码								//执行代码	
	});  								  });
	
```

### JQuery语法结构

```
	
	JQuery语句主要包含三大部分 工厂函数、选择器、方法
	
	$(selector).action();
	
	工厂函数$() //将DOM对象转化为jQuery对象
	
	$(selector);		//选择器用来选择元素
	$(element);			//DOM元素,以DOM元素来创建JQuery对象
	$(html);		    //HTML代码 使用HTML字符串创建JQuery对象
	
	//$等价于jQuery 即$()=jQuery()
	//只有将DOM对象转化为jQuery对象后 才能使用jQuery的方法
	//转为jQuery对象不能再使用DOM对象方法
	//规范条 当$()的参数是DOM对象时 该对象无需使用双引号包裹起来 例如果获取的是document对象则写作	   	      $(document)
	
	
	选择器(selector) //获取需要操作的 DOM元素
	
	//jQuery支持CSS1.0到CSS3.0规则中几乎所有的选择器 
	//使用jQuery选择器和$()工厂函数可以非常方便地获取需要操作的DOM元素
	//ID选择器$("#xxx"); //获取DOM中id为xxx的元素
	//标签选择器$("标签"); //获取DOM中所有的div元素
	//类选择器$(".xxx"); //获取DOM中所有class为xxx的元素 等等选择器
	
	
	方法action() //jQuery中提供的方法,其中包括绑定事件处理的方法 用来绑定事件和事件的处理办法
	
	//JQuery事件 与 JS事件相比只是少了on
	
	load() //一个页面或一副图像完成加载
	click() //鼠标单击某个对象
	mouseover() //鼠标光标移到某元素上
	nmouseout() //鼠标光标从某元素移出
	mousedown() //鼠标按钮被按下
	keydown() //某个键盘按键被按下
	change() //域的内容被改变
	scroll() //捕捉页面垂直或水平的滚动
	
	例
	$(document).ready(function() {   
		$(选择器选择).click(function() {
            //操作	
		});			
	});
	
```

### JQuery选择器

```
	
	jQuery选择器类似于CSS选择器，用来选取网页中的元素
	对事件处理、遍历DOM和Ajax操作都依赖于选择器
	jQuery良好地继承了CSS选择器的语法和其获取页面元素便捷高效的特点 还拥有良好地浏览器兼容性
	
```

#### JQuery选择器的优势

```
	
	简洁的写法
		$(#id) 用来代替 JS中的 document.getElementById()函数 即通过id获取元素
		$("tagName") 用来代替 JS中的 document.getElementsByTagName()函数 即通过标签名来获取元素
	
	完善的处理机制
		选择器不仅比传统获取函数简洁,还能避免某些错误
	
```

#### JQuery选择器类型

```
	
	CSS选择器选取元素 
		基本选择器 
		层次选择器
		属性选择器
	通过过滤选择器选择元素
		基本过滤选择器
		可见性过滤选择器
	
```

#### 基本选择器

|    名称    |           语法构成            |                  描述                  |  返回值  |                           示例                           |
| :--------: | :---------------------------: | :------------------------------------: | :------: | :------------------------------------------------------: |
| 标签选择器 |            element            |        根据给定的标签名匹配元素        | 元素集合 |                  $("h2" )选取所有h2元素                  |
|  类选择器  |            .class             |        根据给定的class匹配元素         | 元素集合 |          $(" .title")选取所有class为title的元素          |
|  ID选择器  |              #id              |          根据给定的id匹配元素          | 单个元素 |             $(" #title")选取id为title的元素              |
| 并集选择器 | selector1,selector2,selectorN | 将每一个选择器匹配的元素合并后一起返回 | 元素集合 | $("div,p,.title" )选取所有div、p和拥有class为title的元素 |
| 全局选择器 |               *               |              匹配所有元素              | 集合元素 |                   $("*" )选取所有元素                    |

#### 层次选择器

|                    名称                     |     语法构成      |                  描述                   |  返回值  |                      示例                       |
| :-----------------------------------------: | :---------------: | :-------------------------------------: | :------: | :---------------------------------------------: |
|         后代选择器(包含所有n级子代)         | root空格offspring | 选取root元素里的所有offspring(后代)元素 | 元素集合 |     $("#menu span" )选取#menu下的<span>元素     |
|      子选择器(直接子元素不包含孙子辈)       |   parent>child    |    选取parent元素下的child（子）元素    | 元素集合 |    $(" #menu>span" )选取#menu的子元素<span>     |
| 相邻元素选择器(常用next()方法代替此选择器)  |     prev+next     |     选取紧邻prev元素之后的next元素      | 元素集合 | $(" h2+dl " )选取紧邻<h2>元素之后的同辈元素<dl> |
| 同辈元素选择器(常用nextAll()代替同辈选择器) |   prev~sibings    |   选取prev元素之后的所有siblings元素    | 元素集合 | $(" h2~dl " )选取<h2>元素之后所有的同辈元素<dl> |

#### 属性选择器

|        语法         |                 描述                 |  返回值  |                        示例                        |
| :-----------------: | :----------------------------------: | :------: | :------------------------------------------------: |
|     [attribute]     |        选取包含给定属性的元素        | 元素集合 |        $(" [href]" )选取含有href属性的元素         |
|  [attribute=value]  |  选取等于给定属性是某个特定值的元素  | 元素集合 |    $(" [href ='#']" )选取href属性值为“*#”的元素    |
| [attribute !=value] | 选取不等于给定属性是某个特定值的元素 | 元素集合 |   $("[href !='#']" )选取href属性值不为“#”的元素    |
| [attribute^=value]  | 选取给定属性是以某些特定值开始的元素 | 元素集合 |  $(" [href^='en']" )选取href属性值以en开头的元素   |
| [attribute$=value]  | 选取给定属性是以某些特定值结尾的元素 | 元素集合 | $("[href$='.jpg']" )选取href属性值以.jpg结尾的元素 |
| [attribute\*=value] |   选取给定属性是以包含某些值的元素   | 元素集合 | $(" [href\*='txt']" )选取href属性值中含有txt的元素 |

#### 条件过滤选择器

```
	
	主要通过过滤规则莱筛选出需要的DOM元素 与CSS中的伪类选择器语法相同都为 : 开头 冒号前是需要过滤的元素
	
	可根据过滤条件分为 基本过滤(常用) 内容过滤 可见性过滤(常用) 属性过滤(常用) 子元素过滤 表单对象属性过滤选择器 (常用)
	
```

##### 基本过滤选择器

|      语法      |                   描述                   |  返回值  |                             示例                             |
| :------------: | :--------------------------------------: | :------: | :----------------------------------------------------------: |
|     :first     |              选取第一个元素              | 单个元素 |      $(" li:first" )选取所有<li>元素中的第一个<li>元素       |
|     :last      |             选取最后一个元素             | 单个元素 |      $(" li:last" )选取所有<li>元素中的最后一个<li>元素      |
| :not(selector) |    选取去除所有与给定选择器匹配的元素    | 集合元素 |         $(" li:not(.three)")选取class不是three的元素         |
|     :even      | 选取索引是偶数的所有元素（index从0开始） | 集合元素 |          $(" li:even" )选取索引是偶数的所有<li>元素          |
|      :odd      | 选取索引是奇数的所有元素（index从0开始） | 集合元素 |          $(" li:odd" )选取索引是奇数的所有<li>元素           |
|   :eq(index)   | 选取索引等于index的元素（index从0开始）  | 单个元素 |            $("li:eq(1)" )选取索引等于1的<li>元素             |
|   :gt(index)   | 选取索引大于index的元素（index从0开始）  | 集合元素 | $(" li:gt(1)" )选取索引大于1的<li>元素（注：大于1，不包括1） |
|   :lt(index)   | 选取索引小于index的元素（index从0开始）  | 集合元素 | $(“li:lt(1)” )选取索引小于1的<li>元素（注：小于1，不包括1）  |
|    :header     |        选取所有标题元素，如h1~h6         | 集合元素 |             $(":header" )选取网页中所有标题元素              |
|     :focus     |          选取当前获取焦点的元素          | 集合元素 |              $(":focus" )选取当前获取焦点的元素              |
|   :animated    |               选择所有动画               | 集合元素 |             $(":animated" )选取当前所有动画元素              |

##### 可见性过滤选择器(通过元素的显示状态 即元素显示或者隐藏来选取元素)

|  选择器  |        描述        |  返回值  |               示例               |
| :------: | :----------------: | :------: | :------------------------------: |
| :visible | 选取所有可见的元素 | 集合元素 | $(":visible" )选取所有可见的元素 |
| :hidden  | 选取所有隐藏的元素 | 集合元素 | $(":hidden" ) 选取所有隐藏的元素 |

##### 表单过滤选择器

```
	
	表单选择器用于选取某些特定的表单元素,比如所有单选按钮或隐藏的元素

```

|   语法    |                     描述                     |                             示例                             |
| :-------: | :------------------------------------------: | :----------------------------------------------------------: |
|  :input   | 匹配所有input、textarea、select和button 元素 | $("#myform  :input")选取表单中所有的input、select和button元素 |
|   :text   |              匹配所有单行文本框              |      $("#myform  :text")选取email 和姓名两个input 元素       |
| :password |                匹配所有密码框                | $("#myform  :password" )选取所有<input type="password" />元素 |
|  :radio   |               匹配所有单项按钮               |       $("#myform  :radio")选取<input type="radio">元素       |
| :checkbox |                匹配所有复选框                |   $("#myform  :checkbox " )选取<input type="checkbox">元素   |
|  :submit  |               匹配所有提交按钮               |     $("#myform  :submit " )选取<input type="submit>元素      |
|  :image   |         匹配所有图像域(图像提交按钮)         |     $("#myform  :image" )选取<input type=" image" />元素     |
|  :reset   |               匹配所有重置按钮               |    $("#myform  :reset " )选取<input type=" reset "/>元素     |
|  :button  |                 匹配所有按钮                 |            $("#myform  :button" )选取button 元素             |
|   :file   |                匹配所有文件域                |     $("#myform  :file" )选取<input type=" file " />元素      |
|  :hidden  |  匹配所有不可见元素，或者type为hidden的元素  | $("#myform  :hidden" )选取<input type="hidden" />、style="display:none"等元素(包括其它类型元素) |

##### 属性过滤选择器

|   语法    |                           描述                           |                             示例                             |
| :-------: | :------------------------------------------------------: | :----------------------------------------------------------: |
| :enabled  |                     匹配所有可用元素                     | $(" #userform :enabled" )匹配form内部除编号输入框外的所有元素 |
| :disabled |                    匹配所有不可用元素                    |           $(" #userform :disabled" )匹配编号输入框           |
| :checked  | 匹配所有被选中元素（复选框、单项按钮、select中的option） |         $(" #userform :checked" )匹配所有选中的选项          |
| :selected |                匹配所有选中的option 元素                 |        $(" #userform :selected" ) 匹配下拉列表的选项         |

#### JQuery选择器的注意事项

```
	
	1.选择器中含有特殊符号的注意事项
		可能会遇到表达式中含有"#" "."等特殊字符的情况 如果按照普通的方式去处理就会出错 解决此类错误的方法是使用转移符转义
		如 <div id="id#a"></div>
		使用 $("#id\\#a");
		
	2.选择器中含有空格的注意事项
		多一个空格或少一个空格 可能会得到截然不同的结果
		如 
			var $AA = $(".test :hidden"); //选中的是class为test的元素 内部的隐藏元素
			var $AA = $(".test:hidden"); //选中的是隐藏的class为test的元素
		
```

### JQuery中的事件

```
	
	通过种种时间实现各项功能或执行某项操作 时间在元素对象与功能代码中起着重要作用	
	
	事件绑定和处理函数的语法格式如下
	事件名 = "函数名()";
	或者
	DOM对象.事件名 = 函数;
	//在进行事件绑定处理函数后 可以通过DOM对象.事件名()的方式显示调用处理函数
	
```

#### 基础事件(鼠标事件、键盘事件、window事件、表单事件)

##### 载入事件

```
	
	载入事件是Window事件的一种 表示当用户执行某些会影响浏览器的操作时 而触发的时间
	例如 打开网页是加载页面、关闭窗口、调解窗口大小、移动窗口 等操作引发的时间处理
	常用方法ready() //文档载入事件
	
```

##### 鼠标事件

|     方法     |                    描述                    |    执行时机    |
| :----------: | :----------------------------------------: | :------------: |
|   click()    |   触发或将函数绑定到指定元素的click事件    |   单击鼠标时   |
| mouseover()  | 触发或将函数绑定到指定元素的mouseover事件  | 鼠标指针移过时 |
|  mouseout()  |  触发或将函数绑定到指定元素的mouseout事件  | 鼠标指针移出时 |
| mouseenter() | 触发或将函数绑定到指定元素的mouseenter事件 | 鼠标指针进入时 |
| mouseleave() | 触发或将函数绑定到指定元素的mouseleave事件 | 鼠标指针离开时 |

```
	
	方法相同点和不同点
	mouseover() mouseenter() 
	//鼠标进入被选元素时会被触发
	//鼠标在其被选元素的子元素上来回进入时 触发mouseover() 不触发mouseenter()
	
	mouseout() mouseleave()
	//鼠标离开被选元素时会触发
	//鼠标在其被选元素的子元素上来回离开时 触发mouseout() 不触发mouseleave()
	
```

##### 键盘事件

|    方法    |                   描述                   |      执行时机      |
| :--------: | :--------------------------------------: | :----------------: |
| keydown()  | 触发或将函数绑定到指定元素的keydown事件  |     按下键盘时     |
|  keyup()   |  触发或将函数绑定到指定元素的keyup事件   |     释放按键时     |
| keypress() | 触发或将函数绑定到指定元素的keypress事件 | 产生可打印的字符时 |

```
	
	//从键盘事件方法中,可以获取当前案件的键值(keyCode) 识别按下了那个键
	//键盘事件执行顺序是 keydown() keypress() keyup()
	
```

##### 浏览器事件

```
	
	调整窗口大小时 页面会有一些变化 这些都是通过resize()方法触发的事件配合函数 完成特性
	
	//语法   $(selector).resize();
	
```

##### 绑定事件与移除事件

```
	
	绑定与移除同属于基础时间,它们主要用于绑定或移除其他基础事件,click、mouseover等
	
```

###### 绑定事件

```
	
	语法bind(type,[data],fn)
	type 事件类型 主要包括基础事件,或自定义事件
	data 可选参数 作为event.data属性值传递给事件对象的额外数据对象,该参数不是必须的
	fn  处理函数 用来绑定处理函数
	
	绑定单个事件
	$(document).ready(function() {
		$("li").bind("click",AA=function() {
			//对li的操作
		});
	});
	绑定多个事件
	$(document).ready(function() {
            $("li").bind({mouseover:AA=function() {
                //对li的操作
            },mouseout:BB=function() {
           	   //对li的操作
            }
          });
	});
	
	//AA、BB名字用于之后解除指定的处理函数
	
```

###### 移除事件

```
	
	有时候事件执行完了 需要把绑定的事件通过一定的办法取消
	
```

```
	
	语法unbind([type],[fn]) 
	//两个参数都不是必须的 , 不带任何参数时 表示移除所绑定的全部事件
	type  事件类型  主要包括基础事件,或自定义事件
	fn    处理函数  用来解除绑定的处理函数 参考绑定事件AA BB
	
```

#### 复合事件(鼠标光标悬停、鼠标连续点击)

```
	
	包含hover()、toggle()方法 与ready()方法类似,是jQuery自定义的方法 
	
```

##### hover()

```
	
	hover()方法用于模拟鼠标指针移入和移除事件
	当鼠标移至元素上时会触发指定的第一个元素,鼠标移出这个元素时 会触发指定的第二个函数 
	//该方法相当于mouseenter mouseleave 事件的组合 
	
	语法
	 hover(enter,leave);
	 
	例
	 $(document).ready(function() {
	 	$("li").hover(function() {
	 		$("li").show();
	 	}),function(){
	 		$("li").hide();	
	 	}
	 });
	
```

##### toggle()

```
	
	toggle()分为带参的方法和不带参的方法
	
	toggle()带参方法 用于模拟鼠标练习click事件,第一次单击元素,触发指定的第一个函数(fn1) 当再次单击同一个元素时,则触发指定的fn2函数;如果有更多函数则 依次触发 知道最后一个 随后的每次单击都重复对这几个函数轮番调用
	语法
		toggle(fn1,fn2,...,fnN);
	例
	  $(document).ready(function() {
	  	$("li").toggle(
	  		function() { $("li").css(//省略样式等等);},
	  		function() { $("li").css(//省略样式等等);},
	  		function() { $("li").css(//省略样式等等);}
	  	);
	  });
	
	toggle()不带参数时,与show()和hide()方法作用一样
	单击元素会切换元素的可见状态
	衍生方法toggleClass(className); 实现事件触发对象在加载某个样式和移除某个样式之间切换
	
	
	
```

#### 表单验证事件和方法

```
	
	可以实现表单验证的 一些主要事件和方法
	
```

| 类别 |       名称       |                    描述                    |
| :--: | :--------------: | :----------------------------------------: |
| 事件 |    onblur(js)    |    失去焦点，当光标离开某个文本框时触发    |
| 事件 |   onfocus(js)    |    获得焦点，当光标进入某个文本框时触发    |
| 事件 |   onsubmit(js)   |               提交表单时触发               |
| 方法 |  blur()(JQuery)  |             从文本域中移开焦点             |
| 方法 | focus()(JQuery)  |     在文本域中设置焦点，即获得鼠标光标     |
| 方法 | select()(JQuery) | 选取文本域中的内容，突出显示输入区域的内容 |

###  JQuery中的动画

```
	
	//增加页面的艺术性
	//通过效果吸引用户的注意力
	//创建出精致的动画
	//增加页面可用性
	
	注意 JQuery中所有的动画效果 都可以设置三种速度参数 slow normal fast(三者对应的时间分别为 0.6秒 0.4秒 0.2秒)
	当使用关键字作为速度参数时 需要使用双引号引起来 如fadeIn("slow") 而使用时间值作为速度参数时不需要双引号 注意单位 为毫秒(1000)
	
```

#### 控制元素显示与隐藏

```
	
	可以使用css()方法改变元素的display属性的值达到显示(block)和隐藏(none)	元素的目的
	
	$(selector).show(); $(select).hide();  //显示、隐藏HTML元素
	
	
	具体设置
	
	元素显示
	$(selector).show([speed],[callback]); //等同于display:block;
	
	//speed 可选 规定元素从隐藏到完全可见的速度 默认为0 可能值 毫秒(如1000)、show、normal、fast
在设置速度的情况下 元素从隐藏到完全可见的过程中,会逐渐地改变高度、宽度、外边距、内边距和透明度
	//callback 可选 show函数执行完成后,要执行的函数
	
	元素隐藏
	$(selector).hide([speed],[callback]); //等同于display:none;
	
	//参数设置与show()相同
	
```

#### 改变元素透明度

```
	
	控制元素淡入
	
	//如果元素是隐藏的 则可以使用fadeIn()方法控制元素淡入 它与show()方法相同可以定义元素淡入时的效果,如显示速度
	语法
	  $(selector).fadeIn([speed],[callback]);
	  
	//speed 可选 规定元素从隐藏到完全可见的速度 默认为0 可能值 毫秒(如1000)、show、normal、fast
在设置速度的情况下 元素从隐藏到完全可见的过程中,会逐渐地改变透明度 给视觉以淡入的效果
	//callback 可选 show函数执行完成后,要执行的函数 除非设置了speed参数 否则不能设置该参数
	
	
	控制元素淡出
	
	语法
	  $(selector).fadeOut([speed],[callback]);
	  
	//参数设置与fadeIn()相同
	
```

#### 改变元素高度

```
	
	//元素的display属性值为none调用 slideDown()方法时 这个元素会从上向下延伸显示 slideUp()方法相反 元素从下往上缩短至隐藏
	
	语法
	  $(selector).slideUP([speed],[callback]);
	  $(selector).slideDown([speed],[callback]);
	  
	  //参数设置于fadeIn() fadeDown() 参数相同
	
```

#### 自定义动画

```
	
	$(selector).animate({params},speed,callback);
	params //必须 定义形成动画的css属性
	speed  //可选 规定效果时长、取值、毫秒、fast、slow
	callback //可选 滑动完成后执行的函数名称
	
```

### JQuery常用方法

#### $(this)是一个jQuery对象 是触发该事件的对象

```
		
	//this指向鼠标指针当前移向的元素	
    
	例
	<ul>
		<li></li>
		<li></li>
	</ul>
	
	$(document).ready(function() {
        $("li").mouseover(function() {
            $(this).css({//css样式});
        }).mouseout(function() {
            $(this).css({//css样式});
        });
	});
	
	
```

### JQuery对象和DOM对象

```
	
	JQuery对象就是包装后的DOM对象产生的对象 能使用JQuery中的方法
	
	//DOM对象只能使用DOM中的方法,jQuery对象不可以直接使用DOM中的方法 但jQuery提供了一套更加完善的对象成员用于操作DOM
	
```

#### JQuery与DOM对象的互相转换

```

	Jquery对象转换成DOM对象 jQuery对象是一个类似数组的对象 
	操作不多见 除非希望使用DOM对象特有成员 如outerHTML属性 通过该属性可以输出相应的DOM元素的完整代码 而jQuery并没有直接提供该功能
	
		一 [index]方法得到相应的DOM对象
			var $tagName = $("#tagName"); //jQuery对象
			var tagName = $tagName[0]; //DOM对象
			alert(tagName.checked); //检测这个checkbox是否被选中了
		
		二 get(index)方法的到相应的DOM对象
			var $tagName = $("#tagName"); //jQuery对象
			var tagName = $tagName.get(0); //DOM对象
			alert(tagName.checked); //检测这个checkbox是否被选中了
			
	将DOM对象转换成jQuery对象
	
		对于DOM对象只需要用$() 函数将DOM对象包装起来 就可以获得一个jQuery对象
		var tagName = document.getElementById("tagName"); //DOM对象
		var $tagName = $(tagName); //jQuery对象

```

### JQuery操作DOM

```
	
	JQuery提供了一系列操作DOM强有力的方法
	//jQuery对JavaScript中的DOM操作进行了封装
	
	//简化了传统JavaScript操作DOM时繁余的代码
	//解决了跨平台浏览器兼容性
	//让页面真正动起来
	//动态的增减修改数据
	//令用户与计算机交互更加便捷
	//交互形式更加多样
	
```

#### 操作DOM类型

```
		
	样式操作 文本操作 value属性值操作 节点操作(属性操作、节点遍历、CSS-DOM操作)
	DOM操作分为DOM Core 、HTML-DOM、CSS-DOM 三种操作类型
	
```

#### 对元素样式的操作

```
	
	//设置样式值 
	//获取样式值
	//追加样式
	//移除样式
	//切换样式
	
```

##### css()方法设置元素样式

```
	
	为匹配的元素添加CSS样式
	
	语法
	 $(selector).css(name,value); //设置单个属性
	 $(selector).css({name:value,name:value...}); //同时设置多个css属性
	
	//css("属性","属性值"); //设置一个css属性
	//({"属性1":"属性值1","属性2":"属性值2",...}); //同时设置多个css属性
	
```

##### addClass()方法为元素添加(追加)样式名

```
	
	$(selector).addClass([样式名]);	//添加追加单个 样式名
	$(selector).addClass([样式名1] [样式名2] ...);	//添加多个类样式 用空格隔开
	
	//注意使用此方法添加class样式名时,该类名前不带有类符号"."
	//样式名 就是 添加.class名 后 根据添加.class名选择元素设置样式
	//使用此方法仅仅是追加类样式 即它依旧保存原有的类样式,在此基础上追加新样式
	//addClass()添加样式更加符合W3C规范 结构与样式分离 的准则
	
```

##### removeClass()移除样式方法

```
	
	$(selector).removeClass([样式名]);	//移除单个样式
	$(selector).removeClass([样式名1] [样式名2] ...);	//移除多个样式
	
	//与addClass()方法相对
	
```

##### toggleClass()切换样式方法

```
	
	$(selector).toggleClass(class);	//可以切换元素的可见状态 切换不同元素的类样式
	
	//当元素中含有名称为class的CSS类样式时,删除该类样式 否则添加一个该名称的类样式
	//模拟了addClass()方法与remove方法实现样式切换的过程 与toggle()方法有异曲同工之妙 减少代码量,增加代码运行效率
	
```

##### hasClass()判断某元素是否已应用指定的样式

```
	
	$(selector).hasClass(class); //判断某元素是否已应用指定的样式
	
	//参数class是类名 该名称是必选的 返回值为布尔类型(包含 true 不包含 false)
	
```

##### addClass()和css()的区别

```
	
	css()方法为所匹配的元素设置给定的css样式 该方式不会删除已经存在的样式
	addClass()方法向所匹配的元素添加一个或多个类,该方式不会删除已经存在的类,仅在原有基础上追加新的类样式
	
	//基于结构与样式分离的原则 通常在实际应用中 为某元素添加样式 使用addClass()方法比css()方法的频率高很多,建议使用addClass()方法为元素添加样式
	
```

#### 内容操作

```
	
	对HTML代码(包括标签、标签内容、标签属性值内容) 三者 的操作
	
```

##### HTML代码操作 html()

```
	
	html([content]);	//类似于传统JavaScript中的innerHTML 通常用于动态新增页面内容
	
	//content 可选 规定被选元素的新内容 该参数可以包含HTML标签 html("<span></span>"); 这样
	//无参数时表示获取被选元素的文本内容或HTML内容
	//有参根据content类型 设置匹配元素的HTML内容或文本内容
	//因为既可以设置文本内容 也可以 设置 HTML内容所以更常用
	
	//仅支持(X)HTML文档 不能用于XML文档
	
```

##### 标签内容操作 text()

```
	
	text([content]);		//获取或设置元素的文本内容 不含HTML标签(特殊字符会被编码) 就单纯的文本里面写啥样网页上就啥样
	
	//content 可选 规定被选元素的新文本内容 注释字符会被编码 
	//无参数时,表示获取被选元素的文本内容
	//有参设置所有匹配元素的文本内容
	
	//支持HTML、XML文档
	
```

##### 属性值操作 val()

```

	val([value]);	//常用于操作表单元素的value属性值
	
	//value 可选 规定被选元素的新内容(input表单) 注意不要往span div 这种元素用 是value属性值！！！
	//无参数时,返回值为第一个被选元素的value属性值

```

#### 节点与属性操作(JQuery操作DOM核心部分)

```
	
	主要分两种类型 
	 一种是对节点本身的操作
	 一种是对节点中属性节点的操作
	
```

##### 节点操作

```
	
	主要分为查找、创建、插入、删除、替换、复制 6种操作方法
	
```

###### 查找节点(选择节点)

```
	
	就是通过选择器选择标签元素
	
```

###### 创建节点元素

```
	
	$(selector);		//选择器用来选择元素
	$(element);			//DOM元素,以DOM元素来创建JQuery对象
	$(html);		    //HTML代码 使用HTML字符串创建JQuery对象
	
	例
	 var $tage = $("<li></li>");			//空li
	 var $tage = $("<li>xxx</li>");			//含有文本li
	 var $tage = $("<li id='xx'>xxx</li>");  //带属性li //注意属性值单引号包括
	 
	//以上JQuery代码仅是创建了一个新元素,而并未将该元素添加到DOM文档中,所以必须把创建好的新元素插入DOM文档中
	
```

###### 插入节点

```
	
	主要分为内部插入节点、外部插入节点
	
```

```
	
	内部插入节点
	
	append(content);	//向所选择的元素内部插入内容		$(A).append(B)表示将B追加到A中
	appendTo(content);  //把所选择的元素追加到另一个指定的元素集合中 $(A).appendTo(B)表示把A追加到B中
	prepend(content);	//向每个选的元素内部前置内容	$(A).prepend(B)表示将B前置插入到A中
	prepentTo(content);	//将所有匹配元素前置到指定的元素中	$(A).prependTo(B)表示将A前置插入到B中
	
```

```
	
	外部插入节点
	
	after(content);	//在每个匹配的元素后插入内容	$(A).after(B)表示将B插入到A之后
	insertAfter(content); //将所有匹配元素插入指定元素的后面 $(A).insertAfter(B)表示将A插入到B之后
	before(content); //向所选择的元素外部前面插入内容 $(A).before(B)表示将B插入至A之前
	insertBefore(content); //将所匹配的元素插入指定元素的前面 $(A).insertBefore(B)表示将A插入到B之前

```

###### 删除节点

```

	JQuery提供了三种删除节点的方法
	
	remove();	//删除整个节点
	empty();	//清空节点内容,能清空元素中所有的后代节点
	detach();	//删除整个节点，保留元素的绑定事件、附加的数据 //了解

```

```
	
	选择器.remove([expr]);	//删除整个节点
	//参数expr为可选项 如果接收参数 则该参数为筛选元素的JQuery表达式.通过该表达式获取指定元素 并删除
	
	//remove()与detach()方法都能将匹配的元素从DOM文档中删除 两者的相同之处是都能将匹配的元素从DOM中删除,并且删除后该元素在JQuery对象中仍然存在 例如 var $name =$("#name").remove(); 虽然id为"name"的元素在页面中不存在了但是$name对象中仍然包含这个元素		两者不同的地方在于detach()可以在删除元素后, 在JQuery对象中保留元素的绑定事件、附加的数据 例如上述代码中 id为"name"的元素已经绑定了click事件 再删除后 $name包含的元素仍然绑定着该事件,而remove则没有这种作用
	
	选择器.empty(); //清空节点内容 
	
	//remove()与empty()方法的区别就在于前者删除了整个节点 后者仅仅删除了节点中的内容
	
```

###### 替换节点

```
	
	replaceWith("//指定的HTML或DOM元素"); //将所有匹配的元素都替换成指定的HTML或者DOM元素	
	replaceAll(); //与replaceWith()方法作用相同只是颠倒了replaceWith()方法的操作

```

###### 复制节点

```
	
	选择器.clone([includeEvents])
	//includeEvents 为可选值 为布尔值true或false 规定是否复制元素的所有事件处理
	
```

##### 属性节点操作

###### attr()方法 //获取与设置元素属性

```
	
	选择器.attr([name]); //获取属性值 //属性名称需要""
	选择器.attr({[name1:value],[name2:value]...}); //最后一个没有,号 //设置多个属性值 属性名称不需要双引号,value需要使用""括起来(数值也要)
	
```

###### removeAttr() //删除元素属性

```
	
	选择器.removeAttr(name); //删除元素属性 //属性名称需要""
	
```

##### 节点遍历

```
	
	包括遍历子元素、同辈元素、前辈元素、和其他一些特别的遍历方法
	children()、next()、prev()、siblings()、parent()、parents()等
	
```

###### children()遍历子元素 //只有这一个方法

```
	
	选择器.children({[expr]}); //用来获取所有直接子元素 而不考虑其它后代元素
	
	//expr参数可选 用于过滤子元素的表达式
	
	
```

###### next()、prev()、siblings()遍历同辈元素

```
	
	它们分别用来获取匹配元素紧邻其后、前、和位于该元素所有同辈元素
	
```

```
	
	 选择器.next([expr]);	//用于获取紧邻匹配元素之后的元素 //注意只有一个
	 
	 //expr可选用于过滤同辈元素的表达式
	
```

```
	
	选择器.prev([expr]);	//用于获取紧邻匹配元素之前的元素 //注意只有一个
	
	//expr可选用于过滤同辈元素的表达式
	
```

```
	
	选择器.siblings([expr]);	//用于获取该元素所有同辈元素 不包括本身
	
	//expr可选用于过滤同辈元素的表达式
	
```

###### 遍历前辈元素

```
	
	主要有parent() 和 parents() 方法
	
```

```
	
	选择器.parent([selector]);	//用于获取当前匹配元素集合中每个匹配元素的父级元素 //只有父亲被选中
	
	//selector参数可选 被匹配元素的选择器表达式
	
```

```
	
	选择器.parents([selector]); //用于获取当前匹配元素集合中每个匹配元素的祖先元素 //选中所有祖辈
	
	//selector参数可选 被匹配元素的选择器表达式
	
```

##### 其它遍历方法

```
	
	//还有许多遍历的方法 each()、end()、find()、filter()、eq()、first()、last()等
	这里只记录each() 和 end()方法 其它进行百度
	//first() 方法为匹配元素集合中的第一个元素
	//last() 方法为匹配元素集合中的最后一个元素
	
```

###### each() 规定为每个匹配元素规定运行的函数(相当于遍历选择元素集合)

```
	
	选择器.each(function(index,element));
	//index选择器的位置 //element当前的元素
	
	//配合$(this). 使用
	例
	 $(".xxx").each(function() { //.xxx获取所有class为xxx的 元素集合
	 	//each() 遍历每个xxx集合中的元素 给其设置css样式
	 	var $xx = $(this).css(//省略样式);
	 });
	
```

###### end() 结束当前链条中的最近的筛选操作，并将匹配元素集还原为之前的状态

```
		
	例 前置 $(".xxx") 为某元素集合 我们想要在一条语句设置 元素集合开头和结尾元素的css样式
	
	$(".xxx").first().css(//省略样式).end().last().css(//省略样式);
	
```

##### CSS-DOM操作

```
	
	css()	//设置或返回匹配元素的样式属性
	height([value])	//参数可选 设置或返回匹配元素的高度 如果没有规定长度单位 则默认使用px //带参设置 //不带获取
	width([value]) //参数可选 设置或返回匹配元素的宽度 如果没有规定长度单位 则默认使用px //带参设置 //不带获取
	offset([value]) //返回以像素为单位的top和left坐标 //此方法只对可见元素有效
	offsetParent() //返回最近的已定位祖先元素 //定位指position值被设置为relative、absolute、fixed元素
	position() //返回第一个匹配元素相对于父元素的位置
	scrollLeft([position]) //参数可选 设置或返回匹配元素相对滚动条左侧的偏移
	scrollTop([position]) //参数可选 设置或返回匹配元素相对滚动条顶部的偏移
	
	//此外获取高度除了可以使用height()方法之外 还能使用css()方法 代码为$("#xx").css("height");
两者的区别在于使用css()方法获取元素高度值与样式设置有关 可能会得到 "auto" "60px" 之类的字符串 而使用height()方法获得的高度值则是元素在页面中的实际高度 与样式的设置无关 且不带单位 其它方法也类似
	
	//这些方法不需要考虑浏览器的兼容性 仅用较少的代码就可以实现相同的效果
	
```

### JQuery表单效验

```
	
	JQuery可以检查用户输入的无效或错误数据 还能检查用户遗漏的必选项
	从而 减轻服务器压力 保证输入的数据符合要求
	
	//养成添加return true/false 语句的习惯 在验证代码中 onsubmit事件将根据返回结果决定是否提交表单到服务器(JQury的submit事件可以实现)
	
```

#### 表单验证思路

```
	
	获得表单元素值   //使用val( )方法获取文本框的值
	使用JavaScript的一些方法对数据进行判断 //使用正则表达式 等等方法判断是否符合规范
	当表单提交时,触发事件,对获取的数据进行验证 //根据返回值是true还是false来决定是否提交表单
	
	//通过String字符串的方法 判断验证内容可靠性 规范性
	//通过一些事件调用验证方法 失去焦点 点击提交等等
	//form表单有个onsubmit事件根据它的属性值true 或者 false 可以设置 表单是否可以提交 onsubmit='return 验证方法'
	
```

#### 常见表单验证

```
	
	日期格式
	表单元素是否为空
	用户名和密码是否为空
	游戏地址
	身份证号码
	
```

#### 正则表达式(可以实现非常严谨的邮箱验证)(并且简介的代码)(基本不用自己写了解 用的时候百度就可以)

```
	
	它是一个描述字符模式的对象 是由一些特殊的符号组成的 RegExp对象是Regular Expression(正则表达式)的缩写 是对字符串执行模式匹配的强大工具
	
```

##### 定义正则表达式

```
	
	定义正则表达式 有两种构造形式 一种是普通方式 另一种是构造函数的方式
	
```

###### 普通方式语法

```
	
	var reg = /表达式/附加参数
	
	//表达式 一个字符串代表了某种规则 其中可以使用某些特殊字符来代表特殊的规则
	//附加参数 用来扩展表达式的含义 主要有三个参数 
	g 代表可以进行全局匹配	i 代表不区分大小写匹配   m 代表可以进行多行匹配  三个参数可以任意组合 代表复合含义 也可以不加参数
	
```

###### 构造函数语法

```
	
	var reg = new RegExp("表达式","附加参数");
	
	//表达式 和 附加参数 与普通方式相同
	//普通方式中的表达式必须是一个常量字符串 而构造函数中的表达式可以是常量字符串,也可以是一个JS变量 例如根据用户的输入作为表达式的参数
	var reg = new RegExp($("#id").val,"g");
	
```

###### 表达式的模式

```
	
	从规范上 表达式的模式 分为 简单模式 和 复合模式
	
```

简单模式(只能表示具体的匹配)

```
	
	简单模式值通过普通字符的组合来表达的模式例如
	
	var reg = /china/;
	var reg = /abc8/;
	
	//这样对比的值是固定的 如果要匹配邮箱或者电话号码 就需要复合模式
	
```

复合模式(可以使用通配符表达更为抽象的规则模式)

```
	
	var reg = /^\w+$/;
	var reg = /^\w+@\w+.[a-zA-Z]{2,3}(.[a-zA-Z]{2,3})?$/;
	var regMobile=/^1\d{10}$/; //手机号码都是11位，并且第1位都是1
	var regCode=/^\d{6}$/; //中国的邮政编码都是6位

```

```
	
	()	是为了提取匹配的字符串 表达式中有几个()就有几个相应的匹配字符串  //粗略理解为一个整体
	[]	是定义匹配的字符串
	{}  用来匹配长度
	
```

###### 正则表达式常用符号

|      |                        描述                        |
| :--: | :------------------------------------------------: |
| /…/  |              代表一个模式的开始和结束              |
|  ^   |                  匹配字符串的开始                  |
|  $   |                  匹配字符串的结束                  |
|  \s  |                    任何空白字符                    |
|  \S  |                   任何非空白字符                   |
|  \d  |           匹配一个数字字符，等价于[0-9]            |
|  \D  |        除了数字之外的任何字符，等价于[^0-9]        |
|  \w  | 匹配一个数字、下划线或字母字符，等价于[A-Za-z0-9_] |
|  \W  |        任何非单字字符，等价于[^a-zA-z0-9_]         |
|  .   |              除了换行符之外的任意字符              |

###### 正则表达式的重复字符

| 符号  |                          描述                           |
| :---: | :-----------------------------------------------------: |
|  {n}  |                      匹配前一项n次                      |
| {n,}  |                 匹配前一项n次，或者多次                 |
| {n,m} |           匹配前一项至少n次，但是不能超过m次            |
|   *   |             匹配前一项0次或多次，等价于{0,}             |
|   +   |             匹配前一项1次或多次，等价于{1,}             |
|   ?   | 匹配前一项0次或1次，也就是说前一项是可选的，等价于{0,1} |

###### RegExp对象(使用正则表达式)

|          方法          |                           描述                           |
| :--------------------: | :------------------------------------------------------: |
|         exec()         | 检索字符中是正则表达式的区配，返回找到的值，并确定其位置 |
| test([要检查的字符串]) |          检索字符串中指定的值，返回true或false           |

|    属性    |          描述           |
| :--------: | :---------------------: |
|   global   | RegExp对象是否具有标志g |
| ignoreCase | RegExp对象是否具有标志i |
| multiline  | RegExp对象是否具有标志m |

###### String对象的方法

|                   方法                   |                             描述                             |
| :--------------------------------------: | :----------------------------------------------------------: |
|        字符串对象.match(字符串);         | 找到一个或多个正则表达式的匹配(类似于indexOf()方法 但是返回的是指定的值) |
|        字符串对象.search(字符串);        |                  检索与正则表达式相匹配的值                  |
| 字符串对象.replace(字符串,替换的字符串); |                 替换与正则表达式匹配的字符串                 |
|       字符串对象.split(分割符,n);        |                   把字符串分割为字符串数组                   |

#### HTML5验证表单

```
	
	主要就是 表单属性  
	required  //提供一种提示（hint），输入域为空时显示，获得焦点输入内容后消失
    placeholder //规定输入域不能为空
    pattern 进行表单验证 //规定验证input域的模式（正则表达式）	
```

##### validity属性(了解)

```
	
	validity属性 可以获取表单元素的validityState对象 
	
	var validityState = document.getElementById("uName").validity;
	
	validityState对象主要包括8个属性 针对摆个方面的错误验证
	
	
	valueMissing
	表单元素设置了required特性，则为必填项。如果必填项的值为空，就无法通过表单验证，valueMissing属性会返回true，否则返回false。
	
	typeMismatch
	输入值与type类型不匹配。HTML 5新增的表单类型如email、number、url等，都包含一个原始的类型验证。如果用户输入的内容与表单类型不符合，则typeMismatch属性将返回true，否则返回false。
	
	patternMismatch
	输入值与pattern特性的正则表达式不匹配。如果输入的内容不符合pattern验证模式的规则，则patternMismatch属性将返回true，否则返回false。

	tooLong
	输入的内容超过了表单元素的maxLength 特性限定的字符长度。虽然在输入的时候会限制表单内容的长度，但在某种情况下，如通过程序设置，还是会超出最大长度限制。如果输入的内容超过了最大长度限制，则tooLong属性返回true，否则返回false。
	
	rangeUnderflow
	输入的值小于min特性的值。如果输入的数值小于最小值，则rangeUnderflow属性返回true，否则返回false。
	
	rangeOverflow
	输入的值大于max特性的值。如果输入的数值大于最大值，则rangeOverflow属性返回true，否则返回false。

	stepMismatch
	输入的值不符合step特性所推算出的规则。用于填写数值的表单元素可能需要同时设置min、max和step特性，这就限制了输入的值必须是最小值与step特性值的倍数之和。例如范围从0到10，step特性值为2，因为合法值为该范围内的偶数，其他数值均无法通过验证。如果输入值不符合要求，则stepMismatch属性返回true，否则返回false

	customError
	使用自定义的验证错误提示信息。使用setCustomValidity( )方法自定义错误提示信息：setCustomValidity(message)会把错误提示信息自定义为message，此时customError属性值为true；setCustomValidity("")会清除自定义的错误信息，此时customError属性值为false。

```

### JQuery让渡$操作符

```
	
	能百度先百度
	
	jQuery不是唯一使用 $ 的脚本库 项目中有其他同样使用 $ 的脚本库时就会引起冲突

	// Prototype的 $ 会覆盖jQuery的 $
        <script type="text/javascript" src="../js/jquery-1.12.4.min.js" />
        <script type="text/javascript" src="../js/prototype.js" />
    或者
    // jQuery的 $ 会覆盖Prototype的 $
        <script type="text/javascript" src="../js/prototype.js" />
        <script type="text/javascript" src="../js/jquery-1.12.4.min.js" />
	
	
	jQuery定义了jQuery.noConflict()方法 放弃对$的使用权，以免与其它脚本库冲突

	jQuery.noConflict(); // 让渡$使用权，后续jQuery代码使用jQuery代替$
    jQuery( document ).ready( … );
    或者重新指定一个替代符号：
    var  $j = jQuery.noConflict(); // 让渡$使用权，并指定用 $j 代替$
    $j( document ).ready( … );
	//改变了jQuery的编码风格 烦琐且不利于重用已有代码

	
	可以这样使用 利于重用代码 保留编码风格
	jQuery.noConflict(); // 让渡$使用权，其他脚本库可以使用$
    jQuery( document ).ready( function( $ ) {
        // 在这里继续使用$编写jQuery代码
        $( "#show" ).click( … );
    } );
    或者
    jQuery.noConflict(); // 让渡$使用权，其他脚本库可以使用$
    ( function( $ ) {
        // 在这里继续使用$编写jQuery代码
        $( document ).ready( function() {
            $( "#show" ).click( … );
        } );
    } )( jQuery );

```
