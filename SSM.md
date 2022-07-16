```
	2019年10月16日16:27:24创建
```

# 目录

[TOC]

# SSM

## 框架技术

### 什么是框架 (Framework)

```
	
	框架是可重用的公共结构的半成品 能带来极大便利
    按一定规则组织的一组组件
    凝结着前人的经验和智慧 使用框架 就站在了巨人肩上

```

### 框架的优势

```
	
	不用再考虑公共问题
    专心在业务实现上
    结构统一，易于学习、维护
    新手也可写出好程序 
    
    降低了培训成本和软件的维护成本 框架在结构统一和创造力之间维持着一个合适的平衡

```

### 主流框架介绍(详细百度去)

#### MyBatis

```
	
	半自动化的ORM实现
    DAO层
    动态SQL
    小巧灵活、简单易学
	
```

#### Spring

```
	
	依赖注入容器 / AOP实现
    声明式事务
    简化Java EE应用
    黏合剂，将大家组装到一起

	Spring MVC
        结构最清晰的MVC Model2实现
        高度可配置，支持多种视图技术
        定制化开发

```

#### Struts2

```
	
	MVC设计模式的实现
    拦截器
    可变和可重用的标签
	
```

#### HIBERNATE

```
	
	ORM 简化数据库操作
    DAO层	
	
```

## 持久化与ORM

### 持久化

```
	
    持久化是程序数据在瞬时状态和持久状态间转换的过程	

    是将内存中的数据模型转换为储存模型 以及将储存模型转化为内存中的数据模型 例如 文件的储存 数据的读取都是数据持久化操作
    //数据模型可以是任何数据结构 或 对象模型
    //存储模型可以是关系模型、XML、二进制流等

    //例从内存存入到数据库 | 从数据库读出来到内存
	
```

### ORM

```
	
	ORM（Object Relational Mapping）
        编写程序的时候，以面向对象的方式处理数据 ， 存数据的时候，却以关系型数据库的方式存储 这样造成了不便 ORM在对象模型和关系数据库的表之间建立了一做桥梁 有了ORM就不需要使用SQL语句操作数据库中的表 使用API直接操作 JavaBean对象就可以实现数据的储存 查询 更改等操作
    ORM解决方案包含下面四个部分
        在持久化对象上执行基本的增、删、改、查操作
        对持久化对象提供一种查询语言或者API
        对象关系映射工具
        提供与事务对象交互、执行检查、延迟加载以及其他优化功能	
	
```

## MyBatis

```

	https://www.w3cschool.cn/mybatis/
	
```

```
	
	Mybatis 是一个开源的数据持久层框架 它内部封装了通过JDBC访问数据库的操作 支持普通的SQL查询、存储过程和高级映射 //几乎消除了所有JDBC代码和参数的手工设置以及结果集的检索
	
	Mybatis主要思想是将程序中大量的SQL语句剥离出来 配置在配置文件中 实现SQL的灵活配置 达到SQL与程序代码分离
可以在不修改程序代码的情况下 直接在配置文件中修改SQL 便于统一管理与维护，降低程序的耦合度
	
	MyBatis前身是iBatis,本是Apache的一个开源的项目
	//2010由Apache Software Foundation迁移到了Google Code 并改名为Mybatis
	//2013年迁移到了Github

	MyBatis官网 http://mybatis.org	Github官网 https://github.com/mybatis
	
	MyBatis 通过简单的XML或者注释进行配置和原始映射 将实体类和SQL语句之间建立 映射关系 是一种半自动化的ORM实现
	//MyBatis是ORM解决方案 MyBatis通过建立了SQL关系映射 便捷的实现数据储存 查询 更改 删除
	
```

### 搭建MyBatis环境

```
	
	使用MyBatis的开发步骤
        下载mybatis-3.2.2.jar包并导入工程 //注意也将log4j.jar jdbc.jar包导入
        编写MyBatis核心配置文件(mybatis-configuration.xml)
        创建实体类-POJO
        DAO层-SQL映射文件(xxxmapper.xml)
        创建测试类
            读取核心配置文件mybatis-config.xml
            创建SqlSessionFactory对象，读取配置文件
            创建SqlSession对象
            调用mapper文件进行数据操作

```

#### 创建MyBatis核心配置文件configuration.xml

```xml
	
	核心配置文件 主要用于配置数据库连接 和 MyBatis运行时所需的各种特性 包含了设置和影响MyBatis行为的属性
	
	为了方便管理以后各框架的配置文件 需要在项目工程下新建Source Folder类型的resources目录 在此目录下建立MyBatis核心配置文件 默认文件名为configuration.xml但是 可能以后还要使用其它框架 所以一般将文件名命名为 mybatis-config.xml
	
	<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN" "http://mybatis.org/dtd/mybatis-3-config.dtd">

<!-- 此配置文件实现：
     mybatis与数据库的连接配置
     mybatis运行特性配置
     mapper文件配置
 -->
<configuration>
    <!-- 引入 database.properties 文件-->
    <properties resource="database.properties"/>
    <!-- MyBatis运行特性全局设置 -->
    <settings>
        <!-- 配置mybatis的log实现为LOG4J -->
        <setting name="logImpl" value="LOG4J"/>
        <!-- 开启缓存 -->
        <setting name="cacheEnabled" value="true"/>
    </settings>
    <!-- 配置类型别名 -->
    <typeAliases>
        <!--指定POJO类 类别名-->
            <!--<typeAlias alias="user" type="com.ttelite.smbms.pojo.User"/>-->
         <!--指定POJO类扫描路径-->
            <package name="cn.smbms.pojo"></package>
    </typeAliases>

    <!-- 配置mybatis多套运行环境 -->
    <environments default="development">
        <environment id="development">
            <!--配置事务管理，采用JDBC的事务管理  -->
            <transactionManager type="JDBC"></transactionManager>
            <!-- POOLED:mybatis自带的数据源，JNDI:基于tomcat的数据源 -->
            <dataSource type="POOLED">
                <property name="driver" value="${driver}"/>
                <property name="url" value="${url}"/>
                <property name="username" value="${user}"/>
                <property name="password" value="${password}"/>
            </dataSource>
        </environment>
    </environments>

    <!-- 将mapper文件加入到配置文件中 -->
    <mappers>
        <mapper resource="cn/smbms/dao/user/UserMapper.xml"/>
<!--        <mapper resource="com/ttelite/smbms/dao/ProviderMapper.xml"/>-->
<!--        <mapper resource="com/ttelite/smbms/dao/BillMapper.xml"/>-->
    </mappers>
</configuration>
	
	
	configuration	//配置文件的根元素节点
	properties	//通过resource属性从外部指定properties属性文件(database.properties) 该属性文件描述数据库连接的相关配置(数据库驱动、连接数据库的url、数据库用户名、数据库密码) 在/resources目录下
	settings //设置MyBatis运行中的一些行为 比如此处设置MyBatis的log日志实现为LOG4J即使用log4j实现日志功能
	environments //表示配置MyBatis的多套运行环境 需指定运行环境ID、事务管理、数据源配置等相关信息
	mappers //作用是告诉MyBatis去哪里找到SQL映射文件(该文件内容时开发者定义的映射SQL语句) 整个项目中可以有1个或多个SQL映射文件
	mapper //mappers的子元素节点 具体指定SQL映射文件的路径 其中resource属性的值表述了SQL映射文件的路径(类资源路径)
	!!! //注意该文件的元素节点是有一定顺序的 节点位置不按顺序排列 那么XML文件会报错
	
```

#### 创建持久化类(POJO)和SQL映射文件

```
	
	持久化类指其实力状态 需要被MyBatis持久化到数据库中的类 MyBatis一般采用POJO编程模型来实现持久化类 与POJO类配合完成持久化工作是MyBatis最常见的工作模式
	
	POJO(Plain Ordinary Java Object) 从字面讲就是普通的Java对象 可以简单理解为符合JavaBean规范的实体类 不需要继承和实现任何特殊的Java基类或接口 访问属性必须通过对应的 getter/setter方法
	//MyBatis中 不需要POJO类名 与 数据库表名一致 因为MyBatis是POJO与SQL语句之间的映射机制 一般情况 保证POJO对象的属性与数据库表的字段名一致即可
	//保证POJO对象的属性与数据库表的字段名一致(Java驼峰命名) 是为了可以让数据库查询的结果和返回类型中的属性能够自动匹配以便开发,这样在常规需求下就不需要手动映射(数据库的字段名和属性不一致的情况下需要手动映射)
	//SQL映射文件一般都对应 相应于相应的POJO 所以一般都是采用 POJO的名称 + Mapper的规则来进行命名 当然该mapper文件属于DAO层的操作 应该放置在 dao包下
	

	<?xml version="1.0" encoding="UTF-8" ?>
	<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
    <!-- 命名空间全局唯一，一般是DAO接口的全限定名 -->
    <mapper namespace="映射SQL的DAO接口的全限定名">
        <!-- SQL映射语句 -->
		
    </mapper>
	
	mapper 映射文件的根元素节点 只有一个属性 namespace
		namespace //用于区分不同mapper 全局唯一
	
```

#### 调用使用相关SQL映射方法

```
	
	创建获取 SqlSession 根据相关调用方法 调用相关方法
	
	//创建获取 SqlSession 将此封装 示例在下面 或者 查看技术示例
	
	SqlSession的两种使用方式
		通过SqlSession实例直接运行映射的SQL语句 //抛弃详细百度
		基于Mapper接口方式操作数据(推荐) //接口的方法必须与SQL映射文件中SQL语句的ID一一对应
	
	//例 获取映射器 调用方法 sqlSession.getMapper(xxxMapper.class).方法();
	//第一种方法是旧版本MyBatis提供的操作方式 现在也能正常工作 但是 第二种方式是官方推荐的
	表达方式更加直白 代码更加清晰 类型安全 不用担心易错的字符串字面值以及强制类型转换
	
```

### MyBatis框架的优缺点及适用场合

```
	
	优点
	
		与JDBC相比 减少了50%以上的代码量
		//JDBC查询的是结果集对象 往往不能直接使用 还需要转换成对象
		//MyBatis将此分解包装
		最简单的持久化框架 小巧并简单易学
		SQL代码从程序代码中彻底分离可以 重用
		提供XML标签 支持编写动态SQL
		提供映射标签 支持对象与数据库的ORM字段映射
	
	缺点 
		
		SQL语句编写工作量大 对开发人员有一定要求
		数据库移植性差,不能随意更换数据库
		框架还是比较简陋，功能尚有缺失，虽然简化了数据绑定代码，但是整个底层数据库查询实际还是要自己写的，工作量也比较大，而且不太容易适应快速数据库修改。 
		
	适用场合
	
		MyBatis专注于SQL本身 是一个足够灵活的DAO层解决方案 适用于性能要求高 需求变化比较多的项目 
	
```

### MyBatis的基本要素

```
	
	核心接口和类		MyBatis核心配置文件(mybatis-config.xml)		SQL映射文件(mapper.xml)
	
```

#### 核心接口和类

```
	
	SqlSessionFactoryBuilder >build()> SqlSessionFactory >openSession()> SqlSession
	
	//首先获取SqlSessionFactoryBuilder对象 可以根据XML配置文件 或 Configuration类的实例构建该对象
	//有了SqlSessionFactory对象后 获取SqlSession实例 
	//SqlSession对象 完全包含以数据库为背景的所有执行SQL操作的方法 对象实例可以直接 执行已映射的SQL语句
	
	
	SqlSessionFactoryBuilder
	//负责构建SqlSessionFactory 提供了多个build()方法的重载
	//用过即丢 因此SqlSessionFactoryBuilder的最佳范围 就是存在于方法体内 也就是局部变量
	//配置信息以三种形式提供给SqlSessionFactory的build方法 InputStream(字节流) Reader(字符流) Configuration(类)
	常用创建方法 读取XML文件构造方法
		InputStream inputStream = Resources.getResourceAsStream("mybatis-configuration.xml");
         public SqlSessionFactory factory = new SqlSessionFactoryBuilder().build(inputStream);
	
	SqlSessionFactory
	//每个MyBatis的应用程序 都以一个 SqlSessionFactory 对象的实例为核心
	//作用创建 SqlSession实例 
	//SqlSession session = sqlSessionFactory.openSession(boolean autoCommit); autoCommit true关闭事务控制(默认) false开启事务控制
	//作用域Application
	//生命周期与应用的生命周期相同
	//单例 存在于整个应用运行时 并且同时只存在一个对象实例
	
	SqlSession
	//包含了执行SQL所需的所有方法
	//要处于一个请求(request)期间(作用域) 或 方法体作用域内
	//对应一次数据库会话 会话结束必须关闭 
	//线程级别 不能共享 
	//注意!!! 关闭SqlSession 必须要确保在finally方法体中正常关闭 try - finally
	//可以执行多次SQL语句 但一旦关闭了SqlSession就需要重新创建 
	
	SqlSession的两种使用方式
		通过SqlSession实例直接运行映射的SQL语句 //抛弃详细百度
		基于Mapper接口方式操作数据(推荐) //接口的方法必须与SQL映射文件中SQL语句的ID一一对应
		//第一种方法时旧版本MyBatis提供的操作方式 现在也能正常工作 但是 第二种方式是官方推荐的
	表达方式更加直白 代码更加清晰 类型安全 不用担心易错的字符串字面值以及强制类型转换
		
```

#### 系统核心配置文件(configuration.xml)

```xml
	
	核心配置文件 需要配置一些基本元素 注意元素节点有先后顺序
	
	configuration配置
		properties 可以配置在Java属性配置文件中
		settings 修改MyBatis在运行时的行为方式
		typeAliases 为Java类型命名一个别名(简称)
		typeHandlers 类型处理器
		objectFactory 对象工厂
		plugins 插件
		environments 环境
		environment 环境变量
			transactionManager 事务管理器
			dataSource 数据源
		mappers 映射器
			
	配置properties元素的两种方式
	
		通过外部指定的方式(database.properties //示例包括) 实现动态配置
			配置properties的resource属性
			<properties resource="database.properties"/>
			//省略中间元素 注意元素顺序不要乱 
			<!-- POOLED:mybatis自带的数据源，JNDI:基于tomcat的数据源 -->
                    <dataSource type="POOLED">
                        <property name="driver" value="${driver}"/>
                        <property name="url" value="${url}"/>
                        <property name="username" value="${user}"/>
                        <property name="password" value="${password}"/>
                    </dataSource>
            
		直接配置为xml 实现动态配置
			配置property的name和value
			<properties>
				<property name="driver" value="com.mysql.jdbc.Driver"/>
				<property name="url" value="jdbc:mysql://127.0.0.1:3306/库名"/>
				<property name="user" value="root"/>
				<property name="password" value="root"/>
			</properties>
			//省略中间元素 注意元素顺序不要乱 
			<!-- POOLED:mybatis自带的数据源，JNDI:基于tomcat的数据源 -->
                    <dataSource type="POOLED">
                        <property name="driver" value="${driver}"/>
                        <property name="url" value="${url}"/>
                        <property name="username" value="${user}"/>
                        <property name="password" value="${password}"/>
                    </dataSource>
		
		//如果两种方式同时使用 则resource属性值的优先级高于property子节点配置的值
		
		
	配置settings元素 //修改MyBatis在运行时的行为方式
	
        <!-- MyBatis运行特性全局设置 -->
        <settings>
            <!-- 配置mybatis的log实现为LOG4J -->
            <setting name="logImpl" value="LOG4J"/>
            <!-- 开启缓存 -->
            <setting name="cacheEnabled" value="true"/>
        </settings>
        //设置格式参考以上 或百度
        cacheEnabled 对在此配置文件下所有缓存进行全局性开/关设置 默认值true
        lazyLoadingEnabled 全局性设置懒加载 如果设置为false则所有关联的都会被初始化加载 默认值true
        autoMappingBehavior MyBatis对于resultMap自动映射的匹配级别 NONE|PARTIAL|FULL 默认值PARTIAL
	
	
	配置typeAliases元素 //作用是配置类型别名 通过MyBatis的SQL映射相关联 减少输入多余的完整类名 以简化操作
        <typeAliases>
            <!--给实体类取别名 方便在mapper配置文件中使用--> //弊端如果项目POJO多 需要一一配置
                <typeAlias alias="user" type="com.ttelite.smbms.pojo.User"/>
             <!--指定POJO类扫描路径--> //推荐 通过package指定包名 MyBatis会自动扫描指定包下的JavaBean 并设置一个别名 默认名称为JavaBean的非限定类名
                <package name="cn.smbms.pojo"/>
        </typeAliases>
	
	配置environments元素 //配置运行环境
		//可以配置多套运行环境 开发环境 测试环境 生产环境等 可以灵活选择不同的配置 从而将SQL映射应用到不同的数据库环境上
		//但因为  每个SqlSessionFactory实例只能选择一个运行环境 所以必须指定一个默认的运行环境(default指定)	
		//environment元素的id要唯一
		//transactionManager事务管理器 设置其类型为JDBC MyBatis有两种事务管理类型 JDBC|MANAGED(托管)
直接使用JDBC的提交和回滚功能 依赖于从数据源获得连接来管理事务的声明周期
		//dataSource元素使用基本的JDBC数据源接口来配置JDBC连接对象的资源 它有三种数据源类型UNPOOLED|POOLED|JNDI 这里使用POOLED数据源类型  
		//POOLED数据源类型  实现利用 池 的概念将JDBC连接对象组织起来 避免了创建新的连接实例时必须的初始化和认证时间 是MyBatis实现的简单的数据库连接池类型 它使数据库连接可被复用 不必每次请求时都去创建一个物理连接 这对于高并发的WEB应用是一种流行的处理方式 有利于款速响应请求

        <!-- 配置mybatis多套运行环境 -->
        <environments default="development">
            <environment id="development">
                <!--配置事务管理，采用JDBC的事务管理  -->
                <transactionManager type="JDBC"></transactionManager>
                <!-- POOLED:mybatis自带的数据源，JNDI:基于tomcat的数据源 -->
                <dataSource type="POOLED">
                    <property name="driver" value="${driver}"/>
                    <property name="url" value="${url}"/>
                    <property name="username" value="${user}"/>
                    <property name="password" value="${password}"/>
                </dataSource>
            </environment>
        </environments>
	
	配置mappers元素 //映射器用来定义SQL的映射语句 我们只需要告诉MyBatis在哪找到相应的SQL映射文件 可以使用类资源路径 或 URL等
	//
	<!-- 将mapper映射文件加入到系统核心配置文件中 -->
    <mappers> //使用类资源路径获取资源
        <mapper  resource="cn/smbms/dao/user/UserMapper.xml"/>
    </mappers>

	<mappers> //使用URL获取资源
		<mapper url="file:///E:/sqlmappers/UserMapper.xml"/>
		<mapper url="file:///E:/sqlmappers/ProviderMapper.xml"/>
	</mappers>
	
```

#### SQL映射文件(mapper.xml)

```
	
	MyBatis 真正的强大在于映射语句 专注于SQL 功能强大 SQL映射的配置却是相当简单
	
	SQL映射文件的几个顶级元素(按照定义的顺序)
        mapper - namespace属性(命名空间)
        cache - 配置给定命名空间的缓存
        cache-ref – 从其他命名空间引用缓存配置
        resultMap –用来描述数据库结果集和对象的对应关系
        sql – 可以重用的SQL块，也可以被其他语句引用
        insert – 映射插入语句
        update – 映射更新语句
        delete – 映射删除语句
        select – 映射查询语句
	
	<?xml version="1.0" encoding="UTF-8" ?>
	<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
    <!-- 命名空间全局唯一，一般是DAO接口的全限定名 -->
    <mapper namespace="映射SQL的DAO接口的全限定名">
        <!-- SQL映射语句 -->
		<select>...</select>
		<delete>...</delete>
		......
    </mapper>
	
	mapper 映射文件的根节点 只有一个属性namespace
		//namespace作用 用于区分不同的mapper全局唯一
		//namespace指定接口 并且和 子元素的id联合保证唯一 在不同的mapper文件中子元素的id可以相同
		//绑定Dao接口 namespace的命名必须跟某个接口同名 接口中的方法与映射文件中SQL语句id 一一对应 
		//MyBatis会根据接口的完整限定名查找到对应的mapper配置来执行SQL语句 因此namespace必须和接口同名
       	//映射文件应该与Dao接口放置在同一包下
        
        
	select   //没法一起解释 可以先看规范 之后 分析参考 实现示例
		//是MyBatis中最常用的元素之一
		//有很多属性可以详细配置每一条语句
		//下面为属性
         id //命名空间中唯一的标识符 接口中的方法与映射文件中的SQL语句id一一对应
         flushCache //将其设置为true 无论语句什么时候被调用 都会导致缓存被清空 fasle(默认值) //注意还有总开关在核心配置文件 <setting name="cacheEnabled" value="true"/>
         useCache //将其设置为true 会将语句结果缓存 默认值true
         
         parameterType 
         	//传入SQL语句的参数类型 包含基本类型(int、String、Date等) 和 复杂参数类型(Java实体类或Map)
         	//传入的参数使用#{参数名调出} 它告诉MyBatis生成PreparedStatement 若采用JDBC实现 该参数会被标识为"?" 
         	//！！！传入基本类型(int、String、Date等)只能传入一个参数 多参可以使用复杂参数类型进行支持
         	//复杂参数类型传入SQL语句的参数类型(实体类)的完全限定名或别名  传入包装实体类 则调用(#{xxx})的时候需要根据 实体类的属性名   传入Map则 要根据定义map的 keyName(键名)取值 
         	//注意使用parameterType只能传入一个参数
         	MyBatis有许多内建的类型别名 并且它们对大小写不敏感 例如 别名(string)映射类型(String) 别名(double)映射类型(Double)等等 也可以在核心配置文件设置自定义类型别名 减少配置代码
         	另外传参方式可以使用 @Param注解实现传参 可以实现1到多个参数的传参
         	
         	
         resultType //自动映射 //详细寻找示例
         	//直接表示返回类型 基本数据类型 复杂数据类型
         	//SQL语句返回值类型的完整类名或别名(对象实体属性与数据库字段对应 自动映射)(对象实体属性与数据库字段不一样要采用自定义映射)
         	//注意 字段名和实体类的属性名 必须一致 若不一致 则 需要给字段起别名 保证别名与字段一致
         	和parameterType 一致也支持别名的使用 
         	
         resultMap //手动自定义映射 //详细寻找示例 //自由控制映射结果
         	//用来描述如何将结果集映射到Java对象
         	//对外部resultMap的引用 自定义映射
         	//应用场景 数据库字段信息与对象属性不一致
         	//复杂的联合查询 自由控制映射结果  例如需要查询另一个表的数据 但是返回结果的类型实体类中没有 这里就要用自定义映射 特别是数据库的字段名与属性名不一致的情况下 可以自己设置映射结果
         	//resultMap 有自动映射级别 可根据需求在核心配置文件 settings元素下设置自动映射级别	!!!注意自动映射匹配的前提是 字段名与属性名一致
         	示例
         	    <settings>
         	    	<!-- 设置resultMap的自动映射级别 -->
         	    	<setting name="autoMappingBehavior" value="NONE"/>
         	    	//NONE 为禁止自动匹配
         	    	//PARTIAL(默认) 自动匹配所有属性 //注意内部嵌套除外
         	    	//FULL 自动匹配所有 包含内部嵌套
         	    </settings>
         	//下面为属性
         	id //唯一标识 用于select元素 resultMap属性的引用
         	type //表示该resultMap的映射结果类型
                result子节点 用于标识一些简单属性 //映射到JavaBean的某个 简单类型属性
                    其中column属性表示从数据库中查询的字段名 
                    property表示查询出来的字段对应的值赋给实体对象的哪个属性
         		association //映射到JavaBean的某个 复杂类型属性 比如JavaBean类 //一对一关系 映射一个嵌套结果到实体类中的对象属性 //内部嵌套
         			//javaType属性 完整Java类名或者别名 若映射到JavaBean则MyBatis通常会自行检测类型 若映射到一个HashMap应该明确指定javaType
                     //property属性 映射数据库列的实体对象的属性 是在实体类里定义的属性
                     //resultMap属性 可以扩展resultMap进行联合映射 可以达到resultMap复用的结果 
                     //id元素 指定一个或多个属性来唯一标识结果集 虽然不指定id 也能工作 但是会导致严重的性能开销 所以最好选择 属性结果少的属性 来标识唯一结果 主键或联合主键均可
                     //result元素 和普通result元素使用一致 property work实体类属性名 column数据库列名或别名
                     //注意内部嵌套映射级别 是PARTIAL还是FULL PARTIAL自动匹配所有属性 内部嵌套除外 FULL匹配所有属性 包含内部嵌套
         		collection //映射到JavaBean的某个 复杂类型属性 比如集合 //一对多关系 映射一个嵌套结果集到一个列表	//与association 使用基本一致 //内部嵌套
         			//ofType属性 完整Java类名或者别名(集合所包含的类型)
         			//property属性 映射数据库列的实体对象的属性 是在实体类里定义的属性
                     //resultMap属性 可以扩展resultMap进行联合映射 可以达到resultMap复用的结果 
                     //id元素 指定一个或多个属性来唯一标识结果集 虽然不指定id 也能工作 但是会导致严重的性能开销 所以最好选择 属性结果少的属性 来标识唯一结果 主键或联合主键均可
                     //result元素 和普通result元素使用一致 property work实体类属性名 column数据库列名或别名
                     //注意内部嵌套映射级别 是PARTIAL还是FULL PARTIAL自动匹配所有属性 内部嵌套除外 FULL匹配所有属性 包含内部嵌套
         	
          resultType和resultMap的关联
            !!!!!!!!!!!!!! resultType和resultMap不能同时存在 本质上都是Map数据结构
          	//resultType 直接表示返回类型 包括基础数据类型 和 复杂数据类型
          	//resultMap 是对外部resultMap元素的引用 应用场景为 数据库字段信息与实体类对象属性不一致 或 需要做复杂的联合查询 以便自由控制映射结果
         	//MyBatis进行查询映射的时候 查询出来的每个字段值 都放在对应的一个Map中(键是字段名 值是其字段名对应的值) 当返回类型属性为resultType的时候 MyBatis将Map结果映射给实体类对象属性(通过实体类中的setter方法) 可以看出 MyBatis每个查询结果的映射返回类型都是resultMap 只是返回类型属性为resultType的时候 MyBatis进行了自动映射 而当返回类型是resultMap因为Map不能很好地表示领域模型 我们就需要自定义映射将它转化成实体对象
            
     
     //对于增删改(insert update delete)这类数据库更新操作
     	//该类型的操作本身默认返回执行SQL影响的行数 所以DAO层的接口方法返回值一般为int类型(最好不要返回boolean类型)
     	//insert|update|delete 元素中均没有resultType属性 只有查询操作需要resultType/resultMap设定
     
         
	insert //映射插入语句 //可参考示例
		id //命名空间中唯一的标识符 接口中的方法与映射文件中的SQL语句id一一对应
		parameterType 
         	//传入SQL语句的参数类型 包含基本类型(int、String、Date等) 和 复杂参数类型(Java实体类或Map)
         	//传入的参数使用#{参数名调出} 它告诉MyBatis生成PreparedStatement 若采用JDBC实现 该参数会被标识为"?" 
         	//！！！传入基本类型(int、String、Date等)只能传入一个参数 多参可以使用复杂参数类型进行支持
         	//复杂参数类型传入SQL语句的参数类型(实体类)的完全限定名或别名  传入包装实体类 则调用(#{xxx})的时候需要根据 实体类的属性名   传入Map则 要根据定义map的 keyName(键名)取值 
         	//注意使用parameterType只能传入一个参数
         	MyBatis有许多内建的类型别名 并且它们对大小写不敏感 例如 别名(string)映射类型(String) 别名(double)映射类型(Double)等等 也可以在核心配置文件设置自定义类型别名 减少配置代码
			另外传参方式可以使用 @Param注解实现传参 可以实现1到多个参数的传参
	
	//update delete 使用相同 
	
         
```

