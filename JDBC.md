```
	2019年5月29日08:43:59创建
```

# 目录

[TOC]

# JDBC

# 软件开发三层架构

## 表示层(UI) 业务逻辑层(BO) 数据访问层(DAO)

```
	
	表示层 系统最外层 提供软件系统与用户交互的界面 负责接收用户输入将输出呈现给用户以及访问安全性验证
	
	业务逻辑层 负责数据处理和传递 组合底面 数据访问层 组成完整业务逻辑
	
	数据访问层 提供多个原子性的DAO操作 添加 删除 修改 等
	
	可以开发效率和质量大幅度提升 业务和表现逻辑层分离 构架结构更加清晰
	提高代码复用性 和 可维护性 减低代码依赖
	
```

## JDBC的基本介绍	

```
	
	Java DataBase Connectivity //Java 数据库连接 //Java语言操作数据库
	
	JDBC 是Java 数据库连接技术 的简称 提供连接各种常用数据库的能力
	
	JAVA < JDBC > 数据库服务器
	
	JDBC本质是 官方(sun公司)定义的一套操作所有关系型数据库的规则,即接口 //规范定义接口
	各个数据库厂商去实现这套接口,提供数据库驱动jar包
	我们可以使用这套接口(JDBC)编程,真正执行的代码是驱动jar包中的实现类
	
```

## 两种常见驱动方式

```
	
	在个人开发与测试中 可以使用JDBC-ODBC桥联方式
 	在生产性开发中 推荐使用纯JAVA驱动方式
	
  第一种主用方法
  
	纯JAVA方式连接数据库 JDBC
	 由JDBC驱动直接访问数据库
	 优点 完全JAVA代码 快速 跨平台
	 缺点 访问不同的数据库需要下载专用的JDBC驱动 JDBC只对应一种数据库 甚至只对应某个版本的数据库
 
 第二种方法 //了解 详细实践百度  https://blog.csdn.net/cn130404/article/details/74370377
    
 	将对JDBC API的调用 转化为对另一组数据库连接API的调用
 	优点 可以访问所有ODBC可以访问的数据库
 	缺点 执行效率低 功能不够强大
	
	Class.forName("sun.jdbc.pdbc.JdbcOdbcDriver");//加载驱动
	Connection A = DriverManager.getConnection("jdbc:odbc:myDB","用户名","密码");
	
	JAVA应用程序 - JDBC API - JDBC-ODBC桥 -- ODBC API - ODBC层 -数据库 了解 
	
```

## JDBC工作原理

```java
	
	JDBC API   //API应用程序编程接口 (Application Programming Interface) 目的是提供应用程序开发人员基于某软件或硬件访问或调用一组功能的能力 不需要访问源代码 只需要改变表示层
	
	提供 Sun公司
	内容 供程序员调用的接口与类,集成在java.sql和javax.sql包中
	 //如DriverManager类 Connection接口 Staterment接口 ResultSet接口
PreparedStatement接口
	作用 主要做三件事 与数据库建立连接 执行SQL语句 处理结果
	 DriverManager 依据数据库的不同 管理JDBC驱动
	 Connnection 负责连接数据库并担任传送数据的任务 //具体的实现类由数据库的厂商实现
	 Statement 由Connection产生 负责执行SQL语句 //可能受到 SQL语句注入攻击
	 ResultSet 负责保存Statement 执行后所产生的查询结果 结果集接口 封装查询结果
	 PreparedStatement Statement的子接口 也有Connection产生 负责执行SQL语句 它与Statement接口相比更具有 高安全性 高性能 高可读性 高可维护性的优点 //它是一个预编译的SQL语句
	 
	 
	DriverManager //驱动程序管理器 //作用于用户和驱动程序之间
	提供 Sun公司
	作用 管理各种不同的JDBC驱动 告诉程序该使用哪一个数据库驱动
	注意 mysql5(JDBC3)之后的驱动jar包可以省略注册驱动的步骤
	
	JDBC驱动
	提供 数据库厂商
	作用 负责连接各种不同的数据库
	
	Java应用程序 <--> JDBC API [JDBC Driver Manager >> JDBC驱动根据数据库连接不同的数据库驱动 <--> 数据库]
	
```

## DAO模式(DataAccessObject)

### 解释

