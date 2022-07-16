```
	2019年3月8日16:20:39创建
```

# 目录

[TOC]

# Emmet

## EMMET基本介绍

```
	
	Emmet是一款插件 编辑器
	只需要敲一行代码就能生完整HTML结构
	
```

## EMMET基本语法

### HTML初始结构

```css
	
	! + Tab键   、  html:5 + Tab键
	
	//将会出现html的初始结构
	
```

### 属性快捷写法

```css
	
	height ,width,color,padding,margin等属性快捷写法


	h属性值单位
	例
	h50px + Tab键
	将会出现以下声明
	height:50px;
	
	w50px + Tab键
	将会出现以下声明
	width:50px;
	
	p50px + Tab键
	将会出现以下声明
	padding:50px;
	
	pt50px + Tab键
	将会出现以下声明
	padding-top:50px;
	
	c#FFFFFF + Tab键
	将会出现以下声明
	color:#FFF;
	
	fz14px + Tab键
	将会出现以下声明
	font-size:14px;
	
	lg(left, #fff 50%, #000)
	将会出现以下声明
	background-image: -webkit-linear-gradient(left, #fff 50%, #000);
	background-image: -o-linear-gradient(left, #fff 50%, #000);
	background-image: linear-gradient(to right, #fff 50%, #000);
	
```

### ID选择器和类选择器渐变写法

```html
	
	ID (#),CLASS (.)


	ID (#)   //标签(元素)名#id名
	
	例 
	div#text + Tab键
	将会出现以下结构
	<div id="text"></div>
	
	
	CLASS(.)	//标签(元素)名.类名
	
	例
	div.text + Tab键
	将会出现以下结构
	<div class="text"></div>
	
```

### 快速创建HTML节点结构

```html
	
	子节点 (>),兄弟节点 (+),上级节点 (^)

	
	子节点 (>)		//标签(元素)名>标签(元素)名>标签(元素)名
	
	例
	div>div>div + Tab键
	将会出现以下结构
	<div>
		<div>
			<div></div>
		</div>
	</div>
	
	
	兄弟节点 (+)	//标签(元素)名+标签(元素)名+标签(元素)名
	
	例
	div+div+div + Tab键
	将会出现以下结构
	<div></div>
	<div></div>
	<div></div>
	
	
	上级节点(^)		//标签(元素)名+标签(元素)名^标签(元素)名
	
	例
	div+div^p + Tab键
	将会出现以下结构
	<div>
		<div></div>
	</div>
	<p></p>
	
	//这里的^接在 div后面 所以p在div的上一级 与div成了兄弟关系
	//两个^^就是上上级 ^可以无数个但是 前提是它的上一级足够 超过的会让其保持到最后一个上一级
	
```

### 让一个结构重复(*)

```html
	
	重复*	 //标签(元素)名*想要的个数
	
	例
	div*5 + Tab键
	将会出现以下结构
	<div></div>
	<div></div>
	<div></div>
	<div></div>
	<div></div>
	
```

### 分组(())

```html
	
	分组 (())
	
	例
	div > (ul > li > a) + div > p + Tab键
    将会出现以下结构
    <div>
		<ul>
			<li><a href=""></a></li>
		</ul>
		<div>
			<p></p>
		</div>
	</div>
    
    
	//括号里面的内容为一个代码块 表示与括号内部嵌套和外面的的层级无关
    //这里如果不加括号的话 猜想下 a+div这样div就是和a是兄弟关系了 会包含在li里面
	
```

### 属性 ([attr]) 用于设置id,class属性  掌握程度低可能会写错 慎用

```
	
	标签(元素)名 [标签(元素)的属性=属性值 标签(元素)的属性=属性值]
	
```

### 编号($)

```html
	
	例
	ul>li.test$*3 + Tab键
	将会出现以下结构
	<ul>
		<li class="test1"></li>
		<li class="test2"></li>
		<li class="test3"></li>
	</ul>
	
	一个$代表一位数  $*4  1、2、3、4
	类推$$ $$*2 001 002
	......
	
	
	如果想自定义从几开始递增的话就利用
	$@+数字数字
	
```

### 文本({})

```html
	
	例
	ul>li.test${测试$}*5 + Tab键
	将会出现以下结构
	<ul>
		<li class="test1">测试1</li>
		<li class="test2">测试2</li>
		<li class="test3">测试3</li>
		<li class="test4">测试4</li>
		<li class="test5">测试5</li>
	</ul>
	
	ul>li.text{测试$}*5 + Tab键
	将会出现以下结构
	<ul>
		<li class="text">测试1</li>
		<li class="text">测试2</li>
		<li class="text">测试3</li>
		<li class="text">测试4</li>
		<li class="text">测试5</li>
	</ul>
	
	ul>li.item$@-*5 + Tab键
	将会出现以下结构
	<ul>
		<li class="item5"></li>
        <li class="item4"></li>
        <li class="item3"></li>
        <li class="item2"></li>
        <li class="item1"></li>
    </ul> 

	ul>li.item$@3* + Tab键
	将会出现以下结构
	<ul>
		<li class="item3"></li>
		<li class="item4"></li>
		<li class="item5"></li>
		<li class="item6"></li>
		<li class="item7"></li>
	</ul>
	
	ul>li.text$@-3*5 + Tab键
	将会出现以下结构
	<ul>
		<li class="text7"></li>
		<li class="text6"></li>
		<li class="text5"></li>
		<li class="text4"></li>
		<li class="text3"></li>
	</ul>
	
```

### 隐式标签

```html
	
	例
	.类名(#id名) + Tab键
	将会出现以下结构
	<div class="test"></div>
	
	ul>.test$*3 + Tab键
	将会出现以下结构
    <ul>
 	  <li class="test1"></li>
   	  <li class="test2"></li>
      <li class="test3"></li>
    </ul>
    
    select>.test$*5
    <select name="" id=""> 
    	<option class="test1"></option>
        <option class="test2"></option>
        <option class="test3"></option>
        <option class="test4"></option> 
        <option class="test5"></option> 
    </select>
    
    等等
	
```