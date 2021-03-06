```
	2022年4月4日11:18:30创建
```

# 目录

[TOC]

# Numeraton system

## 简写表

```
	
	//此处为简写 内容 例子 Hello > H 某些特殊情况下全写
	
```

## 进制基础

```
	
	数制
		每一位的构成
		从低位向高位的进制规则(逢几进一)
	
	常见进制 二进制 八进制 十进制 十六进制
	//生活中常用10进制
	
	任意一个进制都是 从0开始数 例如 2进制 取值是 0 1
	
	
```

### 基数(radix or base 简写为r)

```
	
	一个数字系统中 数的个数 称为基数 从0开始
	
	// 0 1 二进制 基数为 2 r=2
	// 0 1 2 3 4 5 6 7 8 9 十进制 基数为10 r=10
	
```

### 二进制(binary)

```
	
	每个位的取值范围是0 到 1 当超过1时 就需要进位
	
	
	0 1 10 11 100 101 110 111 1000 ......
	    2^1   2^2             2^3
		//2的几次方 就是后面带了几个0 
		//2^n 是n+1位数的最小值
	
	0 1 10 11 100 101 110 111 1000 ......
		//2^1-1 = 1   2^2-1= 11   2^3-1 = 111 
		//(2^n)-1 是n位数的最大值
	  
	
	
```

### 八进制(octal)

```
	
	每个位的取值范围是0 到 7 当超过7时 就需要进位
	
```

### 十进制(decimal)

```
	
	个位的取值范围都是0 到 9 如果表示比9大的数字 那就需要进位
	
	//可以写成多项式的形式
	194.32 = 1*10^2 + 9*10^1 + 4*10^0 + 3*10^-1 + 2*10^-2
	
	//在此权指的是
	10^2 10^1 10^0
	//二进制则为
	2^2 2^1 2^0
	
```

### 十六进制(hexadecimal)

```
	
	十六进制就是逢16进1 但我们只有0 到 9这十个数字 所以我们用A,B,C,D,E,F这六个字母来分别表示10 11 12 13 14 15字母不区分大小写   
	例如 十进制的15 用十六进制表示就是F
	
	//经常用来描述 计算机存储器的地址空间
	
```

## 进制运算

### 二进制

```
	
	0 + 0 = 0
	0 + 1 = 1
	1 + 0 = 0
	1 + 1 = 10
	
```

## 进制转换

```
	
	https://jingyan.baidu.com/article/495ba84109665338b30ede98.html
	任何进制转成10进制 就是通过位权法 之后通过10进制加分加起来
	十进制转换成其它进制 
		//整数部分 除以基数 取余 直到商为0 取不够的余它本身 之后结束 逆序
		//小数部分 乘以基数 取整 顺序 取得越多越准确 但是不知道用不用
		
		例 39十进制转2进制 除二取余法
			39%2 余1
			19%2 余1
			9%2 余1
			4%2 余0
			2%2 余0
			1%2 余1
			0
			100111
		
```

### 二转十

```
	
	位权法
	10010110=1 * 2^7 + 1* 2^4 + 1 * 2^2 +1 * 2^1=150 
	
	//算1就好 之后用10进制加起来就是十进制数
	//位权指的是 2^7 2^4 2^2 
	
```

### 十转二

```
	
	除二取余法
	
	//二的几次方 就是后面带了几个0
		128 = 2^7 = 10000000 //8位数中 最小的数
	//二的几次方-1 就是有几个1
		255 = 2^8 - 1 = 11111111 //8位数中 最大的数
	
	
```

### 二转八

```
	
	8 = 2^3 一位八进制数可以用 3位二进制数表示
	//以小数点为界向两侧划分 三位一组 不够添0
	
	例 
		1101110011.1011 
		划分001 101 110 011 . 101 100
		001是1  101是5 110是6 011是3 . 5 4
		转为8进制则为1563.54
	
```

### 八转二

```
	
	1563 转 二进制
	
	1是 001 
	5是 101
	6是 110
	3是 011
	
	001101110011  //两端的0可以去掉
	1101110011
	
```

### 八转十

```
	
    位权法
	
	326.4(8进制) 位权之后 用十进制加起来
	= 3 * 8^2 + 2 * 8^1 + 6 * 8^0 + 4 * 8^-1 
	= 192 + 16 + 6 + 0.5
	214.62(10进制)
	
```

### 十转八

```
	
	除八取余
	179转8进制 
	179%8 余3
	22%8 余6
	2%8 余2
	0
	八进制263
	
```

### 二转十六

```
	
	16 = 2^4 一位十六进制数可以用 4位二进制数表示
	//以小数点为界向两侧划分 四位一组 不够添0
	
	1010111101101.
	
	//划分
	
	0001 0101 1110 1101
	1	 5    E    D   
	
	十六进制为15ED
	
```

### 十转十六

```
	
	178转16进制
	178%16 余2
	11%16 余11(B)
	0
	B2
	
```

## 代码码制

### 代码

```
	
	代表信息的数码 称为代码(Code) 常用在计算机和数字系统中处理、存储以及传输各种信息
	
```

![](Images\进制码制\进制列举表.jpg)

#### BCD码

```
	
	用四位 二进制数 中的任意 十种 组合 表示一位 二进制数
	即 二 - 十 进制代码
	
	BCD //binary coded decimal 二进制编码的十进制
	*//用 四位二进制数 可以表示 2^4 16种状态 但是十进制只用0~9 所以有很多种表示状态
	
	
```

#### 8421BCD码(十进制)

