```
	2019年3月4日19:11:09创建
	2021年10月2日10:30:34 - 2021年10月4日11:37:32 第二次校增
```

# 目录

[TOC]

# CSS3 层叠样式总结

![](Images\CSS3.jpg)

# Hello World

## CSS3基本介绍

```
	
	CSS 级联样式表(Cascading Style sheet) 又称为风格样式表(Style sheet) 用来进行网页风格设计
	
	美化页面、统一控制HTML各标签的显示属性、精确定位网页元素位置
	
	部分元素有兼容问题 www.caniuse.com 能查询浏览器对CSS3属性的支持情况
	
	CSS1.0(1996)>CSS2.0>CSS2.1>CSS3(2010)
	
	CSS的外部文件后缀必须为.css
	
```

### CSS3的优势

```
	
	内容与表现分离 
	表现统一
	丰富的样式(页面更吸引用户,良好用户体验)
	减少网页代码量
	运用独立于页面的CSS
	
```

### CSS3的继承

```
	
	子标签可以继承父标签的样式风格 //可以用此简化代码
	子标签的样式不会影响父标签的样式风格
	
	//不是所有的样式都会被继承
	
```

### CSS3的层叠

```
	
	标签的样式是可以 叠加的
	可以用行内样式和外部样式表 给同一个标签添加不同的样式 样式是叠加起来的
	
```

### CSS3就近原则

```
	
	同一个选择器中 样式声明重叠 后写样式 会覆盖 先写样式
	后写样式 优先于 先写样式
	靠近元素的样式具有最大的优先级 排在最后的样式优先级最大
	
```

### CSS3对行内元素

```
	
	行内元素的大小是被撑开的 设置width和height属性不会起作用
	//但也有例外 img 和 input 元素 也称为 行内块元素
	
```

## CSS3基本语法结构

### 基本结构

```css
	
	CSS由 两部分 组成 选择器 和 声明
		
		//声明必须放在{}中,可以是一条或者多条
		//声明由一个 属性 和 值 和值组成 属性和值用冒号(:)分开 以分号(;)结尾
		//在最后一条声明中 结束的冒号可写 可不写 但基于W3C标注 必须写上
		//选择器严格区分大小写 属性和值不区分大小写 属性属性值选择器一般都全部小写
		//如果属性值 有多个单词组成 中间包含空格 必须为这个属性值加上引号
		//CSS代码中 空格 不会被解析
		
		例
			
			(选择器){
				属性 : 值;
				属性 : 值;
			}
	
```

### CSS的注释

```css
	
	/* 这是CSS的注释 */
	
```

### 行内样式表(优先级最高 遵循就近原则)

```css
	
	<xx style="属性:值;"></xx>
	
	//不是内容与表现分离 没有体现CSS的优势 不推荐使用
	
```

### 内部样式表(优先级次级 遵循就近原则)

```css
	
	<head>
		省略其他...
		<style type="text/css">
			选择器{
				属性 : 值;
			}
		</style>
	</head>
	
	//通常书写在<head>标签中 <title>后 保证提前解析 也可放到其它地方
	//不利于 多页面 间共享 复用代码 不常用
	//type="text/css" 不写也可解析 规范要写
	
```

### 外部样式表(优先级最次 遵循就近原则)

```css
	
	将CSS代码保存在一个单独的样式表文件 文件的扩展名为.css 在页面代码中 导入该.css文件
	
	//如果是内部、行内样式改为外部导入css样式表 图片位置需要重新考虑
	//在CSS文件中 不需要<style>标签 可直接写 选择器和声明 
	//样式与结构的彻底分离 减少 重复工作 利于 样式统一 网站维护 提高了网站 运行速度
	
	导入方法
	
		链接式(主要)
		
            <link href(样式表位置)="样式表名称.css" rel(指在页面中使用此外部样式表)="stylesheet" type(指文件的类型是样式表文本)="text/css" />放在head标签中就可以
		
		导入式
		
			@import url("样式表名称.css");写在head标签下style标签中
			@import是属于CSS2.1特有的，对不兼容CSS2.1的浏览器是无效的
		
	两种导入方式区别
			
		<link/>标签属于XHTML,@import是属于CSS2.1
		使用<link/>链接的CSS文件先加载到网页当中,再进行编译显示,网速再慢也是一样的效果
		使用@import导入的CSS文件,客户端显示HTML结构,再把CSS文件加载到网页当中
	
```

## CSS3的选择器

### CSS3的基本选择器

```
	
	用基本选择器基本定位 再用高级选择器精确定位
	
```

#### CSS3选择器优先级

```css
	
	CSS给每个基础选择器定义了权重
	标记选择器 权重1
	类选择器 权重10
	id选择器 权重100
	
	//样式遵循权重最高的
	//权重相同时 遵循就近原则
	//继承样式的权重为0 不管父类的权重多大 被子元素继承都为0 子元素定义的样式会覆盖继承来的样式 
	//选择器用的很多的话 例如 p span{} 权重为1+1  p.blue .header{} 权重为1+10+10

	注: CSS定义了一个 !important 命令 该命令被赋予最大的优先级 无视就近原则 使用方式 p{color: red!important;}
	//命令必须位于 属性值 和 分号之间 否则无效
	
```

#### 标签选择器(优先级最次 不遵循就近原则)

```css
	
	所有的标签都可以作为选择器
	p{
		属性 : 值;
	}
	也可在一行写p{属性:值;}
	
```