```
	
	Data Access Objects 数据库存取对象 位于业务逻辑和持久化数据之间 实现两者的分离 实现对持久化数据的访问
	
	将数据库操作都封装起来 对外提供相应的接口
	
	持久化就是将程序在瞬时状态和持久状态下转换的机制 JDBC是一种持久化机制 将程序直接保存成文本文件也是持久化机制的一种实现
	
```

### 目的(优势)

```
	
	随着项目规模扩大和业务的复杂 将一个软件分成多个层次进行开发 化大为小 分而治之 目前软件开发一直使用的方法
	程序持久化操作可能保存到不同的数据库中 Oracle DB2 等等 另外业务代码和数据访问代码耦合在一起 代码结构不清晰 可维护 可读性 低
	
	提高软件开发效率 缩短软件开发效率的有效方法
	
	完全分离 数据访问代码和业务逻辑代码
	
	隔离了不同数据库实现
	
```

### 实现原理

```
	
	定义统一抽象的API 
	将操作数据的代码抽象成接口
	业务类调用这些接口就可以实现对数据的访问
	
```

### 实现规化

```
	
	根据规划条数 简化书写
    
    创建工具类  创建对应数据库类(继承 BaseDao 实现 操作类)  
	
	把 用户名 密码 URL 驱动类 几个字符串定义成常量  存到String字符串调用 或者 创建.properties配置文件
	利用方法进行导入
	
	创建共同父类提取其共同操作方法 构成 接口
	
	尽量以对象为单位 而不是以属性为单位传递参数 //以属性传参 会导致参数个数过多 增加接口和实现类中方法的数量
	
```

### 实现概括(主要类概括)

```java
	
	主要类 和其中方法(仅作参考) 遵循Java抽象化原则 (SOLID原则)
	
	一个典型的DAO模式主要由一下几部分组成
	DAO接口 把对数据库的所有操作定义成抽象方法 可以提供多种实现
	DAO实现类 针对不同数据库给出DAO接口定义方法的具体实现
	实体类 用于存放与传输对象数据
	数据库连接和关闭类 避免了数据库连接和关闭代码的重复使用 方便修改
	
	数据库连接简化类(所有DAO类的父类)(加载数据库驱动方法 获得Connection对象方法)(关闭所有打开的资源方法 ) 根据继承此类 
	  子类获得共同的数据库连接方法 子类调用相关方法创建对应数据库连接对象 关闭数据库连接使用对象 简化书写
	  
	  //关闭所有打开的资源 close(Cinnection A,Statement B,ResultSet C)
	  //子类使用此方法如果没有关闭全部对象 则将没有创建的对象以null值作为实参
	  //关闭都写在一个finally
	  //Statement 是 PreparedStatement 的父接口
	
	数据库表类(例 某个数据库下master表 对应 Master类) 一个类的实例对象 表示在数据库表中的一条记录(表的字段 与 抽象对象的属性 对应)(属性进行封装 生成 对应的getter setter方法)(按需创建构造方法) //用于对象传参 
	
	对应数据库DAO操作接口(例masterDao 对master表进行的操作的一些抽象方法) 像 添加 删除 更新 查找(根据区别一个master的属性)等等
	
	对应数据表对应数据操作接口实现类(MasterDaoMySQLImpl类) 继承数据库连接简化类(BaseDAO) 实现对应数据库DAO操作接口(masterDAO) 实现接口中所有方法 补充业务 功能细节
	
```

## 使用实体类传递数据

```java
	
	数据访问代码和业务逻辑代码之间通过实体类 来实现传递数据 简化参数传递
	
	实体类主要特征
	一 属性一般使用private修饰
	二 根据业务需要和封装需求 提供getter/setter方法 负责属性的读取和修改 一般使用public修饰
	三 对实体类提供无参构造方法 根据业务需要提供 有参构造方法
	四 最好实现java.io.Serializble接口 支持序列化机制 可以将对象转换成字节序而保存到磁盘上或网络传输
	 如果实现了序列化就应该定义serialVersionUID 解决不同版本之间的序列化问题
	 private static final long serialVersinUID = 2070056025956126480L;
	
```

## 数据库连接信息简化(Properties配置文件)