### 单元测试

```
	
	@Test
	public void testSomeAction(){
		SqlSession sqlSession = null;
		try{	
			//省略获取SqlSession实例对象 控制是否事务
			//调用映射方法
			sqlSession.commit(); //如果是事务 提交
		}catch(Exception e){
			e.printStackTrace();
			sqlSession.rollback(); //如果是事务 回滚
			//注意将 方法值返回为 默认正常值
		}finally{
			//关闭sqlSession对象
		}
	}
	
	//测试方法必须 public void 无参
	
```

### #{}与${}的相同点和区别

```
	
	相同
		可以获取map中的值或者pojo对象属性的值
	区别
		#{}:是以预编译的形式，将参数设置到sql语句中 PreparedStatement 防止sql注入 
			//大多数使用
		${}:取出的值直接拼装在sql语句中；会有安全问题；
			//原生jdbc不支持占位符的地方我们就可以使用${}进行取值,比如列名、分表、排序
	
```

### 使用@Param注解实现多参数入参 

```
	
	可以灵活方式处理需求 直接多参数入参 代码可读性高 可以清晰地看出接口方法所需的参数
	
	public List<User> findUserByNameAndWork(@Param("name1")String,@Param("workId1")Integer workId); 
在取参时 使用 #{name1} 和 #{workId1}
	
	//可以参考@param传参示例
	//当方法参数有多个是 每个参数都需要添加@Param注解
	//使用@Param 相当于将该参数重命名 在映射SQL文件中需要 使用#{注解名称}进行取值 例如
	//只有select示例 使用方法一致
	//若不使用@Param注解 则会报错 MyBatis的参数类型为Map 若使用@Param注解参数 那么就会记录指定参数名为key 从而取到值
	
	超过4个以上的参数最好封装成对象入参（特别是在常规的增加和修改操作时，字段较多，封装成对象比较方便）
参数固定的业务方法，最好使用多参数入参
（这种方法比较灵活，代码的可读性高，可以清晰看出来这个接口方法的所需的参数是什么
并且对于固定的接口方法，参数一般是固定的，所以可以使用直接参数入参即可，无需封装对象
	
```

### 封装创建/关闭SqlSession对象

```
	
	package cn.smbms.util;

    import org.apache.ibatis.io.Resources;
    import org.apache.ibatis.session.SqlSession;
    import org.apache.ibatis.session.SqlSessionFactory;
    import org.apache.ibatis.session.SqlSessionFactoryBuilder;

    import java.io.IOException;
    import java.io.InputStream;

    public class MyBastisUtil {
        private static SqlSessionFactory factory;

        //只创建一次SqlSessionFactory对象
        //static代码块在加载时只执行一次 从而只创建一次SqlSessionFactory对象
        static { //单例模式+
            try {
                //创建SqlSessionFactory对象
                InputStream inputStream = Resources.getResourceAsStream("mybatis-configuration.xml");
                factory = new SqlSessionFactoryBuilder().build(inputStream);
            } catch (IOException e) {
                e.printStackTrace();
            }

        }

        /**
         * 创建SqlSession对象
         * @return SqlSession
         */
        public static SqlSession createSqlSession(boolean autoCommit){
            return factory.openSession(autoCommit);
        }

        /**
         * 关闭SqlSession对象
         * @param sqlSession
         */
        public static void closeSqlSession(SqlSession sqlSession){
            if (sqlSession != null){
                sqlSession.close();
            }
        }
    }

```

### MyBatis缓存(了解)

```
	
	MyBatis 包括一级缓存和二级缓存  一级缓存缓存SQL语句 二级缓存缓存是结果对象
    
    一级缓存
		是MyBatis的HashMap本地缓存 作用范围在session域内 session flush或者close之后 所有缓存会被清空
	二级缓存
		二级缓存 超出session范围外 可被所有SqlSession共享
		配置方式
		<settings> //核心配置文件 开启全局缓存配置
            <setting name="cacheEnabled" value="true"/>
        </settings>
        //注意缓存作用域针对 namespace而言 只有namespace内的查询才能共享缓存
		mapper文件xxxMapper.xml设置缓存  默认缓存关闭 
		
		SQL映射文件下
	    <cache eviction="FIFO" flushInterval="60000" size="512" readOnly="true"/> //详细百度
		
		个别查询标签下
		<select id="xxxx" resultType="xxxx" useCache="true">
		</select>
		
	//了解即可 因为MyBatis应该是专心做Sql语句映射 在面对一定规模的数据量时候 就会采用 OSCache、Memcached等专门的缓存服务器来做更为合理
		
```

### 需求实现参考示例

```
	
	全局配置约束
	
    MyBatis核心配置文件(mybatis-config.xml)
    SQL映射文件(userMapper.xml) //所有元素(select|insert|delect)都在根元素 节点内 
	接口文件(userMapper.java)
	用户实体类(User)
	表名(user_base 字段name姓名 sex性别 id用户ID workId用户角色(1-经理 2-组长 3-组员))
	二表(work_base id字段工作ID cnName角色名称)
	
	//总体皆为用户业务需求 配置文件具体实现省略
	//示例内容主要为SQL映射文件 元素设置(SQL语句具体映射) 和 接口方法书写  和业务需求 之间的实现
	//调用测试省略 皆为单元测试(@Test)/装载业务逻辑层   调用映射器(sqlSession.getMapper) 调用方法(根据方法名称)传入参数(根据需求) 
	
```

#### select实现简单无条件查询

```
	
	使用select查询整个表的用户信息  (不带参数 返回复杂类型)(自动映射)
	
	接口
		public List<User> getAllUser();
	映射文件
		<select id="getAllUser" resultType="User">
			SELECT * FROM user_base
		</select>
	调用映射器
		List<User> userList = sqlSession.getMapper(UserMapper.class).getAllUser();
	
	resultType //指定返回  集合结果中 单个元素的类型
	
```

```
	
	查询用户的总个数  (不带参数 返回简单类型)(自动映射)
	
	接口
		public int getCount();
	映射文件
		<select id="getCount" resultType="int">  
			SELECT COUNT(0) FROM user_base
		</select>
	调用映射器
		int count = sqlSession.getMapper(UserMapper.class).getCount();
	
	//resultType="int"可以省略
	
```

#### select实现单条件查询

```
	
	根据用户模糊名称 查找用户信息  (带参数返回复杂类型)(单参)(自动映射)
	
	接口
		public List<User> findUserByName(String name);
	映射文件
		<select id="findUserByName" parameterType="String" resultType="User">
			SELECT * FROM user_base WHERE name LIKE CONCAT('%',#{name},'%') //双引号|单引号都行
		</select>
	调用映射器
		List<User> userList = sqlSession.getMapper(UserMapper.class).findUserByName("模糊用户名");
	
	//#{name} 当前是一个参数 //里面随便填(但是不能为空)也可以还是会正常运行 但要注意语义化
	//!!! 不能用这个方法进行多条件查询
	
```

#### select实现多条件查询

```
	
	根据用户模糊名称 和用户角色 查找用户信息  (带参数返回复杂类型)(实体类传递多参)(自动映射)
	
	接口
		public List<User> findUserByNameAndWork(User user); //此处user包装了请求参数
	映射文件
		<select id="findUserByNameAndWork" parameterType="User" resultType="User">
			SELECT * FROM user_base WHERE workId = #{workId} AND name LIKE CONCAT('%',#{name},'%') 
			//双引号|单引号
			//此处#{xx} xx为实体类对象的属性
		</select>
	调用映射器
		User user = new User();
		user.setName("模糊用户名");
		user.setWorkId(1);
		List<User> userList = sqlSession.getMapper(UserMapper.class).findUserByNameAndWork(user);
	
```

```
	
	根据用户模糊名称 和用户角色 查找用户信息  (带参数返回复杂类型)(Map传递多参)(自动映射)
	
	接口
		public List<User> findUserByNameAndWork(Map map); //此处user包装了请求参数
	映射文件
		<select id="findUserByNameAndWork" parameterType="Map" resultType="User">
			SELECT * FROM user_base WHERE workId = #{workId} AND name LIKE CONCAT('%',#{nameKey},'%') 
			//双引号|单引号
			//此处#{xx} xx为Map 的键(key)名 
		</select>
	调用映射器
		Map<String,String> map = new HashMap<String,String>();
		map.put("nameKey","模糊用户名");
		map.put("workKey","1");
		List<User> userList = sqlSession.getMapper(UserMapper.class).findUserByNameAndWork(user);
	
```

```
	
	根据用户模糊名称 和用户角色 查找用户信息  (带参数返回复杂类型)(@Param传参)(自动映射)
	
	接口
		public List<User> findUserByNameAndWork(@Param("name")String,@Param("workId")Integer workId); 
	映射文件
		<select id="findUserByNameAndWork" parameterType="Map" resultType="User">
			SELECT * FROM user_base WHERE workId = #{workId} AND name LIKE CONCAT('%',#{name},'%') 
	调用映射器
		List<User> userList = sqlSession.getMapper(UserMapper.class).findUserByNameAndWork("模糊用户名",1);
	
```

#### select实现跨表自动映射

```
	
	根据用户模糊名称 查找用户信息 注意用户信息需要中文 (需要跨表查询)(带参数返回复杂类型)(自动映射)
	
	实体类添加属性 用户职位中文名属性 cnName //注意要和链表查询 r.cnName 的名称一致 让其可以自动映射 或者可以给其添加别名 例如实体类属性定义成了roleName 就修改查询字段为 r.cnName AS roleName   //注意添加getter setter方法 因为属性都是封装的
	
	接口
		public List<User> findUserByName(String name);
	映射文件
		<select d="findUserByName" parameterType="String" resultMap="User">
			SELECT u.*,r.cnName
        	 FROM user_base AS u JOIN work_base AS r ON u.id = r.id
        	 WHERE u.name LIKE CONCAT('%',#{name},'%')
		</select>
	调用映射器
		List<User> userList = sqlSession.getMapper(UserMapper.class).findUserByName("模糊用户名");
		for (User user : userList) {
                logger.debug(user.getCnName());
         }
     
     //可能出现没有结果 的情况 注意 实体类属性 和 查询字段名称 要一致(起别名)
     //如果字段中出现两个id 比如要查 A表的id和B表的id 就会遭到强制限制性 对应两个实体类属性如果都为id则 会引起混乱(虽然可以解决 再添加新的属性bID这样) 推荐使用自定义映射
     
```

#### select实现自定义映射列表

```
	
	根据用户模糊名称 查找用户信息 注意用户信息需要中文 (需要跨表查询)(带参数返回复杂类型)(自定义映射)(默认映射级别PARTIAL)
	
	实体类添加属性 用户职位中文名属性 cnName //注意要和链表查询 r.cnName 的名称一致 让其可以自动映射 或者可以给其添加别名 例如实体类属性定义成了roleName 就修改查询字段为 r.cnName AS roleName //注意添加getter setter方法 因为属性都是封装的
	
	接口
		public List<User> findUserByName(String name);
	映射文件
		<resultMap type="User" id="UserWorkCnName">
		   <result property="id" column="id" />
		   <result property="name" column="name" />
            <result property="cnName" column="r_cnName" />
           	//省略其它字段映射 使用时注意 映射类型 是否自动映射名称对应字段/实体类属性
           	//property表示查询出来的属性对应的值赋给 实体对象的那个属性
           	//column表示从数据库中查询的列名或别名
        </resultMap>
		<select d="findUserByName" parameterType="String" resultMap="UserWorkCnName">
			SELECT u.*,r.cnName AS r_cnName
        	 FROM user_base AS u JOIN work_base AS r ON u.id = r.id
        	 WHERE u.name LIKE CONCAT('%',#{name},'%')
        	 //resultMap 一个外部resultMap的id 表示返回结果映射到 那个resultMap上
		</select>
	调用映射器
		List<User> userList = sqlSession.getMapper(UserMapper.class).findUserByName("模糊用户名");
		for (User user : userList) {
                logger.debug(user.getCnName());
         }
     //较综合示例 提供了 起别名映射示例 r.cnName AS r_cnName  
     //可以自定义映射结果 高度自定义 好用
     
```

#### select实现高级自定义映射

```
	
    
    根据用户模糊名称 查找用户信息 并且带work表信息  (带参数返回复杂类型)(单参)(高级自定义映射)(实体类与表是一对一关系)
	
	实体类添加属性 表work_base对应的实体类Work(PoJo类) 并添加setter方法 //注意不加cnName属性
	
	接口
		public List<User> findUserByName(String name); //此处user包装了请求参数
	映射文件
		<resultMap type="User" id="userList">
		    <result property="id" column="id" />
		    <result property="name" column="name" />
             ......
             <association property="work" javaType="Work">
             	<id property="id" column="r_id">
             	<result property="cnName" column="cnName"/>
             </association>
             association 属性 元素
             //javaType 完整Java类名或者别名 若映射到JavaBean则MyBatis通常会自行检测类型 若映射到一个HashMap应该明确指定javaType
             //resultMap属性 可以扩展resultMap进行联合映射 可以达到resultMap复用的结果 
             //property属性 映射数据库列的实体对象的属性 是在实体类里定义的属性
             //id元素 指定一个或多个属性来唯一标识结果集 虽然不指定id 也能工作 但是会导致严重的性能开销 所以最好选择 属性结果少的属性 来标识唯一结果 主键或联合主键均可
             //result元素 和普通result元素使用一致 property work实体类属性名 column数据库列名或别名
		</resultMap>
		<select id="findUserByName" parameterType="String" resultMap="userList">
			SELECT u.*,r.cnName,r.id AS r_id
        	 FROM user_base AS u JOIN work_base AS r ON u.id = r.id
        	 WHERE u.name LIKE CONCAT('%',#{name},'%')
			//双引号|单引号
			//此处#{xx} xx为实体类对象的属性
		</select>
	调用映射器
		List<User> userList = sqlSession.getMapper(UserMapper.class).findUserByName("模糊用户名");
		for (User user : userList) {
                logger.debug(user.getWork().getCnName());
         }
     
     //注意内部嵌套映射级别 是PARTIAL还是FULL PARTIAL自动匹配所有属性 内部嵌套除外 FULL匹配所有属性 包含内部嵌套
	
```

```
	
	例如 一个User 可能有 多个地址 比如说家乡地址和现住地址 这样一个User和地址是 一对多关系
	模拟表地址 address_base 字段id 地址address	添加Address实体类
	需求根据User id获取用户和它的地址列表 User添加List<Address> addressList 集合属性
	
	接口
		public User findUserById(int id);
	映射文件
		<resultMap type="User" id="userList">
		    <result property="id" column="id" />
		    <result property="name" column="name" />
             ......
             <collection property="addressList" ofType="Address">
             	<id property="id" column="a_id">
             	<result property="address" column="address"/>
             </collection>
             collection 属性 元素
             //ofType 完整Java类名或者别名 集合所包含的类型
             //resultMap属性 可以扩展resultMap进行联合映射 可以达到resultMap复用的结果 
             //property属性 映射数据库列的实体对象的属性 是在实体类里定义的属性
             //id元素 指定一个或多个属性来唯一标识结果集 虽然不指定id 也能工作 但是会导致严重的性能开销 所以最好选择 属性结果少的属性 来标识唯一结果 主键或联合主键均可
             //result元素 和普通result元素使用一致 property work实体类属性名 column数据库列名或别名
		</resultMap>
		<select id="findUserById" parameterType="int" resultMap="userList">
			SELECT u.*,a.cnName,a.id AS a_id
        	 FROM user_base AS u JOIN address_base AS a ON u.id = a.id
        	 WHERE u.id = #{id}
		<select/>
	调用映射器
		List<User> userList = sqlSession.getMapper(UserMapper.class).findUserByName("模糊用户名");
		for (User user : userList) {
                logger.debug(user.getAddressList()[index].getaddress());
         }
         
	//注意内部嵌套映射级别 是PARTIAL还是FULL PARTIAL自动匹配所有属性 内部嵌套除外 FULL匹配所有属性 包含内部嵌套
	
```

#### insert实现增加操作

```
	
	添加用户信息 (实体类传参)
	
	接口
		public int addUser(User user);
	映射文件
		<insert id="addUser" parameterType="User">
			INSERT INTO user_base(name,sex,workId) VALUES(#{name},#{sex},#{workId})
		</insert>
	调用映射器
		User user = new User();
		user.setName("添加用户名称");
		.....
		int line = sqlSession.getMapper(UserMapper.class).addUser(user);
		
	//返回的是数据库影响行数
	
```

#### update实现修改操作

```
	
	修改用户信息 (实体类传参)
	
	接口
		public int modifyUser(User user);
	映射文件
		<update id="modifyUser" parameterType="User">
			UPDATE user_base SET name=#{name},workId=#{workId} WHERE id=#{id}
		</update>
	调用映射器
		User user = new User();
		user.id(5);
		user.setWordID(2);
		user.setName("xxx");
		.......
		int line = qlSession.getMapper(UserMapper.class).modifyUser(user);
	
```

#### delete实现删除操作

```
	
	删除用户信息 (实体类传参)
	
	接口
		public int deleteUser(int id);
	映射文件
		<update id="deleteUser" parameterType="int">
			DELETE FROM user_base WHERE id=#{id}
		</update>
	调用映射器
		int line = qlSession.getMapper(UserMapper.class).deleteUser(1);
		
```

### 动态SQL

```
	
	https://blog.csdn.net/peach_garden/article/details/80047039 //详细参考 
	
	动态SQL是MyBatis的强大特性
	
	在使用JDBC操作数据时 如果查询条件特别多 将条件串联成SQL字符串是一件痛苦的事情
	通常解决方案是利用if-else条件语句 拼合SQL语句字符串 并不能忘了空格或逗号
	
	MyBatis提供动态SQL语言改善这种情形 动态SQL基于OGNL的表达式 可以方便在SQL语句中实现某些逻辑 实现元素如下
	
	//这里只做简单解释 详细百度
	
	if //利用if实现简单的条件选择
		判断参数 实现简单的条件判断 //简单 复杂条件下 只使用if会出错
		select * from xxxx where 1=1
           <if test="name !=null and name !=''">
               and name like concat('%',#{name},'%')
           </if>
           
	choose(when,othewise) //想当于Java中的Switch语句 通常与when和otherwise搭配  //简单 复杂条件下 只使用choose会出错 //注意条件满足就会跳出choose
		select * from xxxx where 1=1
        <choose> 
            <when test="name !=null and name !=''">
                and name like concat('%',#{name},'%')
            </when>
            <when test="money !=null and money !=''">
                and money = #{money}
            </when>
            <otherwise>
                .......
            </otherwise>
        </choose>
        
	where //简化SQL语句中where的条件判断 //简化SQL语句中where条件判断 //智能处理and和or
		 select * from xxxx
          <where>
          <if test="name !=null and name !=''">
              and name like concat('%',#{name},'%')
          </if>
          </where>
		
	set //解决动态更新语句 //可以在遇到逗号的时候，把对应的逗号去掉 //主要用在update语句
	
	trim //可以灵活地去除多余的关键字  替代where 和 set
		属性
		prefix suffix prefixOverrides suffixOverrides
		prefix suffix //会在trim包含内容的前面 加上某些前缀|后缀
		prefixOverrides suffixOverrides //把包含内容的首部|尾部某些内容覆盖(忽略)

		UPDATE xxxx
        <trim prefix="set" suffixOverrides=",">
            <if test="proCode != null and proCode != ''">proCode = #{proCode},</if>
            <if test="proName != null and proName != ''">proName = #{proName},</if>
        </trim>
        WHERE id = #{id}
        
	foreach //迭代一个集合 通常用于in条件
		属性
		item //表示集合中每一个元素进行迭代时的别名  
		index //指定一个名称用于表示在迭代过程中 每次迭代到的位置
		collection //必须指定 list array map-key
			//若入参为单参数 且 参数类型是一个List的时候 collection属性值为list
			//若入参为单参数 且 参数类型是一个数组的时候 属性值为array
			//若传入参数为多参数 就需要 封装为一个Map进行处理
		open //表示语句以什么开始 因为是in条件 所有必须是以 "(" 开始
		separator //表示每次进行迭代之间以什么符号作为分割符 因为是in条件分割符为","
		close  //表示语句以什么结束 因为是in条件 所有必须是以 ")" 结束
		//功能强大 允许指定一个集合,并指定开始和结束的字符 也可以加入一个分割符到迭代器中 智能处理分割符 不会出现多余的分隔符
		单参数List类型
			public List<Blog> dynamicForeachTest(List<Integer> ids); 
			select * from xxxx where id in  
             <foreach collection="list" item="item" open="(" separator="," close=")">  
                 #{item} 
             </foreach> 
		单参数array数组的类型
            select * from xxxx where id in  
            <foreach collection="array" item="item" open="(" separator="," close=")">  
                #{item} 
            </foreach> 
		多参数传入 可以使用@Param注解 也可以将参数封装成Map
			select * from t_blog where title like "%"#{title}"%" and id in  
             <foreach collection="ids" index="index" item="item" open="(" separator="," close=")">  
                 #{item}  
             </foreach>
			//注意点 更改点 为 foreach collection属性 的值为@Param注解名称 或者 Map的key名
		
		
	使用if+where 实现多条件查询
	使用if+set 实现更新语句SQL拼合
	使用if+trim 实现多条件查询 //推荐 更灵活 
	
```

