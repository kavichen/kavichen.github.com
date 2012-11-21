---
layout: post
title:Objective-C Protocol Wiki 
---

## Protocols
### **Similar to @interface, but someone else does the implementing**

	`@protocol Foo <Other,NSObject>`// implementors must implement Other and NSObject too  
	`-(void)doSomething;` // implementors *must* implement this (methods are `@require` by default)  
	`@optional`  
	`- (int)getSomething;`  
	`- (void)doSomethingOptionalWithArgument:(NSString *)argument;` // also optional  
	`@require`  
	`- (NSArray *)getManySomethins:(int)howMany;` //back to being "mush implement"  
	`@property (nonatomic, strong) NSString *fooProp;` // note that you mush specify strength (unless it's readonly,of course)  
	`@end` 