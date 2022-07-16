```
	2019年12月2日14:57:11创建
```

# 目录

[TOC]

# SpringBoot

## 为什么学习SpringBoot

```
	
	简单开发模式解放出更多的生产力
	技术栈集成了几乎各个互联网公司在使用的技术
	和微服务架构一起 是未来软件开发的大趋势
	
```

## SpringBoot 简介

```
	
	简化Spring应用开发的一个框架
	整个Spring技术栈的一个大整合
	J2EE开发的一站式解决方案
	低侵入式设计 独立于各种应用服务器
	IOC容器实现各组件之间的松耦合
	AOP提供通用任务的复用性
	框架开放性
	
```

## SpringBoot 主要特性

```
	
	约定优先于配置 很少配置即可构建一个项目
	简化Maven配置 自动化配置 开箱即用
	可以独立运行Spring项目
	内嵌Servlet容器 如Tomcat jetty
	纯Java注解配置方式 支持热启动
	自动管理依赖
	自动整合第三方框架
	自带准生产应用监控（在测试阶段可以观察生产阶段的数据）
	与Spring Cloud微服务无缝结合
	
```

## 微服务

```
	
	是一种架构风格 
	一个应用应该是一组小型服务 可以通过HTTP的方式 进行互通
	每一个小型服务最终都是一个可独立替换和独立开发升级的软件单元
	
```







```

Maven项目坐标scope元素不同值含义

compile：默认的scope。任何定义在compile scope下的依赖将会在所有的class paths下可用。maven工程会将其打包到最终的artifact中。

provided：假定对应的依赖会由运行这个应用的JDK或者容器来提供。最好的例子就是servlet API。任何在provided scope下定义的依赖在构建时的类路径里是可用的，但是不会被打包到最终的artifact中。

runtime：定义的依赖只会在运行期可用，而在构建期的类路径下不可用。这些依赖将会被打包到最终的artifact中。比如一个web应用需要在运行时访问MySQL数据库。代码仅仅是基于JDBC API来编写，在构建期并不需要MySQL数据库驱动。而在运行期需要相应的驱动来操作MySQL数据库。

test：只用于测试编译的依赖（比如JUnit），execution必须定义在test scope下。这些依赖不会被打包到最终的artifact中。

```

# SpringBoot整合poi导入导出excel

## POI概述

```
	
	Apache POI是Apache软件基金会的开放源码函式库 POI提供API给Java程序对Microsoft Office格式档案读和写的功能
	
	   结构
        HSSF － 提供读写Microsoft Excel格式档案的功能  HSSF是指2007年以前的
        XSSF － 提供读写Microsoft Excel OOXML格式档案的功能  XSSF是指2007年版本以上的
        HWPF － 提供读写Microsoft Word格式档案的功能
        HSLF － 提供读写Microsoft PowerPoint格式档案的功能
        HDGF － 提供读写Microsoft Visio格式档案的功能
	
	HSSF 是Horrible SpreadSheet Format的缩写 通过HSSF  可以用纯Java代码来读取、写入、修改Excel文件 HSSF 为读取操作提供了两类API usermodel和eventusermodel 即 用户模型 和 事件-用户模型 
	
```

## POI的文档结构类

```
	
    HSSFWorkbook excel文档对象
    HSSFSheet excel的sheet
    HSSFRow excel的行
    HSSFCell excel的单元格
    HSSFFont excel字体
    HSSFName 名称
    HSSFDataFormat 日期格式
    HSSFHeader sheet头
    HSSFFooter sheet尾
    HSSFCellStyle cell样式
    HSSFDateUtil 日期
    HSSFPrintSetup 打印
    HSSFErrorConstants 错误信息表
	
```

## 使用SpringBoot+Poi进行Excel导入

```xml
	
	引入Maven poi依赖
		
		<dependency>
          <groupId>org.apache.poi</groupId>
          <artifactId>poi-ooxml</artifactId>
          <version>3.17</version>
        </dependency>
        <dependency>
          <groupId>org.apache.poi</groupId>
          <artifactId>poi-ooxml-schemas</artifactId>
          <version>3.17</version>
        </dependency>
        <dependency>
          <groupId>org.apache.poi</groupId>
          <artifactId>poi</artifactId>
          <version>3.17</version>
        </dependency>

```