### MyBatis实现分页功能

```
	
	大体构造很简单 一个方法 设置其方法时 起始位置(from) 页面容量(pageSize) //注意命名就行
	//并且 注意DAO层不涉及 业务实现 所以 传入的参应该是起始位置下标 而不是 用户请求的当前页码 要在 业务逻辑层计算好了之后 传入到方法中
	
```

## Spring

```
	
	企业级应用开发 可以是Spring的出现就是为了满足企业级系统的需求
	
	企业级应用指 为商业组织 大型企业 而创建部署的解决方案和应用
	//结构复杂 涉及外部资源多 事务密集 数据规模大 用户数量多 有较强的安全性考虑和较高的性能要求
	
	当代企业级应用 绝不可能 是一个个的独立系统 在企业中 一般都会部署多个进行交互的应用 同时这些应用都有可能与其他企业相关应用连接 从而构成结构复杂的 跨越Internet的 分布式企业应用集群 此外还要能够满足未来业务需求的变化 易于扩展和维护
	使用传统JavaEE解决 问题时的 重量级架构体系 开发效率、难度、实际性能都让人失望 
	
	Spring致力于 JavaEE应用的各种解决方案 Spring是企业应用开发的 "一站式" 选择 
	Spring贯穿表现层、业务层、持久层 
	Spring不想取代已有框架 而是以高度的开发性与它们无缝整合
	
```

### Spring的绿草丛

```
	
	Spring
		轻量级框架 JavaEE的春天 当前主流框架
	核心
		依赖注入|依赖注入(IOC)和面向切面编程(AOP)
	目标
		使现有的技术更加有易用 推进编码最佳实践(促进良好的编程习惯)
	原则
		不重复开发轮子 已经有较好解决方案的领域 Spring绝不做重复性的实现 例如对象持久化和ORM Spring只是对现有的JDBC、MyBatis、Hibernate等技术提供支持 使它更易用 而不是重新做一个实现
	组成 (了解)
		框架大概有20个功能模块组成 模块被分为6个部分 
		Core Container 、Data Access/Integration、Web、AOP(Aspect Oriented Programming)、Instrumentation、Test
		
		Spring Core //框架的最基础部分 提供了IoC特性
		Spring Context //为企业级开发提供便利和集成的工具
		Spring AOP //是基于Spring Core的符合规范的面向切面编程的实现
		Spring JDBC //提供了JDBC的抽象层 简化了JDBC编码 使代码更健壮
		Spring ORM //对市面上刘翔的ORM框架提供了支持
		Spring Web //为Spring在Web应用中的使用提供了支持
		......其他百度
	
```

### Spring的优点

```
	
	低侵入式设计
    独立于各种应用服务器 真正实现 一次编写，到处运行
    依赖注入特性将组件关系透明化，降低了耦合度 让我们更专注于应用逻辑
    面向切面编程特性允许将通用任务(安全、事务、日志)进行集中式处理
    与第三方框架的良好整合

```

### Spring设计理念

```
	
	面向Bean编程 一切皆Bean
	
```

### Spring框架资源包文件夹目录结构

```
	
	docs 文件夹下包含Spring的相关文档 API参考文档、开发手册
	libs 文件夹存放Spring各个模块的jar文件 每个模块均提供三项内容 开发所需的jar文件 以javadoc 后缀表示的API和 以 sources 后缀表示的源文件
	schema 配置Spring的某些功能时需要用到的schema文件
	
```

### 使用Spring

```
	
	添加Spring lib到项目
	编写程序代码和配置文件(配置Bean)
	获取Bean实例 调用功能方法
	
```

### Spring两大核心技术

```
	
	控制反转(IOC:Inversion of Control)/依赖注入(DI:Dependency Injection)
	面向切面编程(AOP:Aspect Oriented Programming)
	
```

#### 控制反转/依赖注入 SpringIoC

```
	
	控制反转 也称为 依赖注入 是面向对象编程中的一种设计理念 用来降低程序代码之间的耦合度
	
	依赖 在代码中一般指通过局部变量 方法参数 返回值等建立的对于其他对象的调用关系	例如 在A类的方法中 实例化了B类的对象并调用 其方法以完成特定的功能 我们就说A类依赖于B类
	几乎所有的应用都是有两个或者更多的类通过彼此合作 来实现完整的功能 这样增加了程序开发的复杂程度 (在开发一个类的时候,还要考虑对正在使用该类的其他类的影响)
	A类依赖于B 高度耦合 如果需求变化需要替换A中实例化B类中的方法 将导致A中的代码随之发生修改 这样程序将不具备优良的可扩展性和维护性,甚至难以在开发中测试 我们可以利用简单工厂和工厂方法解决这个问题 创建C类 A类调用C类相关方法 C类相关方法中实现B类的方法的创建 并注入到A类中  如果需要更改实现 只需要更改C类中实现B类的方法 避免了A类和B类的耦合
	上面的问题得到了解决 但是大量的工厂类会被 引入开发过程 明显增加了开发的工作量 而Spring能够 替我们分担这些额外的工作 为我们提供完整的IoC实现 让我们专注于业务类和DAO类的设计
	创建被调用者的工作不再由调用者来完成.因此被称为控制反转 创建被调用者实例的工作通常由spring容器来完成,然后注入调用者,因此也称为依赖注入.这样给程序带来很大的灵活性,这样也实现了我们的接口和实现的分离
	简而言之也就是说我们要获得一个对象,不由我们开发者自己创建,而是由我们的容器来注入给我们的程序来使用
	相对于 控制翻转 依赖注入更容易理解 即容器负责把组件所以来的具体对象 注入(赋值) 给组件 从而避免 组件之间 硬编码耦合
	//依赖注入让组件之间 以 配置文件的 形式组织在一起 而不是以硬编码的方式耦合在一起
	
	目的 
		解耦合 实现每个组件时只关注组件内部的事情
		
	作用 
		将组件对象的控制权 从代码本身 转移到外部容器
		组件化思想 分离关注点 使用接口 不在关注实现
		依赖的注入 将组件的构建和使用分开 组件更加灵活
	
```

##### Spring applicationContext.xml配置文件

```
	
	<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xmlns:tx="http://www.springframework.org/schema/tx"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans-3.2.xsd
       http://www.springframework.org/schema/context
       http://www.springframework.org/schema/context/spring-context-3.2.xsd
       http://www.springframework.org/schema/aop
       http://www.springframework.org/schema/aop/spring-aop-3.2.xsd
       http://www.springframework.org/schema/tx
       http://www.springframework.org/schema/tx/spring-tx-3.2.xsd"
>
    <!-- 配置组件 -->
    <!-- 通过bean元素 声明需要Spring创建的实例 该实例的类型通过class属性指定 并通过id属性为该实例指定一个名称 以便访问 name属性还可以指定多个别名 名字之间使用逗号|分号|空格进行分隔 -->
    <bean id="定义Bean实例的名称" class="定义Bean实例的类型">
    	<!-- property元素用来为实例的属性赋值 此处原理是调用class中指定属性的setter方法实现赋值操作 一对property一个属性 -->
    	<property name="实例属性名称">
    		<value>注入属性的值</value>
    	</property>
    	//也可以向下面这样
    	<property name="实例属性名称" value="注入属性的值"></property>
    </bean>
</beans>
	
```

```
	
	区片解释 防止混乱
	
	//面向接口编程 一切皆Bean
	
	
	<property name="实例属性名称">
    		<value>注入属性的值</value>
    </property>
	<property name="实例属性名称" value="注入属性的值"></property>
	
	//像这两种属性赋值 是通过调用属性的setter方法实现的 称为设值注入 而不是直接给属性赋值 若属性名为show但是setter方法名字为setSShow() Spring配置文件应该写成name="sShow" 而不是show 一定要注意setter方法规范
	//value属性用于注入基本数据类型以及字符串类型值
	//ref属性用于注入已经定义好的bean 面向接口编程的好处就出来了 只要class指定的类是 接口的实现列就能注入(联合 使用示例理解)
	
	
	举例要组装一台打印机 有墨盒(颜色属性) 纸张(大小)
	将墨盒 纸张看成Bean 之后 在 创建打印机Bean之后在配置文件 将墨盒Bean和纸张Bean组装成打印机Bean 之后通过 ApplicationContext 实例化
	//这里将墨盒和纸张 定义成接口  墨盒可以有多种颜色 纸张有多种大小 将它们写成实体类 之后通过Bean给属性根据墨盒或纸张的特征定义成不同 的Bean  蓝色墨盒Bean 黑色墨盒Bean A4纸Bean A5纸Bean 之后创建打印机Bean(还有打印机实体类 里面包含墨盒和纸张 接口属性 利用设值注入(ref) 等组装打印机Bean 之后在使用测试类 或者 实用类 通过ApplicationContext实例化 调用打印机打印方法......
	//实体类实现接口 -防止蒙圈 不要忘了
	
```

##### 在测试类、使用类中使用Spring Bean示例

```
	
 ApplicationContext applicationContext = new ClassPathXmlApplicationContext("applicationContext.xml");
    //通过ClassPathXmlApplicationContext实例化Spring的上下文
    //ApplicationContext是一个接口 负责读取Spring配置文件 管理对象的加载、生成 维护Bean对象与Bean对象之间的依赖关系 负责Bean的生命周期等 ClassPathXmlApplicationContext是ApplicationContext接口的实现类 用于从classpath路径中读取Spring配置文件 
    //除了这种 这种实现还可以通过BeanFactory接口及其实现类对Bean组件进行管理 ApplicationContext是其子接口 可以对企业级开发提供更全面的支持 详细百度
 转换出来的类型 xxxx = (取出来是对象需要强制转换)applicationContext.getBean("配置文件中bean的id");
 	//注意面向接口编程  转换出来的类型 最好为接口 可以根据需求 更改接口的实现
	//通过ApplicationContext的getBean()方法 根据id来获取Bean的实例
	
```

#### 面向切面编程 SpringAop

```
	
	面向切面编程(Aspect Oriented Programming,AOP) 是软件编程思想发展到一定阶段的产物
	//它是对面向对象编程(Object Oriented Programming,OOP) 的 有益 补充 一般适用于 具有横切逻辑的场合 如访问控制 事务管理 性能监测等
	//在业务系统中 总有一些散落、渗透到系统各处且不得不处理的事情 这些穿插在既定业务中的操作 就是所谓的 横切逻辑 也称为切面 例如日志、异常处理、事务控制 为了保证系统健壮可用 就要在众多业务方法反复编写类似的代码
	//那么如果想不瘦这些附加要求的干扰 我们很容易想到将重复性的代码 抽取出来 放在专门的类和方法中 这样便于管理和维护 但依然无法实现既定业务和横切逻辑的彻底解耦合(代码还要保留这些方法的调用代码 当需要增加减少横切逻辑的时候 还要修改业务方法中的调入代码)我们希望无需编写显示的调用 在需要的时候 系统能够 自动 调用所需的功能 这是AOP要解决的问题
	//面向切面编程 简单的说就是 在不改变原程序的基础上 为代码 增加新的功能 对代码进行增强处理 它的设计思想源于代理设计模式 这种模式下 给编程人员的感觉是 在原有代码乃至原业务流程都不修改的情况下 直接在业务流程中切入新代码 增加新功能 这就是所谓的面向切面编程
	
	目标 
		从系统中分离出切面 独立于业务逻辑实现 让我们可以专心做事 在程序执行时 织入程序运行
	
	原理 
		将复杂的需求分解出不同方面 将散布在系统中的公共功能集中解决
		采用代理机制组装起来运行 在不改变原程序的程序基础上对代码段进行增强处理 添加新的功能
	理解
		//就是在预编译和运行期动态代理的方式 是在不修改源代码的情况下动态给程序添加功能的技术
		//AOP是一种思想 与具体实现技术无关 任何一种符合AOP思想的 技术实现 都可以看做是AOP 通过Java的动态处理机制 就能很容易实现AOP的思想 实际上Spring的AOP也是建立在Java的代理机制上
		//AOP实际上是由目标类的代理类实现的。AOP代理其实是由AOP框架动态生成的一个对象，该对象可作为目标对象使用。AOP代理包含了目标对象的全部方法，但是AOP代理中的方法与目标对象的方法存在差异，AOP方法在特定切入点添加了增强处理，并回调了目标对象的方法
	
```

##### 面向切面编程基本概念

```
	
	切面(Aspect) //一个模块化的横切逻辑(或称横切关注点) 可能会横切多个对象
	连接点(Join Point) //程序执行中的某个具体的执行点 
	增强处理(Advice) //切面在某个特定连接点上执行的代码逻辑
	切入点(Pointcut) //对连接点的特征进行描述 可以使用正则表达式 增强处理和一个切入点表达式相关联 并在于这个切入点匹配的某个连接点上运行
	目标对象(Target object) //被一个或多个切面增强的对象
	AOP代理(AOP proxy) //由AOP框架所创建的对象 实现执行增强处理方法等功能
	织入(Weaving) //将增强处理连接到应用程序中的类型或对象上的过程 AOP有三种织入的方式 编译期织入、类装载期织入、动态代理织入(Spring采用)
	增强处理类型 //前置增强、后置增强、环绕增强、异常抛出增强、最终增强
	
	//面向切面编程主要关心两个问题 在什么位置 执行什么功能
	
```

##### 使用Spring AOP实现日志输出示例(解释 重要部分意义和写法 仅作参考)

```
	
    实现步骤 
    	在项目中添加Spring AOP的jar文件
    	创建增强类 在其中编写前值增强和后置增强实现日志功能
	    编写Spring配置文件 对业务方法进行增强 处理
	    编写代码 获取带有增强处理的业务对象
	
```

```
	
	目标方法  //该类没有日志功能 给其添加日志功能 //用户业务类 实现对User功能的业务管理
	
	public class UserServiceImpl implements UserService{
	
		//声明接口类型的引用和具体实现类解耦合
		public UserDao dao;
		
		//dao属性的setter访问器
		public void setDao(UserDao dao){
			this.dao = dao;
		}
		
		//目标对象
		@Override
		public int addNewUser(User user){
			调用用户Dao的方法 保存用户信息
			return dao.save(user);
		}
	}
	
```

```
	
	UserDao接口 面向接口编程 降低依赖
	
    public interface UserDao {
        /**
         * 模拟储存到数据库方法 
         * @param user
         * @return
         */
        public int save(User user);
    }
	
	UserDaoImpl UserDao接口实现类 
	
	public class UserDaoImpl  implements UserDao {

        @Override
        public int save(User user) {
            System.out.println("保存用户信息方法已调用!"); //模拟保存到数据库
            return 1;
    }
}
	
```

```
	
	创建 增强处理对象 就是写增强方法的     你要增强什么
	
	//增强类有两个方法 我们希望把before()方法作为前置增强使用 目标方法之前执行before()方法
	//afterReturing() 方法做为后置增强使用 目标方法之后执行 afterReturing()
	//为了能够在增强方法中获得当前 连接点的信息 以便实施相应的 判断和处理 可以在增强方法中声明一个JoinPoint类型的参数 Spring会自动注入该实例 通过 
	//该实例的getTarget()方法 得到被代理对象的目标对象
	//getSignature()方法返回被代理的目标方法
	//getArgs()方法 返回传递给目标方法的参数数组 
	//对于后置增强方法还可以 定义一个参数(Object result)用于接收 目标方法 的返回值
	
	/**
     * UserServiceLogger 用户业务逻辑处理 日志增强实现类 
     * 定义包含增强方法的JavaBean
     */
    public class UserServiceLogger {
        private static Logger logger = Logger.getLogger(UserServiceLogger.class);

        /**
         * 前置增强方法
         * @param joinPoint AOP连接点对象
         */
        public void before(JoinPoint joinPoint){
            logger.debug("调用"+joinPoint.getTarget()+"的"+joinPoint.getSignature().getName()
                    +"方法-方法入参:"+joinPoint.getArgs());
        }
        
        /**
         * 后置增强方法
         * @param joinPoint AOP连接点对象
         * @param result 方法返回值
         */
        public void afterReturing(JoinPoint joinPoint,Object result){
            logger.debug("调用"+joinPoint.getTarget()+"的"+joinPoint.getSignature().getName()
                    +"方法-方法返回值:"+result);
        }
    }
	
```

```
	
	Spring配置文件中相关组件 进行声明 在bean中需要添加aop名称空间 导入AOP相关的标签
	
	<aop:config>
        <aop:pointcut id="pointcut" expression="execution(public int addNewUser(..))"/>
        <aop:aspect ref="theLogger">
                <aop:before method="before" pointcut-ref="pointcut"></aop:before>
                <aop:after-returning method="afterReturing" pointcut-ref="pointcut" returning="result"/>
        </aop:aspect>
    </aop:config>
	
	//与AOP相关的 配置 都放在 <aop:config> 标签中
	//<aop:pointcut> 标签用于定义切入点 简单说 就是 连接点 的 查询条件 id是这个切入点的名称 expression属性是 切入点指示符 它的括号中是一个切入点表达式 可以配置需要切入增强处理的方法的特征 
	//切入点支持 模糊匹配 常用模糊匹配 有以下几种
		public * addNewUser(entity.User); //* 表示匹配所有类型的返回值
		public void *(entity.User); //* 表示匹配所有方法
		public void addNewUser(..); //..表示匹配所有 参数个数和类型的 该方法
		* com.service.*.*(..); //这个表达式匹配com.service包下所有类 的所有方法
		* com.service..*.*(..); //这个表达式匹配com.service包及其子包下所有类的所有方法
	    可以根据需求 设置匹配规则 其它规则百度
	//<aop:aspect>定义切面 ref属性用来指定 增强处理类(包含增强方法) 相关增强处理标签的method属性 用来指定增强处理类中的增强方法
	//<aop:aspect>引用包含增强方法的Bean 然后通过<aop:before>和<aop:after-returning>将方法声明为 前置增强和后置增强 在<aop:after-returning>中可以通过returning属性指定需要注入返回值的属性名 方法的JoinPoint类型参数无须特殊处理 Spring会自动为其注入连接点实例 pointcut-ref属性指定切入点
	//UserService的addNewUser()方法可以和切入点pointcut相匹配 Spring会生成代理对象在它执行前后分别调用 前置增强和后置增强 这样就完成了日志输出
	
	
	<?xml version="1.0" encoding="UTF-8"?>
    <beans xmlns="http://www.springframework.org/schema/beans"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xmlns:context="http://www.springframework.org/schema/context"
           xmlns:aop="http://www.springframework.org/schema/aop"
           xsi:schemaLocation="http://www.springframework.org/schema/beans
           http://www.springframework.org/schema/beans/spring-beans-3.2.xsd
           http://www.springframework.org/schema/context
           http://www.springframework.org/schema/context/spring-context-3.2.xsd
           http://www.springframework.org/schema/aop
           http://www.springframework.org/schema/aop/spring-aop-3.2.xsd
           http://www.springframework.org/schema/tx"
    >
        <bean id="userDao" class="com.ttelite.smbms.dao.impl.UserDaoImpl"></bean>
        <bean id="userService" class="com.ttelite.smbms.service.UserServiceImpl">
            <property name="dao" ref="userDao"></property>
        </bean>
    <!--        定义包含增强方法的类Bean利于 之后进行指定增强方法-->
        <bean id="theLogger" class="com.ttelite.smbms.log.UserServiceLogger"></bean>
        <aop:config>
    <!--        定义切入点 指出 在什么地方进行增强-->
            <aop:pointcut id="pointcut" expression="execution(public * addNewUser(..))"/>
    <!--        理解为具体 目标对象 的 哪里使用什么增强 -->
            <aop:aspect ref="theLogger">
    <!--        将before()方法定义为前置增强 并 引用pointcut切入点-->
                <aop:before method="before" pointcut-ref="pointcut"></aop:before>
    <!--        将afterReturning()方法定义为后置增强并引用pointcut切入点-->
    <!--        通过returning属性指定为名Wieresult的参数注入返回值-->
                <aop:after-returning method="afterReturing" pointcut-ref="pointcut" returning="result"/>
            </aop:aspect>
        </aop:config>
	</beans>

```

```
	
	测试类 或者 Servlet等
	
	public class TestUserService {
        @Test
        public void testAddNewUser(){
            //通过ClassPathXmlApplicationContext实例化Spring的上下文
            ApplicationContext applicationContext = new ClassPathXmlApplicationContext("applicationContext.xml");
            //通过ApplicationContext的getBean()方法 根据id来获取Bean的实例
            UserService userService = (UserService)applicationContext.getBean("userService");
            //通过实例调用业务处理方法
            userService.addNewUser(new User());
	    }
}

```

### IoC和AOP使用扩展

#### 构造注入

```
	
	可以通过 构造方法 为业务类注入 所依赖的 数据访问层对象 实现保存用户数据的功能
	
	在业务类 创建带参构造方法 之后 在Spring配置文件 进行构造方法进行 属性注入
	//注意 业务类编写 构造方法后 需要自行添加无参构造方法  有了任何构造方法 jvm就不自动生成
	
	在Spring配置文件 中通过<constructor-arg>元素 为构造方法 传参
	<bean id="userDao" class="dao.impl.UserDaoImpl" />
    <bean id="userService" class="service.impl.UserServiceImpl">  
    	<constructor-arg><ref bean="userDao" /></constructor-arg>
    </bean>
	//一个<constructor-arg> 元素表示构造方法 的一个参数 且使用时 不区分顺序
	//<constructor-arg> 通过 其属性 index  指定该参数的位置索引(从0开始)
	//<constructor-arg> 还提供了type属性 用来指定参数的类型 避免字符串和基本数据类型的混淆
	
```

#### 设值注入和构造注入的区别

```
	
	设值注入
	
		通过setter 访问器实现 
		灵活性好 但setter方法数量多
		时效性差  
		通过无参构造实例化
	
	构造注入
		
		通过构造方法实现
		灵活性差 仅靠重载限制太多 受限于重载的形式
		时效性好 在对象实例化时 就得到所依赖的对象 便于在对象的初始化方法中使用依赖对象
		通过匹配的构造方法 实例化但 建议保留无参构造方法
	
```

#### 使用p命名空间实现属性注入

```
	
	Spring 从2.0版本 开始采用schema形式 使用不同的命名空间管理 不同类型的配置
	
	Spring 基于 schema的配置方案 为许多领域的问题 提供了简化的配置方法 大大简化了配置工作量
	
	p命名空间  是使用属性 而不是子元素 的形式配置Bean的属性 从而简化了Bean的配置
	
	使用前要在Spring配置文件 中 引入p命名空间
	xmlns:p="http://www.springframework.org/schema/p"

	语法
		对于直接量(基本数据类型、字符串)属性 
		p:属性名="属性值"
		对于引用Bean的属性
		p:属性名-ref="Baen的id"
		
		//注意 虽然是p:属性名 但是属性名 指的还是setter方法的 对应名 
		
	使用p命名空间注入属性值
		<bean id="user" class="entity.User" p:age="23" p:username="张三" 	p:email="zhangsan@xxx.com" />
	    <bean id="userService" class="service.impl.UserServiceImpl" p:dao-ref="userDao" />
	
```

#### 注入不同数据类型

