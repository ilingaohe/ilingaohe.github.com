---
layout: post
title: "学习Markdown"
category: 学习笔记
tags: [markdown]
---
{% include JB/setup %}


## 学习目的

markdown语法使用的学习与提高

## 学习工具

markdown是纯文本，所以可以使用任何的文本编辑器，不过为了提高编辑的效率，建议使用一款markdwon的编辑器，Mac OS X下我使用的是[Mou](http://mouapp.com/)

![Mou_Screenshot](http://mouapp.com/images/Mou_Screenshot_1.png)

## 语法学习

以下内容，主要根据Mou的帮助文档整理，以后根据实际用到的经验，陆续添加更新。

### 强调

使用两个`**`或者两个`__`包围内容表示加粗强调
使用一个`*`或者一个`_`包围内容表示倾斜强调

#### Markdown写法

	**加粗强调**
	
	__倾斜强调__
	
	**
	也可以嵌套使用，比如整个加粗，
	并且里面的_内容_这两个字进行倾斜
	**
	
#### 实际显示效果

**加粗强调**

__倾斜强调__
	
**也可以嵌套使用，比如整个加粗，
并且里面的_内容_这两个字进行倾斜**

### 块引用

内容以右角尖括号>开始的话则显示的是进行整块的引用

#### Markdown写法

	内容以右角尖括号>开始的话则显示的是进行整块的引用
	
#### 实际显示效果

>内容以右角尖括号>开始的话则显示的是进行整块的引用

### 链接与邮箱

邮箱只要用`<>`括起来就可以

#### Markdown写法
	
	<ilingaohe@gmail.com>
	
#### 实际显示效果

<ilingaohe@gmail.com>


链接有4种方式：

1.直接使用`<>`括起来即可

2.使用`[链接文字](链接地址)`的方式

3.使用`[链接文字](链接地址 "链接说明文字")`的方式

4.使用`[链接文字][链接id]`，而`链接id`可以在文章的任何地方给出，形式为`[链接id]:链接地址 "链接说明文字"`

#### Markdown写法

	1.<http://ilingaohe.github.com>
	2.[我的博客](http://ilingaohe.github.com)
	3.[我的博客](http://ilingaohe.github.com "ilingaohe的博客")
	4.[我的博客][id]
	  [id]:http://ilingaohe.github.com "ilingaohe的博客"
	  
#### 实际显示效果

1.<http://ilingaohe.github.com>

2.[我的博客](http://ilingaohe.github.com)

3.[我的博客](http://ilingaohe.github.com "ilingaohe的博客")

4.[我的博客][id]
[id]:http://ilingaohe.github.com "ilingaohe的博客"

### 图片添加

和文字链接类似，图片添加也有两种方式:

1.使用`![图片名字](图片链接地址 "图片标题文字")`的方式,标题文字可选

2.使用`![图片名字][链接id]`的方式，而`链接id`和上面提到过的使用方式一样，可以在文章的任何地方给出，形式为`[链接id]:链接地址 "链接说明文字"`，链接说明文字可选

#### Markdown写法

	1.![Mou icon](http://mouapp.com/Mou_128.png)
	2.![Mou icon][id_2]
	   [id_2]: http://mouapp.com/Mou_128.png 
	   
#### 实际显示效果

1.![Mou icon](http://mouapp.com/Mou_128.png)

2.![Mou icon][id_2]
[id_2]: http://mouapp.com/Mou_128.png 

### 行内代码及代码块

行内代码标注和代码块前面我们已经有用到了，行内代码的话用``(Esc按键下面那个)符号包围，代码块的话每行使用1个Tab或者4个空格。

#### Markdown写法

	行内代码的例子，`NSString *name = @"ilingaohe";`
	
	//代码块的例子
	NSString *name = @"ilingaohe";
	NSLog(@"Name:%@",name);
	
#### 实际显示效果

行内代码的例子，`NSString *name = @"ilingaohe";`

代码块的例子：
	
	//代码块的例子
	NSString *name = @"ilingaohe";
	NSLog(@"Name:%@",name);
	
### 列表

有序列表使用类似"1."+空格的方式
无序列表使用类似"*"或者"-"+空格的方式
 
#### Markdown写法

	有序列表
	1. 第一条
	2. 第二条
	3. 第三条 
	
	无序列表
	* Java
	* C
	* Objectiv-C
	
	- C++
	- Ruby
	- Javascript 
	
#### 实际显示效果

有序列表

1. 第一条
2. 第二条
3. 第三条 

无序列表

* Java
* C
* Objectiv-C

- C++
- Ruby
- Javascript 

### 换行

在一行的结尾添加大于等于两个的空格才可以实际换行

#### Markdown写法

	第一行（后面还添加了两个空格）  
	第二行
	
#### 实际显示效果

第一行（后面还添加了两个空格）  
第二行

### 水平线

使用3个及以上的星号及虚线能够产生一条水平线

#### Markdown写法

	***  
	---  
	- - - 
	
#### 实际显示效果

***  
---  
- - - 

### 标题

标题有两种类型风格，Setext风格和atx风格

#### Markdown写法

	//Setext风格
	标题1  
	=====  
	标题2  
	-----
	
	//atx风格
	#标题1  
	##标题2  
	###标题3  
	####标题4 
	#####标题5  
	######标题6 
	
#### 实际显示效果

//Setext风格
   
标题1  
====
 
标题2  
----
	

//atx风格
#标题1  
##标题2  
###标题3  
####标题4 
#####标题5  
######标题6 

### 错误更正

使用两个`~~`(都是Esc下面的按键)波浪号可以显示错误更正的效果

#### Markdown写法

	~~错误内容~~
	
#### 实际显示效果

~~错误内容~~

### 包围代码快

以三个及以上的反引号` `` `（还是Esc下面的按键）开始一行，并且在结尾的时候使用和开头一样多的反引号作为结尾行，可以包围一个代码块

#### Markdown写法
	
	```
	代码块开始部分
	代码块正文部分
	代码块结尾部分
	```
	
#### 实际显示效果

```  
代码块开始部分
代码块正文部分
代码块结尾部分
```

### 表格

表格使用虚线进行划分，并且可以使用冒号`:`进行表格内容的对齐

#### Markdown写法

	//
	First Header | Second Header | Third Header
	------------ | ------------- | ------------
	Content Cell | Content Cell  | Content Cell
	Content Cell | Content Cell  | Content Cell
	
	//也可以在两边再添加虚线
	| First Header | Second Header | Third Header |
	| ------------ | ------------- | ------------ |
	| Content Cell | Content Cell  | Content Cell |
	| Content Cell | Content Cell  | Content Cell |
	
	//使用:号进行表格内容的对齐
	First Header | Second Header | Third Header
	:----------- | :-----------: | -----------:
	Left         | Center        | Right
	Left         | Center        | Right
	
#### 实际显示效果
  


First Header | Second Header | Third Header
------------ | ------------- | ------------
Content Cell | Content Cell  | Content Cell
Content Cell | Content Cell  | Content Cell  

  

| First Header | Second Header | Third Header |
| ------------ | ------------- | ------------ |
| Content Cell | Content Cell  | Content Cell |
| Content Cell | Content Cell  | Content Cell |


First Header | Second Header | Third Header
:----------- | :-----------: | -----------:
Left         | Center        | Right
Left         | Center        | Right


## 其他资料
1. [Markdown 语法说明 (简体中文版)](http://wowubuntu.com/markdown/)
2. [Markdown语法](http://www.ituring.com.cn/article/775)
3. [Markdown语法简单介绍](http://sebug.net/node/t-24)
4. [MarkDown语法](http://blog.ouyang.me/2011/06/markdown语法/)