#### 类选择器(优先级次级 不遵循就近原则)

```css
	
	给标签起一个类名  同一个类名可以出现多次(常用)
	
	//HTML中
	<p class="类名 类名">你好</p>
	
	//CSS中
	.类名{
		属性 : 值;
	}
	
	类名需要遵循:
	class可以应用多个样式 在多个类名之间用空格隔开
	类名的第一个字符不能使用数字
	使用英文字母小写
	不和ID选择器同名
	使用具有语义化的单词命名
	长名称或词组可以使用驼峰命名方式命名选择器
	
```

#### ID选择器(优先级最高 不遵循就近原则)

```css
	
	给标签起一个id名  一个id只能使用一次(常用) //用一个id浏览器不会报错 但是JavaScript调用id是会报错
	
	//HTML中
	<p id="id名">你好</p>
	
	//CSS中
	#id名{
		属性 : 值;
	}
	
	类名需要遵循:
	只能应用一个样式
	使用英文字母小写
	不和class选择器同名
	使用具有语义化的单词命名
	长名称或词组可以使用驼峰命名方式命名选择器
	
```

#### 交集选择器(了解没啥用)

```css
	
	有两个选择器构成 中间不能有空格 第一个必须是标签选择器 第二个必须是类选择器或id选择器
	
	标签选择器 类选择器或id选择器{
		属性 : 属性值;
	}
	
```

#### 并集选择器

```css
	
	多个选择器通过逗号连接  选择器可以是任何模式
	
	第一个标签,第二个标签,第n个标签{
		属性 : 属性值;
	}
	
```

### CSS3的高级选择器(根据元素之间的层次关系进行选择定位)(类似于筛选条件)

#### 父元素和子元素

```css
	
	把直接 嵌套入 其它元素 的元素 称作 这些元素的 子元素
	子元素的 外部元素 称作 父元素
	
```

#### 层次选择器

##### 后代选择器

```css
	
    选中A标签内的 所有B标签 B元素无论是 A的子元素、孙辈元素、或者更深层次的关系 都被选中
	A 与 B 之间 必须以空格隔开 中间不能含有 其它字符
	
	A B{
		属性 : 值;
	}

	//不限于只有AB两代可以选择孙辈 用空格隔开就好
	
```

##### 子选择器

```css
	
	选择A标签下的 B标签 且B标签 仅仅是A标签的 子标签 其中A为父元素 B为子元素 只有纯子元素被选
	
	A>B{
		属性 : 值;
	}
	
```

##### 相邻兄弟选择器

```css
	
	选中与A标签 相邻的 B标签 B标签是 A标签相邻的 下一个 A和B元素是同辈元素
	选中的 只是与 A元素 后紧挨的 B元素 选中的只是一个
	
	A+B{
		属性:值;
	}
	
```

##### 通用兄弟选择器

```css
	
	选中 与A标签 相邻的 后面的 所有(同辈的)B标签
	选中的 是A元素相邻的 后面的 B元素 选中的是 一个 或 多个元素(有多少选多少)
	
```

#### 结构伪类选择器(可以将一段不存在的HTML当做独立元素来定位)

```css
	
	//https://blog.csdn.net/ixygj197875/article/details/79038041
	有助于理解 结构伪类选择器 

	//减少HTML文档对ID或类的依赖 有助于保持代码干净整洁
	
	:root{}
	//不太常用
	//匹配文档根元素 根元素始终是HTML元素  定义的样式页面元素都生效 可以继承的属性继承(字体大小和背景图片样式有区别)
	
    :empty{}
	//选择 没有子元素 或 文本内容为空的所有元素
	
	:target{}
	//设置锚链接 后设置该属性 在用户点击锚链接之后 跳转到的元素会被应用此样式

	父辈元素(定位选择区间) :not(排除的子辈元素){}  或  :not(排除的元素){} //除了被排除元素以外的元素
	//可以对结构元素使用样式 并且 排除 某个子元素结构
	
    父辈元素(定位选择区间) A:only-child{属性 : 值;}
	//选择 属于父元素的 唯一子元素A (选择的元素是 父元素的唯一子元素)
	
	父辈元素(定位选择区间) A:first-child{属性 : 值;} 
	//选择A的 父辈的第一个子A标签 先看位置后看类型 (选择父元素下的第一个子元素 A)
	
	父辈元素(定位选择区间) A:last-child{属性 : 值;}
	//选择A的 父辈的最后一个子A标签 先看位置后看类型 (选择父元素下的最后一个子元素 A)
	
	父辈元素(定位选择区间) A:nth-child(n[可以n3-1这种写]){属性 : 值;}
	//选择A的 父辈的第n个A标签 先看位置后看类型 (选择父元素下的第n个子元素 A)
	//n写成even选中的偶数的标签 odd奇数的标签
	
	父辈元素(定位选择区间) A:nth-last-child(n[可以n3-1这种写]){属性 : 值;}
	//选择A的 父辈的倒数第n个A标签 先看位置后看类型 (选择父元素下的第n个子元素 A)
	//n写成even选中的偶数的标签 odd奇数的标签

	注: 
	//关于父辈元素(定位选择区间)  栗子 基础选择器(选择区间) p:first-child 选择 
	//上面的选择器 用于 匹配 属于父元素的 特定类型的 第n个子元素/倒数的第n个子元素
	//先看位置后看类型 栗如 "父元素 p:first-child" 先看位置第一个是div 不是元素p所以不会选中任何元素 
        <父元素>
            <div></div>
            <p></p>
            <p></p>
        </父元素>	


	父辈元素(定位选择区间) A:first-of-type{属性 : 值;}
	//选择A的 父辈的第一个类型为A的子标签 先看类型再看位置
	
	父辈元素(定位选择区间) A:last-of-type{属性 : 值;}
	//选择A的 父辈的最后一个类型为A的子标签 并且子标签的类型是A 先看类型再看位置

	父辈元素(定位选择区间) A:nth-of-type(n[可以n3-1这种写]){属性 : 值;}
	//选择A的 父辈的第n个类型为A的子标签 并且子标签的类型是A 先看类型再看位置 如果写成even选中的偶数的标签 odd奇数的标签
	
	父辈元素(定位选择区间) A:nth-last-of-type(n[可以n3-1这种写]){属性 : 值;}
	//选择A的 父辈的倒数第n个类型为A的子标签 并且子标签的类型是A 先看类型再看位置 如果写成even选中的偶数的标签 odd奇数的标签

	//先看类型再看位置 栗如 "父元素 p:first-of-type" 先看类型再看位置 先找第一个p之后选中 第一个p元素(有则必定选中)
        <父元素>
            <div></div>
            <p></p>
            <p></p>
        </父元素>	
	
	
```