```
	
	Spring 提供了不同 的标签来实现 各种 不同类型参数的注入  对于设值注入 和 构造注入 都适用
	这里以设值注入 为例  对于构造注入 将标签添加到<constructor-arg>与</constructor-arg>中间即可
	
	注入直接量(基本数据类型、字符串)
		//对于 基本数据类型 及其 包装类、字符串 除了可以使用value属性 还可以通过<value>子元素进行注入
	
	如果属性值包含了XML的特殊字(&、<、>、"、') 注入时需要进行处理 通常有两种方法 
		//使用<![CDATA[]]>标记    
		例 <value><![CDATA[p&G]]></value>
		//特殊字符 替换为 实体引用 XML有5个预定义的实体引用 <[&lt;]、'[&apos;]、"[&quot;]、&[&amp;]、>[&gt;]
		例 <value>p&amp;G</value>
	
```

```
	
	引用其它Bean组件
		//除了ref属性 还可以通过<ref>子元素进行注入
		//ref子元素基友 local属性 它与bean属性的用法是一致的 但是区别是Spring的配置文件 可以拆分成多个 使用local属性只能在同一个配置文件中 检索bean的id  bean属性可以在其它配置文件中检索
	使用内部Bean
		//如果Bean组件仅在 一处需要使用 可以把它定义为内部Bean 就是在 <property/>或 <constructor-arg/> 元素内使用<bean/> 元素
		例 <property name="dao"> <bean class="dao.impl.UserDaoImpl"/> </property>

```

```
	
	注入集合类型的属性
	
	对于List或数组类型的属性 可以使用<list>标签注入
	
		<property name="xxx">
            <list>
                <value>1</value>
                <value>2</value>
            </list>
         </property>
	
	//<list>标签中间 可以使用 <value> <ref> 注入集合元素  甚至是另一个<list>标签
	
	
	Set类型的属性 <set>
	
		<property name="xxx">
            <set>
                <value>1</value>
                <value>2</value>
            </set>
         </property>
	
	
	Map类型的属性  <map> <entry> <key> 
	
		<property name="xxx">
            <map>
                <entry> //一个entry相当于一个 键值对
                	<key><value>键值</value></key>
                	<value>value值</value>
                </entry>
                <entry> //注意键值 是唯一的
                	<key><value>键值</value></key>
                	<value>value值</value>
                </entry>
            </map>
         </property>
	
	//如果map中的键或值是Bean对象 可以吧上面代码中的 <value>换成<ref>
	
	
	对于Properties类型的属性
		
		<property name="xxx">
			<props>
				<prop key="键值">value值</prop>
				<prop key="键值">value值</prop>
			</props>
		</property>
	
	//通常 键和值 都是字符串类型
	
	
	注入null和空字符串值
		//可以使用<value></value> 注入空字符串值
		//使用<null/>注入null值  例 <property name="xxx"><null/></property> 注意外面没有<value>标签 
	
```

#### 其它增强类型

```
	
	//只解释部分 结合 面向切面 使用示例进行 使用理解  
	
	前置增强 <aop:before>
	后置增强 <aop:after-returing>  可通过属性 returning属性 获取方法运行后的返回值
	
	异常抛出增强 <aop:after-throwing> 可通过属性 throwing属性 获取方法抛出的异常
		//在目标方法抛出异常时 织入增强处理 使用异常抛出增强
		//可提供统一 可插拔的异常处理方案
		例
			增强方法
			public void afterThrowing(JoinPoint jp,RuntimeException e){
				//jp.getSignature().getName()+"方法异常"+e
			}
			配置文件
			<aop:after-throwing method="afterThrowing" pointcut-ref="pointcut" throwing="e" />
	
	最终增强 <aop:after> 
		//无论方法抛出异常还是正常退出 该增强都会得到执行 类似于finally块的作用
		//一般用于释放资源
		例
			增强方法
			public void addLogger(JoinPoint jp){
				//jp.getSignature().getName()+"方法结束执行"
			}
			配置文件
			<aop:after method="addLogger" pointcut-ref="pointcut" />
	
	环绕增强 <aop:around>
		//在目标方法的前后都可以织入增强处理
		//功能最强大的增强处理
		//可获取或修改目标方法或修改目标方法的参数、返回值、可以对方法进行异常处理 甚至决定目标方法是否被执行
		//通过为增强方法声明ProceedingJoinPoint类型的参数 可以获得连接点信息 所用方法与JoinPoint相同
ProceedingJoinPoint是JoinPoint的子接口 其不但封装了 目标方法和入参数组  还封装了被代理的目标对象 通过他的proceed()方法可以调用真正的目标方法  实现对连接点的完全控制
		例
			增强方法
			public Object aroundLogger(ProceedingJoinPoint jp)throws Throwable{
				log.info("调用"+jp.getTarget()+"的"+jp.getSignature().getName()+"方法"+"方法入参"+Arrays.toString(jp.getArgs()));
				try{
					Object result = jp.proceed(); //执行目标方法并获取其返回值
					log.info(//省略);
					return result;
				}catch(Throwable e){
					log.error(//省略);
					throw e;
				}finally{
					//关闭流对象
					log.info(//省略);
				}
			}
			配置文件
			<aop:around method="aroundLogger"  pointcut-ref="pointcut"/>
	
```

#### 常用增强处理类型 概述表

|  增强处理类型  |                             特点                             |
| :------------: | :----------------------------------------------------------: |
|     Before     |                前置增强 在目标方法前织入增强                 |
| AfterReturning |      后置增强 在目标方法正常执行(不出现异常)后织入增强       |
| AfterThrowing  |            异常增强 在目标方法抛出异常后织入增强             |
|     After      |  最终增强 不论方法是否抛出异常 都会在目标方法 最后织入增强   |
|     Around     | 环绕增强 在目标方法全方位 都可以织入增强 甚至让目标方法不执行 |

#### Spring AOP配置元素 简述表

|        AOP配置元素        |                  描述                   |
| :-----------------------: | :-------------------------------------: |
|      < aop:config >       | AOP配置顶级元素 大部分aop:*元素都在其下 |
|     < aop:pointcut >      |                定义切点                 |
|      < aop:aspect >       |                定义切面                 |
|       < aop:after >       |                最终增强                 |
|  < aop:after-returning >  |                后置增强                 |
|  < aop:after-throwing >   |                异常增强                 |
|      < aop:around >       |                环绕增强                 |
|      < aop:before >       |                前置增强                 |
| < aop:aspectj-autoproxy > |       启动@AspectJ注解驱动的切面        |

### 使用注解实现IoC

#### 注解解释

```
	
	Spring从 2.0版本 开始注入注解的配置方式 将Bean的配置信息 和 Bean实现类结合在一起 进一步减少了配置文件的代码量
	
	注解方式 将Bean的定义信息 和 Bean实现类结合在一起 注解包括  //定义组件
	
	@Component 实现Bean组件的定义
	@Repository 用于标注DAO类
	@Service 用于标注业务类
	@Controller 用于标注控制器类
	
	例
		@Repository("userDao")
		public class UserDaoImpl implements UserDao{
			...	
		}
		与XML配置中 编写以下代码 等效
		<bean id="userDap" class="dao.impl.UserDaoImpl" />
			
	//都可以 标注Bean组件 只是 更语义化更好的 表示类型
	//使用特定的注解使组件的用途更加清晰 并且Spring 在以后的版本 可能会为它们添加特殊的功能 所以推荐使用特定的注解 来标注特定的实现类
		
	Spring提供了@Autowired注解实现Bean的装配
	//使用@Autowired注解实现Bean的自动装配 默认按类型匹配  若一个容器中有一个以上类型相匹配的Bean时 可以使用@Qualifier指定Bean的名称
	
	!!!注意 在设置注解完成后 需要使用注册信息启动Spring容器(在核心配置文件添加component-scan标签)
	<!-- 扫描包中注解标注的类 -->
	<context:component-scan base-package="//指定需要扫描的基类包 多个包可以用逗号隔开">
	
```

#### 使用注解拼装注解 示例

```
	
	//UserDao接口
	public interface UserDao {
   		 public void save(User user);
	}
	
	//UserDaoImpl  UserDao接口实现类
	@Repository("userDao")
    public class UserDaoImpl implements UserDao {
        @Override
        public void save(User user) {
            System.out.println("保存用户信息到数据库");
        }
    }

	//UserService接口
	public interface UserService {
        public void save(User user);
    }
	
	//UserServiceImpl  UserService接口实现类
	@Service("AA")
    public class UserServiceImpl implements UserService {
        @Autowired
        private UserDao userDao;
        @Override
        public void save(User user) {
            userDao.save(user);
        }
    }
    
    //如果有一个以上类型相匹配的Bean时 使用@Qualifier指定Bean 可以对类的成员变量进行标注
    //UserServiceImpl  UserService接口实现类
	@Service("AA")
    public class UserServiceImpl implements UserService {
        @Autowired
        //@Qualifier("userDao")
        private UserDao userDao;
        @Override
        public void save(User user) {
            userDao.save(user);
        }
    }
    
    //如果有一个以上类型相匹配的Bean时 使用@Qualifier指定Bean 也可以对方法的入参进行标注 也可适用于构造方法
    //UserServiceImpl  UserService接口实现类
	@Service("AA")
    public class UserServiceImpl implements UserService {
        private UserDao userDao;
        @Autowired
        public void setUserDao((@Qualifier("userDao")UserDao userDao)){
        	this.userDao = userDao;
        }
        .......
        @Override
        public void save(User user) {
            userDao.save(user);
        }
    }
    
    核心配置文件
    <beans xmlns="http://www.springframework.org/schema/beans"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xmlns:context="http://www.springframework.org/schema/context"
        xsi:schemaLocation="......
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context-3.2.xsd">
        <!-- 扫描包中注解标注的类 -->
        <context:component-scan base-package="//指定需要扫描的基类包" />
    </beans>

	//使用@Autowired注解进行 装配时 如果找不到匹配的Bean组件 Spring就会抛出异常 此时如果依赖不是 必须的 为了避免抛出异常 可以将required属性设置成false   required属性默认为true 即必须找到匹配Bean否则异常
	例 
		@Autowired(required = false)
		private UserDao userDao;
	
	//如果对类中集合类型的成员变量 或 方法入参 使用@Autowired注解 Spring会将 所有和集合中元素匹配类型的Bean组件都注入进来 可以轻松 灵活地实现任务组件的识别和注入工作
	例
		@Autowired(required = false)
		private List<Job> toDoList;
	
```

#### 使用Java标准注解完成装配

```
	
	除了@Autowired注解 也可以通过 @Resource注解 实现组件装配
	
	@Resource 有一个name属性 默认情况下Spring将 这个属性的值 解释为要注入的Bean的名称
如果没有显式的 指定Bean的名称 注解将根据字段名或者setter方法名产生默认的 名称 -如果注解应用于setter方法 名称为通过setter方法得到的属性名 -应用于字段名 使用字段名 作为Bean的名称
	例	
	    @Resource(name = "bean名称") //为userDao属性注入名为 bean名称 的Bean
		private UserDao userDao;
	
	    @Resource //为userDao属性注入名为 userDao 的Bean
		private UserDao userDao;
	
		private UserDao userDao;
		@Resource //为userDao属性注入名为 userDao 的Bean
		public void setUserDao(UserDao userDao){
			this.userDao = userDao;
		}
	
```

### 使用注解定义切面AOP

```
	
	AspectJ 是一个面向切面的框架 扩展了Java语言 定义了AOP语法 能够在编译器提供代码的织入 
	
	@AspectJ 是 AspectJ 5 新增的功能 使用JDK5.0 注解技术 和正规的AspectJ切点 表达式语言 描述切面
	//!!! 使用@AspectJ 首先要保证所用JDK是5.0或以上
		
	Spring通过集成AspectJ 实现了以注解的方法定义切面 大大减少了配置文件 的工作量
	此外因为Java的反射机制 无法获取方法参数名 Spring集成了轻量级 的字节码处理框架asm(已集成在Spring Core模块中) 处理@AspectJ中所描述的方法参数名
	
	就是在增强方法的类中
		首先编写Spring配置文件 完成切面织入
			//<aop:aspectj-autoproxy />启用对于@AspectJ注解的支持
		之后使用注解 定义其增强类型 和增强使用的切入点 ！！！注意还要在核心配置文件注册定义好的切面
			@Aspect //标注整个 包含增强方法的类
			@Before //前置增强
			@AfterReturning //后置增强 
				//如果使用返回值 注意 必须在@AfterReturning注解中 通过returning属性指定该参数的名称
			@AfterThrowing //异常增强
				//如果需要获取抛出的异常 必须在@AfterThrowing注解中 通过throwing属性指定该参数名称
			@After //最终增强
			@Around //环绕增强
		
		注册定义好的切面
			在配置文件中声明增强处理类的Bean 如果不需要被其它Bean使用 可以不指定id属性
		
	例
		/**
         * UserServiceLogger 用户业务逻辑处理 日志增强实现类
         */
        @Aspect
        public class UserServiceLogger {
            private static Logger logger = Logger.getLogger(UserServiceLogger.class);

            /**
             * 前置增强方法
             * @param joinPoint AOP连接点对象
             */
            @Before("execution(public int addNewUser(..))")
            public void before(JoinPoint joinPoint){
                logger.debug("调用"+joinPoint.getTarget()+"的"+joinPoint.getSignature().getName()
                        +"方法-方法入参:"+joinPoint.getArgs());
            }

            /**
             * 后置增强方法
             * @param joinPoint AOP连接点对象
             * @param result 方法返回值
             */
            @AfterReturning(value = "execution(public int addNewUser(..))",returning = "result") //注意如果需要使用返回值 需要在注解中标注
            public void afterReturing(JoinPoint joinPoint,Object result) {
                logger.debug("调用" + joinPoint.getTarget() + "的" + joinPoint.getSignature().getName()
                        + "方法-方法返回值:" + result);
            }
        }
	
	//以上例子 @Before注解 和@AfterReturning注解 分别指定了 各自的切入点 为UserService接口的所有方法 对于相同的的切入点需求 可以统一定义(@Pointcut) 便于重用和维护
	例
		@Pointcut("execution(public int addNewUser(..))")
		public void pointcut(){}
		//切入点签名需要 通过一个普通的方法定义来提供
		//作为切入点签名的方法 必须返回void类型
		
		
		//增强就可以这样写 
		//!!! 注意增强注释中()必须写 不写报错
		@Before("pointcut()")
		@AfterReturning(pointcut = "pointcut()",returning = "result")
	
	//核心配置文件
	
		<context:component-scan base-package="扫描注解包位置"/> //指定扫描注解包
	    <aop:aspectj-autoproxy></aop:aspectj-autoproxy> //开启AspectJ注解
	    <bean class="UserServiceLogger位置"></bean> //注册定义好的切面
	
```

```
	
	Spring在定义切面时提供了多种选择 应根据项目的具体情况做出选择 

	如果项目采用JDK 5.0或以上版本 可以考虑使用@AspectJ注解方式 减少配置的工作量

	如果不愿意使用注解或项目采用的JDK版本较低无法使用注解 则可以选择使用<aop:aspect>配合普通JavaBean的形式
	
```

## MyBatis与Spring的整合

### Spring和MyBatis的整合步骤		

#### 建立Web工程 加入Spring和MyBatis的有关JAR

```
	
		//MyBatis-Spring.jar 整合资源包
		//aopalliance-1.0.jar
		//aspectjweaver-1.6.9.jar
		//spring-jdbc-3.2.13.RELEASE.jar //Spring数据源支持
		//spring-tx-3.2.13.RELEASE.jar	//Spring事务支持
		//mysql-connector-java-5.1.45-bin.jar
		//log4j-1.2.17.jar
		//mybatis-3.2.2.jar
		//spring-aop-3.2.13.RELEASE.jar
		//spring-beans-3.2.13.RELEASE.jar
		//spring-context-3.2.13.RELEASE.jar
		//spring-core-3.2.13.RELEASE.jar
		//spring-expression-3.2.13.RELEASE.jar
		//commons-dbcp-1.4.jar dbcp数据源技术
		//commons-pool-1.6.jar dbcp数据源技术
		
		...等等 !!!此jar列表可能不准确
	
	
```

#### 根据需求自己琢么的步骤

```
	
	建立开发目录结构 创建实体类
	创建数据访问接口
	配置SQL映射语句文件 //和MyBatis创建相同 //根据需求

```

#### 配置MyBatis应用配置文件

```
	
	//因为Spring可以接管 MyBatis配置信息的维护工作 所以这里把数据源配置 和SQL映射信息转移至Spring配置文件中
	
	<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN" "http://mybatis.org/dtd/mybatis-3-config.dtd">
		<configuration>
			<!-- MyBatis运行特性全局设置 -->
            <settings>
                <!-- 配置mybatis的log实现为LOG4J -->
                <setting name="logImpl" value="LOG4J"/>
            </settings>
            <!-- 配置类型别名 -->
            <typeAliases>
                <!-- 使用别名指定实体类 -->
                <!--<typeAlias alias="user" type="com.ttelite.smbms.pojo.User"/>-->
                <!-- 指定实体类的基准包路径 -->
                <package name="com.ttelite.smbms.pojo"/>
            </typeAliases>
		</configuration>	
	
```

#### 配置Spring应用配置文件以及测试使用

```
	
	//首先对于 任何 持久化解决方案 数据库都是首先要解决的问题 
	//在Spring数据源可以作为一个重要的组件可以单独进行配置和维护
	//数据源实现技术 现在流行的有dbcp、c3p0、Proxool等 都实现了连接池 功能 
	//这里以dbcp技术配置数据源
	
	dbcp 属于Apache Commons项目  引入jar包
		//commons-dbcp-1.4.jar
		//commons-pool-1.6.jar
	
	要在Spring中使用MyBatis 需要在Spring的配置文件中定义一些类
	SqlSessionFactoryBean //为应用提供SqlSession对象资源
	SqlSessionTemplate //负责管理MyBatis的SqlSession 调用SQL映射语句 实现对数据库的访问
	MapperFactoryBean //根据指定Mapper接口生成Bean实例 或者下面这个
	MapperScannerConfigurer //根据指定包批量扫描Mapper接口并生成实例
	
```

##### Spring配置数据源 dataSource

```
	
	    <bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource" destroy-method="close">
            <property name="driverClassName" value="com.mysql.jdbc.Driver"></property>
            <property name="url" value="jdbc:mysql://127.0.0.1:3306/smbms?useUnicode=true&amp;characterEncoding=utf-8"></property> //注意这里只是示例
            <property name="username" value="root"></property>
            <property name="password" value="密码"></property>
        </bean>
	//注意尽量不要留空格 可能会造成读取错误
	//注意 & 符号的特殊注入方式
	
```

##### 配置SqlSessionFactoryBean

```
	
	//在MyBatis中 SqlSessionFactory 的实例需要使用 SqlSessionFactoryBuilder创建 而在集成环境中 可以使用MyBatis-Spring整合包中的SqlSessionFactoryBean来代替 
	//SqlSessionFactoryBean 封装了使用SqlSessionFactoryBuilder创建SqlSessionFactory的过程 我们可以在Spring配置文件通过配置SqlSessionFactoryBean获取SqlSessionFactory实例
	
	<-- 配置SqlSessionFactoryBean -->
	<bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <!-- 引用数据源组件 -->
        <property name="dataSource" ref="dataSource"></property>
        <!-- 引用MyBatis配置文件中的配置 -->
        <property name="configLocation" value="classpath:mybatis-config.xml"></property>
        <!-- 配置SQL映射文件信息 -->
        <property name="mapperLocations">
            <list>
                <value>classpath:com/ttelite/smbms/dao/UserMapper.xml</value>
                //上面为添加指定的SQL映射文件位置  或者利用下面自动扫描
                <value>classpath:com/ttelite/smbms/dao/**/*.xml</value>
                //这样表示扫目标com/ttelite/smbms/dao包及其任意子包的任意xml类型文件
            </list>
        </property>
    </bean>
	//除了数据源 和 SQL映射信息 其它的MyBatis配置信息 也可以转移至Spring配置文件中 进行维护 只需要通过SqlSessionFactoryBean 的对应属性赋值就行 详细百度
	//例如这个 是配置别名包 <property name="typeAliasesPackage" value="com.zhangguo.bookstore.entities"></property>
	
```

##### 使用SqlSessionTemplate实现数据库的操作

```
	
	//对于MyBatis得到 SqlSessionFactory实例 就可以进一步获取 SqlSession实例进行数据库操作
	//而在集成环境中 为了更好的使用SqlSession 充分利用Spring框架 MyBatis-Spring整合包 提供了SqlSessionTemplate类 它可以替换MyBatis中原有的 SqlSession实现类提供数据库访问操作 使用SqlSessionTemplate 能够 更好地 与Spring服务融合简化部分流程化工作  保证和当前Spring事务相关联 自动管理会话的声明周期 包括必要关闭、提交、和回滚操作
	
	User实体类 //省略
	
	UserMapper接口 //里面就一个抽象方法getUserList() 获取所有用户信息
	
	UserMapper.xml 
		//主要部分
		<select id="getUserList" resultType="User">
            SELECT * FROM smbms_user
        </select>
        
	UserMapperImpl类 //定义Dao接口的实现类 实现UserMapper接口
		public class UserMapperImpl implements UserMapper {
            private SqlSessionTemplate sqlSession;

                /**
                 * 查询所有用户信息
                 *
                 * @return List<User> 用户对象集合
                 */
                @Override
                public List<User> getUserList() {
                    return sqlSession.selectList("com.ttelite.smbms.dao.UserMapper.getUserList");
                }

                //setter方法
                public void setSqlSession(SqlSessionTemplate sqlSession) {
                    this.sqlSession = sqlSession;
                }
            }
	
	Spring配置文件 
	
	 	//省略DataSource和SqlSessionFactoryBean的配置
		<!-- 配置SqlSessionTemplate -->
		<bean id="sqlSessionTemplate" class="org.mybatis.spring.SqlSessionTemplate">
            <constructor-arg name="sqlSessionFactory" ref="sqlSessionFactory"></constructor-arg>
        </bean>
		//创建sqlSessionTemplate实例时 需要通过构造方法注入 sqlSessionFactory实例 这里引用的是上面的
		//与MyBatis中默认的SqlSession 不同 sqlSessionTemplate是线程安全的 可以以单例模式 配置并被多个DAO对象共用 而不用为每个DAO单独配置一个SqlSessionTemplate实例
		<!-- 配置DAO组件并注入SqlSessionTemplate实例 -->
		<bean id="userMapper" class="cn.smbms.dao.user.UserMapperImpl">
			<property name="sqlSession" ref="sqlSessionTemplate">
		</bean>
		
	测试类 //简单测试 实际根据需求生成 业务逻辑层
		ApplicationContext applicationContext = new ClassPathXmlApplicationContext("applicationContext.xml");
        UserMapper userMapper = (UserMapper) applicationContext.getBean("UserMapperImpl");
        List<User> list = userMapper.getUserList();
	
```

##### SqlSessionDaoSupport简化SqlSessionTemplate的配置和获取

```
	
	MyBatis-Spring提供了SqlSessionDaoSupport类 来简化SqlSessionTemplate的配置和获取
	
	public class UserMapperImpl extends SqlSessionDaoSupport implements UserMapper{
		@Override
		public List<User> getUserList(User user){
			return this.getSqlSession().selectList("com.ttelite.smbms.dao.UserMapper.getUserList");
		}
	}
	
	Spring配置文件
	
	//省略配置数据源 和 SqlSessionFactoryBean
	<!-- 配置Dao -->
	<bean id="userMapper" class="cn.smbms.dao.user.UserMapperImpl">
		<property name="sqlSessionFactory" ref="sqlSessionFactory"></property>
	</bean>
	
	//SqlSessionDaoSupport类 提供了 setSqlSessionFactory()方法 用来注入SqlSessionFactory实例并创建 SqlSessionsTemplate实例 同时提供了getSqlSession()方法 用来返回创建好的SqlSessionTemplate实例 
	//DAO实现类 只需继承SqlSessionDaoSupport类 即可获得SqlSessionTeplate实例 无需额外定义SqlSessionTemplate属性 和 setter方法  并且 Spring配置文件也不需要再配置 SqlSessionTemplate 只需要配置通过该DAO对象的setSqlSessionFactory() 方法 为其注入 SqlSessionFactory即可 进一步简化了DAO组件的开发工作
	
```