```
	
	在使用JDBC访问数据库时 把驱动程序的URL、user、password 写在程序代码中 那么在换用其他数据库或用户时 必须要重新修改并编译程序  可以有Properties类他可以实现读取Java配置文件 方便维护 和 修改
	
```

### Properties配置文件

```properties
	
	.properties文件 是文本文件 文件格式是 键 = 值 格式 注释信息可以用 "#" 来注释
	
	xxx.properties内容
	
	# MySQL 数据库连接信息
	driver = com.mysql.jdbc.Driver
	url = jdbc:mysql:///mypet?useUnicode=true&characterEncoding=utf-8
	user = root
	password = myselfyourself
	
	在Java代码中读取Properties配置文件  主要用Util包下的Properties类 继承 Hashtable类	
	
```

### 连接Properties示例代码

```java
	
	private static String driver; //数据库驱动字符串
    private static String url; //数据库连接字符串
    private static String user; //数据库访问用户名
    private static String password; //数据库访问密码
	
	//静态代码块 在类加载的时候执行
    static{
        init();
    }
	
	//读取配置文件信息
    private static void init(){
        Properties properties = new Properties();
        String configFile = "database.properties";//配置文件路径
        //以文件流方式读取配置文件 加载到输入流中
        InputStream inputStream = BaseDao.class.getClassLoader().getResourceAsStream(configFile);
        //加载文件流中的属性列表 键-值对
        try {
            properties.load(inputStream);
        } catch (IOException e) {
            System.err.println("读取配置文件异常!");
            e.printStackTrace();
        }finally {
            try {
                inputStream.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
        //分别取出各个属性值  根据键取值 注意双引号!!!
        driver = properties.getProperty("driver");
        url = properties.getProperty("url");
        user = properties.getProperty("user");
        password = properties.getProperty("password");
    }
	
	
	Properties类 
	
	getProperty(String key) //返回值String类型 用指定的键在此属性列表中搜索属性 通过参数key得到其所对应的值
	setProperty(String key,String value) //返回值Object类型 调用Hashtable方法put调用基类的put()方法设置 键-值 对
	load(InputStream inStream) //无返回值 从输入流中读取属性列表(键-值对)
	clear() //无返回值 清除所装载的键-值对 该方法由基类Hashtable提供
	
```

## JDBC实现步骤

