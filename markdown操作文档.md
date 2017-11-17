---
title: MarkDown操作文档
date: 2017-10-31 12:50:00
tags:
  - Markdown
categories: 操作文档
---
# 编写Markdown
<!-- more -->
## Markdown基本要素
### 什么是Markdown
&emsp;`markdown`是一种文本格式。你可以用它来控制文档的显示。使用 markdown，你可以创建粗体的文字，斜体的文字，添加图片，并且创建列表 等等。基本上来讲，Markdown 就是普通的文字加上`#` 或者`*`等符号。
### 语法说明
#### 标题
&emsp;\# 这是一级标题  
&emsp;\## 这是二级标题  
&emsp;\### 这是三级标题  
&emsp;\#### 这是四级标题

#### 强调
&emsp;*这是斜体字*  
&emsp;_这是斜体字_  
&emsp;**这是粗体字**  
&emsp;__这是粗体字__  
&emsp;_你也**组合**这些符号_  
&emsp;~~这个文字将被横线删除~~  

#### 列表
##### 无序列表
* Item 1
* Item 2
    * Item 2a
    * Item 2b
        * Item 2b1
        * Item 2b2
##### 有序列表
1. Item 1
1. Item 2
1. Item 3
    1. Item 3a
    1. Item 3b
  
#### 添加图片
Format: !["图片"](http://oyqcgxhz9.bkt.clouddn.com/17-11-1/12931998.jpg)

#### 链接
http://github.com - 自动生成  
[GitHub](http://github.com)

#### 引用
&emsp; 正如kanye west所说：  
>We're living the future so  
>the present is our past

#### 分割线
如下，三个或者更多的:  


-----  

连字符  

***  

星号  

___  

下划线

#### 行内代码
我觉得你应该在这里使用`<addr>`才对。  

#### 代码块
你可以在你的代码上面和下面添加 ``` 来表示代码块。
```
#include"iostream"
```

#### 语法高亮
你可以给你的代码块添加任何一种语言的语法高亮  
  
例如，给 ruby 代码添加语法高亮：
```
require 'redcarpet'
markdown=Redcarpet.new("Hello World")
puts markdown.to_html
```  
下面的代码显示代码的行号
```
function add(x,y){
    return x+y
}
```