##### MapperFactoryBean注入映射器实现数据库操作

```
	
	使用SqlSessionTemlate实现数据库操作  都是采用字符串指定 映射项 这种方式 比较容易产生错误 如果存在拼写错误 只能等到运行的时候发现 如果命名空间发生变化 会导致很多地方修改 不利于维护
	
	SqlSessionTemplate 作为SqlSession接口的实现自然也具备 相同作用的getMapper()方法实现 但是在集成环境当中 直接在代码中使用getMapper()方法并非最佳选择 利用MyBatis-Spring组件 可以不必每次调用getMapper()方法 而是通过配置的方式 直接为业务对象注入映射器实现 无需额外编码 对于不包含其它非MyBatis的工作的数据访问操作 这是首选做法
	
	对于不包含其它 非MyBatis的数据访问操作 可以不用手工编写SqlSessionTemplate或SqlSessionDaoSupport来实现此类DAO MyBatis-Spring提供了MapperFactoryBean能够以配置的方式 生成映射器实现并注入给业务组件 //也就是不用创建DAO实现类了 //注意Sql映射文件 命名空间要和映射器接口的名称 相同 映射元素的id和映射器接口方法相同
	
	Spring配置文件
		//省略配置数据源 和 SqlSessionFactoryBean
		<!-- 配置DAO -->
		<bean id="userMapper" class="org.mybatis.spring.mapper.MapperFactoryBean">
			<property name="sqlSessionFactory" ref="sqlSessionFactory"></property>
             <property name="mapperInterface" value="com.ttelite.smbms.dao.UserMapper"></property>
		</bean>
		
		测试类 //简单测试 实际根据需求生成 业务逻辑层
		ApplicationContext applicationContext = new ClassPathXmlApplicationContext("applicationContext.xml");
        UserMapper userMapper = (UserMapper) applicationContext.getBean("userMapper");
        List<User> list = userMapper.getUserList();
		
	//省略了Mapper映射器的获取 省略DAO接口实现类编写
	//配置DAO组件时 class属性不是某个实现类 而是MapperFactoryBean
	//通过mapperInterface属性指定映射器 注意只能是接口
	//MapperFactoryBean是SqlSessionDaoSupport的子类 需要通过setSQLSessionFactory()方法注入sqlSessionFactory以创建SqlSessionTemplate实例 本质上应该还是封装了
	//注意映射器对应的SQL映射文件与映射器的类路径要相同 MapperFactoryBean就会自动解析SQL映射文件 如果不同则需要配置SqlSessionFactoryBean时明确指定映射文件的位置
	
```

##### MapperScannerConfigurer注入映射器(常用)

```
	
	使用MapperFactoryBean实现数据库操作 简化了DAO模块的编码 但是如果映射器很多 相应的配置项也会很多 为了简化配置工作量 MyBatis-Spring提供了MapperScannerConfigurer 它可以扫描指定包中的接口并且将它们直接注册为MapperFactoryBean
	
	Spring配置文件
		//省略配置数据源 和 SqlSessionFactoryBean
		<!-- 配置DAO -->
		<bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
			<property name="basePackage" value="com.smbms.dao" />
		</bean>
		//basePackage属性 指定了扫描的基准包 MapperScannerConfigurer将递归扫描基准包(包括各层级子包)下所有接口 如果它们在SQL映射文件中定义过 则将它们动态注册为MapperFactoryBean 就可以批量产生映射器实现类 
		//映射器被注册到Spring容器时 Spring会根据其接口名称 为其命名 默认规则是首字母小写的非完全限定类名 例如UserMapper类会被默认命名userMapper 按照此规则 依然可以使用ref注入业务逻辑层作为组件 更普通的做法是 !!!使用注解自动装配(注意不要忘了 引入context命名空间) 能够最大程度减少编码和配置
		//basePackage属性中可以包含多个包名 多个包名之间使用逗号或分号隔开
		//若环境中处于不同目的 配置了多个SqlSessionFactory时 自动装配无法进行 要显式指定依赖的SqlSessionFactory
		<bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
			<property name="sqlSessionFactoryBeanName" value="sqlSessionFactory" />
			<property name="basePackage" value="com.smbms.dao" />
		</bean>
		//注意 这个属性关注的是Bean的名称 所以为其赋值使用的是value而不是ref
	
```

##### Spring的事务处理

```
	
	业务层的只能不仅仅是调用DAO 事务处理是任何企业级应用开发 中不能回避的一个重要问题 
	//以硬编码的方式进行 事务处理 弊端显而易见 事务代码分散在业务方法中难以重用 需要调整时工作量也比较大 复杂事务的编码难度较高 增加了开发难度
	Spring提供了声明式事务处理机制 它基于AOP实现无需编写任何 事务管理代码 所有的工作全在配置文件中完成 这意味着与业务代码完全分离 配置即可用 降低了开发和维护难度
	//注意业务方法中没有事务控制的相关代码
	
	//核心就是 对哪些方法 采取什么样的事务策略
	
```

###### XML配置事务管理

```

	配置步骤
		导入tx和aop命名空间
		定义事务管理器Bean 并为其注入数据源Bean
		通过<tx:advice>配置事务增强 绑定事务管理器 并针对不同方法定义事务规则
		配置切面 将事务增强与方法切入点组合

	首先需要 导入tx和aop两个命名空间下的标签 
	
        <beans xmlns="http://www.springframework.org/schema/beans"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xmlns:context="http://www.springframework.org/schema/context"
           xmlns:aop="http://www.springframework.org/schema/aop"
           xmlns:tx="http://www.springframework.org/schema/tx"
           xsi:schemaLocation="http://www.springframework.org/schema/beans
           http://www.springframework.org/schema/beans/spring-beans-3.2.xsd
           http://www.springframework.org/schema/context
           http://www.springframework.org/schema/context/spring-context-3.2.xsd
           http://www.springframework.org/schema/aop
           http://www.springframework.org/schema/aop/spring-aop-3.2.xsd
           http://www.springframework.org/schema/tx
           http://www.springframework.org/schema/tx/spring-tx-3.2.xsd"
        ></beans>
	
	之后配置事务管理器组件 它提供了对事务处理的全面支持和统一管理 在切面相当于增强处理的角色
	
	Spring配置文件
		//省略定义数据源 SqlSessionFactroyBean DAO及业务Bean的配置
		<!-- 定义事务管理器 -->
		<bean id="txManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
            <property name="dataSource" ref="dataSource"/>
        </bean>
        //使用Spring提供的 事务管理器类 DataSourceTransactionManager 和 事先定义好的数据源组件 定义
        
        可以通过<tx:advice>标签进行进一步的配置 以便更好地适应不同业务方法对于事务的不同要求
	
		<tx:advice>标签 用来配置事务增强 设定事务的属性 为不同的业务方法指定具体的事务规则 advice意为增强处理(好理解)
		
		<!-- 通过<tx:advice>标签为指定的事务管理器设置事务属性 -->
		<tx:advice id="txAdvice" transaction-manager="txManager">
			<!-- 定义属性,声明事务规则 -->
			<tx:attributes>
				<tx:method name="find*" propagation="SUPPORTS" />
				<tx:method name="add*" propagation="REQUIRED" />
				<tx:method name="del*" propagation="REQUIRED" />
				<tx:method name="update*" propagation="REQUIRED" />
				<tx:method name="*" propagation="REQUIRED" />
			</tx:attributes>
		</tx:advice>
		//<tx:advice>标签可以设置id数和transaction-manager属性(引用一个事务管理器Bean)
		//transaction-manager属性的默认值是transactionManager 也就是说如果定义事务管理器的Bean名称是transactionManager 则可以不用指定该属性值
		//可以通过<tx:attributes>子标签定制事务属性 
		//事务属性通过<tx:method>标签进行设置 Spring支持对不同的方法 设置不同的事务属性
		//<tx:method>标签的name属性是必须的 用于指定匹配方法 其它属性可选 
		propagation属性 //配置事务传播机制 
			//属性可选值
			REQUIRED 默认值 表示如果存在一个事务 则支持当前事务 如果当前没有事务 则开启一个新的事务
				//REQUIRED能够满足大多数的事务需求 可以作为首选的事务传播行为
			REQUIRES_NEW 表示总是开始一个新的事务 如果一个事务已经存在 则将这个存在的事务挂起 开启新事务执行该方法
			MANDATORY 表示如果存在一个事务,则支持当前事务 如果当前没有一个活动的事务 则抛出异常
			NESTED 表示如果当前存在一个活动的事务 则创建一个事务作为当前事务的嵌套事务运行 如果没有当前事务 该取值与REQUIRED相同
			SUPPORTS 表示如果存在一个事务 则支持当前事务 如果当前没有事务 则按非事务方式执行
			NOT_SUPPORTED 表示总是以非事务方式执行 如果一个事务已经存在 则将这个存在的事务挂起 然后执行该方法
			NEVER 表示总是以非事务方式执行 如果当前存在一个活动的事务 则抛出异常
			
		isolation属性(了解) //事务隔离等级(当前事务和其它事务的隔离程度 在并发事务处理 的情况下需要考虑它的设置) 
			//属性可选值
			DEFAULT 默认值 表示使用数据库默认的事务隔离级别
			READ_UNCOMMITTED 未提交读
			READ_COMMITTED 提交读
			REPEATABLE_READ 可重复读
			SERIALIZABLE 串行读
			
		timeout属性 //事务超时时间 允许事务运行的最长时间 以秒为单位 超过给定的时间自动回滚 防止事务执行时间过长而影响系统性能 该属性需要底层的实现支持 默认值为-1 表示不超时
		
		read-only //事务是否为只读 默认值为false 对于只执行查询功能的事务 把它设置为true能提高事务处理的性能
		
		rollback-for //设定能够触发回滚的异常类型 Spring默认只在抛出Runtimely Exception时才进行事务回滚 //可以通过 全限定类名自行指定需要回滚事务的异常 多个类名用英文逗号隔开
		
		no-rollback-for //设定不触发回滚的异常 Spring默认 checked Exception 不会触发事务回滚 可以通过 全限定类名自行指定不需要回滚事务的异常 多个类名用英文逗号隔开
			
			
			
		定义完 事务规则 最后 要定义切面 将事务规则 应用 到 指定方法 
		//可以这样想 因为业务逻辑层一个方法可能会涉及到多个DAO方法 所以这样设计
		
		<!-- 定义切面 -->
        <aop:config>
            <!-- 定义切入点 -->
            <aop:pointcut id="UserServiceImpl" expression="execution(* com.ttelite.smbms.service.impl.UserServiceImpl.*(..))"/>
            <!-- 将事务增强与切入点组合 -->
            <aop:advisor advice-ref="txAdvice" pointcut-ref="UserServiceImpl"/>
        </aop:config>
		//注意是advisor标签 它的advice-ref 用来指定增强处理规则 
		//注意 切入点 表达式不要写错 如果写错会报异常 详细看debug总结
		
		
	这样基本配置就完成了 之后进行测试 ......
		
```


###### 注解配置事务管理

```
	
	Spring还支持 注解实现 声明式事务处理  @Transactional
	
	//首先仍然需要 配置事务管理器 
    //并且添加对注解配置的事务支持 <tx:annotation-driven transaction-manager="txManager"/>
	//如果要使用其它注解 注意添加注解标签支持 和指定扫描包 <context:component-scan base-package="com.ttelite.smbms" />
	//估摸 实际方法管理 是通过<tx:annotation-driven>标签的 transaction-manager 指定的 事务管理器 txManager
	
	它主要是给 业务逻辑层 添加事务控制 
	
	示例 	
	
		@Transactional
        @Service("userService")
        public class UserServiceImpl implements UserService {
            @Autowired
            private UserMapper userMapper; //数据访问层对象
            //setter方法
            public void setUserMapper(UserMapper userMapper) {
                this.userMapper = userMapper;
            }

            /**
             * 获得所有用户信息
             *
             * @return userList 用户对象列表
             */
            @Override
            @Transactional(propagation = Propagation.SUPPORTS)
            public List<User> findUserList() {
                return userMapper.getUserList();
            }
        }
	
	//在业务实现类 添加@Transactional注解即可为该类的 所有业务方法 统一添加事务处理 
	//如果需要 指定某业务方法 采用不不同的事物规则 可以在该业务方法上 添加@Transactional注解单独进行设置
	默认的@Transactional 设置如下
		事务传播设置是 PROPAGATION_REQUIRED
		事务隔离级别 ISOLATION_DEFAULT
		事务是 读/写
		事务超时默认是依赖于事务系统的 或者 事务超时没有被支持
		任何RuntimeException 将触发事务回滚  checked Exception 将不触发事务回滚
		
		这些设置可以改变
		
		详细百度
			
		https://www.cnblogs.com/xinruyi/p/11037724.html
		
	
```

### Spring配置补充

#### 属性文件和JNDI配置DataSource数据源

```
	
	使用 属性文件配置数据源
	
        属性文件配置 让DataSource的可配置性增强 便于维护

        使用Spring提供的PropertyPlaceholderConfigurer类可以加载属性文件 在配置文件用${...}的方式引用属性文件中的键值对 //注意使用${...}时 前面后面不要添加空格 会引起异常

        database.properties文件

            #在和mysql传递数据的过程中，使用unicode编码格式，并且字符集设置为utf-8
            driver=com.mysql.jdbc.Driver
            url=jdbc:mysql://127.0.0.1:3306/数据库?useUnicode=true&characterEncoding=utf-8
            user=root
            password=密码

        Spring配置文件 

            <!-- 引入properties文件 -->
            <bean class="org.springframework.beans.factory.config.PropertyPlaceholderConfigurer">
                <property name="location" value="classpath:database.properties"></property>
            </bean>
            <!-- 数据源 -->
            <bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource" destroy-method="close">
                <property name="driverClassName" value="${driver}"/>
                <property name="url" value="${url}"/>
                <property name="username" value="${user}"/>
                <property name="password" value="${password}"/>
            </bean>
	
	
	使用JNDI数据源
		//如果应用部署 在高性能的应用服务器(Tomcat、WebLogic等)上 希望使用应用服务器的数据源使用JNDI方式供使用者调用 Spring为此专门提供 引用JNDI资源的 JndiObjectFactoryBean类
		使用JNDI的方式配置数据源 步骤
			在应用服务器配置好JNDI数据源 //具体查看JNDI配置笔记 //注意添加数据库驱动Jar包
			在Spring配置文件引用JNDI数据源
                 <!--  通过JNDI配置DataSource  -->
                 <bean id="dataSource" class="org.springframework.jndi.JndiObjectFactoryBean">
                	 <!--  通过jndiName指定引用的JNDI数据源名称  -->
                	 <property name="jndiName" value="java:comp/env/jdbc/smbms"/>
                 </bean> 
				//注意需要在Web环境下使用JNDI获得数据源对象
		
```

#### Spring中Bean的作用域

```
	
	在Spring中定义Bean除了 可以创建Bean实例并对Bean的属性进行注入外 还可以为定义的Bean指定一个作用域
	作用域 取值 决定了 Spring创建实例 的策略 进而影响程序的运行效率 和 数据安全
	
	通过<bean>标签 的 scope属性 属性定义Bean的作用域
	
	singleton是默认作用域 对于不存在线程安全的组件 采用这种方式 可以大大减少创建对象的开销 提高运行效率0
	而对于存在线程安全问题的组件 则不能使用singleton模式 可以使用protptype作用域 就避免了因为共用一个实例 产生线程安全问题
	
	可以使用注解 @Scope("作用域名称") 设置作用域
	
```

##### Bean的作用域

|     作用域     |                             解释                             |
| :------------: | :----------------------------------------------------------: |
|   singleton    | 默认值 以 单例模式 创建Bean的实例  即容器中该Bean的实例只有一个 |
|   prototype    |         每次从容器中获取Bean时 都会创建一个新的实例          |
|    request     |       用于Web应用环境 针对每次HTTP请求都会创建一个实例       |
|    session     |  用于Web应用环境 同一个会话共享同一个实例 不同会话不同实例   |
| golbal session | 仅在Portlet的Web应用中使用 同一个全局会话共享一个实例 对于非Portlet环境 等同于session |

#### Spring的自动装配

```
	
	不仅通过 注解实现 依赖注入可以 使用自动装配  基于XML的配置 也同样可以使用 自动装配
	
	例
		//传统配置
		<bean id="xxx" class="...">
			<property name="xxx" ref="xxx">
		</bean>
			
		//自动装配
		<bean id="xxx" class="..." autowire="byName"></bean>
			
	通过bean标签的autowire属性 代替了 通过property标签进行属性注入
	
	//后面是由BeanFactroy检查 XML配置文件的内容 进行自动注入 大大简化了维护 Bean注入的配置
	
	//如果配置文件很多 可以统一设置自动注入 而不必配置每个Bean 解决方法 <beans>元素提供了default-autowire属性  设置这个属性 影响全局 减少维护单个Bean的注入方式 其子节点<bean>节点 还可设置autowire属性 覆盖全局设置
	
	//对于大型应用 不建议使用自动装配 虽然可以减少配置工作量 但降低了依赖关系的清晰性和透明性
	
```

##### autowire属性值

| autowire属性值 |                             解释                             |
| :------------: | :----------------------------------------------------------: |
|       no       |     不适用自动装配 Bean依赖关系必须通过property元素定义      |
|     byType     | 根据属性类型自动装配  如果只有一个适配类则自动装配属性  如果有多个Spring无法决定抛出致命异常  如果没有匹配异常 就什么都没有发生 |
|     byName     | 根据属性名 自动装配 找到id与属性setter方法匹配的 找到就自动注入 否则什么都不做 |
|  constructor   | 与byType的方式类似 不同之处 在于它应用于构造器参数 如果没有找到和构造器参数类型一致的Bean 那么会抛出异常 |

#### 拆分Spring配置文件

##### 拆分策略

```
	
	对于使用XML方式 进行配置的Spring项目 项目规模较大时 配置文件可读性 可维护性差 庞大的Spring配置文件 难以阅读
	进行团队开发时 多人修改同一配置文件容易发生冲突 降低开发效率 
	
	如果是一个开发人员负责一个模块 我们采用公用配置(包含数据源、事务等) + 每个系统模块一个单独配置文件 (包含Dao、Service及Web控制器)的形式
	如果开发是按照分层进行的分工 我们采用公用配置(包含数据源、事务) + DAO Bean配置 + 业务逻辑Bean配置 + Web控制器配置的形式 
	
	拆分Spring配置文件件 可以分散配置文件 降低修改配置文件的难度和冲突的风险 符合 分而治之的 软件工程原理
	
```

##### 拆分方法

```

	根据 ClassPathXmlApplicationContext类的构造方法的几种 重载形式
		//public ClassPathXmlApplicationContext(String configLococation);
		//public ClassPathXmlApplicationContext(String... configLococation);
	
	//如果有多个配置文件需要载入 分别传入多个配置文件名 或者 以String[]方式 传入多个配置文件名
	
	或者 使用通配符 * 加载 多个具有一定命名规则的配置文件  //!!! 推荐使用
		ApplicationContext xx = new ClassPathXmlApplicationContext("applicationContext*.xml");
		
	此外可以通过import子元素 导入其它配置文件 将多个配置文件整合到一起 形成完整的Spring配置文件
		Spring配置文件
		<!-- 导入多个Spring配置文件 -->
		<import resource="applicationContext-dao.xml" />
		<import resource="applicationContext-xxx.xml" />
	
```

## SpringMVC体系结构和处理请求控制器

```
	
	单纯使用 JSP开发web应用弊端明显 在应用中引入控制器(Servlet或者Filter)可以有效避免JSP页面编写大量业务和页面跳转代码 而JSP专门用于显示内容
	//SpringMVC基于请求驱动的Web框架
	
```

### MVC设计模式

```
	
	软件架构模式 为
	
	数据访问接口 DAO层
	处理业务逻辑 Service层
	数据实体 POJO
	负责前端请求的接受并处理 Servlet
	负责前端页面展示 JSP
	
	这种架构模式就是MVC设计模式 它是软件工程中的一种软件架构模式 它强制性地使软件系统的输入、处理和输出分开
	把软件系统分为三个基本部分 模型(Model) 视图(View) 控制器(Controller)
	
	
	视图(View)
		负责格式化数据呈现给用户 包括数据展示、用户交互、数据验证、界面设计等功能 
		对应组件JSP或者HTML文件 PDF XML JSON等
	控制器(Controller)
    	负责接收 转发请求 对请求进行处理后 指派视图 并将响应结果 发送给客户端
    	对应组件Servlet
	模型(Model)
		具有最多处理任务 是应用的主体部分 它负责数据逻辑的处理和实现数据操作(就是在数据库中存取数据) 对应组件JavaBean  
		对应组件JavaBean 处理业务逻辑Service层 数据库操作相关DAO层 数据实体类POJO
	
```

#### JSP Model1

```
	
	在业务流程简单时 将控制器的功能交给视图实现 称为JSP Model1
	JSP Model1模式只有视图和模型 没有控制器  //JSP+JavaBean
	
	浏览器 >发送请求> JSP接受请求进行业务逻辑处理 > 将结果返回给客户端浏览器
	
	//一定程度上实现了MVC JSP控制层和视图层合二为一 JavaBean为模型层  JSP要负责视图层的数据显示、还要负责业务流程的控制 结构较为混乱 而且还不是松耦合架构 不建议使用
	
```

#### JSP Model2

```
	
	业务流程复杂 业务流程控制交给 控制器实现 JSP专注于视图的展现即可 //JSP Model2 //JSP+Servlet+JavaBean
	
	相比Model1 控制器接受请求 创建所需的JavaBean实例 将处理后的数据返回给视图层(JSP) JSP进行展示
	
	//结构清晰 松耦合架构 建议使用
	
```

### MVC请求处理过程

```
	
	首先 视图提供 系统与用户交互界面 发送用户输入给控制器
	控制器接受用户的请求 决定 调用哪个模型进行处理
	模型根据用户请求 进行相应的业务逻辑处理 并返回处理结果(数据)
	控制器根据返回的处理结果 调用相应的视图  格式化模型返回的数据 并通过视图呈现给用户
	
	
	用户发送URL请求 服务器根据web.xml 中对于DispatherServlet的配置 将此请求被DispatherServlet所截获 
	DispatherServlet 根据HandlerMapping找到处理相应请求的Controller 来处理请求 Controller处理完成后 返回ModelAndView对象 该对象告诉DispatherServlet 需要通过那个视图来进行数据模型的展示 DispatherServlet根据视图解析器把Controller返回的逻辑视图名 转换成真正的View(将模型数据也一并传给View)并输出 View(JSP)渲染 前端控制器收回控制权将响应结果 返回给用户

```

### MVC体系结构

```
	
	DispatherServlet(前端控制器)
    //SpringMVC 最核心的类
    //web.xml中配置
    
    Handler(处理) 对应MVC中的C控制器
    //类型Object
    //作用实际处理请求
    //标注了@RequestMapping的所有方法都可以看做一个Handler
	
	ModelAndView
	//逻辑视图名
	//模型对象
	
	HandlerMapping(处理器映射)
	//BeanNameUrlHandlerMapping(默认)
	//DefaultAnnotationHandlerMapping 将请求映射到标注@RequestMapping注解的控制器和处理方法上
	//RequestMappingHandlerMapping
	
	HandlerAdapter(适配器)
	//AnnotationMethodHandlerAdapter
	RequestMappingHandlerAdapter
	
	ViewResolver(视图解析器)
	//InternalResourceView
	
```

### MVC特点

```
	
	清晰地角色划分
	灵活的配置功能
	提供了大量的控制器接口和实现类
	真正做到与View层的实现无关(JSP、Velocity、Xsit等)
	国际化支持
	面向接口编程
	Spring提供了Web应用开发的一整套流程 不仅仅是MVC 它们之间可以很方便的结合在一起
	
```

### MVC优缺点

