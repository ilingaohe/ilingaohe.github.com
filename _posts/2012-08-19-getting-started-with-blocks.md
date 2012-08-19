---
layout: post
title: "iOS的Block学习"
category: 学习笔记
tags: [iOS Block]
---
{% include JB/setup %}

## 学习目的
iOS中Objective-C提供的Block功能，能够方便的实现函数的回调及GCD功能，因此需要学习了解和深入的理解。

## 具体内容
之前通过看苹果的文档，对Block的基本使用已经有所了解，并且已经在代码中采用block实现更方便的函数回调。现在在看[《Pro Multithreading and Memory Management￼for iOS and OS X》](http://www.amazon.com/Pro-Multithreading-Memory-Management-iOS/dp/1430241160)，看完书中的Block部分的介绍，对iOS的Block有了进一步的认识和深入的理解。本篇先对Block做个简单的了解，之后再做个深入的理解。

### Block的认识
Blocks是Objective-C对C语言的扩展，用一句话来解释Blocks就是“捕获局部变量的匿名函数”，即（1）Blocks是一个匿名函数，（2）Blocks可以带有局部变量。

#### 匿名函数
在标准的C和Objective-C中，如果不借用Blocks是没法定义匿名函数（没有名字的函数）的，在C++11中引入了lambda从而才可以定义匿名函数。
Objective-C使用Blocks来实现可以定义匿名函数。

#### 捕获局部变量
在C语言中，使用到变量有：

* 局部变量
* 函数参数
* 局部静态变量
* 全局静态变量
* 全局变量

在标准的C语言中，如果要在一个函数中使用不是函数参数列表中传进来的外部变量，那这个变量得是全局变量（静态或非静态），没法使用定义范围内的局部变量。而使用Blocks，可以在函数体内捕获并使用局部变量。

“捕获局部变量的匿名函数”概念也叫“闭包”或者“lambda算子”。


### Block的语法
block的定义和函数的定义形式很像：

函数的定义例子：

	void func(int arg){
		printf("%d",arg);
	}

则定义一个对应的block为：

	^void (int arg){
		printf("%d",arg);
	}
	
通过比较可以看到，block和函数的定义只有两处区别：（1）匿名的，没有函数名，（2）返回类型前多了一个^符号。

Block的语法为：

`^` `返回类型` `(参数列表)` `{实现体}`

其中返回类型，参数列表及定义体和实现体语法中的概念都是一样的。
如果`返回类型`和`函数体`中通过`return`返回的内容的类型一样的话，那`返回类型`可以省略。

即没有返回值或者返回值由`return`指定的Block的语法可以简化为：

`^` `(参数列表)` `{实现体}`

如果Block没有参数，则还可以省略`(参数列表)`：

`^` `{实现体}`

### Block类型的变量
我们知道函数可以赋值给函数指针类型的变量，和函数类似的Block也可以赋值给Block类型的变量。
先来看下函数指针类型变量的定义，如果有一个函数：

	int func(int count){
		return count + １;
	}	
	
则可以定义对应的函数指针：

	int (*funcptr)(int);   //定义函数指针变量
	funcptr = func;        //为函数指针变量赋值

而Block变量的定义和函数指针的定义类似，只是把`*`改为了`^`，
比如：

	int (^blk)(int);	//定义Block变量

有了Block变量的定义之后，就可以为其赋值：

	int (^blk)(int) = ^(int count){
		return count + 1;
	};
Block变量的使用上和其他变量一样。	
和函数指针的调用类似：

	int result = (*funcprt)(10);
		
Block的调用为：

	int result = (^blk)(10);
	
### 捕获局部变量
前面说到，Block有可以看成有两种特点，第一种是前面说到的匿名函数，第二种就是能够捕获局部变量。
看一个实际的代码例子：
	
	int main(){
		int val = 10;
		const char *fmt = "val = %d\n";
		void (^blk)(void) = ^{
			printf(fmt, val);
		};
		
		val = 20;
		fmt = "The value was changed, val = %d\n";
		
		blk();
		
		return 0;
	}	
	
在上面的示例代码中，我们定义了两个局部变量，val和fmt，并且在blk这个Block中用到了，因为Block能够捕获局部变量，所以用到的这两个局部变量会被保存在Block块中。因为当前的局部变量被捕获并且保存，因此即使后面对这些变量进行了改变，当blk这个Block块执行的时候，里面的局部变量值依旧是捕获时的值，因此上面示例代码的输出为：

	val = 10
	
而不会输出:`The value was changed, val = 2`。

### __block修饰符

当局部变量在Block块中被捕获时，这些值在Block块中是只读属性的，因此不能被修改。如果需要在Block块中修改局部变量，需要在局部变量声明的时候__block修饰符。被__block修饰的变量也叫__block变量。

## 后续学习
以上部分只是简单的介绍了Block的基本语法和基本使用，之后我们再深入学下一下Block的具体实现方式。 

		