#### 伪元素选择器

```css
	
    :before{
		conter:文字/url();
        //对插入内容的
    }
	//在元素内容之前插入 文字/图片
	//必须配合 content属性 指定要插入的具体内容	插入内容可以为文本和图片
		
    :after{
		conter:文字/url();
        //对插入内容的
    }
	//在元素内容之后插入 文字/图片
	//必须配合 content属性 指定要插入的具体内容	插入内容可以为文本和图片
	
```

#### 属性选择器(type属性可能有问题 不能正常区分大小写)

```css
	
	选择有attr属性的A标签 无论这个属性的值是什么
	A[attr]{
		属性 : 值;
	}
	
	
	可以同时设置 多个属性 只要都能匹配 就可以选择到 想要的元素
	A[attr1] [attr2]{
		属性 : 值;
	}

	//A可以省略 可以匹配满足条件的任意元素
	
```

```css
	
	选择有attr属性 值为val的A标签 其中val区分大小写需要完全匹配 
	A[attr="val"]{
		属性 : 值;
	}
	
```

```css
	
	选中属性attr 值为val开头的任意字符串的A标签
	A[attr^="val"]{
		属性 : 值;
	}
	
```

```css
	
	选中属性attr 值为val结尾的任意字符串的A标签
	A[attr$="val"]{
		属性 : 值;
	}
	
```

```css
	
	选中属性attr 值中含有val的任意字符串的A标签
	A[attr*="val"]{
		属性 : 值;
	}
	
```

### 通配符*

```css
	
	通配符 * 就是选中 页面中的所有元素
	//不建议使用因为 不是所有的元素都需要 该样式 降低了 代码的执行速度
	
```

## CSS3的美化网页元素

### 字体样式

```css
	
	font 综合属性简便写法、将前四种结合起来一起写
	font: 字体风格(style) 字体粗细(weight) 字体大小(size) 字体样式(family);
	顺序不能错
	风格 宽度 大小 类型
	
```

#### 字体类型

```css
	
	font-family: 字体名称|字体名称,字体名称; 
	微软雅黑、Arial、宋体、楷体、Times、Times New Roman //中文字体需要加引号(自定都用双引号)
	
	//一些字体名称中带有空格 或 中文 需要用""引起来(可以不加) 让浏览器知道这是一种字体名称 尽量使用计算机常用的字  
	//如果有多个 识别顺序为左到右 
	//在实际网页开发中 网页中的文本如果没有特殊要求 通常设置为宋体 宋体是计算机中默认的字体 其它比较炫的字体则使用图片来替代
	//当需要同时设置英文字体和中文字体时 一定要将英文字体设置在中文字体之前 如果中文字体设置在英文字体之前 英文字体设置将不起作用
	//同时声明两种字体 浏览器会先加载左边的 如果左边是英文字体(不支持中文字体) 则从后面的字体中找中文字体 会达到英文使用英文字体 中文使用中文字体的效果
	
```

#### 字体字号

```css
	
	font-size: 像素大小px;
	单位px(像素)、em(相对于当前对象内文本的字体尺寸)、rem、cm(厘米)、mm(毫迷)、pt(点)、pc
	
```

#### 字体粗细

```css
	
	font-weight: 宽度代码或者数字;
	normal正常、bold加粗、bolder更粗、lighter更细
	//数字百度

```

#### 字体风格

```css
	
	设置字体的风格 正常/斜体
	font-style: 样式代码;
	normal正常、italic/oblique斜体
	中文字体没有斜体库 出现的斜体只是计算机模拟出来的
	英文字体大部分有斜体库 没有的话 计算机会模拟
	
```

### 字间距

```css
	
	letter-spacing:字间距;  //定义字间距(字符与字符之间的空白) 允许使用负值
	word-spacing:单词间距;  //定义英文单词之间的间距 英文单词为一个整体 对中文无用
	
```

### 空白符处理

```css

	white-space: 属性值;

	normal(默认) 文本中的空格 空行无效 满行后自动换行
	pre(预格式化) 按文档的书写方式 保留空格空行 原样显示
	nowrap(空格空行无效) 强制文本不能换行 除非遇到换行标记br 超出元素标记边界 增加滚动条 
	
```