```java
	
	在idea中导入JDBC的jar包 在模块设置中导入并打勾
	
	一 加载JDBC驱动 //注册驱动
	
		//注意 mysql5之后的驱动jar包可以省略注册驱动的步骤
	 
		Class.forName(JDBC驱动类); //处理可能出现的异常[ClassNotFoundException]
		//使用Class.forName()方法将给定的JDBC驱动类加载到JVM虚拟机中
	
		//JDBC驱动类 值 "com.mysql.jdbc.Driver" //包括""
	
	二 与数据库建立连接 //代表一个或多个连接对象
	 
	 第一种
	 
		Connection connection = DriverManagergetConnection(URL,数据库用户名,密码); //处理可能出现的异常[SQLException] //根据URL 用户名 密码 连接到数据库中
		
		//URL 用来标识数据库  数据库用户名 和 密码 要用""引起来
		//jdbc:mysql......
	
	 第二种
	  	Properties info = new Properties();//创建属性对象
	  	//将用户名和密码放入info对象中
	  	info.setProperty("user","账号");
	  	info.setProperty("password","密码");
	  	Connection connection = DriverManagergetConnection(URL,info);
	
	
		//URL 用来标识数据库  数据库用户名 和 密码 要用""引起来
		
		//如果连接的是本机Mysql服务器 并且Mysql服务默认端口是3306 则URL可以简写为 jdbc:mysql:///数据库名称 用户名 密码
		
		//如果数据库出现乱码 可以指定参数 ?useUnicode=true&characterEncoding=utf-8 表示让数据库以UTF-8编码来处理数据
		--jdbc:mysql:///数据库?useUnicode=true&characterEncoding=utf-8
	
	三 发送SQL语句 并得到返回结果  //可以在之前 定义sql语句
	 
	 第一种 使用Statement接口 可能受到SQL语句注入攻击!!!!
	 
		利用connection获取Statement对象
	
		Statement statement = connection.createStatement();
		
		利用statement对象 执行SQL语句
		
		 //查询数据库 [利用ResultSet接受结果集]
		  ResultSet resultSet =  statement.executeQuery("SQL DQL语句")
		  //SQL语句为String类型 可利用变量拼接出合法SQL语句 StringBuffer效果更好
		  
	     //增删改数据库记录 [利用int类型变量 接受返回的结果] 
	      int sqlTrue = statement.executeUpdate("SQL DML语句");
	      //注意DML后面可能会加入括号")"
	      
	 第二种 使用PrearedStatement接口  不会发生 注入攻击 并且 可维护性和可读性较好 性能更好 优先使用 
	 
	 	//创建PreparedStatement对象 并 将SQL语句发送给数据库预编译
	 	String sql = "INSERT INTO 表名 Values(?,?,?)";
	 	//注意这里的表名 不要填错成数据库 一定要指定对应的表
	 	PreparedStatement preparedStatement = connection.prepareStatement(sql);//注意没d
	 	
	 	//设置参数
	 	preparedStatement.setString(1,"值"); //set后面根据 数据表 字段数据类型进行更改
	 	//注意这里设置值为String类型之后 不需要再给值加‘’用于在数据库中区分字符串 它会默认加上""
	 	preparedStatement.setInt(2,值); //set后面根据 数据表 字段数据类型进行更改
	 	preparedStatement.setString(3,"值"); //set后面根据 数据表 字段数据类型进行更改
	 	preparedStatement.executeUpdate();//让数据库执行
	 	
	 	//再次设置参数*N
	 	...
	 	preparedStatement.executeUpdate();//执行参数化SQL语句 //根据执行的SQL语句选择 //无参
	
	四 处理返回结果 //多个结果和处理方法
	
	 第一种 //查询数据库
	 
		while(resultSet.next()){ //判断结果集有没有下一行 下移一行
			//根据DQL查询的字段列表 进行取值 取一行(一条记录)的每一个字段值  !!可以使用列号或列名标识列
			例有一个字段为 int 类型  
			int A = resultSet.getInt("字段名"[或者DQL查询字段的数字顺序1.2.3...]);
			String B =  resultSet.getString("字段名"[或者DQL查询字段的数字顺序1.2.3...]);
			利用输出语句 或者 操作语句对值进行处理
		}
		//可以利用DQL特定查询 语句判断有没有对应 (用户名,密码) 的记录 和 resultSet.next() 配合使用进行一些登录的判定
		
	 第二种 //增删改数据库记录
	 
	    对返回值sqlTrue 的判断 结果有两种
	    值 = 0 //没有记录
	    值 > 0 //DQL语句操作影响的行数
	
	五 释放资源
	  
	  //放在finally块
	  //关闭前要先判断 对象是否为空 [!= null] 避免空指针异常
	  
	  resultSet.close(); //关闭结果集对象 
	  statement.close(); //关闭Statement对象 SQL对象
	  connection.close(); //关闭数据库连接对象
	  
	  //关闭statement connection resultSet 对象 关闭数据库连接 结果集 ...
      //根据声明顺序 进行关闭 最晚的声明的先关 最早声明的最后关
      //并处理其出现的 各种关闭异常
      //用户如果不关闭ResultSet 当Statement关闭 重新执行或用于从多结果序列中获取下一个结果时,该ResultSet将被自动关闭
      
```

## JDBC事务处理

```java
	
	//连接数据库 
	//开启事务 connection.setAutoCommit(false);
	//PreparedStatement接口 操作......
	//正常提交事务 //失败回滚事务
	//关闭事务 connection.setAutoCommit(true);
	//关闭资源

```

## JDBC常见错误

```java
	
	JDBC 驱动类的名称书写错误 出现CLassNotFoundException异常
	数据连接字符串 数据库用户名 密码书写错误 出现SQLexception异常
	数据库操作结束后 没有关闭数据库连接 导致仍旧占有系统资源
	关闭数据库连接语句没有放到finally语句中 导致语句可能没有被执行
	SQL语句拼接错误
	//注意添加值时 表后面的字段列表 不能加‘’否则会报错
	//注意SQL语句操作的数据库要分别开 不要写成库 要是表
	
```

## SQL注入攻击

