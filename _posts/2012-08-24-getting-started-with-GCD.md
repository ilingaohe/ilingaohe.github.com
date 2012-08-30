---
layout: post
title: "iOS的GCD学习"
category: 学习笔记
tags: [iOS GCD]
---
{% include JB/setup %}

## 学习目的
iOS的GCD是一种方便进行多线程编程的技术，学习和掌握GCD，可以更方便的编写高质量的多线程代码。

## 具体内容
这篇内容根据对[《Pro Multithreading and Memory Management￼for iOS and OS X》](http://www.amazon.com/Pro-Multithreading-Memory-Management-iOS/dp/1430241160)中GCD部分的学习而整理，做个笔记，为了更好的理解GCD。
### GCD的认识
GCD（Grand Central Dispatch）是苹果自iOS 4之后引入的帮助用户更好进行多线程编程的技术，苹果在[Concurrency Programming Guide](https://developer.apple.com/library/ios/#documentation/General/Conceptual/ConcurrencyProgrammingGuide/ConcurrencyandApplicationDesign/ConcurrencyandApplicationDesign.html)对GCD的介绍为：

One of the technologies for starting tasks asynchronously is Grand Central Dispatch (GCD). This technology takes the thread management code you would normally write in your own applications and moves that code down to the system level. All you have to do is define the tasks you want to execute and add them to an appropriate dispatch queue. GCD takes care of creating the needed threads and of scheduling your tasks to run on those threads. Because the thread management is now part of the system, GCD provides a holistic approach to task management and execution, providing better efficiency than traditional threads.

(翻译为：一种为实现异步启动任务的技术叫做GCD：Grand Central Dispatch，这种技术把原来需要程序员在应用程序中实现的线程管理部分代码移到系统级别来实现，这样留给程序员需要做的只是定义你想执行的任务，并且把他们加入到合适的分发队列中。GCD负责创建需要的线程和把你的任务调度到这些线程上。因为这些线程管理的代码已经属于系统的一部分，所以GCD能够提供一种整体的方式来进行任务的管理和执行，比传统的线程管理具有更好的效率。)

再来认识一下GCD代码的形式：

	dispatch_async(queue_for_background_threads, ^{
		/*
			这里是在后台线程执行，可以在这里执行比较费时的任务而不用阻塞界面，
			比如联网下载图片之类的。
		*/
		/*
			任务执行完毕，比如下载到了网上的图片之后，就可以在主线程进行更新界面
		*/
		dispatch_async(dispatch_get_main_queue(),^{
			/*
				这里是在主线程执行，可以进行更新界面相关的任务
			*/
		});
	});	`dispatch_async(queue_for_background_threads,^{ })`表示在后台线程中执行任务，相当于NSObject的实例方法`performSelectorInBackground:withObject`。
`dispatch_async(dispatch_get_main_queue(),^{ })`表示在主线程中执行任务，相当于NSObject的实例方法`performSelectorOnMainThread`。
即GCD只是对多线程编写实现的一种更方便的封装，可以用GCD实现的多线程方法，也可以用之前的传统多线程编写方式实现，比如以上的GCD代码可以等效为用NSObject的实例方法`performSelectorXXX`方式实现：
	/*
		使用NSObject的performSelectorInBackground:withObject方法开始一个
		在后台执行的线程	*/
	- (void)launchThreadByNSObject_performSelecorInBackground_withObject
	{	
		[self performSelectorInBackground:@selector(doWorkInBackground) withObject:nil];	}
	
	/*
		在后台线程中执行的一个方法
	*/	- (void)doWorkInBackground
	{
		NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
		/*
			这里是在后台线程执行，可以在这里执行比较费时的任务而不用阻塞界面，
			比如联网下载图片之类的。
		*/
		/*
			任务执行完毕，比如下载到了网上的图片之后，就可以在主线程进行更新界面
		*/
		[self performSelectorOnMainThread:@selector(doneWorkOnMain) withObject:nil waitUntilDone:NO];
		[pool drain];	}
	- (void)doneWorkOnMain
	{
			/*
				这里是在主线程执行，可以进行更新界面相关的任务
			*/		}

以上就是使用`performSelectorXXX`的NSObject实例方法完成的多线程执行任务的等效形式，可以看到，虽然都可以实现相同的小效果，但是GCD的方式编写出来的代码明显上代码量更加少，结构更加紧凑，更加优美。

对GCD的大概形式有个了解之后，下面来具体的学习下GCD的各个细节。

### 分发队列
GCD会维护一个分发队列，使用先进先出的方式管理添加进来需要执行的任务。
队列有两种类型，串行队列和并行队列：



串行队列的特点是一个一个执行任务，只有当前一个任务执行完了，才会执行下一个任务。
而并行队列会一次同时执行多个任务（一次执行任务的个数由系统根据当前可以调配的系统空闲资源来确定）。
即串行队列只会创建一个线程，而并行队列会创建多个线程：

![串并行队列与创建的线程数量关系](https://raw.github.com/ilingaohe/ilingaohe.github.com/master/_posts/images/2012-08-24-02.png)

图-2 串并行队列与创建的线程数量关系

下面介绍一下如何获取或者创建一个GCD的分发队列。
### 获取分发队列
GCD分发队列有两种方式获取，一种是使用`dispatch_queue_create`方法创建一个新的分发队列，另一种是直接获取系统已经提供好的`main dispatch queue`或者`global dispatch queue`。

#### dispatch_queue_create创建
使用`dispatch_queue_create`可以创建自己的串行和并行队列：
	
	//创建串行队列，第一个参数用来表示这个队列的名称，第二个参数为NULL表示是串行队列
	dispatch_queue_t mySerialDispatchQueue = dispatch_queue_create("com.ilingaohe.gcd.MySerialDispatchQueue", NULL);
	
	//第二个参数为DISPATCH_QUEUE_CONCURRENT指定创建的为并行队列
	dispatch_queue_t myConcurrentDispatchQueue = dispatch_queue_create("com.ilingaohe.gcd.MyConcurrentDispatchQueue", DISPATCH_QUEUE_CONCURRENT);
	
然后就可以使用以上创建的队列名称，传人作为`dispatch_async(队列名称，Block)`的第一个参数，表示把一个任务放在这个队列中执行。

队列也使用引用计数的内存管理方式进行管理，到使用`dispatch_queue_create`方式创建出来的队列，因为使用了`create`，默认引用计数已经加1，因此在使用完队列之后，需要使用`dispatch_release(队列名称)`方法来释放队列。

注意点：因为新建一个串行队列就会新建一个线程，	因此如果有很多任务，利用为每个任务都新建一个串行队列，然后放进去执行的方式来达到对所有这些任务进行并行处理的效果的话，那会非常耗费资源，此时建议使用创建一个并行队列，把所有的任务都放入并行队列，由系统更加空闲资源的情况来决定创建线程的数目，即并行执行任务的数目。

#### 获取Main和Global的分发队列
系统默认会为程序创建好一个在主线程执行的Main Dispatch Queue和4个不同优先级的Global Dispatch Queue。
Main Dispatch Queue会在主线程中执行，因此建议只执行一些和UI界面相关的任务，并且这个队列是串行的队列。使用`dispatch_get_main_queue()`方法来获取Main Dispatch Queue。


Global Dispatch Queue是分别为DISPATCH_QUEUE_PRIORITY_HEIGH,DISPATCH_QUEUE_PRIORITY_DEFAULT,DISPATCH_QUEUE_PRIORITY_LOW和DISPATCH_QUEUE_PRIORITY_BACKGROUND优先级的4个全局的并行队列。使用`dispatch_get_global_queue(优先级，0)`方法来获取。

### dispatch_after延迟执行
使用`dispatch_after`方法可以设置任务添加到队列中的时间。比如：

	dispatch_time_t time = dispatch_time(DISPATCH_TIME_NOW, 3ull * NSEC_PRE_SEC);
	dispatch_after(time, dispatch_get_main_queue(), ^{
		NSLog(@"Waited at least three seconds");
	});
这段代码的意思就是在三秒后才把任务添加进队列，因此任务至少要等3秒（如果添加进去就执行，主线程的串行队列前面没有其他任务等待的话那刚好3秒）。

### Dispatch Group
当需要一组任务执行完成之后才能执行接下来的任务的时候，可以把那一组的任务放进一个`dispatch_group_t`中，比如：

	dispatch_queue_t queue = dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0);
	dispatch_group_t group = dispatch_group_create();
	dispatch_group_async(group, queue, ^{
    	NSLog(@"Tack0");
	});
	dispatch_group_async(group, queue, ^{
    	NSLog(@"Tack1");
	});
	dispatch_group_async(group, queue, ^{
    	NSLog(@"Tack2");
	});
	dispatch_group_notify(group, queue, ^{
    	NSLog(@"Done");
	});
则`Done`的执行一定是在`Task0,Task1,Task2`执行之后才执行：

`dispatch_group_notify`会在`group`里的任务都执行完毕后得到通知，然后把一个新的任务（第三个参数）放到一个queue（第二个参数）中执行。

	dispatch_group_notify(group, queue, ^{
    	NSLog(@"Done");
	});
等效于

	disptch_group_wait(group,DISPATCH_TIME_FOREVER);
	dispatch_async(queue, ^{
		NSLog(@"Done");
	});	
	
`dispatch_group_wait`方法除了一直等待group中的任务完成外，还可以指定等待多少时间，并且根据返回值来判断是group中的任务都执行完了，还是等待的时间到了：

	dispatch_time_t time = dispatch_time(DISPATCH_TIME_NOW, 1ull * NSEC_PER_SEC);
	long result = dispatch_group_wait(group, time);
	if(result == 0){
		/*
			返回0表示group中的所有任务都执行完毕
		*/
	}else{
		/*
			否则表示还有些任务没有完成，只是等待的时间到了
		*/
	}	### dispatch_barrier_async
`dispatch_barrier_async`方法是为了在并行队列中控制某个任务执行顺利的方法，即当任务在并行队列中执行时，任务的执行顺序是没法确定的，如果需要确定某个任务在后续的其他任务前完成，比如有很多并行`read`的任务，但是在并行`read`到一定的数据之后，需要先串行`write`完才能继续并行`read`，则可以使用如下的方式实现：

	//这里的queue是一个自己使用dispatch_queue_creat创建的并行dispatch队列	dispatch_async(queue, blk0_for_reading);
	dispatch_async(queue, blk1_for_reading);
	dispatch_barrier_async(queue, blk0_for_writing);
	dispatch_async(queue, blk2_for_reading);
	dispatch_async(queue, blk3_for_reading);
	
以上代码表示在并行读完`blk0_for_reading`,`blk1_for_reading`之后，需要先串行执行`blk0_for_writing`,之后等这个任务执行完成之后，才可以继续并行执行下面的任务。
用图来表示`dispatch_barrier_async`的执行顺序关系为：
![dispatch_barrier_async的执行顺序](https://raw.github.com/ilingaohe/ilingaohe.github.com/master/_posts/images/2012-08-24-03.png)

图-3 dispatch_barrier_aysnc的执行顺序

注意点：`dispatch_barrier_async`的第一个参数queue必须是一个自己使用dispatch_queue_creat创建的并行dispatch队列，如果是一个串行队列或者是系统global的并行队列，那这个函数等效于`dispatch_aysnc`，会立即返回。

### dispatch_sync
`dispatch_sync`是和`dispatch_async`对应的方法。`dispatch_async`是指把任务添加进分发队列和任务的执行都是异步的，即会立即返回。而`dispatch_sync`是同步的，即需要等到当前这个添加进队列的任务执行完毕后，才会返回。

注意点：`dispatch_sync`很容易造成死锁，特别是在串行队列上执行的时候。比如：
	
	dispatch_sync(dispatch_get_main_queue(), ^{
		/* 具体的任务 */
	});
这个是在主的串行线程上执行一个任务，实际上这是一个死锁，因为`dispatch_sync`需要在主线程上执行完任务才能返回，而当前流程也是在主线程执行的，即主线程也需要等待`dispatch_sync`返回才能继续执行，这就造成了死锁，程序卡死。
因此在使用这个方法的时候，需要考虑到死锁会不会出现的情况，建议尽量不用。

### dispatch_apply
`dispatch_apply`可以把一个任务放进一个队列中执行指定的次数，并且这个方法是同步的，只有执行完了，才会返回。可以用来做一个高效的迭代器。

	dispatch_apply([array count], queue, ^(size_t index){
		NSLog(@"%uz:%@",index, [array objectAtIndex:index]);
	});


### dispatch_suspend/dispatch_resume
当你想先暂停然后再恢复一个执行队列的时候，可以使用以上的方法。
但是这个不影响已经在执行的任务，只是对在队列中但还没有开始执行的任务有效。

### dispatch_semaphore
`dispatch_semaphore`是比串行队列或者并行队列的`dispatch_barrier_async`更低粒度的控制执行顺序的一种方式。
`dispatch_semaphore_create(long value)`表示创建可以并发执行value个任务的信号量，
`dispatch_semaphore_wait`为等待信号量，
`dispatch_semaphore_signal`为释放信号量

### dispatch_once
`dispatch_once`会确保里面的任务只会执行一次，即使在多现成的环境下，因此可以用来实现单例模式。

## 后续学习
以上部分只是介绍了GCD的内容和基本使用，之后我们再深入学习一下GCD的具体实现方式。