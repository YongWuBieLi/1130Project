```
	2021年10月13日20:32:54创建
```

# 目录

[TOC]

# DataBase

## 基本定义

### 信息

```
	
	信息 就是 新的 有用的事实 和 知识
	能够在 空间(上传递信息 称为 信息通信) 和 时间(上传递信息 称为 信息储存) 被传递 
		 
```

### 数据

```
	
	数据是用于 载荷 信息的 物理符号
		数据有 形 和 值 之分
		数据受 数据类型 和 取值范围的 约束
        数据有 定性表示 和 定量表示 之分
        数据应具有 载体 和 多种表现形式
		
```

### 数据库系统(DBS)

```
	
	包含 数据库 和 数据库管理系统
	
```

#### 数据库发展历史

```
	
	数据库的发展历史经历了人工管理 文件系统  数据库系统 三个 发展阶段 
	
		人工管理数据(数据不保存 数据需要由应用程序自己管理 没有相应的软件系统负责数据的管理工作 数据不共享 数据不具有独立性)
		文件系统(数据可以长期保存 由专门的文件系统 进行 数据管理 数据共享性差 数据独立性低)
		数据库系统(数据结构化 数据独立性高 数据由DBMS统一管理和控制 数据的共享性好冗余度低)
			和文件方法相比 
				数据库中的数据具有 数据整体性
				数据库中的数据具有 数据共享性(多个用户共享数据库资源)
	
```

#### 数据库的类型

```
	
	层次模型() 网状模型() 关系模型() 
		//之间的根本区别 数据之间 联系 的 表示方式 不同
	
	非关系型数据库(层次型 网状型) MongoDB  redis  HBase
	关系型数据库 SQLite ORACLE(ORACLE) MySQL(ORACLE) DB2(IBM) Sybase(Sybase) SQLserver(Microsoft)
	
```

#### 数据库(Database 简称DB)

```
	
	数据库 
		//是按数据结构 存储和管理 数据的 计算机软件系统
		//期存放在计算机内 有组织 可共享的大量数据的集合 是数据的仓库
		//储存的基本对象是数据表
		//数据库数据独立性 包括 逻辑独立性 物理独立性
		//保证数据库的 数据独立性 需要修改 三级模式之间的两层映射
	
```

#### 数据库管理系统(Database Management System)(DBMS)

```
	
	是数据库系统的核心
	数据管理软件	科学组织存储数据 高效获取 维护数据
	专门 管理 数据库 的 计算机系统软件 为数据库 提供 定义 建立 维护 查询 统计 完成 数据完整性 安全性 控制 
    
    由 计算机硬件 数据库 数据库管理系统 应用软件 数据库管理员  组成
    
    DBMS 进行 数据控制
    数据的安全性控制(保护数据库) 数据库的完整性控制(数据的正确性 有效性 相容性) 数据的并发控制(提供用户并行使用数据) 数据恢复(定期做备份)
     
```

## 数据模型(Data Model)

```
	
	是对现实世界数据 的 模拟 和 抽象 是数据库系统 用于提供信息表示 和 操作手段的形式构架
	//作用 确定系统 中数据的 定义和格式 使人更容易理解 便于在数据库系统 实现
	
	树形结构 是 层次模型
	二维表 是 结构关系模型
	
```

### 数据模型的类型

```
	
	概念数据模型(Conceptual Data Model) //描述现实世界数据 的 概念化结构
	逻辑数据模型(Logixal Data Model) //数据库中看到的数据模型 主要包括层次数据模型 网状数据模型 关系数据模型
	物理数据模型(Physical Data Model) //考虑数据在物理上如何实现 实现工作由系统自动完成 数据在储介质的组织结构
	
```

### 数据模型的三要素

```
	
	数据模型描述了系统的 
		数据结构(静态特征) //数据的类型 内容 性质 数据间的关系
		数据操作(动态特征) //增删改查 
		完整性约束条件 //数据之间相互的制约 和 依存关系
	
```

### 数据库三级模式

```
	
	内模式(有一个) 外模式 概念模式
	保证 数据库的 数据独立性 需要修改 三级模式之间的两层映射
	
```

## 关系数据库

### 关系的完整性

```
	
	实体完整性 参照完整性 用户定义完整性
	
```

### 关系操作

```
	
	分为		查询 插入 修改 删除	//主要是查询操作
	
```

#### 查询操作

```
	
	分为		除 并 差 交 选择 投影 连接 笛卡尔积
	//基本操作 选择 投影 并 差 笛卡尔积
	
```

