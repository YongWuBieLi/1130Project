```
	2018年12月12日10:14:52创建
	2021年10月1日09:46:21-2021年10月1日20:28:36  -第三次校增
	2021年10月13日20:42:09 lable 更正 label
```

# 目录

[TOC]

# Html5

## html5基本介绍

#### 什么是HTML

```
	
	Hyper Text Markup Language（超文本标记语言）边解释边运行
	
	html结构   css表现   JavaScript行为
	
	超文本 不仅可以传输文字 还可以传输 视频 音频等
	标记语言 纯文本文件中包含了html代码 只是一种在网页中标记显示位置的标记结构语言 不是程序语言
	
```

#### HTML5的优势

```
	
	主要的浏览器都在支持html5
	html5被标准化统一了Web兼容性标准
	跨屏台极大减少开发人员的工作量
	内容和表现分离
	
```

### 基础开始

#### 编辑器

```
	
	Dream weaver
	WebStorm
	Sublime Text
		
	UltraEdit
	Hbuilder
	
	//html:5 + Tab 或者 ！ 网页基本框架
	//ctrl+shift+/ 加注释
	//ctrl+/  加注释
	//标签名字*数量   出现数量行标签
	
```

#### 零散

```
	
	文件命名最好都是小英文
	全角的空格浏览器可以识别 (搜狗输入法转换全角半角 shift + space)
	
```

#### 功能属性

```html
	
	<div align="left、right、center"></div>
	
	//用作图文混排
	//align 属性规定 元素中的内容的水平对齐方式
	//现在不赞成使用元素的 align 属性 通过css进行代替使用
	

	<div title="鼠标悬停显示信息">内容</div>

	//title="鼠标悬停提示文字"
	
```

#### 开放(开始)标签和闭合(结束)标签 单标签和双标签

```html

	<body></body>等成对的标签 分别叫做开放标签和闭合标签
	单独呈现的标签(空元素) 如<hr/>意为用/来关闭空元素
	直接使用<br/>表示标签的开始和结束的标签叫单标
	成对出现的 如<html></html>这样有开始标签和结束标签的标签叫双标签
	
	//单标签的斜杠结尾在最后
	
```

#### 块元素和行内元素

```
	
	块级元素
		无论内容多少，该元素独占一行（p、h1-h6、li、header、div、table、ul...）
	行内元素(内联元素)
		内容撑开宽度，左右都是行内元素的可以排在一行(img、a、strong、em...)
		
```

#### 绝对路径、相对路径

```
	
	绝对路径	 /从盘符开始找到想要得到的文件路径 指向目标地址的完整描述 一般指向本站点外的文件
	绝对路径就是你的主页上的文件或目录在硬盘上真正的路径 
	 
	相对路径  	 相对于本文件的路径找到另一个文件的路径 
	相对路径就是指由这个文件所在的路径引起的跟其它文件（或文件夹）的路径关系 
	 
    ./  代表文件所在的目录(可以省略)  ../ 表示当前目录的上级目录 /路径符
	/文件根目录
	
```

### html5基本网页编码框架

```html
	
	<!DOCTYPE html>告诉浏览器使用什么规范  DOCTYPE声明必须位于html文档的第一行
	<html  lang="en"> lang="en"意为表示本页是英文的，chrome之类的浏览器会提示是否需要翻译
	<head>网页头部 提供整个网页的描述
		<meta charset = "UTF-8">网页字符编码  如果网页打开乱码 删除或添加这个
		<title>网页标签名字</title>网页标签
	</head>网页头部结束 
	<body>主体部分
	网页内容
	</body>主体部分结束
	</html>
	
	注意 
	网页中所有的内容都放在<xxx>和</xxx>之间
	HTML标签都以“< >”开始、“</ >”结束
	UTF-8也可以写成utf-8(大小写无所谓)，还可以设置为gb2312
	gb2312包含全部中文字符
	utf-8则包含全世界所有国家需要用到的字符
	html中不是所有的标签都是成对的
	标签不区分大小写 属性值可以不使用引号
	
```

### 主要标签

#### 注释

```html
	
	<!--注释内容--> 注释
	
```

#### 页面布局标签