```java
	
	原理 使用Statement接口 用户输入的密码和SQL语句进行字符串连接 用户输入的内容作为了SQK语句语法的一部分 改变了原有SQL的真正意义
	攻击实现语句 a' OR '1' = '1'
	
	解决方法 使用PreparedStatement接口 可以有效地防止SQL注入问题
	
```

## 登录案例

```
	
	通过JAVA和Mysql联合 创建一个登录功能
	 //连接数据库
	 //创建语句对象 拼接字符串的方式生成SQL语句 //可能出现SQL语句注入攻击
	 //查询数据库 有记录则表示登录成功 否则登录失败[判断操作影响的行数]
	 //释放资源
	 //可以通过在取值的时候 用输出语句包括起来 实现 查询并输出信息
	
```

## DriverManager类中的静态方法

```java
   
    getConnection("URL","用户名","密码") //返回值 Connection //通过参数获取数据库连接对象
    getConnection("URL",Properties info) //返回值 Connection //通过URL,属性对象得到连接对象
    
    URL 不同数据库是不同的
    格式 协议名:子协议://服务器名或IP地址:端口号/数据库名?参数=参数值
    
    MySQL jdbc:mysql://localhost:3306/数据库[?参数名=参数值]
    
```

## Connection接口中的方法

```java
	
	createStatement //返回值Statement 创建一条SQL语句对象
	prepareStatement("SQL语句") //返回值PreparedStament 指定预编译的SQL语句 SQL语句中使用占位符"?" 创建一个语句对象
	isClosed() //返回值boolean  查询此Connection对象是否已经被关闭
	close() //无返回值 //关闭Connection对象
	
	事务方法
	setAutoCommit(true或false) //无返回值 true开启自动提交 false关闭自动提交 <==> 开启事务
	commit() //无返回值 //提交事务
	rollback() //无返回值 //回滚事务
	
```

## Statement常用方法

```java
	
	executeQuery(String sql) //返回值 ResultSet  //执行SQL查询并获取到ResultSet对象 DDL
	executeUpdate(String sql) //返回值 int //可以执行插入、删除、更新等操作 返回值时执行该操作影响的行数 DML
	execute(String sql) //返回值 boolean //可以执行任意SQL语句 然后获得一个布尔值 表示是否返回ResultSet //了解 //返回值 若结果为ResultSet对象 则返回true 若为更新计数或者不存在结果 则返回false
	close() //无返回值 //关闭Statement对象
	
```

## PreparedStatement执行原理(与Statement的优点)

```java

	Statement对象每执行一条SQL语句 都会先将SQL发送给数据库 数据库先编译后执行
	如果有一万条 数据库需要编译一万次 效率低
	
	PrepareStatement[注意没有d因为是预编译] 会先将SQL语句发送给数据库预编译
	PreparedStatement 会引用着预编译后的结果
	可以多次传入不同的参数给PreparedStatement对象并执行
	传入一万次不同的参数并执行 减少了SQL语句的编译次数 提高了执行效率 大大提高性能
	提高了代码的可读性和可维护性 虽然会比Statement多几行代码但是 避免了SQL注入攻击(安全性)
	PreparedStatement可以写动态查询语句 
	生产环境下一定要使用PreparedStatement
	
```

## PreparedStatement接口中的方法

```java
	
	executeUpdate(无参) //返回值 int //执行DML 增删改的操作 返回影响的行数
	executeQuery(无参) //返回值 ResultSet //执行DQL 查询的操作 返回结果集
	execute(无参) //返回值 boolean //可以执行任意SQL语句 然后获得一个布尔值 表示是否返回ResultSet //了解 //返回值 若结果为ResultSet对象 则返回true 若为更新计数或者不存在结果 则返回false
	
	//设置参数的方法 //参数位置从1开始数 //无返回值
	setDouble(参数位置,参数值) //将制定参数设置为给定 JAVA double值 //无返回值
	setInt(参数位置,参数值) //将制定参数设置为给定 JAVA int值 //无返回值
	setObject(参数位置,参数值) //使用给定对象设置指定参数的值 //无返回值
	setString(参数位置,参数值) //将指定参数设置为给定 JAVA String值 //无返回值 //注意这里设置成String类型之后 不需要再给值加‘’用于在数据库中区分字符串 它会默认加上""
	//set后面还有FLoat Long 等类型......
	
	close() //无返回值 //关闭PreparedStatement对象
	
```