```
	
	优点
		多视图共享一个模型 大大提高代码的可重用
		MVC三个模块互相独立 松耦合结构
		控制器提高了应用程序的灵活性和可配置型
		有利于软件工程化管理
		完美的系统架构 = 松耦合 + 高重用性 + 高扩展性
		
	缺点
		原理复杂
		增加了系统结构和实现的复杂性
		视图对模型数据的低效率访问
		//对于小型甚至中型规模的项目 花费大量时间将MVC 应用到不是很大的应用程序通常得不偿失 
	
```

### SpringMVC框架

```
	
	SpringMVC是 Spring框架中 用于Web应用开发的一个模块 是Spring提供的一个基于MVC设计模式的优秀Web开发框架
	本质上相当于Servlet  在MVC设计模式中 SpringMVC作为控制器(Controller)建立模型与视图的数据交互 是结构最清晰的MVC Model2实现 可以成为典型MVC框架
	在SpringMVC框架中 Controller替换Servlet来负担控制器的职责
		//Controller接受请求 调用相应的Model进行处理 处理器完成业务处理后返回处理结果 Controller调用相应的View并对处理结果进行视图渲染 最终客户端得到响应消息
	
```

### SpringMVC环境搭建

#### 引入jar文件

```

    spring-web-3.213.RELEASE.jar 在Web应用开发时使用Spring框架所需的核心类
	spring-webmvc-3.2.13.RELEASE.jar Spring MVC框架相关的所有类 包含框架的ServletsWeb MVC框架 以及对控制器和视图的支持
	//省略其它需求包

```

#### SpringMVC配置

```
	
		在web.xml 中配置Servlet 定义DispatherServlet
			//SpringMVC是基于Servlet的 DispatcherServlet 是整个SpringMVC的核心 负责截获请求 并将其分派给负责响应的处理器处理 
			//配置SpringMVC 首先就要进行DispatcherServlet的配置 和Servlet一样 在web.xml中配置
			
			web.xml
		   <!-- 配置Spring MVC前端控制器 -->
            <servlet>
                <servlet-name>springmvc</servlet-name>
                <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
                <!-- 定义Spring MVC框架配置文件路径参数 -->
                <init-param>
                    <param-name>contextConfigLocation</param-name>
                    <param-value>classpath:springmvc-servlet.xml</param-value>
                </init-param>
                <!-- 定义Spring MVC框架初始化顺序 1Tomcat初始化完成后 初始化此Servlet -->
                <load-on-startup>1</load-on-startup>
            </servlet>
            <servlet-mapping>
                <servlet-name>springmvc</servlet-name>
                <url-pattern>/</url-pattern>
            </servlet-mapping>
			
			//上述代码 配置了springmvc 的Servlet Servlet类型是DispatcherServlet 它就是SpringMVC的入口
SpringMVC的本质就是Servlet
			//通过<load-on-startup>1</load-on-startup>配置容器在启动的时候就加载此DispatcharServlet 即自动启动
			//通过映射标签 将所有URL请求交给 DispatcharServlet
			//通过设置contextConfigLocation参数 指定SpringMVC配置文件位置 此处使用Spring资源路径的方式进行指定(classpath:springmvc-servlet.xml) springmvc-servlet为配置文件名
		
		
		创建SpringMVC的配置文件 
			//主要配置 两部分内容  处理器映射 和 视图解析器
			
			<?xml version="1.0" encoding="UTF-8"?>
            <beans xmlns="http://www.springframework.org/schema/beans"
                   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                   xmlns:mvc="http://www.springframework.org/schema/mvc"
                   xmlns:p="http://www.springframework.org/schema/p"
                   xmlns:context="http://www.springframework.org/schema/context"
                   xsi:schemaLocation="
                    http://www.springframework.org/schema/beans
                    http://www.springframework.org/schema/beans/spring-beans.xsd
                    http://www.springframework.org/schema/context
                    http://www.springframework.org/schema/context/spring-context.xsd
                    http://www.springframework.org/schema/mvc
                    http://www.springframework.org/schema/mvc/spring-mvc.xsd">

                <!-- 配置处理器映射 -->
                    <!-- 完成视图的对应 -->
                    <bean name="/index.html" class="com.ttelite.controller.IndexController" />
                <!-- 配置视图解析器 -->
                <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
                    <property name="prefix" value="/WEB-INF/jsp/"/>
                    <property name="suffix" value=".jsp"/>
                </bean>
            </beans>
		
		//配置处理器映射  用来告诉DispatcherServlet要将一个请求交给 那个特定的Controller处理
它需要咨询一个Bean(HandlerMapping) Bean的作用就是 指定 一个URL请求应该由那个Controller处理
		//Spring提供了多种处理器映射的支持 可以根据需求进行选择 用到再说  如果没有明确声明任何处理器映射 Spring会默认使用BeanNameUrlHandlerMapping(即 在Spring容器中查找 与请求URL同名的Bean 这个映射器不需要配置 根据请求URL路径映射到控制器Bean的名称)
		<bean name="/index.html" class="com.ttelite.controller.WelcomeController" /> //指定的URL请求/index.html //处理该URL请求的控制器 com.ttelite.controller.WelcomeController(全限定类包名)
		
	
		//配置视图解析器  指定的请求需要使用 那个视图进行请求结果的渲染输出 DispatcherServlet会查找到一个视图解析器 将控制器返回的 逻辑视图名称 转换成 进行渲染的实际视图 
		<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
            <property name="prefix" value="/WEB-INF/jsp/"/>
            <property name="suffix" value=".jsp"/>
        </bean>
        //也提供了多个类 定义视图解析器 此处使用 InternalResourceViewResolver 通过配置前缀和后缀 将试图逻辑名解析为/WEB-INF/jsp/<viewName>.jspb
        
        
       	到此为止 SpringMVC环境配置完成 接下来编写 Cotroller和View 之后进行测试 
       
	
```

#### 编写Cotroller页面

```
	
    将JavaBean编程 处理前端请求的控制器 需要继承org.springframework.web.servlet.mvc.AbstractController 并实现handleRequestInternal方法
	
	/**
     * IndexController 首页控制器
     */
    public class IndexController extends AbstractController {
        @Override
        protected ModelAndView handleRequestInternal(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse) throws Exception {
            //省略根据需求 进行业务逻辑访问
            return new ModelAndView("index");
        }
    }
	
	//返回值为ModelAndView对象 该对象既包含视图信息 也 包含模型数据信息
	//index为逻辑视图名称 之后经过视图解析器 解析成实际地址 /WEB-INF/jsp/index.jsp页面
	
```

#### 创建View页面JSP视图

```
	
	在路径 /WEB-INF/jsp/index.jsp 下创建此文件 
	
	//index.jsp  接收 可能有的模型数据(此示例不需要返回模型数据)进行 显示等等 官方叫做渲染 
	//接受模型数据 可以使用EL表达式 更加方便简洁
	
```

#### 搭建优化

```
		
	上面的搭建过程 通过设置BeanNameUrlHandlerMapping 的方式完成了 请求与Controller之间的映射关系
	但是如果请求过多 那就需要在xml中配置多个映射关系 还要建立多个JavaBean作为控制器进行请求处理 
	
	解决方式 是使用SpringMVC提供的一键式配置方法 <mvc:annotation-driven/> 通过注解方式 进行SpringMVC开发
	
	在配置文件 添加<mvc:annotation-driven/> 标签 配置之后SpringMVC就会自动做一些注册组件的事情 通过注解的方式 把URL映射到Controller上
	
	springmvc-servlet.xml配置文件更改如下
		//删除处理器映射标签 <bean name="/index.html" class="com.ttelite.controller.WelcomeController" />		
		//添加<context:component-scan base-package="xx.xx.controller" />标签
		//添加<mvc:annotation-driven />标签开启 MVP注解
		
		<mvc:annotation-driven />标签 会自动注册DefaultAnnotationHandlerMapping(处理器映射)与AnnotationMethodHandlerAdapter(处理器适配器)这两个Bean 这两个Bean实例是 @Controller和@RequestMapping等注解的必要支持  从而找出URL和Handler method的关系并关联
		//Spring3.2之前的版本 开启注解式处理器支持的配置为DefaultAnnotationHandlerMapping(处理器映射)与AnnotationMethodHandlerAdapter(处理器适配器) 3.2版本之后 使用RequestMappingHandlerMapping和RequestMappingHandlerAdapter来代替DefaultAnnotationHandlerMapping被标注 @Deprecated弃用
		<context:component-scan base-package="xx.xx.controller" />标签 对包进行扫描 实现注解驱动Bean的定义 同时将Bean注入容器使用 如果没有配置此标签 标注@Controller的Bean仅仅是一个普通的JavaBean 而不是可以处理请求的控制器 
	
	控制器内编码如下
	
		@Controller
         public class WelcomeController {
             @RequestMapping("/index.html")
             public String index(){
                 //省略根据需求 进行业务逻辑访问
                 return "视图逻辑名";
             }
         }
	
		@Controller标注控制器类 让其成为可处理HTTP请求的控制器
		@RequestMapping标注index()方法 确定index()方法对应的请求URL
         //方法名可以随便起 语义化
		//index()方法将处理所有URL为"/index.html"的请求(注意相对于Web容器部署根目录)
		//需要添加其它业务需求(URL需求) 只需要在WelcomeController类下 添加方法并利用@RequestMapping进行URL标注   无需再新建控制器 并减少处理器映射配置
		//!!!注意@RequestMapping 映射的请求信息必须保证全局(Web应用)唯一
		
```

#### 使用@RequestMapping映射请求

```
	
	@RequestMapping 负责将不同的请求 映射到 相应的控制器方法上
	
	@RequestMapping可以映射 URL映射请求 请求方法 请求参数 等映射请求
	//使用@RequestMapping完成 映射具体需要4个信息项 请求URL 请求参数 请求方法 请求头
	//value表示请求的URL 
	//method表示请求方法  RequestMethod.GET RequestMethod.POST
	//params 表示请求参数
	
	
	
	通过 请求URL 进行映射 
		@RequestMapping("/xxxx")
		...
		
		@RequestMapping(value = "/xxxx")
		....
		
		//上面两种 写法一致 上面的是简写
		//此外@RequestMapping也可以在 类定义处 
			@Controller
			@RequestMapping(/xxx)
             public class WelcomeController {
                 @RequestMapping("/xxxx")
                 public String index(){
                     //省略根据需求 进行业务逻辑访问
                     return "视图逻辑名";
                 }
             }
             //不在类定义处定义@RequestMapping URL应该如下 ../xxxx
			//在类定义处定义@RequestMapping URL应该如下 ../xxx/xxxx
			//!!!注意@RequestMapping 映射的请求信息必须保证全局(Web应用)唯一
			//对于@RequestMapping的value返回值是一个Stirng[] 所以可以写成这样@RequestMapping({"/xx","/"})
		
		
	通过请求参数 请求方法进行映射 //多条件 映射更加精准
		@RequestMapping(value = "/index",method = RequestMethod.GET,params = "userName")
         public String index(String userName){
             logger.debug(userName);
             return "index";
         }
         //params可以不写 只是举例说明例子
         //URL请求必须和@RequestMapping指定的一致才能进来 URL请求参数名也要相同
		//注意如果URL请求参数名和params相同(正常进入处理器方法) 处理器方法的参数名称也要相同 否则取不到值 即 选择方法参数直接入参 方法入参名必须与请求中参数名保持一致
		
```

#### 参数传递

##### 视图到控制器

```
	
	视图传递参数值给控制器
	
	第一种 直接进行入参
		@RequestMapping(value = "/index")
         public String index(String userName){
             logger.debug(userName);
             return "index";
         }
		//注意如果URL请求参数名和params相同(正常进入处理器方法) 处理器方法的参数名称也要相同 否则取不到值(null) 即 选择方法参数直接入参 方法入参名必须与请求中参数名保持一致
	
	
	第二种 Controller方法中 参数前加@RequestParam进行直接入参
	
	@RequestMapping("/index")
    public String index(@RequestParam String someOne){
        //省略根据需求 进行业务逻辑访问
        return "index";
    }
	//存在问题 若在地址栏没有添加参数 页面会报400错误(参数是必须的)  以下方法解决问题
	
    @RequestMapping("/index")
    public String index(@RequestParam(value = "someOne",required = false) String someOne){
    	logger.debug(someOne);
        return "index";
    }
	
	@RequestParam注解 指定其对应的请求参数 有一下3个参数
		value 参数名
		required 是否为必须 默认为true 表示请求中必须包含对应的参数名 若不存在将抛出异常
		defaultValue 默认参数值 不推荐使用 实际开发
	
```

##### 控制器到视图

```
	
	控制器将模型数据传给视图  对于MVC框架模型数据时最重要的 因为Controller是为了产生模型数据(Model) 视图(View)也是为了渲染模型数据并进行输出
	
	第一种 设置控制器处理方法的返回值为 ModelAndView 即包含视图信息又包含模型数据信息
		
		//处理器方法
	    @RequestMapping(value = "/index")
        public ModelAndView index(String userName){
            ModelAndView modelAndView = new ModelAndView();
            modelAndView.addObject("userName",userName); //添加模块数据
            modelAndView.setViewName("index"); //设置逻辑视图名
            return modelAndView;
        }
	
		//视图界面 利用EL表达式进行取值
		<h1>${userName}</h1>
		......
		
		添加模块数据 
			ModelAndView addObject(String attributeName,Object attributeValue) //第一个参数key 第二个参数value key可以随意指定 只要在Model作用域内唯一就行
			ModelAndView addAllObjects(Map<Stirng,?> modeMap) //模型数据也是一个Map对象 可以添加Map对象到Model中 //注意Map用key取值
			
		设置视图
			void setView(View view) //指定一个具体的视图对象
			void setViewName(String viewName) //指定一个逻辑视图名
		
		
	第二种 使用框架提供的Model对象完成模型数据的传递 框架在调用方法前会创建一个隐含的模型对象 作为模型数据的储存容器一般称为 "隐含对象" //若处理方法的入参为Model类型 框架会将隐含模型的引用传递给这些入参 简单理解 在方法体内 可以通过 一个Model类型的入参对象访问到模型中的所有数据 或者 向其添加新的属性数据
		
		//处理器方法
		@RequestMapping(value = "/index")
         public String index(String userName,Model model){
             model.addAttribute("userName",userName);
             return "index";
         }
		
		//视图界面 利用EL表达式进行取值
		<h1>${userName}</h1>
		......
		
		不管是Model或者ModelAndView 用法都很相似 运用起来也都很灵活
		Model对象的 addAttribute方法与ModelAndView对象添加模型数据的方法用法都一样 Model对象也是Map类型的数据结构 并且对于key值的指定不是必须的 参考以下示例
		
		//处理器方法
		@RequestMapping(value = "/index")
         public String index(String userName,Model model){
             model.addAttribute(userName);
             return "index";
         }
		
		//视图界面 利用EL表达式进行取值
		<h1>${string}</h1>
		......
		
		这样情况下 传递参数值 会默认使用对象的类型作为key 注意类型名称别写错 比如说类型为String EL表达式取得时候要写成string 首字母小写 !!! 像这样类型为UserXx 取得时候userXx这样
		
	
	第三种 使用Map作为处理方法入参  //不推荐 建议使用Model
	//框架处理方法中若有Map或者Model类型的入参 就会将请求的模型对象传递给这些入参
		
		@RequestMapping(value = "/index")
         public String index(String userName, Map<String,Object> model){
             model.put("userName",userName);
             return "index";
         }
	
		//视图界面 利用EL表达式进行取值
		<h1>${userName}</h1>
		......
	
```

##### 自动绑定POJO实体类  视图到控制器 简化传参

```
	
    在进行视图向控制器传参时 可以将一些多参需求方法 进行实体绑定 比如说用户添加
    
    	//视图页面要写各项表单 (每个表单还需要有name名称)
    		<form>
    			<input name="xxx" />*n
    		</form>
    	//处理器方法需要接受每个表单的参数 (很多参数)
    		@RequestMapping("//省略")
            public String xxx(@RequestParam(value = "xxx",required = false) String xxx,value = "xxx",required = false) String xxx ......){
                //省略
            }
    		
    SpringMVC提供了自动绑定 只需要在视图表单当中的name名称 与 绑定实体类的属性名一致 它就会自动进行绑定
    	
    	@RequestMapping("//省略")
        public String xxx(User user){
                //省略
        }
        
        //出现时间属性 可能出现绑定错误 因为传入是字符串 而实体类属性是Date  解决方法在下面
   
```

##### 解决自动绑定类型异常

```
	
	SpringMVC框架中 时间数据无法自动绑定 当form表单 中出现时间字段 需要跟 POJO对象中的成员变量进行数据绑定时 会出现这个问题
	
	解决第一种方法
		
		在POJO中 时间类型的属性上标注 格式化注解 @DateTimeFormat即可 
		// @DateTimeFormat("yyyy-MM-dd") 可以将字符串 转为 java.util.Date类型
	
	
	
```

##### @ModelAttribute注解 控制器到视图 简化传参

```
	
	要将入参的数据对象放入数据模型中 可以在相应入参前使用 @ModelAttribute注解 
	要在多请求间共享属性 可以将属性存入HttpSession 利用 @SessionAttributes注解
	
	示例
		将user对象放入到Model中
		@RequestMapping("//省略")
		public String xxx(User user , Model model){
			model.addAttribute("user",user);
			return "xxx";
		}
		
		通过注解简化
		@RequestMapping("//省略")
		public String xxx(@ModelAttribute("user") User user){
			return "xxx";
		}
		
```

##### 使用Servlet API对象作为入参 控制器到视图 简化传参

```
	
	在SpringMVC 控制器可以不依赖任何ServletAPI对象 也可以作为处理方法的入参使用
	例如 我们需要使用HttpSession对象 那么可以直接将HttpSession作为入参使用
	@RequestMapper(//省略请求)
	public String xxx(HttpSession session,HttpServletRequest request){
		//省略使用session|request对象 getAttribute等等完成需求
	} 
	
	//Spring中使用ServletAPI作为入参时 SpringMVC会自动将Web层对应的Servlet对象传递给处理方法的入参 入参位置、顺序没有特殊要求
	
```

#### 视图解析器

```
	
	请求处理方法执行完成后 最终返回ModelAndView对象 对于那些返回String等类型的处理方法 SpringMVC也会在内部 将它们装配成一个ModelAndView对象 它包含了逻辑视图名 和 数据模型 SpringMVC需要借助视图解析器(ViewResolver) 将控制器返回的逻辑视图名 解析成一个真正的视图对象  
	//ViewResolver是SpringMVC处理视图的重要接口
	//视图对象可以多样 JSP视图 FreeMarker Velocity等模板技术的视图 还可以是JSON、XML、PDF等各种数据格式的视图
	//SpringMVC默认提供了 多种视图解析器 所有的视图解析器都实现了ViewResolver接口
	//对于JSP常见视图技术 通常使用InternalResourceViewResolver作为视图解析器
	//InternalResourceViewResolver通常用于查找JSP和JSTL等视图 它是URLBasedViewResolver子类 它会把返回的视图名称都解析为InternalResourceView对象 该对象会把Controller的处理方法返回的模型属性都放在对应的请求作用域中 然后通过 RequestDispatcher(转发) 在服务端 转发到目标URL 目标URL通过 配置文件 进行前缀和后缀的解析 拼接成真正的URL字符串
	//如果需要进行重定向到视图(一般情况下 控制器方法返回的字符串会被当成逻辑视图名处理 是转发请求) 就要加入"redirect:"前缀SpringMVC将对它进行特殊处理 将redirect:当做指示符 气其后的字符串作为URL处理 例如"redirect:/xx/index.jsp" 它会让浏览器重新发送一个新的请求(使用重定向方法)
	//转发的指示符forward:
	
```

### SpringMVC-Controller的单例管理

```
	
	SpringMVC的Controller类默认是单例的 主要原因基于性能的考虑 不需要每次都创建实例
	//但是这一特点 我们在使用的时候也要千万注意 在默认单例情况下 一般不要在Controller中定义成员变量 如果使用将会导致严重的线程安全以及资源使用问题
	//Controller是默认单例的 成员变量是公用的 在单用户操作没有问题 但是高并发环境下 用户A和用户B同时根据某些不同条件返回不同的成员变量 有可能返回成员变量的结果不正确 即B用户的CPU抢占了资源 那么用户A在页面显示的就是用户B的成员变量结果 
	//若根据业务场景 需要更改Controller的scope为prototype 在@Controller之前增加@Scope("protptype")就不再是单例模式 基本很少用 
	//但是在Controller内 我们可以声明Service成员变量 通过Spring自动装配进行装载
	例如
		@Resource
		private UserService userService;
	这是由于Service是大家公用的 并且它是接口 接口中没有成员变量 都是方法 而且方法中的变量也都是线程级的 固然不会出现数据资源抢占或者内存溢出的问题 所以一般情况下 Controller内的成员变量只有Service对象
	
```

### 静态资源文件的引用

```xml
	
	DispatcherServlet请求映射为 "/" 则SpringMVC将捕获Web容器所有的请求  静态资源也被 当成一个普通请求处理(会造成.js|png|jpg|css等静态文件不能正常加载) 而没有对应处理器 所以需要利用<mvc:resources/>标签解决静态资源访问问题
	
	这里首先可以将所有静态文件(js|css|images)统一放置在statics目录
	之后在SpringMVC配置文件中 添加以下配置
	
	<mvc:resources mapping="/statics/**" location="/statics" />
	
	//mapping 将静态资源映射到指定的路径(/statics)下
	//location 本地静态资源文件所在的目录

	//也可以通过在web.xml 配置文件中使用这样 允许访问 静态资源目录 不推荐 推荐使用上面的方法
	<!--    <servlet-mapping>-->
	<!--        <servlet-name>default</servlet-name>-->
	<!--        <url-pattern>*.png</url-pattern>-->
	<!--    </servlet-mapping>-->
	<!--    <servlet-mapping>-->
	<!--        <servlet-name>default</servlet-name>-->
	<!--        <url-pattern>*.css</url-pattern>-->
	<!--    </servlet-mapping>-->
	<!--    <servlet-mapping>-->
	<!--        <servlet-name>default</servlet-name>-->
	<!--        <url-pattern>*.js</url-pattern>-->
	<!--    </servlet-mapping>-->
	
```

### 异常处理

```
	
	SpringMVC通过HandlerExceptionResolver处理程序异常 包括处理器异常、数据绑定异常、处理器执行时发送的异常
		//HandlerExceptionResolver只有一个接口方法 当发生异常时 SpringMVC会调用resolveException()方法 并转到相应的ModealAndView对应的视图中作为一个异常页面 反馈给用户
		//对于异常处理 我们一般分为局部异常处理和全局异常处理
	
```

#### 局部异常处理

```
	
	局部异常处理 仅能处理指定Controller中的异常 使用@ExceptionHandler注解实现
		示例代码
			@RequestMapping("//省略")
			public String xxx(...){
				//此方法 产生异常
				throw new RuntimeException("异常信息");
			}
			
			//异常处理器
			@ExceptionHandler(value={RuntimeException.class})
			public String exceptionHandler(RuntimeException e,HttpServletRequest request){
				request.setAttribute("e",e); //将异常对象传递给视图
				return "error"; //异常信息显示异常
			}
			
			//视图当中通过请求对象的 "e" 进行异常显示
			
		//上面xxx方法抛出异常后 它会被在同一个处理器下的exceptionHandler()方法捕获 (@ExceptionHandler可以指定多个异常) 之后进行处理
	
```

#### 全局异常处理

```

	使用局部异常处理 只能处理某个Controller中的异常 若想对所有异常统一处理 就需要进行全局异常处理
	全局异常处理可以使用SimpleMappingExceptionResolver实现 它将异常类名映射为视图名 发生异常时使用对应的视图报告异常
	然后在springMVC配置中配置全局异常
		<!-- 全局异常处理 -->
        <bean class="org.springframework.web.servlet.handler.SimpleMappingExceptionResolver">
            <property name="exceptionMappings">
                <props>
                    <prop key="java.lang.RuntimeException">error</prop>
                </props>
            </property>
        </bean>
		
		//不需要在控制器中写异常处理器
		//视图当中通过${exception.message}进行异常信息显示
	
```

## SSM使用技术扩展