#### 关系代数

##### 关系代数运算符

```
	
	集合运算符
		∪   并
		-	差
		∩	交
		x	笛卡尔积 //就是握手问题 每行互乘
	
	
	专门关系运算符
		σ	选择 	//相当于WHERE
		Π	投影	//相当于SELECT
		⋈   连接  //相当于JOIN 自然连接 两个表 //在自然连接中被舍弃的元祖 称为悬浮元组
		÷	除
		
```

###### σ	选择

$$
查询信息系全体学生\quadσ_{系别字段="信息系"}(表名)
$$

###### Π	投影	

$$
选择显示列\quadΠ_{字段名\quad字段名}(表名)
$$

##### 条件表达式运算符

```
	
	比较运算符
	
        > < = 等
        <> 不等于
        
	逻辑运算符
	
        ㄱ	非
        ∧	与
        ∨	或
	
```

## 并发

```
	
	并发不加以控制 会导致数据不一致
	封锁机制 是 并发控制的主要方法
	
```

## 数据库的设计

```
	
	良好的数据库设计要求 //在数据库比较复杂的时候需要设计数据库
	尽量减少数据重复 保证数据完整性 满足应用系统开发需求
	
	需求分析 物理设计 概念设计 逻辑设计 数据库实施 数据库运行与维护
	
	需求分析 分析客户的业务和数据处理需求
	概要设计 设计数据库的E-R模型图 确认需求信息的正确和完整
	详细设计 应用三大范式进行优化审核数据库结构
	代码编写 使用编码语句数据库 编码实现应用
	软件测试 ......
	安装部署 ......
	
	需求分析
        数据库设计 4 个步骤
        收集信息 收集用户数据需求
        标识实体 一般是名词 是数据库主要描述的事物
        标识实体属性 一般是名词 是与事物相关的具体描述信息
        标识实体之间的关系 一般是动词 描述实体之间的业务关系
	
	概要设计 //E-R图中 长方框 为实体 椭圆框 为属性 菱形框 为关系 直线用来连接属性和实体集 还有实体集和关系集 直线可以有方向 用来表示联系集的映射基数 (实体关系图)(Entity-Relationship)
        画出E-R模型图 建立实体间映射基数 并最终转换为数据库关系模型
        根据实体间映射基数 在E-R图中标出实体间数量映射关系
        将E-R模型转换为R(U)关系模式 实现实体间联系转换 将数量映射关系转换为 主-外键 关系
        //R(U)关系模式就是 用二维表的形式表示实体和实体键联系的数据模型
        在实体中添加主键属性 唯一标识出一条记录 在对于一对多映射关系在 多方实体中添加外键	
        最后将R(U)关系模式转换为数据库关系模型
   
    详细设计阶段 
    使用三大范式规范数据库设计 减少数据冗余 避免数据添加、更新、删除异常
	
	多表之间的关系(映射基数) //一对多关系多对一关系 都是以参照物说的 通常以从左向右的角度判断映射关系
	 一对一(了解) --例 人和身份证 一个人只有一个身份证 一个身份证只能对应一个人
	 一对多(多对一) --例 部门和员工 一个部门有多个员工 一个员工只能对应一个部门
	 多对多 --例 学生和课程 一个学生可以选择很多门课程 一个课程可以被很多学生选择
	实现关系
	 一对多(多对一)
	  在多的一方建立外键 指向一方的主键
	  把联系数量为1的实体的主键放到联系数量为N的实体关系模式中
	 多对多
	  多对多关系实现需要借助 第三个中间表 中间表至少包含两个字段 这两个字段作为第三张表的外键 分别指向两张表的主键
	 一对一(了解)
	  一对一关系实现 可以在任意一方添加唯一外键指向另一方的主键 
	
	代码编写 使用编码语句数据库 编码实现应用
	
	 创建数据库表的步骤
	  确定表中有哪些字段
	  确定每字段的数据类型 //如果向表中插入数据时 超出该字段的取值范围 则插入的值被截断并显示警告信息
	  给表添加各种约束
	  创建各表之间的关系
	
	软件测试 ......
	安装部署 ......
	
```

### 数据库的范式

