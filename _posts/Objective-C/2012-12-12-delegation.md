---
layout: post
title: Delegation 

---  
# 定义理解  
</br>  
## 理解1  
[原文链接](http://www.cocoachina.com/bbs/read.php?tid=88766)   
 
写出自己心中的委托。。

a 要委托 b 来做某事 ： 那么
1，a必须有一个委托，也就是说， a中必须声明 一个 id<delegate>  delegate 类型的变量；
2，b 是被a委托的对象。 那么， a * a = [[a alloc] a];    a.delegate = b;

这两个也就定义了委托的核心。 id 是任意类型的成员， 当 a.delegate = b;， 也就可以认定， a中的 id<delegete> delegate 也就是b ； 当你在 a中用delegate调用了某方法，也就是说b在调用某方法；

我们经常用的 一个  UITableView ，那么在一个类中，有成员变量UITableView *table,    self.tabelView.delegate = self;  这是我们最长用的一句话。
现在来理解。
tabelView.delegate ,说明 tabelView 中有一个 delegate ，而这个delegate ，由于 self.tabelView.delegate = self;   self 把自己赋给了 delete ，self就是 delegate； 
而 UITableView 中的 各个函数：- tableView: numberOfRowsInSection: heightForRowAtIndexPath； 等等，  这都是  @protocol 的， 这些函数都等同于 c++的虚函数。

UITableView中       id <UITableViewDelegate>   delegate;     这个参数 会调用 numberOfRowsInSection: heightForRowAtIndexPath；等函数，

剩下的 ，也就可以用 c++ 的 虚函数（或者说是@protocol ）一个道理了 。。呵呵

@protocol 也就是 实现了动态绑定，也就是多态。。没啥难理解的。
其中@required， 是必须实现的， 类似于 纯虚函数；
@optional 是非必须的， 类似与 虚函数；。 


## 用delegation时，可能会出现Cannot find protocol declaration的error  
### ANS_1：
[原文链接](http://stackoverflow.com/questions/6447573/cannot-find-protocol-declaration)
  
Let me reduce the sample even further, and label the lines:

	VC1.h
	
	#import "VC2.h"  // A
	
	@class VC1;
	
	@protocol VC1Delegate // B
	@end
	
	@interface VC1 : UIViewController <VC2Delegate> // C
	@end
	VC2.h
	
	#import "VC1.h"  // D
	
	@class VC2;
	
	@protocol VC2Delegate // E
	@end
	
	@interface VC2 : UIViewController <VC1Delegate> // F
	@end  

Consider what happens when something #imports VC1.h: It reaches line A, then the import is processed. Line D does nothing because VC1.h was already imported. Then line E is processed. Then line F, and we get an error because we haven't gotten to line B yet so the protocol is not declared!

Consider then what happens when something #imports VC2.h: It reaches line D, then the import is processed. Line A does nothing because VC2.h was already imported. Then line B is processed. Then line C, and we get an error because we haven't gotten to line E yet so the protocol is not declared!

The first step is to reconsider whether both of these classes really need to be each other's delegates. If you can break the cycle, that would probably be the way to go. If not, you'll need to restructure your headers. The most straightforward way is probably to put the delegates into their own headers:

VC1Delegate.h

	@class VC1;
	
	@protocol VC1Delegate // B
	@end
	VC1.h
	
	#import "VC1Delegate.h"
	#import "VC2Delegate.h"
	
	@interface VC1 : UIViewController <VC2Delegate> // C
	@end
	VC2Delegate.h
	
	@class VC2;
	
	@protocol VC2Delegate // E
	@end
	VC2.h
	
	#import "VC1Delegate.h"
	#import "VC2Delegate.h"
	
	@interface VC2 : UIViewController <VC1Delegate> // F
	@end  

If you trace through the imports now, you'll see that the appropriate protocols will now always be declared before the @interface lines try to use them.  
  
### ANS_2  
I had almost the same problem, and I fixed it thanks to the answer above, but in a slightly different way.

all I did was to put the #import line after the protocol declaration in the header file. hope I can help. and if anyone know that this is bad programing for some reason, pls let me know    