### 文本属性

#### 文本颜色

```css
	
	推荐用颜色值(16进制) 
	color: 颜色值|颜色英文|RGB|RGBA;
	
	颜色值(RGB:十六进制方法(0~F总共16个数)表示颜色：前两位表示红色分量 中间两位表示绿色分量 最后两位表示蓝色分量):#FFFFFF、#666666、#000000、......
	当6位颜色值相邻数字两两相同时可 两两缩写为一位 如#336699可简写为#369
	
	还有一种写法rgb(r,g,b) : 正整数的取值为0～255(十进制),百分比的取值为0%~100%超出范围将截止其最近的取值极限，三个参数都不能取负数。
	color: rgb(0,255,255); //使用时加百分号就都要加 不然就都不加 规范是都加
	
	RGBA 在RGB基础上增加了控制alpha透明度的参数 其中这个透明通道值为0～1,0代表完全透明 1表示完全不透明 取值不能为负数
	color: rgba(0,0,255,0.5);
	
	颜色英文:pink、black、white、purple、skyblue、cyan、orange
	
```

#### 文本水平方式对齐

```css
	
	text-align: 样式代码;
	left(左对齐)  right(右对齐) center(居中) justify(两端对齐)

	//仅适用于块级元素对 行内元素无效
	//如果需要图片设置水平对齐 给图像增加父标记 对父标记设置text-align属性
	
```

#### 文本首行缩进

```css
	
	text-indent: 间隔大小em|px; //最好用em
	间隔单位可用px或者em(空格) em为字符宽度 允许使用负值
	//仅适用于块级元素对 行内元素无效
	
```

#### 文本垂直居中

```css
	
	设置行高、用来使文本垂直居中line-height与height高度相等时 文字可垂直居中
	line-height: 大小px;
	也可以不加任何单位 按倍数表示 此时行高是字体大小的倍数(不常用)
	
```

#### 文本装饰

```css
	
	text-decoration: 样式代码;
	underline(下划线) none(默认无装饰)  overline(上划线)  line-through(删除线)
	//可以同时有两个属性值 用空格隔开
	
```

#### 文本转换

```css
	
	text-transform: 样式代码;
	none(默认不转换) capitalize(首字母大写) uppercase(全部字符转换为大写) lowercase(全部字符转换为小写)
	//用于控制英文字符的大小写 
	
```

#### 图文混排

```css
	
	图片与文本对齐方式图文混排(常用)
	
	img 想要与图片对齐的标签span{
		vertical-align: 样式代码;
	}
	top(上对齐) bottom(下对齐) middle(居中对齐)
	
	
	垂直对齐方式(不常用)
	在目前的浏览器中 只能对表格单元格中的对象使用垂直对齐方式属性 对于h1~h6标签、div标签 都是不起作用的 因此在设置文本标签垂直对齐并不常用
	
```

#### 文本阴影

```css
	
	文本阴影效果(形成的阴影效果永远不会覆盖文件本身)
	
	text-shadow: x轴 y轴 模糊半径 颜色;
	text-shadow: 颜色 x轴 y轴 模糊半径;
	
	x、y轴用来水平直角坐标系 移动阴影位置  
	模糊半径代表阴影向外模糊的模糊范围 值只能是正值 0为没有模糊效果
	颜色是阴影颜色 不设置会使用文本的颜色
	text-shadow属性在CSS2.0中出现 但迟迟未被各大浏览器所支持 因此在CSS2.1中被废弃 如今在CSS3中得到了各大浏览器的支持
	
```

#### 标示对象内溢出文本

```css
	
	text-overflow: 属性值;
	
	clip: 修剪溢出文本 不显示省略标记(...)
	ellipsis: 用省略标记 标示被修剪文本 省略标记插入的位置是最后一个字符
	
	//超出元素大小的字符会被省略成...

	注: 实现这个效果必须 同时使用 white-space: nowrap;(强制文本不能换行) overflow: hidden;(隐藏溢出文本) text-overflow: ellipsis;(用省略号标记被修剪的文本) 还要为包含文本的对象定义宽度

```

### 超链接伪类

```css
	
	样式语法 相当于选择器
	标签名:伪类名{
		声明(效果);
	}
	伪类
	hover 鼠标悬浮其上的超链接样式
	link 单击访问前的超链接样式
	visited 单击访问后的超链接样式
	active 单击未释放的超链接样式
	focus 获得当前光标的焦点
	//设置伪类的顺序	link>visited>hover>active 在ie浏览器中先设置visited后设置的hover就不起作用
	//实际页面开发中 只设置 原标签内容 和 hover 内容
	
```

### 设置鼠标样式

```css
	
	cursor: 样式代码;
	pointer(小手) default(默认光标) help(帮助问号) wait(等待) crosshair(十字状) text(文本)
	
```

### 列表样式

```css
	
	综合属性list-style是简写的方式表示一个设置所有列表的属性
	
	它会按照list-style-type 》list-style-position》list-style-images的顺序设置属性值
	实际使用中 会直接使用list-style: none;设置列表无标记符 不会写position、images 而是通过背景图片的方式把设计的图片设置成列表项标记
	
```

#### 项目编号

```css
	
	list-style-type: 样式代码;
	none(无标记编号) disc(实心圆) circle(空心圆) square(实心方块) decimal(数字)
	
```

#### 项目编号位置(不常用)

```css
	
	list-style-position: 样式代码;
	inside(把项目编号放在li里边)
	outside(把项目编号放在li外边)
	
```