### 输入查询条件时 输入中文 会出现乱码 解决方案

```
	
  	    <!-- 配置过滤器，统一解决POST请求中文乱码问题 -->
        <filter>
            <filter-name>encodingFilter</filter-name>
            <filter-class>
                org.springframework.web.filter.CharacterEncodingFilter
            </filter-class>
            <init-param>
                <param-name>encoding</param-name>
                <param-value>UTF-8</param-value>
            </init-param>
            <init-param>
                <param-name>forceEncoding</param-name>
                <param-value>true</param-value>
            </init-param>
        </filter>
        <filter-mapping>
            <filter-name>encodingFilter</filter-name>
            <url-pattern>/*</url-pattern>
        </filter-mapping>
        
        
        //在web.xml中增加Spring字符编码过滤器 配置字符编码为UTF-8
	
```

### 使用监听器在Web容器启动的时候初始化Spring容器

```
	
        <!-- 配置Spring框架初始化监听器 -->
        <listener>
            <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
        </listener>
        <!-- 配置Spring框架配置文件路径|配置环境参数-->
        <context-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:applicationContext-mybatis.xml</param-value>
        </context-param>
        
        
        //由于Spring需要启动容器才能为其它 框架提供服务器 而Web应用程序的入口是被Web服务器控制的 因此无法在main()方法 中通过创建ClassPathXmlApplicationContext对象来启动Spring容器 Spring提供了一个监听器类org.springframework.web.context.ContextLoaderLitener解决问题(该监听器实现了ServletContextListener接口 可以在Web容器启动时 初始化Spring容器)
        //最好配置contextConfigLocation防止造成资源找不到等等
        //如果没有指定contextConfigLocation参数 ContextLoaderListener默认会去查找/WEB-INF/applicationContext.xml 换句话说如果我们将Spring的配置文件命名为applicationContext.xml并存放在WEB-INF目录下即使不指定contextConfigLocation参数 也能实现配置文件的加载

```

### 定义Constants类 结构性编程

```
	
	Constants类 专门用来储存 一些静态常量 
	用在例如 session作用域存储用户信息的场合
	
		//Constants类定义全局属性
		public final static String USER_SESSION = "userSession";
		//调用处
		session.setAttribute(Constants.USER_SESSION,user);
		
	这样可以让一些变量更直观 
	
```

### Spring表单标签

```
	
	在进行SpringMVC项目开发时 一般使用EL表达式 和 JSTL标签完成页面视图开发 Spring也有自己的一套表单标签库 可以更容易 规范化的完成表单开发 它们在视图使用的时候可以进行动态渲染等等
	和JSTL标签一样 使用也需要添加标签库的声明
	<%@taglib prefix="fm" uri="http://www.springframework.org/tags/form" %>
	具体使用参考 百度 实际使用举例太多了 或者 可以查看下方SSM使用示例
	
	参考网址 https://www.cnblogs.com/drizzlewithwind/p/6065800.html
	
	
	 列举部分常用Spring表单标签
	 <fm:form />	渲染表单元素
	 <fm:input /> 输入框
	 <fm:password /> 密码框
	 <fm:hidden /> 隐藏框
	 <fm:textarea /> 多行输入框
	 <fm:radiobutton /> 单选框
	 <fm:checkbox /> 复选框
	 <fm:select /> 下拉列表
	 <fm:option /> 下拉列表选项 //需要在<select>标签下
	 <fm:error /> 显示表单数据校验 所对应的错误信息
	 
	
	这些标签都拥有HTML标签的各种属性(id、onclick等) 并且基本上包含以下属性 
	//path属性 表示表单对象属性 
	//cssClass 表单组件对应的CSS样式类名
	//cssErrorClass 当提交表单后报错(服务端错误) 采用的CSS样式类
	//cssStyle 表单组件对应的CSS样式
	//htmlEscape 绑定的表单属性值 是否要对HTML特殊字符进行转换 默认为true
	
```

### 数据效验

```
	
	除了前端验证 还需要后端验证 SpringMVC提供了两种方式 验证输入
		
		Spring自带的验证框架
		
			//没有实例 参考https://blog.csdn.net/Satisfy_555/article/details/79816971
			
		JSR 303实现验证
		
			//Spring的DataBinder在进行数据绑定是 可同时调用校验框架 完成数据校验工作 非常简单
			//Spring本身没有提供JSR303的实现 Hibernate Validator实现了JSR303 所以需要加入 Hibernate Validator库的jar文件 需要三个jar文件(版本自配) Spring会进行自动装配
			hibernate-validator-4.3.2.Final.jar
			jboss-logging-3.1.0.CR2.jar
			validation-api-1.0.0.GA.jar
			
			
			//首先给POJO类加 校验注解
			public class User {
                @NotNull(message = "用户编码不能为空") //message属性用于设定不满足验证返回的 错误信息
                @NotEmpty(message = "用户编码不能为空格")
                private String userCode; //用户编码
			}
			
			
			//在Controller中 使用注解进行数据的校验
			//由于<mvc:anntation-driven/>会默认装配好一个LocalValidatorFactoryBean 直接给处理器方法需要验证的入参标注 @Valid注解即可让SpringMVC在完成数据绑定之后 执行数据校验的工作
			//注意@Valid注解标注的参数后面 必须紧挨着一个BindingResult参数 否则Spring会在校验不通过的时候直接抛出异常 因为原理是 校验的结果会存入后面紧跟的入参中 并且这个入参必须是BindingResult或者Error类型 在该方法体内 首先根据BindingResult判断是否存在错误 如果错误则跳转到填写数据的视图页面 
			
			@RequestMapping("//省略")
             public String xxx(@Valid User user,BindingResult bindingResult){
             	if(bindingResult.hasErrors()){
					return "逻辑视图名"; //跳转回收集数据的视图
				}
                 //省略需求实现
             }
			
			
			//视图页面 将错误信息显示在页面中
			<fm:form //省略属性>
				用户编码:<fm:input path="userCode"/><fm:errors path="userCode" />
			</fm:form>
			
```

### SpringMVC的数据绑定流程

```
	
	在请求信息到达处理方法之前,SpringMVC完成了 数据转化、数据格式化、数据校验等
	SpringMVC将ServletRequest对象以及处理方法的Object(入参对象)实例 传递给-> DataBinder 调用-> ConversionService组件进行数据的转换、格式化的工作 并将ServletRequest中请求消息填充到入参对象中, 再调用Validator组件对已经绑定了请求数据的入参对象进行数据合法性的验证,并最终生成数据绑定结果BindingResult对象
	
	DataBinder 数据绑定的核心部件 核心调度作用
	ConversionService Spring类型转换体系的核心接口 可以解决时间字符串到实体类Date数据类型的转换问题
	BindingResult 包含已完成数据绑定的入参对象和相应的效验错误对象 SpringMVC会抽取BindingResult中的入参对象及效验错误对象,将它们赋值给处理方法的相应入参
	
	
	
```

### 数据转换与格式化

```
	
	在对Bean的属性进行数据绑定时出现了问题,出现了400的错误 原因是日期字符串与JavaBean中的日期类型的属性需要转换 而SpringMVC框架默认不支持这个格式转换 即在SpringMVC中时间数据无法实现自动转换 需要进行手动配置数据类型绑定
	
	第一种方法 使用转换注解
	
		在实体类的日期属性上标注格式化注解@DateTimeFormat(pattern="yyyy-MM-dd")
		//注解可以直接使用,是因为<mvc:annotation-driven/>标签 是SpringMVC的简化配置 默认情况下 它会创建并注册一个默认的DefaultAnnotationHandlerMapping和一个AnnotationMethodHandlerAdapter实例 一个ConversionService实例FormattingConversionServiceFactoryBean
		//也可以再去Spring配置配置一个conversionService 
		可以利用org.springframework.context.support.ConversionServiceFactoryBean在Spring的上下文定义一个ConversionService Spring会自动识别出上下文中的ConversionService 在进行Bean属性配置和处理方法入参绑定时 使用它进行数据的转换
		<bean id="conversionService" class="org.springframework.context.support.ConversionServiceFactoryBean"/>
		
	可以编写自定义转换器
		
		//详细百度 https://www.cnblogs.com/caoyc/p/5639652.html
		
	也可以使用@InitBinder装配自定义编辑器
		
		//详细百度 https://blog.csdn.net/weixin_30919429/article/details/96336847
		
```

### JSR303约束

```
	
	JSR303是Java为Bean数据合法性校验提供的标准框架 JSR303通过在Bean属性上标注验证注解 指定校验规则 并通过标准验证接口对Bean进行验证
	它定义了一套可标注在成员变量、属性方法上的校验注解
	JSR303是一个规范 它的核心接口是javax.validation.Validator	

	@Null 被注释的元素必须为null
	@NotNull 被注释的元素必须不为null
	@NotEmpty 被注释的元素必须不为空
	@Length 被注释的字符串的大小必须在指定范围内
	@AssertTrue 被注释的元素必须为true
	@AssertFalse 被注释的元素必须false
	@Min(value) 被注释的元素必须是一个数字,值必须大于等于指定的最小值
	@Max(value) 被注释的元素必须是一个数字,值必须小于等于指定的最大值
	@DecimalMin(value) 被注释的元素必须是一个数字,值必须大于等于指定的最小值
	@DecimalMax(value) 被注释的元素必须是一个数字,值必须小于等于指定的最大值
	@Size(max,min) 被注释的元素必须在指定的范围内
	@Digits(integer,fraction) 被注释的元素必须是一个数字,值必须在可接受的范围内
	@Past 被注释的元素必须是一个过去的日期
	@Future 被注释的元素必须是一个将来的日期
	@Pattern(value) 被注释的元素必须符合指定的正则表达式
	//其它百度 https://www.cnblogs.com/tengfeixinxing/p/7043340.html
	
```

### REST架构风格

```
	
	REST Representational State Transfer 表述性状态转移 是一种软件架构风格 
	//可以简单理解为 使用URL表示资源时 每个资源都用一个独一无二的URL来表示 并使用HTTP方法表示操作 即准确描述服务器对资源的处理动作(GET、POST、PUT、DELETE)实现资源的增删改查 例如/userdelete.html?id=1 变成了/user/delete/12
	//很明显REST风格的URL不使用?传递参数 这种风格可读性好 让项目架构更加清晰 SpringMVC也提供对这种风格的支持 但是对于国内项目 URL参数有时会传递中文 那么会出现中文乱码问题 所以需要根据情况进行灵活处理 传统URL风格与REST风格混搭使用
	
	下面为REST风格实现示例
 		//首先请求地址变为http://localhost:8090/上下文名称/user/delete/223
		
		//处理器
		@RequestMapping(value="/view/{id}",method=RequestMethod.GET)
		public String deleteHandler(@PathVariable String id){
			//省略业务需求实现
		}
		
		SpringMVC 提供了@PathVariable注解 可以将URL中的{xxx}占位符 参数绑定到控制器处理方法的入参中
	
```

### SpringMVC实现文件上传

```
	
	SpringMVC 对文件上传 提供了直接支持 MultipartResolver接口(用于处理上传请求 将上传请求包装成可以直接获取文件的数据 方便操作)
	MultipartResolver接口 有两个实现类
		StandardServletMultipartResolver(使用Servlet3.0标准上传方式)和CommonsMultipartResolver(使用Apache的Commons-fileupload完成具体的上传操作)
	
	 示例使用CommonsMultipartResolver进行单文件上传
	 	
	 	一 导入jar文件
	 		
	 		commons-fileupload-1.3.3.jar
	 		commons-io-2.5.jar
	 		
	 	二 之后在SpringMVC配置文件  配置MultipartResolver解析器 
	 	
		    <!-- 配置MultipartResolver,用于上传文件,使用spring的CommonsMultipartResolver -->
             <bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
                 <property name="maxUploadSize" value="5000000" />
                 <property name="defaultEncoding" value="UTF-8" />
             </bean>
		   
		    //defaultEncoding 请求的编码格式 默认ISO-8859-1 应设置为UTF-8(注意这个编码必须和JSP中的pageEncoding一致 以便正确读取表单内容)
		    //maxUploadSize 上传文件大小上限 单位为字节
		
		三 编写表单页面
			
			//注意上传表单三要素 提交方式post、编码类型"multipart/form-data"、input文件域(这里给例名PicPath)
			
		四 编写控制器
		
			@RequestMapping(//省略)
			public String xxx(@RequestParam("PicPath",required = false) MultipartFile attach , ...){
				String picPath = null; //定义储存图片位置的 数据库字段
				if(!attach.isEmpty()){
					String path = request.getSession().getServletContext().getRealPath("statics"+File.separator+"uploadfiles");
					//获取原文件夹名
                      String oldFileName = multipartFile.getOriginalFilename();
                      //获取原文件名后缀 方便后面进行 格式验证
                      String prefix = FilenameUtils.getExtension(oldFileName);
					//设置上传文件大小
                      int filesize = 500000;
                      //控制上传大小、控制图片格式
                      if(attach.getSize() > filesize){
                      		//省略大小超出 处理操作 抛到异常页面 或者 定义error信息
                      }else if(prefix.equalsIgnoreCase("jpg")//省略其它条件判断){
                      		//进行文件保存操作
                      		String fileName = System.currentTimeMillis() + RandomUtils.nextInt(1000000) + "_Personal.jpg"; //定义不重复文件名
                            File targetFile = new File(path,fileName);
                            if (!targetFile.exists()){ //如果上传包不存在
                                targetFile.mkdirs(); //创建上传包
                            }
                            //保存zf
                            try {
                                multipartFile.transferTo(targetFile); //调用MultipartFile的该方法 把MultipartFile中的文件流的数据输出值目标文件中
                                picPath = pathPrefix + fileName;  //拼装图片位置名称
                            }catch (Exception e){
                                //出现异常处理
                                e.printStackTrace();
                                request.setAttribute(errorInfo,"*上传失败");
                                flag = false;
                            }
                      }else{
                      		//省略图片格式不正确 处理操作 抛到异常页面 或者 定义error信息
                      }
				}
				//省略保存其它字段和保存图片路径的代码块 根据需求
			}
			
			//if(!attach.isEmpty()){}判断上传文件是否为空 根据需求进行编写
			//path为上传目标路径
			//定义上传路径时 需要使用File.separator(Windows、Linux自适应路径分隔符) 因为Windows、Linux服务器可能是Windows系统或者Linux系统 File.separator是自适应路径分隔符 低入侵性的代码实现
			//为了防止 上传文件覆盖服务器上其他用户上传的文件 定义不重复文件名 这里使用了RandomUtils(需要引入jar文件commons-lang-2.6.jar)获取0~1000000以内的随机数 
			
			//多文件上传 表单页面增加file标签即可 上传标签name设成同样值 控制器接受时将MultipartFile设置成数组MultipartFile[]  之后根据需求进行编写 //注意 处理多文件上传上传的到底是哪个文件 //注意使用MultipartFile[](数组)一定要设置@RequestParam注解 否则会报错
			//多文件上传 也可以使用 单独入参 传入多个MultipartFile对象 推荐!!!!!!!!!!
	
```

### 实现Ajax异步请求

```
	
	SpringMVC处理Ajax请求
	
	示例说明
	
	//Ajax请求发出 并且可能附带参数
	
	@RequestMapping(//省略)
	@ResponseBody
	public Object xxx(//省略参数){
		HashMap<String,String> resultMap = new HashMap<String,String>();
		//根据需求 和结果进行resultMap键和值 进行put
		return JSONArray.toJSONString(resultMap);
	}
	
	//JSONArray.toJSONString(resultMap); 将集合对象转换为JSON对象 返回输出
	//JSON.toJSONString(Bean对象); 将Bean对象转换成JSON格式的字符串
	//Object 返回类型为Object
	//@ResponseBody 注解 作用标注该注解的处理方法的返回结果 直接写入HTTP Response Body(Response对象的body数据区) 一般情况 @ResponseBody会在异步获取数据时使用 被其标注的处理方法返回的数据 将输出到响应流 客户端获取并显示数据
	
```

### 解决JSON数据传递出现的问题

```
	
	在Ajax请求中 会出现中文乱码问题和出生日期格式显示不正确的问题
	
	
	解决中文乱码问题
	
		问题 在SpringMVC 控制器的处理器方法 使用@ResponseBody注解向前台页面以JSON格式进行数据传递时 返回值是中文字符串 就会出现乱码 
		
		原因 SpringMVC 消息转换器(org.springframework.http.converter.StringHttpMessageConverter)固定了转换字符编码 (ISO-8859-1) StringHttpMessageConverter作用将请求信息转换为字符串
		
		解决 更改字符串转换编码为UTF-8 
			
			第一种方法 在@RequestMapping注解中配置produces属性 比较灵活 简单实用
			
				produces 指定返回的内容类型 produces={"application/json;charset=UTF-8"} 表示该处理方法将产生JSON格式的数据。 它会和请求报文头中的Accept进行匹配 若请求报文头为Accept:application/json  则匹配成功,设置响应字符串的转换编码为UTF-8
				//可能会出现406状态码 可能是因为请求报文头与响应报文头的Context-Type 类型不一致 检查@ResquestMapping的value属性 和 异步请求URL 是否包含.html这样的后缀 因为有这个后缀SpringMVC会以HTML格式来显示响应信息 去掉请求中的.html 而且最好不要使用.这样的请求URL采用 传统格式+REST风格等等
				
			
			第二种方法 装配消息转换器StringHttpMessageConverter设置字符编码为UTF-8 一次配置 永久搞定
				
			    通过设置StringHttpMessageConverter中的supportedMediaTypes属性 指定媒体类型为application/json 字符编码为UTF-8
				
			    SpringMVC配置文件
			    <!-- 启用Spring MVC注解支持，配置消息转换器 -->
                 <mvc:annotation-driven>
                     <mvc:message-converters>
                         <!-- 配置StringHttpMessageConverter消息转换器，解决JSON数据中文乱码问题 -->
                         <bean class="org.springframework.http.converter.StringHttpMessageConverter">
                             <property name="supportedMediaTypes">
                                 <list>
                                     <value>application/json;charset=UTF-8</value>
                                 </list>
                             </property>
                         </bean>
                     </mvc:message-converters>
                 </mvc:annotation-driven>
	
	
	解决日期格式问题
		
		问题 SpringMVC中使用@ResponseBody 返回JSON数据时 日期格式默认显示为时间戳
		
		原因 SPringMVC使用@ResponseBody返回JSON数据时,日期格式默认显示为时间戳 
		
		解决 将它转换成可读性的"yyyy-MM-dd"日期格式
		
			第一种方法 在实体类的日期属性加上 @JSONField(format="yyyy-MM-dd")进行日期格式化处理 强侵入性 紧耦合 硬编码 注解方式比下面第二种方式优先 可以结合使用
			
			
			第二种方法 配置FastJson的消息转换器 FastJonHttpMessageConverter
			
				使用FastJsonHttpMessageConverter的序列化属性 WriteDateUseDateFormat配置使用默认日期类型(FastJson规定了默认的返回日期类型DEFFAULT_DATE_FORMAT 为yyyy-MM-dd HH:mm:ss) 特殊的日期格式使用@JSONField
				
				//设置了这个方法之后 (配置了FastJsonHttpMessageConverter这个Bean(与设置无关)之后会自动进行,数据Json格式转化) 无需再将 方法返回对象转换成JSON字符串 直接返回对象就行
				
				设置features属性指定输出时的日期转换器为WriteDateUseDateFormat 
				
				SpringMVC配置文件
				<!-- 启用Spring MVC注解支持,配置消息转换器 -->
                 <mvc:annotation-driven>
                     <mvc:message-converters>
                         <bean class="com.alibaba.fastjson.support.spring.FastJsonHttpMessageConverter">
                            <property name="supportedMediaTypes">
                                <list>
                                    <value>text/html;charset=UTF-8</value>
                                    <value>application/json</value>
                                </list>
                            </property>
                            <property name="features">
                                <list>
                                    <!-- 输出Date的日期转换器 -->
                                    <value>WriteDateUseDateFormat</value>
                                </list>
                            </property>
                        </bean>
                     </mvc:message-converters>
                 </mvc:annotation-driven>
			
			
			第三种 通过以上配置 代码侵入性降低 但是实际开发中 我们不想使用yyyy-MM-dd HH:mm:ss 默认格式而且还不想通过@JSONField注解解决 我们可以自己实现FastJson消息转换器 
				
				//具体实现百度 https://blog.csdn.net/u014475245/article/details/78571170
				
```

### 各个JSON技术比较(扩展了解)

```
	
	json-lib 最早应用广泛的JSON解析工具
	
    	缺点 依赖多个三方包 对于复杂类型转换 JSON转换成Bean时有缺陷(例如一个类包含另一个类的List或Map集合) JSON到Bean的转换就会出现问题 功能性能不能满足互联网化的需求
    
    
    Jackson SpringMVC内置的JSON转化工具 
    
    	相比json-lib依赖jar较少 简单易用性能相对较高 社区活跃更新速度较快
    	缺点 对于复杂类型的JSON转换Bean会出现问题 复杂类型的Bean转换成JSON转换的JSON格式不是标准的JSON格式
    
    
    Gson 目前功能最全的JSON解析神器 是应Google公司内部需求 而又Google自行研发来的 2008/5 公开发布 已被许多公司应用
    
    	主要为toJson和fromJson两个转换函数 无依赖 不需要额外的jar文件 能够直接跑在JDK上
    	可以完成复杂类型的JSON到Bean或Bean到JSON的转换 是 JSON解析神器 功能无可挑剔 性能比FastJson稍差
    	
    	
    FastJson Java编写的高性能JSON处理器 由阿里巴巴公司开发 特点 无依赖 不需要额外的jar文件 可以直接跑在JDK上 但是FastJson在复杂类型 的Bean转化JSON上会出现一些问题 可能会出现引用的类型 导致JSON转换出错 需要指定引用 
    	FastJson采用独创算法 将parse的速度提升到极致 超过所有JSON库
    	
    	
    	
    总结 项目选取使用的时候 可以使用Google的Gson和阿里巴巴的FastJson两种并行使用 
    	
        若只是功能要求 没有性能要求 可以使用Google的Gson 
        若性能要求 可以使用Gson将Bean转换JSON确保数据正确 使用FastJson将JSON转换Bean
    	
```

### 多视图解析器

```xml
	
	<!-- 配置多视图解析器：允许同样的内容数据呈现不同的view -->
    <bean class="org.springframework.web.servlet.view.ContentNegotiatingViewResolver">
        <property name="favorParameter" value="true"/>
        <property name="defaultContentType" value="text/html"/>
        <property name="mediaTypes">
            <map>
                <entry key="html" value="text/html;charset=UTF-8"/>
                <entry key="json" value="application/json;charset=UTF-8"/>
                <entry key="xml" value="application/xml;charset=UTF-8"/>
            </map>
        </property>
        <property name="viewResolvers">
            <list>
                <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver" p:prefix="/WEB-INF/jsp/" p:suffix=".jsp"/>
            </list>
        </property>
    </bean>
	
	//大部分需求都是JSP视图 只配置 一个视图解析器(JSP)就够了
	//作用待考究 用到的时候再去 考虑 下面的网址是正确实例 使用时可以进行参考 
	//https://blog.csdn.net/qq_41731166/article/details/81483832	

```

### 配置拦截器