```
	
	设计数据库时 需要遵循的一些规范 要遵循后边的范式要求 必须先遵循前边的所有范式要求
	
	规范数据库 是为了消除 数据冗余
	
	设计关系数据库时 遵从不同的规范要求 设计出合理的关系型数据库 这些不同的规范要求被称为不同的范式 各种范式呈递次规范 越高的范式数据库冗余越小 但也会造成数据库性能下降 有时需要专门添加一些冗余设计来满足数据库性能要求 一般数据库需要满足第二范式 根据需要来决定是否满足第三范式 需要通过数据库规范性和性能之间的关系 进行综合考虑
	
	目前关系数据库有六种范式
	第一范式(1st NF)  第二范式(2nd NF)  第三范式(3rd NF)  巴斯-科德范式(BCNF)
	第四范式(4NF)   第五范式(5NF 又称完美范式)
	
	第一范式(1NF) (有主键 每一个列都是不可再分割的数据项)
	
		//每一列都是不可分割的原子数据项 由业务决定 必须有主键
		例	学生表 (不满足) //没有主键 有列不是最小数据列
                学生编号 | 学生姓名 | 学生联系方式 
                1	xxx xxx.163,130xxxxxx
			
        例	学生表 (满足)
                学生编号(pk) | 学生姓名 | 邮箱 | 电话 
                1	xxx xxx.163	130xxxxxx
		
	第二范式(2NF)(不要有部分依赖) --多对多 三张表 关系表两个外键
	
		//在1NF的基础上 非码属性必须完全依赖于码(在1NF基础上消除非主属性对主码的部分函数依赖) 
		//一张表只描述一件事情 除了主键以外的其它字段 都依赖于主键
            例	表(不满足) //不满足满足第第一 第二 范式 //没有主键
                    学生编号 | 学生姓名 | 教师编号 | 教师名称
                    1	xxx 001	xxx
                    2   xxx 002 xxx
            例	表(不满足) //满足第一范式(复合主键) 不满足第二范式 //一个学生可能有个老师 会产生数据冗余空间浪费
                     学生编号 + 教师编号(pk) | 学生姓名 | 教师名称
                     1 001 xxx xxx
                     2 002 xxx xxx
                     1 002 xxx xxx
            例	//为了以表满足 第二范式 需要 使用三张表 来表示多对多的关系
                 学生表
                     学生编号(pk) | 学生姓名
                     ...
                 教师表
                     教师编号(pk) | 教师姓名
                     ...
                 学生教师关系表
                    id(pk) | 学生编号(fk) | 教师编号(fk)
                    ....
       
	第三范式(3NF) (不要产生传递依赖) --一对多 两张表 多的表加外键
	
		//在2NF基础上 所有非主键字段必须直接依赖主键 不要产生传递依赖(在2NF基础上消除传递依赖)
   	    //表中各列必须和主键直接相关 不能间接相关  表中除了主键外的字段 都直接 依赖于主键
			例	一对多关系表(不满足) //没有消除传递依赖
                    学生编号(pk) | 学生姓名 | 班级编号 | 班级名称
                    1	xxx 001	xxx
                    2   xxx 002 xxx
            例	一对多关系表(满足) 
            		学生表
                        学生编号(pk) | 学生姓名 | 班级编号(fk)
                        1	xxx 001
                        2   xxx 002
                    班级表
                    	班级编号(pk) | 班级名称
                    	001	xxx
                    	002 xxx
    
    //对不满足三大范式的表进行拆分
    
    函数依赖  A-->B,如果通过A属性(属性组)的值，可以确定唯一B属性的值 则称B依赖于A
            完全函数依赖  A-->B 如果A是一个属性组 则B属性值的确定需要依赖于A属性组中所有的属性值 
            部分函数依赖  A-->B 如果A是一个属性组 则B属性值的确定只需要依赖于A属性组中某一些值即可
            传递函数依赖  A-- >B  B -- >C 如果通过A属性(属性组)的值 可以确定唯一B属性的值 再通过B属性(属性组)的值可以确定唯一C属性的值, 则称 C 传递函数依赖于A

		码 如果在一张表中 一个属性或属性组 被其他所有属性所完全依赖 则称这个属性(属性组)为该表的码
			主属性 码属性组中的所有属性 	非主属性 除过码属性组的属性
    
```

### 数据库设计最重要的理念

```
	
	一切都是为了实现客户的需求
	三范式 是理论上的 有时候会用 冗余换执行速度	//因为表和表之间连接次数越多 效率越低 因为要做笛卡尔积
	//有的时候 可能会存在冗余 但是为了减少表的连接次数 这样也是合理的 并且对于开发人员来说 sql语句的编写难度也会降低
	
```