```html
	
	<header></header> 页面头部
	<section></section> 页面主体
	<footer></footer> 页面脚步
	<article></article> 独立的文章内容
	<aside></aside> 相关内容或应用(常用于侧边栏 友情链接 广告单元等)
	<nav></nav> 导航(翻页进度s)类辅助内容
	<div></div> 进行网页布局 
	
	//他们没有任何意义
	//用这些标签进行结构划分 通过语义化标签 使网页结构更清晰 明确 利于引擎检索 
	
```

#### link标签定义文档与外部资源的关系

```html
	
	<link rel="关系" type="mime类型" href="位置">
        
	//rel 值 icon 设置网站图标
	//mime类型 https://www.w3school.com.cn/media/media_mimeref.asp
	//最常见的用途是链接样式表
	
```

#### 文本格式化标记

```html

	<p>内容</p> 段落标签
	<span>内容</span>局部突出
	<hr/> 水平线 块元素
	<br/> 换行 行元素 
	
	文本样式标签
		<i>内容</i> 斜体
		<b>内容</b> 粗体
		<s>内容</s> 删除线 不赞成使用
		<u>内容</u> 下划线 不赞成使用
	
	语义化强调标签 //强调、加强语气的作用 带有语义化的标签
		<em>内容</em> 斜体
		<strong>内容</strong> 加粗
	 	<del>内容</del> 删除线 
	 	<ins>内容</ins> 下划线

	//以上效果都可以通过span配合css 实现

```

#### 六级标签

```html
	
    <h1 title="鼠标悬停提示文字"> 内容 </h1> 一级标题标签

    <h2> 内容 </h2> 二级标题标签
    <h3> 内容 </h3> 三级标题标签
    <h4> 内容 </h4> 四级标题标签
    <h5> 内容 </h5> 五级标题标签
    <h6> 内容 </h6> 六级标题标签

    //语义化标签禁用做样式
	//h1语义化 最好全篇只有一个(全页只有一个主题)
	
```

#### 图片标签

```html
	
	<img src="图像路径" alt="图像的替代文字(图像如果不能正常显示(网速过慢)(图片路径错误))" title="鼠标悬停提示文字" width="图像宽度px" height="图像高度px" id="用于跳转" vspace="图片顶底边距 不常用" hspace="图像水平边距 不常用" align="left/right将图像对齐到左/右边、top/middle/bottom将图像的顶端/底端和文本的第一行对齐其它文字居图像下方 ">  
	
	//规范要求src alt 必选
	//通常会把图片保存在image或images目录下
	
```

#### 超链接的应用场合(锚链接，页面间链接，功能性链接)

```html
	
	超链接包含两部分内容  
		链接地址 (链接目标  可能是某个网址或文件的路径)对应标签的href属性
		链接文本或图像  单击该文本或者图像将跳转到href制定的网址或者文件
	
	作用
		页面间链接： A页到B页  最常用常用于导航
		锚链接： A页甲位置到A页乙位置 或 A页甲位置到B页乙位置
			a标签href属性指向跳转位置id 用#名id 来创建锚链接
		功能性链接：在页面中调用其他程序功能  如电子邮件、QQ、等
			功能性链接电子邮件用法"mailto：电子邮件地址"写在href中
	
	<a id="用于跳转" name= "用于跳转" href = "跳入的标签或者网址(不写地址相当于访问本页)" title="鼠标悬停提示文字" target(不写默认原窗口打开)="_self(在原窗口打开跳转地址) _blank(在新窗口打开跳转地址)">锚链接名字或图片</a>`  
	//超链接可以给图片 音频 视频 添加				
	//name属性和id属性都是用来做标记  id的兼容性比name的兼容性高一些
	//规范 a标签 没有确定链接目标是 href属性值定义为# 表示当前是个空链接
	
```

#### 视频元素、音频元素

```html
	
	<video src="视频路径" controls(播放控件(包含播放、暂停、进度条、全屏、声音大小、时间显示)如果不加且autoplay也没有则视频不播放) autoplay(自动播放属性 不能与controls同用) loop(循环播放) preload(预加载视频有autoplay则忽略此属性) poster=(url视频缓存不足时 链接一个图像)	></video>
    //导入视频

	<audio src="音频路径" controls autoplay loop(循环播放)></audio>
	//导入音频 
	
 	source属性用法
    <video src="视频路径">
        <source src="第一种音频格式路径" type="媒体文件类型/格式"/>
        <source src="第二种音频格式路径" type="媒体文件类型/格式"/>
        您的浏览器不支持video标签 //如果上面的不行就显示这一条
    </video>
 	
	//可以将互联网外链 加入到 audio/video 的src路径中
	//自动播放慎用容易引起用户反感
 	//video和audio 可以利用source属性来链接到不同的视频文件(可以多次出现) 浏览器会自动选择一个可以识别的格式
 	//通过source引入的视频文件的格式至少包括WebM和MPEG4或Ogg和MPEG4
 	//通过source引入的音频文件的格式至少包括WAV和MP3或Ogg
 	