```xml
	
	防止用户非法进入系统 跳过登录直接到达管理页面等 最好的解决方案就是增加系统拦截器 在拦截器统一进行session判断
	
	//可以配置此项确保系统数据的安全性 //基于HandlerMapping 对请求实施拦截,根据业务需求,基于不同的HandlerMapping定义多个拦截器 //需要配置自定义拦截器的配置 
	
	使用需要在springmvc配置中配置拦截器 
	
	<!-- 配置拦截器,对sys目录资源进行访问控制 -->
    <mvc:interceptors>
        <mvc:interceptor>
            <mvc:mapping path="/sys/**"/>
            <bean class="xx.xx.interceptor.SysInterceptor" />
        </mvc:interceptor>
    </mvc:interceptors>
	
	//上面拦截器表示 所有以sys开头的请求 都需要通过自定义的Sysinterceptor拦截器
	

	原理 在接受前端请求时 DispatcherServlet会将请求交给处理器映射(HandlerMapping) 它会找出对应请求的HandlerExecutionChain对象 该对象是一个执行链 它包含处理该请求的处理器(Handler) 以及若干个对请求实施拦截的拦截器(HandlerInterceptor) HandlerInterceptor是一个接口 它包含三个方法 
	preHandle() 在请求到达Handler之前 先还行该前置处理方法 当该方法返回false时 请求直接返回 若返回true是 请求继续往下传递(HandlerExecutionChain中下一个节点) 由于preHandler()会在Controller之前执行  我们可以在该方法里进行编码、安全控制等逻辑处理
	postHandler() 在请求被HandlerAdapter执行后 执行这个后置处理方法 由于postHandle()在Controller处理方法生成视图之前执行 我们可以在该方法中修改ModelAndView
	afterCompletion() 在响应已经被渲染之后 最后执行该方法 释放资源


	拦截器示例

        package cn.smbms.interceptor;

        import cn.smbms.pojo.User;
        import cn.smbms.tools.Constants;
        import org.apache.log4j.Logger;
        import org.springframework.web.servlet.handler.HandlerInterceptorAdapter;

        import javax.servlet.http.HttpServletRequest;
        import javax.servlet.http.HttpServletResponse;
        import javax.servlet.http.HttpSession;

        /**
         * SysInterceptor拦截器类
         * @author BIElI
         */
        public class SysInterceptor extends HandlerInterceptorAdapter {
            private Logger logger = Logger.getLogger(SysInterceptor.class);

            @Override
            public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception{
                logger.debug("SysInterceptor preHandle ==========================");
                //获取Session对象
                HttpSession session = request.getSession();
                //判断Session中是否存在用户登录信息
                User user = (User) session.getAttribute(Constants.USER_SESSION);
                if (null == user){
                    response.sendRedirect(request.getContextPath() + "/权限错误页面.jsp");
                    return false;
                }
                return true;
            }
        }

```

## SSM使用示例(具有强化扩展)(省略部分)

### 项目框架设计

```
	
	SSM框架设计 速度快、性能高、配置简单
	数据储存 MySQL数据库进行数据存储
	ORM MyBatis框架 实现数据库持久化操作
	Spring Core 基于IOC AOP处理方式统一管理所有JavaBean
	Web框架 采用SpringMVC进行Web请求的接收与处理
	前端框架 使用JSP作为页面载体 使用jQuery框架以及HTML5、CSS3实现页面的展示和交互 
	
```

### 项目目录结构	

```
	
	Project
		resources //配置资源目录
			applicationContext.xml //spring配置文件
			database.properties //数据库配置
			log4j.properties //Log4j日志框架配置
			mybatis.xml //mybatis框架配置
			springmvc.xml //springMVC配置文件
		src //java代码包
			xxx //项目名 或者 公司项目名 
				controller //控制器包 //前端控制层
				dao //数据库访问层包 //数据库访问接口等
				interceptor //拦截器包
				logs //Log4j日志文件包
					logs.log //日志文件
				pojo //实体类包 //数据对象模型
					Xxx //实体类对象
				service //业务逻辑层包 //系统服务接口
					XxxService //业务逻辑层接口
					XxxServiceImpl //业务逻辑层接口实现类
				tools //工具包 //系统工具类
					Constants //静态常量名类 
		WebRoot //前端包
			statics //静态文件包 //静态资源文件
				css //层叠样式表
				images //图片包
				js //javascript包
				uploadfiles //上传文件包
			WEB-INF //用户无法直接访问包
				classes //项目编译目录
				jsp //视图页面 //前端页面
				lib //jar包目录 
				web.xml //项目配置文件
	
```

### 一些项目简化点和实际需求强化点

```
	
	简化点
		
		p命名空间 简化Spring配置
		@include 导入相同前端页面
		在web.xml配置开启项目默认进入页面
		定义一个Constants类
		${pageContext.request.contextPath} 定义所有URL路径
		利用 @SessionAttributes注解 和 @ModelAttribute注解 简化处理器传参
		视图向服务器传参时可以设置隐藏域向服务端传值
		使用form标签省略action属性根据请求方式进行处理器判断
		配置FastJson消息转化器对 Ajax请求处理器进行简化
		配置拦截器
		
	强化点
		
		配置sql心跳包 //在效验连接的同时,解决数据库重新连接的问题,从而确保连接池 中连接是真实有效的连接 //具体参考Spring配置文件 //
	
```

### 项目运行配置文件

#### web.xml

```xml
	
	<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://java.sun.com/xml/ns/javaee" xmlns:web="http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd" xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd" version="3.0">
    <display-name>springMVC</display-name>
    <!-- 配置欢迎首页 -->
    <welcome-file-list>
        <welcome-file>/WEB-INF/jsp/login.jsp</welcome-file>
    </welcome-file-list>

    <!-- 配置过滤器，统一解决POST请求中文乱码问题 -->
    <filter>
        <filter-name>encodingFilter</filter-name>
        <filter-class>
            org.springframework.web.filter.CharacterEncodingFilter
        </filter-class>
        <init-param>
            <param-name>encoding</param-name>
            <param-value>UTF-8</param-value>
        </init-param>
        <init-param>
            <param-name>forceEncoding</param-name>
            <param-value>true</param-value>
        </init-param>
    </filter>
    <filter-mapping>
        <filter-name>encodingFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>
    <!-- 配置Spring MVC框架核心控制器 -->
    <servlet>
        <servlet-name>springmvc</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <!-- 配置SpringMVC配置文件路径 -->
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:springmvc-servlet.xml</param-value>
        </init-param>
        <!-- 定义Spring MVC框架初始化顺序 1Tomcat初始化完成后 初始化此Servlet -->
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>springmvc</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
    <!-- 配置Spring框架初始化监听器 -->
    <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>
    <!-- 配置Spring框架配置文件路径-->
    <context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>classpath:applicationContext-mybatis.xml</param-value>
    </context-param>

    <!-- 配置Log4j配置文件路径 -->
    <context-param>
        <param-name>log4jConfigLocation</param-name>
        <param-value>classpath:log4j.properties</param-value>
    </context-param>
    <!-- 配置Log4j对象初始化监听器 -->
    <listener>
        <listener-class>org.springframework.web.util.Log4jConfigListener</listener-class>
    </listener>
    //也可以使用下面的配置 进行静态文件访问处理
<!--    <servlet-mapping>-->
<!--        <servlet-name>default</servlet-name>-->
<!--        <url-pattern>*.png</url-pattern>-->
<!--    </servlet-mapping>-->
<!--    <servlet-mapping>-->
<!--        <servlet-name>default</servlet-name>-->
<!--        <url-pattern>*.css</url-pattern>-->
<!--    </servlet-mapping>-->
<!--    <servlet-mapping>-->
<!--        <servlet-name>default</servlet-name>-->
<!--        <url-pattern>*.js</url-pattern>-->
<!--    </servlet-mapping>-->
</web-app>
	
```

#### database.properties

```properties
	
	driver=com.mysql.jdbc.Driver
    url=jdbc:mysql://127.0.0.1:3306/smbms?useUnicode=true&characterEncoding=utf-8
    user=root
    password=----
    minIdle=45
    maxIdle=50
    initialSize=5
    maxActive=100
    maxWait=100
    removeAbandonedTimeout=180
    removeAbandoned=true
	
```

#### applicationContext.xml

```xml
	
	<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	   xmlns:aop="http://www.springframework.org/schema/aop"
	   xmlns:p="http://www.springframework.org/schema/p"
	   xmlns:tx="http://www.springframework.org/schema/tx"
	   xmlns:context="http://www.springframework.org/schema/context"
	   xsi:schemaLocation="
            http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-2.5.xsd   
            http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop-2.5.xsd   
            http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx-2.5.xsd 
            http://www.springframework.org/schema/context 
            http://www.springframework.org/schema/context/spring-context.xsd">
	<!-- 注解自动扫描路径 -->
	<context:component-scan base-package="cn.smbms.service,cn.smbms.controller"/>
	<!-- 读取数据库配置文件 -->
	<bean class="org.springframework.beans.factory.config.PropertyPlaceholderConfigurer" p:location="classpath:database.properties"/>
	<!-- 获取数据源(使用dbcp连接池) -->
	<bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource" destroy-method="close">
		<!--  通过jndiName指定引用的JNDI数据源名称  -->
		<property name="driverClassName" value="${driver}"/>
		<property name="username" value="${user}"/>
		<property name="password" value="${password}"/>
		<property name="url" value="${url}"/>
		<property name="initialSize" value="${initialSize}"/>
		<property name="maxActive" value="${maxActive}"/>
		<property name="maxIdle" value="${maxIdle}"/>
		<property name="minIdle" value="${minIdle}"/>
		<property name="maxWait" value="${maxWait}"/>
		<property name="removeAbandoned" value="${removeAbandoned}"/>
		<property name="removeAbandonedTimeout" value="${removeAbandonedTimeout}"/>
		<!-- sql 心跳 -->
		<property name="testWhileIdle" value="true"/>
		<property name="testOnBorrow" value="false"/>
		<property name="testOnReturn" value="false"/>
		<property name="validationQuery" value="select 1"/>
		<property name="timeBetweenEvictionRunsMillis" value="60000"/>
		<property name="numTestsPerEvictionRun" value="${maxActive}"/>
	</bean>
	<!-- 配置mybitas SqlSessionFactoryBean -->
	<bean id="sqlSessionFactoryBean" class="org.mybatis.spring.SqlSessionFactoryBean">
		<!-- 引用数据源组件 -->
		<property name="dataSource" ref="dataSource"/>
		<!-- 引用MyBatis配置文件中的配置 -->
		<property name="configLocation" value="classpath:mybatis-config.xml"/>
		<!-- 配置别名包 --><!--实体类别名基准包 --><!--指定POJO类扫描路径-->
		<property name="typeAliasesPackage" value="cn.smbms.pojo"/>
		<!-- 配置SQL映射文件信息 -->
		<property name="mapperLocations">
			<list>
				<!-- 自动扫描dao包及其任意 子包下的任意 xml  添加为SQL映射文件位置 -->
				<value>classpath:cn/smbms/dao/**/*.xml</value>
			</list>
		</property>
	</bean>
    <!-- 配置MapperScannerConfigurer自动扫描路径 -->
	<bean class="org.mybatis.spring.mapper.MapperScannerConfigurer" p:basePackage="cn.smbms.dao"/>
	<!-- 定义事务管理器 -->
	<bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager" p:dataSource-ref="dataSource"/>
	<!-- 为指定的 事务管理器 设置事务属性 -->
	<tx:advice id="transactionAdvice">
		<tx:attributes><!-- 定义属性 声明事务规则 -->
			<tx:method name="find*" propagation="SUPPORTS"/>
			<tx:method name="get*" propagation="SUPPORTS"/>
			<tx:method name="add*" propagation="REQUIRED"/>
			<tx:method name="modify*" propagation="REQUIRED"/>
			<tx:method name="delete*" propagation="REQUIRED"/>
			<tx:method name="update*" propagation="REQUIRED"/>
			<tx:method name="*" propagation="REQUIRED"/>
		</tx:attributes>
	</tx:advice>
	<!-- AOP 事务处理 -->
	<aop:aspectj-autoproxy/><!-- 开启aop注解支持 -->
	<!-- 定义切面 -->
	<aop:config>
		<!-- 定义切入点 -->
		<aop:pointcut id="UserServiceImpl" expression="execution(* cn.smbms.service.user.UserServiceImpl.*(..))"/>
		<!-- 将事务增强 与 切入点组合 -->
		<aop:advisor advice-ref="transactionAdvice" pointcut-ref="UserServiceImpl"/>
	</aop:config>
	<bean id="conversionService" class="org.springframework.context.support.ConversionServiceFactoryBean"/>

</beans>
	
```

#### springmvc.xml

```xml
	
	<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xmlns:p="http://www.springframework.org/schema/p"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd
        http://www.springframework.org/schema/mvc
        http://www.springframework.org/schema/mvc/spring-mvc.xsd">

    <!-- 注解自动扫描基准包路径 -->
    <context:component-scan base-package="cn.smbms.controller"/>
    <!-- 启用Spring MVC注解支持，配置消息转换器 -->
    <mvc:annotation-driven>
        <mvc:message-converters>
            <!-- 配置StringHttpMessageConverter消息转换器，解决JSON数据中文乱码问题 -->
            <bean class="org.springframework.http.converter.StringHttpMessageConverter">
                <property name="supportedMediaTypes">
                    <list>
                        <value>application/json;charset=UTF-8</value>
                    </list>
                </property>
            </bean>
<!--             配置FastJsonHttpMessageConverter消息转换器，解决JSON数据日期显示格式问题 -->
            <bean class="com.alibaba.fastjson.support.spring.FastJsonHttpMessageConverter">
                <property name="supportedMediaTypes">
                    <list>
                        <value>text/html;charset=UTF-8</value>
                        <value>application/json</value>
                    </list>
                </property>
                <property name="features">
                    <list>
                        <!-- 输出Date的日期转换器 -->
                        <value>WriteDateUseDateFormat</value>
                    </list>
                </property>
            </bean>
        </mvc:message-converters>
    </mvc:annotation-driven>
    <!-- 静态资源引用处理 -->
    <mvc:default-servlet-handler/>
    <mvc:resources mapping="statics/**" location="/statics/" />
    <!-- 配置多视图解析器：允许同样的内容数据呈现不同的view -->
    <bean class="org.springframework.web.servlet.view.ContentNegotiatingViewResolver">
        <property name="favorParameter" value="true"/>
        <property name="defaultContentType" value="text/html"/>
        <property name="mediaTypes">
            <map>
                <entry key="html" value="text/html;charset=UTF-8"/>
                <entry key="json" value="application/json;charset=UTF-8"/>
                <entry key="xml" value="application/xml;charset=UTF-8"/>
            </map>
        </property>
        <property name="viewResolvers">
            <list>
                <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver" p:prefix="/WEB-INF/jsp/" p:suffix=".jsp"/>
            </list>
        </property>
    </bean>

<!--    单视图解析器-->
    <!-- <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver" p:prefix="/WEB-INF/jsp/" p:suffix=".jsp"/> -->
    <!-- 配置拦截器，对sys目录资源进行访问控制 -->
    <mvc:interceptors>
        <mvc:interceptor>
            <mvc:mapping path="/sys/**"/>
            <bean class="cn.smbms.interceptor.SysInterceptor" />
        </mvc:interceptor>
    </mvc:interceptors>

    <!-- 配置MultipartResolver，用于上传文件，使用spring的CommonsMultipartResolver -->
    <bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
        <property name="maxUploadSize" value="5000000" />
        <property name="defaultEncoding" value="UTF-8" />
    </bean>
    <!-- 全局异常处理 其它特殊异常已被特殊try catch 处理 -->
    <bean class="org.springframework.web.servlet.handler.SimpleMappingExceptionResolver">
        <property name="exceptionMappings">
            <props>
                <prop key="java.lang.Exception">error</prop>
            </props>
        </property>
    </bean>
</beans>

```

#### log4j.properties

```properties
	
	# rootLogger是所有日志的根日志,修改该日志属性将对所有日志起作用
    # 下面的属性配置中,所有日志的输出级别是debug,输出源是con,logfile
    log4j.rootLogger=debug,con,logfile
    # 定义输出源的输出位置是控制台
    log4j.appender.con=org.apache.log4j.ConsoleAppender
    # 定义输出日志的布局采用的类
    log4j.appender.con.layout=org.apache.log4j.PatternLayout
    # 定义日志输出布局
    log4j.appender.con.layout.ConversionPattern=%d{MM-dd HH:mm:ss}[%p]%c%n -%m%n
    # 定义日志输出位置
    log4j.appender.logfile=org.apache.log4j.FileAppender
  log4j.appender.logfile.File=B:/ProgrammingProjects/IdeaWorkSpace/SMBMS_SSM/src/cn/smbms/logs/log.log
    log4j.appender.logfile.layout=org.apache.log4j.PatternLayout
    log4j.appender.logfile.layout.ConversionPattern=%d{yyyy-MM-dd HH:mm:ss} %l %F %p %m%n

```

#### mybatis.xml

```xml
	
	<?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE configuration   
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"   
        "http://mybatis.org/dtd/mybatis-3-config.dtd">  
<configuration>
      <!-- MyBatis运行特性全局设置 -->
      <settings>
          <!-- 设置日志实现类 --><!-- 配置mybatis的log实现为LOG4J -->
          <setting name="logImpl" value="Log4J"/>
          <!-- 设置懒加载模式 设置为false表示 所有相关联的实体都被初始化加载 -->
          <setting name="lazyLoadingEnabled" value="false" />
          <!-- 开启缓存 -->
          <setting name="cacheEnabled" value="true"/>
      </settings>
</configuration>  
	
```

### controller包

#### UserController.java

```java
	
    import ...

    /**
     * UserController用户相关业务控制器
     * @author BIElI
     */
    @Controller
    @RequestMapping("/sys/user")
    public class UserController {
        /**
         * 用户业务逻辑层对象
         */
        @Autowired
        private UserService userService;    

        /**
         * Ajax请求 处理器判断 用户编码是否已经使用
         * @param userCode 要使用的用户编码
         * @return 返回Json数据  userCode 值exist已经存在 noexist不存在
         * @throws Exception -
         */
        @RequestMapping("/ucexist.json")
        @ResponseBody
        public Object userCodeIsExitHandler(@RequestParam String userCode) throws Exception {
            //用于储存响应结果 HashMap创建时尽量指定其大小
            HashMap<String,String> map = new HashMap<String,String>(1);
            if (StringUtils.isNullOrEmpty(userCode)){
                //如果userCode为null或者为空
                map.put("userCode","exist");
            }else {
                //真正去数据库搜索有没有相同编码用户
                map.put("userCode" , null != userService.selectUserCodeExist(userCode) ? "exist" : "noexist");
            }
            //利用FastJson快速JSON格式化
            return map;
        }

        /**
         * 处理查看用户详情请求处理器
         * @param userid 查看用户的id
         * @param model 向JSP页面传参
         * @return 逻辑视图名userview 显示用户详细信息视图
         * @throws Exception -
         */
        @RequestMapping("/view")
        public String getUserViewByIdHandler(@RequestParam("userid") String userid,Model model) throws Exception {
            model.addAttribute("user" , userService.getUserById(userid));
            return "userview";
        }
    }

```

#### LoginController.java

```
	
	/**
     * 登录注销相关业务控制器
     * @author BIElI
     */
    @Controller
    public class LoginController {
        /**
         * 用户业务逻辑层对象
         */
        @Autowired
        private UserService userService;

        /**
         * 登录请求处理器
         * @param userCode 用户编码
         * @param userPassword 用户密码
         * @param request request对象
         * @param session  session对象
         * @return 逻辑视图名 登录成功frame-管理主页面  登录失败login-登录页面
         * @throws Exception -
         */
        @RequestMapping("/dologin")
        public String loginHandler(@RequestParam String userCode, @RequestParam String userPassword, HttpServletRequest request, HttpSession session) throws Exception {
            //调用业务逻辑层方法 进行验证
            User user = userService.login(userCode,userPassword);
            //登陆成功
            if(null != user){
                //将登录用户信息 放入session
                session.setAttribute(Constants.USER_SESSION, user);
                //页面跳转（frame.jsp）
                return "frame";
            }else{
                //页面跳转（login.jsp）带出提示信息--转发
                request.setAttribute("error", "用户名或密码不正确");
                return "login";
            }
        }

        /**
         * 注销请求处理器
         * @param session session对象
         * @return 逻辑视图名login-登录页
         */
        @RequestMapping("/logout")
        public String  loginOutHandler(HttpSession session){
            //清除session
            session.removeAttribute(Constants.USER_SESSION);
            return "login";
        }
    }
	
```

### dao包下user包(用户相关数据库访问层)

#### UserMapper接口

```java
	
    import ...

    /**
     * @author BIElI
     */
    public interface UserMapper {

        /**
         * 通过userId获取user
         * @param id 用户id
         * @return user 对象
         * @throws Exception -
         */
        public User getUserById(String id)throws Exception;

    }
	
```

#### UserMapper.xml SQL映射文件

```xml
	
	<?xml version="1.0" encoding="UTF-8" ?>
	<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
	<!-- 命名空间全局唯一，一般是DAO接口的全限定名 -->
	<mapper namespace="cn.smbms.dao.user.UserMapper">
    <!-- SQL映射语句 -->
	    <!-- 通过userId获取user -->
        <select id="getUserById" parameterType="String" resultType="User">
            SELECT u.*,r.roleName AS userRoleName FROM smbms_user AS u JOIN smbms_role AS r ON u.userRole = r.id
            WHERE u.id = #{id}
        </select>
	</mapper>
	
```

### interceptor拦截器包

#### SysInterceptor拦截器类

```java
	
	/**
     * SysInterceptor拦截器类
     * @author BIElI
     */
    public class SysInterceptor extends HandlerInterceptorAdapter {
        private Logger logger = Logger.getLogger(SysInterceptor.class);

        @Override
        public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception{
            logger.debug("SysInterceptor preHandle ==========================");
            //获取Session对象
            HttpSession session = request.getSession();
            //判断Session中是否存在用户登录信息
            User user = (User) session.getAttribute(Constants.USER_SESSION);
            if (null == user){
                response.sendRedirect(request.getContextPath() + "/401.jsp");
                return false;
            }
            return true;
        }
    }

```

### pojo包 实体类包

#### User实体类

```java
	
	public class User {
        private Integer id; //id
        @NotNull(message = "用户编码不能为空")
        @NotEmpty(message = "用户编码不能为空格")
        private String userCode; //用户编码
        @NotNull(message = "名称不能为空")
        @NotEmpty(message = "名称不能为空格")
        private String userName; //用户名称
        @NotNull(message = "密码不能为空")
        @NotEmpty(message = "密码不能为空格")
        private String userPassword; //用户密码
        private Integer gender;  //性别
        @DateTimeFormat(pattern = "yyyy-MM-dd")
        private Date birthday;  //出生日期
        @NotNull(message = "电话不能为空")
        @NotEmpty(message = "电话不能为空格")
        private String phone;   //电话
        private String address; //地址
        private Integer userRole;    //用户角色
        private Integer createdBy;   //创建者
        private Date creationDate; //创建时间
        private Integer modifyBy;     //更新者
        private Date modifyDate;   //更新时间
        private String idPicPath; //储存上传证件照片的路径
        private String workPicPath; //储存上传工作证照片的路径
        private Integer age; //年龄

        private String userRoleName;    //用户角色名称

        public String getUserRoleName() {
            return userRoleName;
        }
        public void setUserRoleName(String userRoleName) {
            this.userRoleName = userRoleName;
        }
        public Integer getAge() {
            /*long time = System.currentTimeMillis()-birthday.getTime();
            Integer age = Long.valueOf(time/365/24/60/60/1000).IntegerValue();*/
            Date date = new Date();
            Integer age = date.getYear()-birthday.getYear();
            return age;
        }
		//省略其它getter setter方法
}

```

### service业务逻辑包

#### UserService业务逻辑接口

```java
	
	/**
     * @author BIElI
     */
    public interface UserService {
    		/**
             * 通过用户id获取用户信息
             * @param id 用户id
             * @return user 用户对象信息
             * @throws Exception -
             */
            public User getUserById(String id) throws Exception;
    }
	
```

#### UserServiceImpl业务逻辑接口实现类

```java
	
	/**
     * @author BIElI
     */
    @Service("userService")
    public class UserServiceImpl implements UserService{
        /**
         * 从Spring获取UserMapper接口实例
         */
        @Autowired
        private UserMapper userMapper;
	
	   /**
         * 通过用户id获取用户信息
         * @param id 用户id
         * @return user 用户对象信息
         * @throws Exception -
         */
        @Override
        public User getUserById(String id) throws Exception {
            return userMapper.getUserById(id);
        }	
	}
	
```

### Constants常量工具类

```
	
	public class Constants {
        public final static String USER_SESSION = "userSession";
        public final static String SYS_MESSAGE = "message";
        public final static int pageSize = 5;
    }
	
```


