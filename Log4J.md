```
	2019年5月10日16:43:42创建
```

# 目录



[TOC]

# Log4J

## 使用Log4J前置操作

```
	
	在idea中导入Log4j的jar包 在模块设置中导入并打勾
	log4j配置文件 必须在src目录下
	
	使用方法创建对象
	
	private static Logger logger = Logger.getLogger(类名.class.getName());
	logger.info(">>>程序开始运行...");
	logger.debug("日志记录结果......");
	logger.error("出现错误!");
	
```

## 配置文件 (log4j.properties)

```properties
	
	配置文件名字无所谓 但最好还是用log4j便于分别
	log4j.appender.logfile.File= 这行写输出路径 可自定义 结尾为文档后缀和名字
	
	
	### 设置Logger 输出级别和输出目的地 ###
	log4j.rootLogger=debug,console,logfile

	###日志记录级别fatal严重错误>>error错误>>warn警告>>info提示>>debug调试

	###定义控制台日志信息记录格式###
	log4j.appender.console=org.apache.log4j.ConsoleAppender
	log4j.appender.console.Target=System.err
	log4j.appender.console.layout=org.apache.log4j.SimpleLayout

	###定义文件日志信息记录格式###
	log4j.appender.logfile=org.apache.log4j.FileAppender
	log4j.appender.logfile.File=logname.log
    log4j.appender.logfile.layout=org.apache.log4j.PatternLayout
    log4j.appender.logfile.layout.ConversionPattern=%d{yyyy-MM-dd HH:mm:ss} %l %F %p %m%n
	
```