#### 项目编号设置为图片(不常用)

```css
	
	list-style-image: url("图片路径");
	
```

### 背景样式

```css
	
	综合属性简化写法 background
	background: 颜色 图片url 是否平铺 定位;
	
```

#### 背景颜色

```css
	
	background-color: 颜色代码;
	有一个特殊值 transparent 即透明是此属性的默认值
	
```

#### 背景图片

```css
	
	background-image: url("图片路径");
	
```

#### 背景是否平铺

```css
	
	background-repeat: 样式代码;
	repeat(垂直水平平铺)不写即默认 no-repeat(不平铺) repeat-x(水平平铺) repeat-y(垂直平铺)
	
```

#### 背景图片固定

```css
	
	background-attachment: 样式代码;
	scroll(图像岁页面元素一起滚动)(默认) fixed(图像固定在屏幕上[网页上] 不随页面元素滚动)
	
```

#### 背景的显示区域

```css
	
	background-origin: 样式代码;
	padding-box(背景图像相对于内边距区域来定位) border-box(背景图像相对于边框来定位) content-box(背景图像相对于内容来定位)
	
	//background-position 属性总是以元素左上角 为坐标原点 定位背景图像 
	//该属性可以修改定位方式 自行定义背景图像的相对位置
	
```

#### 背景图片的裁剪区域

```css
	
	background-clip: 样式代码;
	border-box(默认值从边框区域向外裁剪背景)  padding-box(从内边距区域向外裁剪背景) content-box(从内容区域向外裁剪背景)	
	//就是设置背景图片到哪里
	
```

#### 背景图片的定位

```css

	//不太确定优先百度 简单参考可以

	 如果不写指图片默认位置在左上角 

	 数值 x y 先水平方向后垂直方向 属于偏移坐标  如果写一个值另一个值是50
	background-position: xpx ypx;
	 
	 使用方位  如果写一个值另一个值是center
	也可写为background-position: 样式代码;    对齐规则 对应方向和盒子对应边对齐
	left(左边，默认垂直居中) right(右边 默认垂直居中) center(居中)
	top(顶部 默认水平居中) bottom(底部 默认水平居中)
	
	
	使用百分比  如果写一个值另一个值是50%
	background-postion: 30% 50%;
	垂直方向居中 水平方式偏移30%;
	将图片的30% 50%和添加背景元素的30% 50%这个点对齐 
	
```

#### 背景图片大小

```css
	
	使用的元素必须有宽度和高度 不然背景图片显示不出来
	
	background-size: xpx ypx; 图片宽为xpx 高为ypx
	background-size: xx% xx%; 图片宽度,高度分别占整个模块的xx% xx%
	
	background-size: 样式代码;
	
        auto(默认值 使用背景图片保持原样)
        cover(图片等比例缩放充满整个模块 会溢出)
        contain(图片等比例缩放放进模块 不会溢出)
        percentage(当使用百分值时 不是相对于背景的尺寸大小来计算的 而是相对于元素宽度来计算的)
	
	
```

#### 渐变色背景

##### 线性渐变

```css
	
	设置渐变色背景 (此属性会存在兼容问题)
	
	background: linear-gradient(样式代码,颜色1,颜色2,...); 
	to top(背景从下到上)
	to bottom(背景从上到下)
	to left(背景从右到左)
	to right(背景从左到右）
	to top left(背景从右下到左上)
	to top right(背景从左下到右上)
	to bottom left(背景从右上到左下)
	to bottom right(背景从左上到右下)
	样式代码也可以为一个角度值 单位为deg(度) 
	
	//可以在颜色属性值后面加 一个百分比数值 表示颜色的位置
		background-image: linear-gradient(90deg,blue 50%,red 80%); //两个百分比数值一样就会有两个或多个颜色背景(没有渐变效果)
	//从某个方向到某个方向 颜色由颜色1渐渐变成颜色2 可有多个颜色渐变区间
	//background-image: repeating-linear-gradient(...); 重复渐变 用时需要 增加颜色位置的百分值
	
```

##### 径向渐变

```css
	
	background-image: radial-gradient(渐变形状 圆心位置,颜色1,颜色2,...);
	
	////可以在颜色属性值后面加 一个百分比数值 表示颜色的位置
	//渐变形状 可以为 定义水平垂直半径的 像素值或百分比 也能是相应的关键词
		circle(圆形的渐变) ellipse(椭圆形的渐变)
	//圆心位置 为 at 加上关键词或参数来定义渐变的中心位置 注:记得加at 省略时不用
		center(默认中心) left right top bottom
		
	//画圆需要设置背景元素 同宽高 设置圆角边框 在加上
		background-image: radial-gradient(circle,blue 50%,red 80%);
	//background-image: repeating-radial-gradient(...); 重复渐变 用时需要 增加颜色位置的百分值

```

## CSS3盒子模型

### 标准盒子模型(标准盒模型:内容的宽高+内边距+边框+外边距)

```css
	
    wwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwww
    wwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwww
    ww----------------------------------------------------------------------------ww
    ww-nnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnn-ww
    ww-n																        n-ww
    ww-n																        n-ww
    ww-n																        n-ww
    ww-n																        n-ww
    ww-nnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnn-ww
    ww----------------------------------------------------------------------------ww
    wwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwww
    wwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwww
    
    w外边距	-边框	   n内边距	   空格是内容的宽高
    
```

### 盒子模型内盒总尺寸