## ResultSet常用方法

```java
	
	//游标概念
	
	next() //返回值 boolean  // 将游标从当前位置移动到下一行 也可以理解为 有没有下一行 
	
	previous() //返回值 boolean // 将游标从当前位置移动到上一行
	
	getRow() //返回值 int //得到光标当前所指行的行号
	
	absolute(行数[int]) //返回值 boolean //光标移动到 指定的 行数
	
	//取记录有两种方式 通过列名 或者 通过列号
	//列号值 从 1 开始数
	
	getInt(DQL查询字段的数字顺序1.2.3...) //返回值 int //"()"中值为int类型 //以int形式获取结果集当前行指定列号值
	
	getInt("字段名") //"()"中值为String类型 //以String形式获取结果集当前行指定列名值
	
	getString(DQL查询字段的数字顺序1.2.3...) //"()"中值为int类型 //以int形式获取结果集当前行指定列号值
	
	getString("字段名") //"()"中值为String类型 //以String形式获取结果集当前行指定列名值
	
	//get数据类型 有多种 Boolean Byte Short Long Float Double 
	
	close() //无返回值 //关闭ResultSet对象
	
```

## 常用数据类型转换表

|     SQL类型     |   JDBC对应方法    |              返回类型               |
| :-------------: | :---------------: | :---------------------------------: |
|  BIT(1) bit(n)  |   getBoolean()    |               boolean               |
|     TINYINT     |     getByte()     |                byte                 |
|    SMALLINT     |    getShort()     |                short                |
|       INT       |     getInt()      |                 int                 |
|     BIGINT      |     getLong()     |                long                 |
|  CHAR,VARCHAR   |    getString()    |               String                |
| Text(Clob) Blob | getClob getBlob() |              Clob Blob              |
|      DATE       |     getDate()     |       java.sql.Date只代表日期       |
|      TIME       |     getTime()     |      java.sql.Time 只表示时间       |
|    TIMESTAMP    |  getTimestamp()   | java.sql.Timestamp 同时有日期和时间 |

```

	java.sql.Date java.sql.Time java.sql.Timestamp 三个共同的父类时java.util.Date
	
```

## 表与类的关系

```
	
	整个表可以看作为一个类
	表的一行称为一条记录 类的实例
	表中一列代表具体类实例的数据
	
	例 
	  创建一个学生类 里面有学生的属性 根据 从数据库取出行的每一个值 给学生对象赋值
	
```

# 实际代码

