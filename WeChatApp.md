```
	2022年2月2日19:22:36创建
```

# 目录

[TOC]

# WeChatApp

## 简编词

```
	
	微信小程序 - 微
	
```

## 关于微信小程序框架

### 简介

```
	
	小程序框架 提供了自己的视图层 描述语言 WXML和WXSS以及JavaScript 并在视图层与逻辑层 提供了数据传输和事件系统 让开发者更专注于数据与逻辑
	
```

### 和传统Web相比

```
	
	传统WEB 三层结构 微 四层结构(多了json配置)
	
```

| 结构 |  传统web   | 微信小程序 |
| :--: | :--------: | :--------: |
| 结构 |    HTML    |    WXML    |
| 样式 |    CSS     |    WXSS    |
| 逻辑 | JavaScript | JavaScript |
| 配置 |     无     |    JSON    |

## 代码构成

### 文件构成

```
	
	.json 后缀的 JSON 配置文件 //静态配置数据格式
	.wxml 后缀的 WXML 模板文件
	.wxss 后缀的 WXSS 样式文件
	.js   后缀的 JS   脚本逻辑文件
	
```

#### json

##### app.json 小程序全局配置

[官方文档]: https://developers.weixin.qq.com/miniprogram/dev/reference/configuration/app.html#%E5%85%A8%E5%B1%80%E9%85%8D%E7%BD%AE

```
	
	//包含小程序所有页面路径 页面表现 网络超时时间

	{
      "pages":[
        "pages/index/index",
        "pages/logs/logs"
      ],
      "window":{
        "backgroundTextStyle":"light",
        "navigationBarBackgroundColor": "#fff",
        "navigationBarTitleText": "Weixin",
        "navigationBarTextStyle":"black"
      }
    }
	
	pages字段 //描述小程序所有页面路径 将页面名称和路径绑定
	window字段 //定义小程序 所有页面的 背景 文字
	
	
```



















































