```css
	
	盒子模型内盒总尺寸(没有外边距) = border(左右|上下) + padding(左右|上下) + 内容宽度
	
```

### 盒子模型外盒总尺寸

```css
	
	盒子模型外盒总尺寸 = border(左右|上下) + padding(左右|上下) + margin(左右|上下) + 内容宽度
	
```

### 盒子尺寸计算模型box-sizing拯救布局

```css
	
	事先定义盒子模型的尺寸解析方式
	box-sizing: 盒子样式代码;
	
	content-box ((默认值)标准盒子模型)
	border-box (盒子的宽度(高度)等于元素内容的宽度(高度) 盒子内容 = padding -border - 盒子高(宽))
	inherit (此值使元素继承父元素的盒子模型模式)
	
```

### 边框

```css
	
	综合属性简化写法
	同时设置三个属性时 顺序没有限制 可以按照任意顺序设置 但通常顺序为粗细、颜色、样式。
	border: width color style;
	border-方向: width color style;
	
```

#### 边框样式

```css
	
	border-style: 样式代码;
	border-方向-style: top、left、right、bottom;
	solid(实线边框) dashed(虚线) dotted(点化线) double(双实线) none(无边框)
	
	方向: left right top bottom
	如果不写方向
	顺序为上、右、下、左（顺时针）
	写两个值的时候顺序为上下、左右
	写三个值的时候顺序为上、左右、下 
	
```

#### 边框宽度

```css
	
	border-width: 样式代码;
	border-方向-width: 样式代码;
	thin(细的边框) medium(默认值中等边框) thick(设置粗的边框) (xpx)像素值
	
```

#### 边框颜色

```css
	
	border-color: 颜色值;
	border-方向-color: 颜色值;
	
```

#### 边框圆角

```css
	
	设置盒子上下左右圆角 
	border-radius: 半径px|百分比;
	
	边角方向顺序(按顺时针排列):left top、right top、left bottom、right bottom
	没有的找对边
	border-radius: 10px 20px; 			左上10px 右上20px 右下10px 左下20px
	border-radius: 10px 20px 30px; 		左上10px 右上20px 右下30px 左下20px
	border-radius: 10px 20px 30px 40px;  左上10px 右上20px 右下30px 左下40px
	
	用此属性画原型 半圆形和扇形差不多  
 	元素的高度和宽度必须相同
 	设置半径为元素宽度的一般或者直接设置半径 为50%;
	
```

#### 图像边框

```css
	
	border-image:border-image-source border-image-slice/border-image-width/border-image-outset border-image-repeat; //简写属性
		
	border-image-source:url() 指定图片的路径
	border-image-slice 指定边框图像顶部/右侧/底部/左侧内偏移量
	border-image-width 指定边框宽度
	border-image-outset 指定边框背景向盒子外部延伸的距离
	border-image-repeat 指定背景图片的平铺方式

	//不常用 用的时候百度吧

```

### 内边距

```css
	
	padding: 像素值;
	padding-方向: 像素值;........................................
	方向:left right top bottom
	
	padding: 1px 2px;            上下1px、左右2px
	padding: 1px 2px 3px;        上1px、左右2px、下3px
	padding: 1px 2px 3px 4px;    上1px、右2px、下3px、左4px
	
	方向: left right top bottom
	如果不写方向
	顺序为上、右、下、左（顺时针）
	写两个值的时候顺序为上下、左右
	写三个值的时候顺序为上、左右、下 
	
	在实际应用中网页很多标签都有默认边距(内外都有) 不同的浏览器也不一样 所以通常通过选择器统一设置这些标签的边距为0px
	*{margin: 0px;padding: 0px;}
	
```

### 外边距

```css
	
	基本与内边距相同 将padding 换为 margin
	
	利用外边距实现文本水平居中
	margin: 0px auto;
	//属性值可以为负值 使相邻元素重叠
	注:此属性适用于块级元素 并且此块级元素必须有宽度
	
```

### 盒子阴影效果

```css
	
	设置盒子阴影效果
	box-shadow: x轴 y轴 模糊半径 颜色;
	
	设置盒子外部阴影效果
	box-shadow: 0px 0px 模糊半径 颜色;

	设置盒子内部阴影效果
	box-shadow: inset x轴 y轴 模糊半径 颜色
	inset(阴影类型内阴影)
	
	//x轴y轴控制阴影效果的位置 可以为负
	//阴影模糊半径阴影向外模糊的模糊范围 只能为正值
	//阴影颜色 定义绘制阴影时所使用的颜色
	
	可以设置多层阴影 每层阴影之间使用逗号隔开
	box-shadow: x轴 y轴 模糊半径 颜色,x轴 y轴 模糊半径 颜色;
	
```

## CSS3的浮动

### 文档流

```
	
	元素默认时候从从上到下 从左到右 根据自身特性自然排列的 即标准文档流 
	设置了浮动后 元素 脱离 标准文档流 前面的位置空了 后面的元素就顺序的往上移了
	
	行内元素为左右
	块状元素为上下
	
```

### display属性(不会脱离文档流)

```css
	
	display属性  行内元素和块级元素的互相转换
	
	display: 样式代码;
	none(设置元素不会被显示)！！！元素会被隐藏
	block(块级元素的默认值，元素会被显示为块级元素，该元素前后会带有换行符)
	inline(内联元素(行内元素)的默认值 元素会被显示为内联元素 该元素前后没有换行符 )
	inline-block(行内块元素 元素既具有内联元素的特性 也具有块元素的特性)

	//块级元素被转换为行内元素后 只可以定义左右外边距 定义上下外边距时无效
	
```

