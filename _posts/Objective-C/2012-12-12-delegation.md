---
layout: post
title: Delegation 

---

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