```

	代码编写 注意根据实际情况

		创建相关的实体类 这里举例 属性有 姓名、班级、年龄、性别 可以附带一个toStirng()方法方便输出测试
		创建一个控制器层
			存放导入的处理器 也就是方法
		    @RequestMapping("/import")
   		    @ResponseBody
			public String importExcelHandler(){
				//用于储存 学生信息集合
       			 ArrayList<Student> studentArrayList = new ArrayList<Student>();
                 //输出字节流对象
                 InputStream inputStream = null;
                 try {
                    //获取文件字节输出流
                    inputStream = new FileInputStream("B:\\ProgrammingProjects\\IdeaWorkSpace\\W4\\src\\main\\java\\com\\twoa\\excel\\学生信息表.xlsx");
                    //获取Excel工作薄对象
                    XSSFWorkbook workbook = new XSSFWorkbook(inputStream);
                    //得到Excel工作表对象
                    XSSFSheet sheet = workbook.getSheetAt(0);
                    //循环读取表格数据
                    for (Row row : sheet){
                        //首行(即表头) 不读取
                        if (row.getRowNum() == 0) {
                            System.out.print("  " + row.getCell(0).getStringCellValue());
                            System.out.print("  " + row.getCell(1).getStringCellValue());
                            System.out.print("  " + row.getCell(2).getStringCellValue());
                            System.out.println("  " + row.getCell(3).getStringCellValue());
                            continue;
                        }
                        //设置数值列 取值的类型
                        row.getCell(2).setCellType(XSSFCell.CELL_TYPE_STRING);
                        //读取当前行中 单元格数据 索引从0开始
                        Student student = new Student();
                        student.setName(row.getCell(0).getStringCellValue());
                        student.setClassName(row.getCell(1).getStringCellValue());
        //                student.setAge((int) row.getCell(2).getNumericCellValue()); 不进行取值类型转换也可以 使用这样的方法
                        student.setAge(Integer.parseInt(row.getCell(2).getStringCellValue()));
                        student.setGender(row.getCell(3).getStringCellValue());
                        //输出控制台测试
                        System.out.println(student.toString());
                        //将所有学生对象 装载入集合当中
                        studentArrayList.add(student);
                    }
                }catch (FileNotFoundException e) {
                    //文件未找到异常
                    e.printStackTrace();
                } catch (IOException e) {
                    //IO异常
                    e.printStackTrace();
                }finally {
                    //关闭字节输出流
                    try {
                        inputStream.close();
                    } catch (IOException e) {
                        e.printStackTrace();
                    }
                } 
                return "导入成功";
			}
			
```

## 使用SpringBoot+Poi进行Excel导出

```xml
	
	引入Maven poi依赖

		<dependency>
          <groupId>org.apache.poi</groupId>
          <artifactId>poi-ooxml</artifactId>
          <version>3.17</version>
        </dependency>
        <dependency>
          <groupId>org.apache.poi</groupId>
          <artifactId>poi-ooxml-schemas</artifactId>
          <version>3.17</version>
        </dependency>
        <dependency>
          <groupId>org.apache.poi</groupId>
          <artifactId>poi</artifactId>
          <version>3.17</version>
        </dependency>
      
```

```
	
	代码编写 注意根据实际情况
	
		@RequestMapping("/export")
        @ResponseBody
        public String exportExcelHandler(HttpServletResponse response){
            //创建XSSFWorkbook对象
            XSSFWorkbook workbook = new XSSFWorkbook();
            //建立sheet对象
            XSSFSheet sheet = workbook.createSheet("学生表");
            //在sheet里创建第一行 参数为行索引
            XSSFRow row1 = sheet.createRow(0);
            //创建单元格
            XSSFCell cell = row1.createCell(0);
            //设置单元格内容
            cell.setCellValue("学生信息表");
            //合并单元格CellRangeAddress构造参数依次表示起始行 截至行 起始列 截至列
            sheet.addMergedRegion(new CellRangeAddress(0,0,0,3));
            //在sheet例创建第二行
            XSSFRow row2 = sheet.createRow(1);
            //创建单元格并设置单元格内容
            row2.createCell(0).setCellValue("姓名");
            row2.createCell(1).setCellValue("年龄");
            row2.createCell(2).setCellValue("性别");
            //在sheet例创建第三行
            XSSFRow row3 = sheet.createRow(2);
            //创建单元格并设置单元格内容
            row3.createCell(0).setCellValue("A");
            row3.createCell(1).setCellValue("20");
            row3.createCell(2).setCellValue("女");
            //在sheet例创建第四行
            XSSFRow row4 = sheet.createRow(3);
            //创建单元格并设置单元格内容
            row4.createCell(0).setCellValue("B");
            row4.createCell(1).setCellValue("20");
            row4.createCell(2).setCellValue("男");
            //输出Excel文件
            try {
                OutputStream outputStream = response.getOutputStream();
                response.reset();
                //设置响应头
                response.setHeader("Content-disposition", "attachment;filename=Student.xls");
                response.setContentType("application/msexcel");
                workbook.write(outputStream);
                outputStream.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
            return "导出成功";
        }
        
```



