### float浮动(脱离文档流)

```css
	
	浮动特性: 贴边、脱流、文字环绕、上浮、收缩
	
	左浮动
	float: left;
	
	右浮动
	float: right;
	
	
	清除浮动
	clear: 样式代码;
	
	none(默认值 允许浮动元素出现在两侧)
	left(在左侧不允许浮动元素)
	right(在右侧不允许浮动元素)
	both(在左、右两侧不允许浮动元素)
	注:将块级元素浮动起来会自动变成行内元素、文字、图片不会被浮动的行内元素覆盖
	
```

### 解决父级边框塌陷(overflow属性)

```css
	
	子元素全部浮动 父元素边框塌陷
	
	
	浮动元素(后面)加空div(设置宽高/对该标记应用clear: both;)	  [空div会造成HTML代码冗余]
	设置父元素的高度(设置宽高)		  [元素固定高会降低扩展性]
	父级添加overflow属性(下例)		 [下拉列表框的场景不能用]
	父级添加伪类after		  [写法比上面稍微复杂一点 但是没有副作用 推荐使用]
	
	
	overflow属性 清除浮动来扩展盒子高度  注:overflow要设给父级元素 并且父级元素要有宽高

		overflow: 样式代码;
	
         visible(默认值 内容不会被修剪 显示在盒子外)
         hidden(如果内容超出父级元素 超出部分被隐藏 不能在有下拉列表框的场景使用[会隐藏下拉列表框])
         scroll(如果内容超出父级元素 超出部分用滚动条显示)横向有滑轨没滑块
         auto(如果内容超出父级元素 超出部分用滚动条显示)超出方向有滑轨和滑块	
	

	添加伪类after
		
		after的意思是选择到class类的后面元素 content添加内容 //上面有单介绍
         例 有个类名kk
         .kk:after{}
         意思是选择类名kk后面的元素并添加样式
         .kk:after{
             height: ();
             content: ' ';(在clear类后面添加内容为空 "或'都无所谓)
             display: block;(把添加的内容转化为块元素)
             clear: both;(清除这个元素两边的浮动)
         }
		//必须设置 height:(); 否则该元素会比其实际高度高处若干像素

```

## CSS3的定位

```css
	
	定位
	position: 样式代码常用relative;
	top: 像素值;向上移动多少
	bottom: 像素值;向下移动多少
	left: 像素值;向左移动多少
	right: 像素值;向右移动多少
	
	static(默认值 没有定位 无法设置定位) 
	relative(相对定位 相对于元素原来的位置来定位的 而且没有脱离文档流 也就是说元素原来的位置别人不能占用)
	absolute(绝对定位 脱离文档流 基本对定位的元素对其他元素的定位不会造成影响使用了绝对定位的元素以它最近的一个"已经定位"的"父级元素"为基准进行偏移 如果它的"父级元素"没有定位或没有"父级元素" 那么它会以浏览器窗口为基准进行偏移)
	fixed(固定定位 脱离文档流、基于浏览器定位)

	//body根元素 为浏览器窗口定位标准
	
```

## CSS3的一行多列

```
	
	利用行元素和块元素的特性  将元素纵向排列
	
```

## CSS3的z-index重叠高低属性

```css
	
	网页中的所有元素都含有两个堆叠层级
	
	设置各元素之间的重叠高低关系
	z-index: 数字值;
	调整层叠元素的位置 默认值是0 值越大越靠上

	//z-index 仅对定位元素生效
	
```

## CSS3的透明度属性

```css
	
	opacity: 透明度大小;
    范围0~1、0表示完全透明、1表示完全不透明、可设置为小数  值越少越透明
	
	
	filter: alpha(opacity=透明度大小) 值越少越透明
	范围0~100、50 、100表示不透明
	
	因为浏览器兼容问题 通常同时设置这两种方法 以适应所有的浏览器
	
```

## CSS3制作网页动画

### CSS3变型

```css
	
	有兼容问题 2D 变型代码放到最终样式中 //解决加入前缀 -webkit- -moz- -o- 
	
	
	通过transform实现2D变化 可以作用在块元素和行内元素上 该属性可以旋转 缩放 移动元素 它的基本的语法如下  
	
	transform: 变型函数; 样式代码可以为多个用空格隔开 //可能会有样式覆盖效果
	
	rotate(旋转度数deg)(旋转函数 取值是一个度数值 要加单位deg 给的角度是正值 元素瞬时间旋转 给的角度值是负值 元素相对原点中心逆时针旋转)只是旋转不会改变元素的形状
	
	scale(放大或者缩小的倍数);(缩放函数 可以使任意元素对象尺寸发生变化 默认值为1、0~0.99的任意值都可以使元素缩小、大于1的任何数都能让元素变大)
	scale(宽度的缩放倍数,高度的缩放倍数);

	scaleX(宽度的缩放倍数);==scale(宽度的缩放倍数,0); //此为3D变换
    scaleY(高度的缩放倍数);==scale(0,高度的缩放倍数);	//此为3D变换
	
	skew(角度值deg);(倾斜函数 取值是一个度数值)平行四边形 x轴左右摆动 y轴上下挫动 不会旋转改变元素的形状 
	skew(角度值deg)
	skewX(角度值deg)(左右摆动的度数);==skew(角度值deg,0px);
	skewY(角度值deg)(上下挫动的度数);==skew(0px,角度值deg);
	
	translate(横向移动的向量px,纵向移动的向量px);(平移函数,基于x、y左边重新定位元素的位置)
	translate(水平偏移量);(一个值只表示水平偏移)
	translateX(横向移动的向量px);==translate(横向移动的向量px,0px); //此为3D变换
    translateY(纵向移动的向量px);==translate(0px,纵向移动的向量px); //此为3D变换
	
	
	浏览器兼容问题
	-o-transform: 样式代码;
	-webkit-transform: 样式代码;
	-moz-transform: 样式代码;

	//可以通过transofrm-orgin 更改变换的中心点 用时百度

```