```

#### iframe框架 内联框架

```html
	
	//作用 使页面中的部分内容用框架实现 一般用于在页面中引用站外的页面内容 使用比较方便、灵活、
	
	<iframe src="准备显示的页面可以为url地址" name="这个iframe的名字" scrolling="是否有滚动条 yes|no" width="设置宽xxxpx" height="设置高xxxpx" frameborde="是否显示 iframe 周围的边框 1|0"></iframe>
	// 和锚链接结合起来利用 iframe的name值和a标签的target值相等时 可以做一个导航栏 跳到指定网页
	<a src="第一个网页地址" target="这个iframe的名字">标签名 一</a>
	<a src="第二个网页地址" target="这个iframe的名字">标签名 二</a>
	
```

#### 列表(无序列表)(有序列表)(自定义列表)、表格

```
	
	列表就是信息资源的一种展示形式 以便浏览者能更快捷的获得相应的信息
	
	所有行符号 不会影响特定行符号  行标签作用大于所有行符号
	表格是表格 列表是列表
	
	无序列表 每一项都是平级的没有级别之分并且内容都是相对简单的标题性的内容
	有序列表 一般用于带有顺序的编号的特定场合
	定义列表一般适用于带有标题和标题解释解释性的内容的场合
	表格标签 块级元素 用于显示表格数据简单通用 结构稳定(同行单元格高度一致且水平对齐 同列单元格宽度一致且垂直对齐)
	
```

```html
	
	<ul【type="所有行符号代码(circle空心圆 square实心正方形 disc实心圆 通常使用CSS来设置项目符号)"】>
		<li【type="这一行符号代码(同上 通常使用CSS来设置项目符号)"】>内容</li>
        <li>内容</li>
        <li>内容</li>
        <li>内容</li>
	</ul>

	//无序列表(有规律)   默认前面的行符号为小正方形块
	//ul标签中 只能(文字也不行) 嵌套li标签不能嵌套其它标签  li标签可以嵌套任意标签(可以再嵌套列表)
	
```

```html
	
	<ol 【type="所有行符号代码 (i、I 、A、a、1)"】 start="规定有序列表的起始值" reversed 倒叙(reversed="reversed" 同效果)>
        <li【type="这一行符号代码(同上 通常使用CSS来设置项目符号)"】>内容</li>
        <li>内容</li>
        <li>内容</li>
        <li>内容</li>
	</ol>
	
	//有序列表(有排序顺序)   默认1.2.3.4.5…… 
	//ol标签中  只能(文字也不行)  嵌套li标签不能嵌套其它标签  li标签可以嵌套任意标签(可以再嵌套列表)

```

```html
	
	<dl>
		<dt>内容</dt>	  声明列表项
		<dd>内容</dd>	  声明内容
		<dd>内容</dd>	  声明内容
		<dt>内容</dt>   声明列表项
		<dd>内容</dd>	  声明内容
		<dd>内容</dd>	  声明内容
	</dl>

	//自定义列表	什么都没有 是高度自定义的
	//在制作解释性导航栏时 dt和dd没有在一列 可利用css margin:0px; 让其处于一列
	
```

```html
	
	属性colspan用于跨列(横)  rowspan用于跨行(竖)  可以同时跨行跨列但是麻烦
	跨列、行代表所跨单元格变成跨格数
	
	表格标签  各单元格的宽度和高度互相影响，结构相对稳定单不能灵活的进行布局控制
	<table【border="2"表格边框的宽度，规范中已经废除了，后续使用css】>	表格标签
        <tr>
            <th>第一行第一列标题</th>标题会加粗
            <th>第一行第二列标题</th>
            <th>第一行第三列标题</th>
        </tr>
        <tr>	除去标题行标签 第一行
            <td>内容</td>	单元格内容  第一行第一列内容
            <td>内容</td> 第一行第二列内容
        </tr>
        <tr>	除去标题行标签 第二行
            <td>内容</td>	第二行第一列内容
            <td>内容</td> 第二行第二列内容
        </tr>
	</table>
	可以根据需要同时设置跨行和跨列
	
