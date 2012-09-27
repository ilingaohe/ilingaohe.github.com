---
layout: post
title: "iOS Thread学习"
category: 学习笔记
tags: [iOS Thread]
---
{% include JB/setup %}

## 学习目的
多线程是应用程序编程中很重要的一项方式，正确的多线程编程方式可以很好的提高程序的性能，但是多线程编程又是很容易产生错误的地方，因此在iOS平台上，从底层到上层，系统提供了多种实现多线程的方式，需要和值得进行深入的学习。
## 具体内容
iOS支持多个层次的多线程编程方式，有NSThread，NSOperation和GCD等。NSThread是较底层的多线程方式，NSOperation和GCD是较高层次的方式。

### NSThread

#### 产生NSThread的方式
NSThread层级的启动一个线程的方式有三种，两种直接的方式

1.创建方式一：

	[NSThread detachNewThreadSelector:@selector(threadMainMethod:) toTarget:self withObject:nil];		

2.创建方式二：
	
	NSThread *thread = [[NSThread alloc] initWithTarget:self selector:@selector(threadMainMethod:) object:nil];
	[thread start];
	
这两种方式的区别为，第一种方式直接就创建一个线程并执行，第二种方式为先创建一个线程，获得这个线程，然后可以设置这个线程的属性，并且在调用`start`方法的时候才会开始执行这个线程。

还有一种间接创建并执行线程的方法，使用NSObject的对象方法：

3.创建方式三：

		[myObj performSeletorInBackground:@selector(threadMainMethod:) withObject:nil];
	
这个方式创建的线程和NSThread的`detachNewThreadSelector:toTarget:withObject`效果是一样的。		


#### 线程方法的写法

在线程方法中，建议添加NSAutoreleasePool自动释放池，

	(void)threadMainMethod
	{
		NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
		//to do something in the thread job
		
		//
		[pool release];
	}
	
#### NSThread线程间通信

iOS的线程间有多种通信方式，其中一种是使用NSObject中的`performSelectorxxx`相关方法。

比如通知到主线程中处理事情：

	-performSelectorOnMainThread:withObject:waitUntilDone:
	-performSelectorOnMainThread:withObject:waitUntilDone:modes:
	
通知在其他线程中处理事情：

	-performSelector:onThread:withObject:waitUntilDone:	-performSelector:onThread:withObject:waitUntilDone:modes
	
通知在当前线程中处理事情：

	-performSelector:withObject:afterDelay:
	-performSelector:withObject:afterDelay:inModes:		
取消发送给点当前线程的消息：

	+cancelPreviousPerformRequestsWithTarget:
	+cancelPreviousPerformRequestsWithTarget:selector:object:

 
  