```
	
	8421 //指的是 0 0 0 0 四位上的 权值 
	//每一位的 权值都是不变的 所以他是 恒权码 
	//使用最广泛的 BCD码 因为其位权 与 二进制位权相同
	//BCD 还包括 2421BCD 4221BCD 5421BCD 都是有权码 
	//注意脚标必须写 (1001 0101 0010)脚标8421BCD
	*//十进制 与 8421BCD 之间可以直接转换
	*//二进制与BCD码不能直接转换 要先转成十进制
	
	像 二进制0 1 0 1 表示的 但是 是10进制
	
	*//编码规律 按排列顺序逐个 加1
	*// 0000 - 1001 表示0-9
	
	0000 0001 0010 0011 0100  0 - 4
	0101 0110 0111 1000 1001  5 - 9
	0001 0000  10 //10进制进 4格子
	0001 0001  11
	....
	
	*//8421BCD 1010-1111为禁用码 因为只用0~9
	
	85.67(十进制) 转 8421BCD
		1000 0101 . 0110 0111
		
	0111 0010 0110 1000 . 1000 0011(8421BCD)转10进制
		7 2 6 8 . 8 3
	
	(0001 1000)8421BCD 转 十进制
		18
		再转2进制10010
	
	(00011000)2 转 十进制
		2^3 + 2^4 = 8 + 16 = 24 
	
```

#### 格雷码(The Gray Code)

```
	
	//任意两个相邻码之间只有 只有一位不同 传输过程中误差较小
	//无权码 是循环码 
	
	
	0000 0001 0011 0010 0110 0111 0101 0100 0 - 7
	1100 1101 1111 1110 1010 1011 1001 1000 8 - 15
	
	//记忆 
		最低位 首末各1个0 然后2个1 2个0
		次低位 首末各2个0 然后4个1 4个0 4个1
		次高位 首末各4个0 中间8个1
		最高位 8个0 8个1
	
```

#### 余3码

```
	
	将8421码 的 前三个 和 后三个 代码去掉 用其余的0011 - 1100 代表0-9
	
	0011 0100 0101 ... 
	
```

#### 余三循环码

```
	
```

## 可靠性编码

```
	
	能减少错误 发现错误 甚至纠正错误 的编码称为可靠性编码
	
	纠错的三个层次
		编码本身不易出错 - 格雷码
		出错能检查出来 - 奇偶校验码
		检查并能纠错 - 汉明码
	
	//纠错是以 增加硬件为代价的
	
```

## 原码 反码 补码

```
	
	二进制的数 和 符号 都用二进制表示 用最高有效位表示数的符号 0是整数 1是负数
	8位 字长可以表示256个数(无符号) 有符号数-128~+127
	将一个 符号 用数值化 表示 这样的 数称为 机器数
	用补码表示数 计算机 的加减法中 不用判断数的正负 符号位参加运算就能自动得到正确的结果
	
	无符号
	
        原码 Sign-magnitude 二进制数

            //例 (13)10 = (1101)2  1101就是13的原码

        反码 1' s complement 


            //原码 全部取反 1变成0 0变成1 为该二进制数的反码
            //例 原码1011010 反码0100101
            //例 原码1101 反码0010

        补码 2‘ s complement

            //反码末位加1(*数) 就为该 二进制数的补码 
            //例 原码1101 反码0010 补码0011 //注意是加数 不是加1位1
            
            
	有符号
		
			最高位 为符号位 0为正 1为负
	
            +89 = 0 1011001
            -89 = 1 1011001(原码)


            正数 的 反码  补码 都是一样的

            负数(-64) 的  
                //原码  
                1 100 0000 //二进制是8bit
                    //1(符号位)(一) 
                    //1(二) //64是2的6次幂 
                    /0(余位)
                //转反码 最高位不变其它位相反
                1 011 1111 
                //补码 反码加1
	
```

### 由原码直接求补码(x*)

```
	
	从右侧数 第一个1不动 向左依次求反
	
		//例 原码1101 补码0011
		//反码 求 反 为 原码
		//补码 求 补 为 原码 
			//补码0011 先转反码 1100 求补码 1101 //1101为原码
	
```

## 练习

```
	
	二进制B转十
		1101.01B  8 + 4 + 1 + 0.25 = 13.25
		101011.0101B 32 + 8 + 2 + 1 + 0.25 + 0.625 = 43.3125
		
	十六进制转十
		A3H  10*16^1 + 3*16^0 =  163
		129.CH 1*16^2 + 2*16^1 + 9 + 12*16^-1 = 256 + 32 + 9 + 0.75 = 297.75 
		
	十进制 转 二 转 八 转 十六
		23 
			10111B
            010 111B 三划分  27Q 
            0001 0111B 四划分 17H
		107 
			1101011B
			001 101 011 三划分 153Q
			0110 1011 四划分 6BH
	
	十进制数转换为 8位 有符号 二进制数
		有符号就是最高位 0是正 1是负
		+32
			原码 = 反码 = 补码 00100000B //正数的反码补码都一样
			
		-12
			原码 10001100B 
			反码 11110011B //最高位不变其它相反 
			补码 11110100B //反码+1
			
		+100
			原码 = 反码 = 补码 01100100B
			
		-92
			原码 11011100B
			反码 10100011B
			补码 10100100B
		
	二进制转换为有符号十进制数
		10000000B 
			上原码 -0
		00110011B
			+51
		10010010B
			上原码 -18
		10001001B
			上原码 -9
		
	十进制转为 压缩BCD 与 非压缩BCD
		93 
			1001 0011
			00001001 00000011
	
```



## 备录

```
	
	33/3 = 11 十进制 3 * 11 按10进制加起来
	41/3 = 13 八进制 13 * 3 按8进制加起来
	
```



```
	
	//取消 度娘栏 简化内容 笔记只 记录 重要的纲要结构 自己读懂就好 但是要有良好的纲要结构 保持高度可读性
	/总结的图片 最后是学完之后或者 有大部分内容了之后 凭借感觉选的图
	
```