```

#### 表单元素

```
	
	表单在网页中应用比较广泛，如注册账号录入信息..
	将需要用户填写的内容放置在表单容器中 当用户点击容器时 表单将数据统一发送给服务器
	用地
	登录、注册、网上订单、调查问卷、网上搜索
	
```

```
	
	表单元素   
	input[type: 单行文本框(text)、密码框(password)、复选框(checkbox)、提交按钮(submit)、普通按钮(button)、重置按钮(reset)、单选框(radio)、多行文本域(textarea)、邮箱(email)、网址(url)、数字(number)、搜索(search)、文件域(file)、滑块(range)、列表框(select 、option)]
	
```

```html
	
	表单的控件通常放在
	<form action="URL(将表单上的信息发到Web服务器上 如果值为空默认提交到本页)" method="post|get(post方法提交方式不会改变地址栏状态 表单数据不会显示 get方法地址栏会变化 会显示表单数据)" name="表单名称(用于区分同一个页面的多个表单)" autocomplete="on/off(指定表单是否有自动完成功能 会将输入的历史显示在一个下拉列表中)" novalidate="true(取消对表单进行有效的检查 form表内的所有表单控件不被验证)">
	
		表单元素
	</form>

	//get方式不安全(还有数据量限制) post方式比较安全(无数据量限制)
	//action　可以为接收数据的ｅｍａｉｌ邮件地址/相对绝对路径/
	
```

```html
	
	input标签 对于表单元素而言name属性与id属性都是必须的，用于form处理和label关联。
	<input type="指定元素的类型" name(必须包括)="指定表单元素的名称" value="表单元素的初始值" size="指定文本框宽度(长度)type如果为text或者password类型，则表单元素的大小以字符为单位。对于其他类型，宽度以元素为单位" maxlength="在type为password或者text时，其中可输入的最大字符数" readonly disabled ...></input>
	input类型 不管type后面是什么类型   它都是行内元素

```

```html
	
	文本框  text  密码框  password(输入单行文本信息)
	在提交时 会将框内的name值和用户输入的值一起提交
	<input name="文本框" type="text"></input>普通的文本框
	<input name="密码框" type="password"></input>用户在输入框中输入的字符会变成黑点
	
```

```html
	
	单选框  radio 注意单选框和复选框的区别 复选框可以再次单击取消 单选框不能
	单选按钮用于一组相互排斥的值，组中每个单选按钮控件应具有相同的名称，用户一次只能选中一个单选按钮。
	在使用单选按钮时，必须需要一个显式的value属性
	在提交时，会将框内的name值和value的值一起提交
	<input type="radio" name="111" value="男"> 男
	<input type="radio" name="111" value="女"> 女
	拥有checked属性 有此属性的选项为 默认选项(只有一个)
	
```

```html
	
	复选框	 checkbox 注意单选框和复选框的区别 复选框可以再次单击取消 单选框不能
	复选框允许用户选择多个选项，命名可以多个复选框选用相同的名称，也可以各自具有不同的名字，关键是怎么用
	如果选项之间是并列关系，可以设置为相同的名称以便同时获取，提高效率，否则每个选项都需要进行读取。
	在提交时，会将复选框的name值和value值一起提交
	<input type"checkbox" name="111" value="选项一"> 选项一
	<input type"checkbox" name="111" value="选项二"> 选项二
	<input type"checkbox" name="111" value="选项三"> 选项三
	<input type"checkbox" name="111" value="选项四"> 选项四
	拥有checked属性 有此属性的选项为 默认选项(可有多个)
	
```

```html
	
	列表框(下拉列表) select option select标签至少包含一个option标签 行内元素
	列表框使用户快速、方便、正确地选择一些选项，并且节省页面空间 
	<select name="指定列表名字" size="确定列表中可同时看到的行数(不点开的情况下)" multiple="multiple(定义后会可以多项选择 方法为按住Ctrl的同时选择多项)"> 
		<option value="可选项的值1"></option>
		<option value="可选项的值2"></option>
        <optgroup>分组描述</optgroup>
		<option value="可选项的值3"></option>
		<option value="可选项的值4"></option>
	</select>
	//optgroup 可选标签将option分组
	拥有selected|selected="selected"属性 有此属性的选项为 默认选项(只有一个)
	