```java
	
    --BaseDao--

    package dao;

    import java.io.IOException;
    import java.io.InputStream;
    import java.sql.*;
    import java.util.Properties;

    /**
     * BaseDao 数据库工具类
     * 所有Dao类的父类 用于简化数据库连接 关闭操作
     */
    public class BaseDao {

    //    private String driver = "com.mysql.jdbc.Driver";
    //    private String url = "jdbc:mysql:///newsmanagersystem?useUnicode=true&characterEncoding=utf-8";
    //    private String user = "root";
    //    private String password = "myselfyourself";


        private static String driver; //数据库驱动字符串
        private static String url; //数据库连接字符串
        private static String user; //数据库访问用户名
        private static String password; //数据库访问密码

        //静态代码块
        static{
            init();
        }

        //读取配置文件信息
        private static void init(){
            Properties properties = new Properties();
            String configFile = "database.properties";
            //以文件流方式读取配置文件
            InputStream inputStream = BaseDao.class.getClassLoader().getResourceAsStream(configFile);
            //加载文件流中的属性列表
            try {
                properties.load(inputStream);
            } catch (IOException e) {
                System.err.println("读取配置文件异常!");
                e.printStackTrace();
            }finally {
                try {
                    inputStream.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            //分别取出各个属性值
            driver = properties.getProperty("driver");
            url = properties.getProperty("url");
            user = properties.getProperty("user");
            password = properties.getProperty("password");
        }


    //    private Connection connection = null; //连接对象  //为了让子类获得对象
        protected Connection connection = null; //连接对象

        /**
         * 获取数据库连接对象
         * @return Connection对象
         */
        public Connection getConnection(){
            try {
                /*加载驱动*/
                Class.forName(driver);
                /*创建数据库*/
                connection = DriverManager.getConnection(url,user,password);
            } catch (ClassNotFoundException e) {
                System.err.println("未找到数据库驱动类!");
                e.printStackTrace();
            } catch (SQLException e) {
                System.err.println("数据库连接异常!");
                e.printStackTrace();
            }
            return connection;
        }

        /**
         * 关闭数据库资源对象
         * @param connection 数据库连接对象
         * @param statement Statement对象
         * @param resultSet 查询结果集对象
         */
        public void closeAll(Connection connection, Statement statement, ResultSet resultSet){
            try {
                if (resultSet != null){
                    resultSet.close();
                }
                if (statement != null){
                    statement.close();
                }
                if (connection != null){
                    connection.close();
                }
            } catch (SQLException e) {
                System.err.println("数据库资源关闭异常!");
                e.printStackTrace();
            }
        }

        /**
         * 执行DML操作方法
         * @param prepareSql 带"?"占位符的SQL模板语句
         * @param params SQL模板语句参数值
         * @return int 影响行数
         */
        public int executeUpdate(String prepareSql,Object[] params){
            int result = 0; //记录操作影响行数
            PreparedStatement preparedStatement = null; //负责执行SQL语句
            /*步骤1.2*/
            this.connection = getConnection();
            /*步骤3创建PreparedStatement对象 执行SQL语句*/
            try {
                preparedStatement = this.connection.prepareStatement(prepareSql);
                if (preparedStatement != null){
                    for (int i = 0 ;i<params.length;i++){
                        //为预设语句设置模块参数
                        preparedStatement.setObject(i+1,params[i]);
                    }
                }
                result = preparedStatement.executeUpdate(); //执行SQL语句
            } catch (SQLException e) {
                System.err.println("数据库操作异常!");
                e.printStackTrace();
            } finally {
                /*步骤5*/
                this.closeAll(connection,preparedStatement,null); //null传递null对象
            }
            return result;
        }

        /**
         * 传值 Object 关参
         *  ！！！！注意关闭 ResultSet对象 Allclose方法
         *  用于执行DQL查询语句
         * @param prepareSql 带"?"占位符的SQL模板语句
         * @param params SQL模板语句参数值
         * @return Object[] 操作结果对象 用于在之后的方法进行关闭 0结果集对象 1数据库连接对象 2preparedStatement对象
         */
        public Object[] executeQuery(String prepareSql, Object[] params){
            Object[] objects = new Object[3];
            ResultSet resultSet = null;
            PreparedStatement preparedStatement = null; //负责执行SQL语句
            /*步骤1.2*/
            this.connection = getConnection();
            /*步骤3创建PreparedStatement对象 执行SQL语句*/
            try {
                preparedStatement = this.connection.prepareStatement(prepareSql);
                if (preparedStatement != null){
                    for (int i = 0; i < params.length; i++) {
                        //为预设语句设置模块参数
                        preparedStatement.setObject(i+1,params[i]);
                    }
                }
                resultSet = preparedStatement.executeQuery();//执行SQL语句
            } catch (SQLException e) {
                System.out.println("数据库查询异常!");
                e.printStackTrace();
            }
            objects[0] = connection;
            objects[1] = preparedStatement;
            objects[2] = resultSet;
            return objects;
        }

        /** 
         * 传值 结果集 关参
         * ！！！！注意关闭 ResultSet对象 Allclose方法
         * 用于执行DQL查询语句
         * @param prepareSql 带"?"占位符的SQL模板语句
         * @param params SQL模板语句参数值
         * @return resultSet 操作结果对象
         */
        public ResultSet executeQueryOnly(String prepareSql, Object... params){
            PreparedStatement preparedStatement = null; //负责执行SQL语句
            ResultSet resultSet = null; //负责接收查询结果集
            /*步骤1.2*/
            Connection connection = getConnection();
            try {
                preparedStatement = connection.prepareStatement(prepareSql); //获取preparedStatement对象 进行预编译
                for (int i = 0; i < params.length; i++) { ///为预设语句设置模块参数
                    preparedStatement.setObject(i+1,params[i]);
                }
                resultSet = preparedStatement.executeQuery(); //获取结果集

            } catch (SQLException e) {
                e.printStackTrace();
            }
            return resultSet;
        }
    }

	
```


