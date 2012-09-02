---
layout: post
title: "iOS的单元测试学习"
category: 学习笔记
tags: [iOS UnitTest]
---
{% include JB/setup %}

## 学习目的
单元测试是程序员自己确认代码正确性的一种有效方式，因此我们需要学习一下XCode自带的单元测试框架和另一个叫做GHUnit的开源iOS单元测试框架。

## 具体内容

### XCode自带的单元测试框架
#### 添加测试框架
XCode开发环境中自带了单元测试框架，有两种方式在程序中使用自带的单元测试框架：

1.第一种是在创建新工程的时候就勾选"include Unit Tests"，比如创建的工程名为"UnitTestDemoOne"，则XCode会自动为你创建一个命名为"UnitTestDemoOneTests"的Target和对应的工程文件。

2.第二种方式是在已有的工程中添加单元测试功能，"File"->"New"->"Target"添加一个新的测试Target，在弹出的选择Target模板中选择iOS类中"Other"里的"Cocoa Touch Unit Testing Bundle"，然后起一个名称即完成添加。

#### 使用测试框架
添加完测试的Target后，选中工程后在XCode的“Targets”栏中，可以看到两个Target，一个是主程序的Target，另一个是测试程序的Target，可以分别对他们进行配置，比如"Building Settings","Building Phases"中的选项。

##### 添加需要测试的文件
要在测试程序中测试主程序的代码，首先需要在测试程序的Target中能够编译进主程序需要测试的代码，也有两种方式：

1.第一种是在New这个代码文件的时候同时勾选测试的Target。

2.第二种是在测试Target的"Build Phases"中的"Compile Sources"中手动添加选择需要包含的这个代码。

其他的需要依赖的工程，静态库或者资源文件的添加方式类似。

然后就可以测试编写测试方法了，比如主程序中有个`printHelloWorld()`方法在`UnitTestCode`文件中需要测试：

		//UnitTestCode.h文件
		#import <Foundation/Foundation.h>
		@interface UnitTestCode : NSObject
		- (void)printHelloWorld;
		@end
	
		//UnitTestCode.m文件
		#import "UnitTestCode.h"
		@implementation UnitTestCode
		- (void)printHelloWorld
		{
			NSLog(@"Hello World");
		}
		@end

##### 编写测试代码 
在Test文件中包含需要测试的主程序代码对应的头文件，比如这里的`UnitTestCode.h`，然后写一个以`test`开头的测试方法，比如：

	- (void)testUnitTestCode
	{
		UnitTestCode *testCode = [[UnitTestCode alloc] init];
		[testCode printHelloWorld];
		[testCode release];
	}

##### 执行测试代码
首先看工程的Scheme中有没有测试Target对应的那个Scheme，如果还没的话，新建一个Scheme，选择测试的那个Target。
然后选择测试的这个Scheme，按Command+U就可以执行测试的代码了。
在Output中会输出测试的结果。

#### 测试框架功能的学习
接下来来简单学习一下苹果自己提供的测试框架，叫做SenTestingKit，使用的时候需要包含SenTestingKit.framework，并且创建的测试文件都需要继承SenTestCase这个基类。

Test的方法的写法为：

	- (void)testSomething
	{
		//具体的测试代码
	}	
即要求没有返回值，也没有参数，需要以`test`开头。

并且提供了一系列以`STAssert`开头的断言方法。

以上简单的介绍了下苹果自带的测试框架SenTestingKit，因为集成在了XCode开发工具中，所以使用起来很方便。但是也有一些缺点：比如只要Command+U执行那就是执行全部的测试方法，没法一个一个的执行测试方法；因为SenTestingKit产生的Target是没有UI界面的，所以也不好测试UI界面相关的功能。

因为有以上这些的不足，所以出现了一些iOS上的开源测试框架，比如GHUnit就是其中最有名的一个，下面来简单的学习一下。


### GHUnit开源iOS测试框架 	
	
[GHUnit](https://github.com/gabriel/gh-unit)是一个开源的Objective-C测试框架，可以一个一个执行测试的方法。下面就来学习一下GHUnit的使用。

####添加测试框架
因为GHUnit不是XCode集成的，所以相对SenTestKit来说，只能使用类似第二种添加方法添加。
"File"->"New"->"Target"->"iOS"->"Application"->"Empty Application"添加一个空的应用。
然后下载[GHUnitIOS.framework](https://github.com/gabriel/gh-unit/downloads)，在Target配置的`Build Phases`中的`Link Binary With Libraries`中添加刚才下载并解压出来的GHUnitIOS.framework。在`Build Settings`->`Linking`->`Other Linker Flags`添加`-ObjC`和`-all_load`。

因为GHUnit框架提供了自己的Delegete，所以对刚才创建的Empty Application自动产生的Delegete文件有两种处理方式：

1.第一种是删除自动产生的Delegate文件，并且到`Supporting Files`下的`main.m`文件中修改为:

	#import <UIKit/UIKit.h>
	int main(int argc, char *argv[])
	{
		@autoreleasepool {
    		return UIApplicationMain(argc, argv, nil, 			@"GHUnitIOSAppDelegate"));
    	}
    }

表示直接使用了GHUnit提供的GHUnitIOSAppDelegate。如果需要在Delegate中进行一些设置，则可以自己创建一个继承自GHUnitIOSAppDelegate的自定义Delegate。即为下面的第二种方式。

2.第二种方式为不删除Delegate文件，但是需要修改为继承GHUnitIOSAppDelegate，比如修改后的Delegate文件为：

	//AppDelegate.h文件
	#import <UIKit/UIKit.h>
	#import <GHUnitIOS/GHUnit.h>
	@interface AppDelegate : GHUnitIOSAppDelegate
	@end

	//AppDelegate.m文件
	#import "AppDelegate.h"
	@implementation AppDelegate
	- (void)dealloc
	{
    	[super dealloc];
	}
	@end

然后就可以在AppDelegate中添加其他需要在启动的时候先做的事情了。

#### 使用测试框架
GHUnit测试框架的时候是和SenTestingKit一样的，选择对应的Scheme，不过因为创建的是属于Applicaiton，而不是Test，所以运行是Command+R。
上一个步骤只添加测试框架，还没有添加测试方法，此时运行的效果为：

![GHUnit空测试方法时的运行效果](http://gabriel.github.com/gh-unit/docs/appledoc_include/images/12_running.png)

图-1 GHUnit空测试方法时的运行效果

与SenTestingKit不同的是，GHUnit的测试类要包含的头文件为：`#import <GHUnitIOS/GHUnit.h>`，并且要继承自`GHTestCase`，并且断言的方法也都是以`GHAssert`开头。
不过测试方法的命名还是类似，需要以`test`开头。


## 后续学习
以上部分只是简单的介绍了iOS测试框架的添加和使用，之后再深入学习测试用例的写法及自动化测试的实施方式。