```

```html
	
	按钮 (普通按钮button)(提交按钮submit)(重置按钮reset)【图片提交按钮】
	按钮要和form结合使用
	<form method="提交的方式post|get" action="提交到的网址L">
		<input type="button" name="命名按钮" value="按钮上显示的字">
		<input type="submit" name="命名按钮" value="按钮上显示的字"> 
		<input type="reset" name="命名按钮" value="按钮上显示的字"> 
	</form>
	reset按钮   无论表单是否已经填写或输入数据，按钮所在form表单内的表单元素都会被重置到初始状态
	submit按钮  表单将会将填写的表单信息，提交到form表单action属性所指定的URL网址
	button按钮  需要与事件关联使用，例onclick="alert(this.value)"事件点击后会显示该按钮的value值
	【图片提交按钮】<input type="image" src="图片路径" name="命名按钮" 没有value属性> 虽然type不是submit但还是具有提交功能
	
```

```html
	
	datalist 定义输入框的选项列表(option元素创建) 通常与input配合定义input的取值 需要给datalist起id名 为input元素指定list属性 指向datalistID
	
	<input type="text" list="ID">
    <datalist id="ID">
        <option value ="可选项的值1"></option>
        <option value ="可选项的值2"></option>
    </datalist>

```

```html
	
	多行文本域 textarea  行内元素
	允许在网页中输入两行或两行以上的文本
	在提交时，会将框内的name值和用户输入的值一起提交 标签中不能使用value属性来赋初始值
	<textarea name="表单元素名称" cols="显示的列数" rows="显示的行数">
		如果此处写了内容则就是默认内容
	</textarea>

	//使用 width 和 height 定义文本域大小 不要用clos 和 rows 因为不同浏览器的规范可能不同
	
```

```html
	 
	文件域 file
	用于实现文件的选择，应用于上传文本、图片
	<input type="file" name="表单元素名称"/>
	文本域在不同浏览器中显示效果不一样，但功能一样，后续可以用css更改
	使用时，由于提交的表单数据包括普通的表单数据 文件数据等等 所以必须设置表单的enctype编码属性为
	multipart/form-data
	
```

```html
	
	邮箱 email
	专门用于输入Email地址的文本框，会自动验证email文本框的值，如果格式不正确，则不允许提交表单
	<input type="email" name="表单元素名称"/>
	
```

```html
	
	网址 url
	用于输入url地址的文本框，会自动验证url文本框的值，如果格式不正确，则不允许提交表单
	<input type="url" name="表单元素名称"/>
	注意不要漏掉前面的协议 http:// 输入网址时最好加上s   https s一种标准
	
```

```html
	
	数字 number
	用于输入数字的文本框，会自动验证输入是否合法
	<input type="number" name="表单元素名称" min="允许的最小值" max="允许的最大值" value="规定的默认值" step="规定和法的数字间隔" />
	
```

```html
	
	滑块 range
	用于输入包含一定范围内的数字值的文本框，在网页中显示为滑动条 (和number类型一样，只是外观表现不同)
	<input type="range" name="表单元素名称" min="允许的最小值" max="允许的最大值" value="规定的默认值" step="规定和法的数字间隔" />
	不支持range类型的浏览器会显示为普通的纯文本框 当做text及处理 可以放心使用 
	
```

```html
	
	搜索框 search
	用于搜索关键词的文本框
	<input type="search" name="表单元素名称"/>
	search类型提供的搜索框不只是Google或百度的搜索框 而是任意页面的一个搜索框
	
```

#### 表单的高级应用和初级验证

```html
	高级应用和初级验证
	
	高级应用
	
	隐藏域
	用于隐藏一些信息 如用户登录后的用户名、用于区别不同用户的id等等
	在浏览器中看不到隐藏域，但是在提交表单时隐藏域的内容被提交至服务器
	<input type="hidden" value="值" name="表单元素名称">
	
	表单元素的标注 label
	增强鼠标的可用性 不一定要在表单里面
	用户使用鼠标单击标注的文本内容时  浏览器会自动将焦点跳转到与该标记相关的表单元素上
	对于表单元素而言name属性与id属性都是必须的 name属性由表单负责处理 而id属性是给label便签进行关联用的
	<label for="标注的表单元素id">标注的文本或图片</label> 
	
	【w3c 对于布尔值的属性 属性值可以省略】例 selected="selected" 写selected 默认属性值为true
	
	对文本框内容只读 readonly 属性 
	不希望用户修改的数据对文本框
	
	禁用 disabled 属性 
	禁用此按钮或只有满足某个条件后才能选用某项功能对按钮
	