### CSS3过渡

```css
	
	有兼容问题 过渡代码要放到原样式中 //解决加入前缀 -webkit- -moz- -o-
	
	
	通过transition实现简单触发样式平滑过渡 它的基本的语法如下 
	
	tramsition: 过渡或动态模拟的css属性 完成过渡需要的时间 指定过渡函数 过渡开始出现的延迟时间;
	过渡或动态模拟的css属性(transition-property)(指定的CSS属性width、height、background-color属性、all:指定所有元素支持transition-property属性的样式，一般为了方便都会使用all)
	过渡所需的时间(transition-duration)(设置旧属性到换新属性所花费的时间，单位为秒s)
	过渡动画函数(transition-timing-function)(ease:速度由快到慢(默认值))、(linear:速度恒速(匀速运动))、(ease-in:速度越来越快(渐显效果))、(ease-out:速度越来越慢(渐隐效果))、(ease-in-out:速度先加速再减速(渐显渐隐效果))、
	过渡开始出现的延迟时间(transition-delay)(0，默认值 元素过渡效果立即执行 正值元素过渡效果不会立即触发 当过了设置的时间值后才会被触发 负值元素过渡效果会从该时间点开始显示 之前的动作被截断)
	
	触发机制是超链接伪类

	.A:hover{
        background-color: yellow;
        transition: all 5s linear; 
        //也可分开设置
        transition-property: all;
        transition-duration: 10s;
        ......
	}
	
```

### CSS3动画(了解)

```css
	
	通过animation实现动画主要有两个部分组成
	通过Flash动画的关键帧来声明一个动画
	在animation属性中调用关键帧声明的动画实现一个更为复杂的动画效果
	设置关键帧(自动计算帧数)
	@keyframes IDENT(声明动画的名称){
    	from{/*CSS样式写在这里*/}
		percentage {/*CSS样式写在这里*/}
		to {/*CSS样式写在这里*/}
	}
	
	具体实现(手动控制帧数)
	@keyframes 动画的名称{
        0%{width: 0px;}
        33%{width: 23px;}
        66%{width: 46px;}
        100%{width: 69px;}
	}
	调用关键帧
	animation:animation-name(由@keyframes创建的动画名称) animation–duration(动画时间) animation-timing-function(动画方式) animation-delay(动画开始出现的延迟时间) animation-iteration-count  (动画的播放次数) animation-direction(动画的播放方向)animation-play-state(动画的播放状态) animation-fill-mode(动画开始之前和结束之后发生的操作);
	
	由@keyframes创建的动画名称(animation:animation-name)用于和keyframes联动
	动画时间(animation–duration)设置旧属性到换新属性所花费的时间 单位为秒s
	动画方式(animation-timing-function)(ease:速度由快到慢(默认值))、(linear:速度恒速(匀速运动))、(ease-in:速度越来越快(渐显效果))、(ease-out:速度越来越慢(渐隐效果))、(ease-in-out:速度先加速再减速(渐显渐隐效果))
	动画开始出现的延迟时间(animation-delay)(0 默认值 元素过渡效果立即执行 正值元素过渡效果不会立即触发 当过了设置的时间值后才会被触发 负值元素过渡效果会从该时间点开始显示 之前的动作被截断)
	动画的播放次数(animation-iteration-count)值通常为整数 默认值为 表示动画执行一次 还有一个特殊值infinite 表示动画无限次播放
	动画的播放方向(animation-direction)主要有两个值normal表示表示动画每次都是循环向前播放 另一个值是alternate 表示动画播放为偶数次则向前播放 奇数次则向反方向播放(跳动动画用这个)
	动画的播放状态(animation-play-state)有两个值，running和paused类似音乐播放器 可以通过paused将正在播放的元素动画停下来 也可以使用running将暂停的动画重新播放
	动画开始之前和结束之后发生的操作(animation-fill-mode)取值为forwards表示动画在结束后继续应用最后关键帧的位置 取值为backwards表示会在向元素应用动画样式时迅速应用动画的初始帧 取值为both表示元素动画同时具有forwards和backwards的效果
	
```

## CSS3的一些扩展和注意

```css
	
	min-width: 最小宽度  需要补充
	
	在有鼠标移上去改变边框宽度造成格子 互相挤开的 将 变大的那边宽度或者高度减小
	
	display:none 暂时去除广告窗口
	
	transform属性同时写两个第一个会失效 写在一个transform里面暂时可以解决
	//原因可能是因为第二个将二个属性顶替掉了

	word-wrap 属性 实现长单词和URL地址的自动换行 normal/break-words 只在允许的断字点换行(浏览器保持默认处理)/在长单词或URL地址内部进行换行 //限制p标签的大小 之后文本会溢出区块 用这个解决
	
	
```



