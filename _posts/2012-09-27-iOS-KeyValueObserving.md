---
layout: post
title: "iOS KeyValueObserving学习"
caterogy: 学习笔记
tags: [iOS KeyValueObserving]
---
{% include JB/setup %}

## 学习目的
KVO是一种监控感兴趣的对象属性变化的方法，使用KVO可以简化代码的编写。
## 具体内容
为了使用KVO机制，首先对象需要实现KVC协议。
如果在A对象中为了监控B对象中bb属性的变化，则在A对象里为B对象的实例设置监听变化，

	[B实例 addObserver:self forKeyPath:@"bb" options:NSKeyValueObservingOptionNew context:nil];
	
然后在A对象里实现监听变化的回调方法：

	- (void) observeValueForKeyPath:(NSString)keyPath ofObject:(id)object change:(NSDictionary *)change context:(void *)context
	{
		//在这里获取变化
	}	
	
	