```

```
	初级验证
	
	提示文本框输入内容 placeholder 属性   占位提示信息
    在输入为空时显示 写入内容时消失
	
	规定文本框内容不能为空 required 属性  非空
    如果为空不允许用户提交表单
	
	验证 pattern属性  匹配模式
	可以减轻服务器压力
    用于验证input类型文本框中用户输入内容是否与自定义表达式相匹配
	例 pattern="^1[358]\d{9}" 输入的需要满足 以13、15、18开头的11位数字
	
```

### 次要功能标签

#### 有一点点用处的标签但是又可以代替的

```html
	
	<pre></pre> 内容原格式输出 标签正常显示 代码内的空格 //还是不同可能是字体问题 可记事本排版
    <font size="字体大小px" color="字体颜色red"></font> 设置字体 行内元素 不推荐使用
	<bdo dir="rtl(right to left 默认ltr)"></bdo> 设置文本的显示方向
	<figure></figure> 用于对元素进行组合 多用于图片与描述组合
	<mark></mark> 马克笔背景颜色标记 background-color 改颜色
	<small></small> 定义小号字体
	<ins></ins> 定义插入的字(待入输入下划线) 和下划线效果一样 意思不一样
	<sub></sub> 下标 圈在哪就是那边的标
	<sup></sup> 上标
	<cite></cite> 引用标记标签 用于文档参考文献的引用说明 内容会以斜体的样式显示s
	<progress value="已完成进度条" max="进度条总量"></progress>  进度条
	
```

##### 用到现查

```
	
	canvas 标签
	meter 元素 表示指定范围内的值
	time 元素用于定义时间或日期没啥用
	
```

#### 分组元素(不常用了解)

##### figure标签

```html
	
	<figure>
		<figcaption></figcaption>
	</figure>
	
	//figure 标签规定独立的流内容（图像、图表、照片、代码等等）
	//figcaption 为figure增加标题 仅能有一个
	
```

##### hgroup标签

```html
	
	<hgroup>
		<figcaption></figcaption>
	</hgroup>
	
	//用于将多个标题组成一个标题组
	//figcaption 为hgroup增加标题
	
```

#### dialog对话框或者窗口

```html
	
	<dialog> 
        <dt>左</dt> dialog下级标签 内容向左对齐
        <dd>右</dd> 内容向右对齐
    </dialog> 

	//定义对话框或者窗口 在chrome浏览器中需要设置属性open值为true	

```

#### details描述控件


```html
	
	<details> 
        <summary></summary> 
    </details>
	
	//交互式描述控件 定义元素的细节 
	//summarys为details标签定义标题
	
```

#### meta标签

```html
	
	<meta http-equiv="refresh" content="3;url=网页地址" > 3秒刷新页面 转到url的网址
	<meta name="description" content="kkk"> 百度引擎搜索描述
	
	//meta用于定义页面的元信息 通过名称/值 的形式成对的使用其属性可定义页面的相关参数 多用于网络优化
	／／...其它度娘
	
```

#### 特殊符号标记

```
	
    &nbsp;   空格 
	&lt;   小于号(<)
	&gt;   大于号(>) 
	&copy;   版权符号(©) 
	&quot;   引号(")
	
```

### 全局属性(了解)

```
	
	draggable属性 定义元素是否可以被拖动 属性有两个值true和false(默认) //需要配合js才能真正拖动
	hidden属性 隐藏元素true/false 装载后可以通过js将该属性取消
	spellcheck属性 主要用于textarea和input标签 对用户输入的文本进行拼写语法检查(红色波浪线) 属性值true/false
	contenteditable属性 规定是否可以编辑元素的内容 
		//属性值true/false 
		//这个很有意思 可以更改p(栗子)上面的网页内容
		//当元素中没有设置 contenteditable 属性时 元素将从父元素继承
	
```

