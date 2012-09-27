---
layout: post
title: "iOS6的自动旋转控制"
caterogy: 开发经验
tags: [iOS Autorotate]
---
{% include JB/setup %}

## 学习目的
iOS可以对屏幕的4个方向进行自动旋转控制，但是最新的iOS6和之前的版本对自动旋转的控制实现方式有所区别，因此记录一下。
## 具体内容
### iOS6之前的自动旋转处理
iOS6之前，单个页面的旋转，通过

	- (BOOL)shouldAutorotateToInterfaceOrientation:(UIInterfaceOrientation)interfaceOrientation

这个方法来控制这个页面支持哪个方向的自动旋转。

并且如果是视图容器类的话，比如UITabBarController和UINavigationController，他们的旋转和其所有子视图类的旋转相关，即只有当容器内所有子视图类都支持旋转的话，整个容器类才支持旋转，否则就不能旋转。

### iOS6的自动旋转处理

iOS6中，对旋转的处理进行了改变，增加了旋转控制配置进行变化处理的能力。

首选需要在info.plist中或者delegate的`- (NSUInteger)supportedInterfaceOrientationsForWindow:(UIWindow *)window`方法中设置可以支持的旋转方向，如果在这两个地方没有设置支持的旋转方向，那在应用中的任何页面也都不会支持旋转。

然后增加了两个新的方法，`- (BOOL)shouldAutorotate`和`- (NSUInteger)supportedInterfaceOrientations`，第一个方法控制这个页面的能否旋转，返回`YES`表示支持旋转，`NO`不支持旋转。第二个方法表示这个页面具体支持的旋转方向，返回的方向必须是在info.plist或者delegate中设置的旋转方向集合的子集。

最后的区别是，在iOS6中，比如UITabBarController和UINavigationController的容器类，不再依赖与其子视图类的旋转控制，而是自己可以直接控制旋转。
因此在实际使用中，可以为这两个类增加类别，把旋转控制和iOS6之前的版本一样，依赖于其子视图类，或者当前选择的子视图类。

UITabBarController的类别扩展：

.h文件为：

	//UITabBarController+Autorotate.h
	#import <UIKit/UIKit.h>

	@interface UITabBarController (Autorotate)
	@end
	
	
.m文件为：	

	//UITabBarController+Autorotate.m
	#import "UITabBarController+Autorotate.h"

	@implementation UITabBarController (Autorotate)
	- (BOOL)shouldAutorotate {
		BOOL rotatable = [self.selectedViewController shouldAutorotate];
		return rotatable;
	}
	
	- (NSUInteger)supportedInterfaceOrientations {
		return [self.selectedViewController supportedInterfaceOrientations];
		}
	@end
	
UINavigationController的类别扩展：

.h文件：

	//UINavigationController+Autorotate.h
	#import <UIKit/UIKit.h>

	@interface UINavigationController (Autorotate)
	@end	
	

.m文件：

	//UINavigationController+Autorotate.m
	#import "UINavigationController+Autorotate.h"

	@implementation UINavigationController (Autorotate)
	- (BOOL)shouldAutorotate {
		BOOL rotatable = [self.visibleViewController shouldAutorotate];
		return rotatable;
	}

	- (NSUInteger)supportedInterfaceOrientations {
		return [self.visibleViewController supportedInterfaceOrientations];
	}
	@end	
	
	