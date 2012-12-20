---
layout: post  
title: The difference between nil, NIL and null

---   
# nil  
</br>
nil is the literal null value for Objective-C objects, corresponding to the abstract type id or any Objective-C type declared via @interface.  
  
For instance:

	NSString *someString = nil;
	NSURL *someURL = nil;
	id someObject = nil;
	
	if (anotherObject == nil) // do something  
  
# Nil  
</br>
Nil is the literal null value for Objective-C classes, corresponding to the type Class. Since most code doesn’t need variables to reference classes, its use is not common. One example is:

	Class someClass = Nil;
	Class anotherClass = [NSString class];  
  
# NULL  
</br>					
NULL is the literal null value for arbitrary C pointers. For instance,

	int *pointerToInt = NULL;
	char *pointerToChar = NULL;
	struct TreeNode *rootNode = NULL;  
  
#NSNull  
</br>  
NSNull is a class for objects that represent null. In fact, there’s only one object, namely the one returned by +[NSNull null]. It is different from nil because nil is a literal null value, i.e., it isn’t an object. The single instance of NSNull, on the other hand, is a proper object.

NSNull is often used in Foundation collections since they cannot store nil values. In the case of dictionaries, -objectForKey: returns nil to indicate that a given key has no corresponding object in the dictionary, i.e., the key hasn’t been added to the dictionary. If you want to make it explicit that you have a certain key but it doesn’t have a value yet, you can use [NSNull null].

For instance, the following throws an exception because dictionaries cannot store nil values:

	NSMutableDictionary *dict = [NSMutableDictionary dictionary];
	[dict setObject:nil forKey:@"someKey"];  

On the other hand, the following code is valid since [NSNull null] is a non-nil object:

	NSMutableDictionary *dict = [NSMutableDictionary dictionary];
	[dict setObject:[NSNull null] forKey:@"someKey"];  

It’s worth mentioning that Foundation collections have initialisers that use nil as a marker for the end of a list of objects without having to specify the number of elements in the list. This can only happen because nil cannot be stored in a Foundation collection. For instance,
  
	NSArray *array = [NSArray arrayWithObjects:@"one", @"two", nil];  

As for NIL or NSNil, there are no such things in Objective-C or Apple Foundation.  
  
## 补充  
  
向`nil`发送消息不会导致系统崩溃  
  
### BOOL陷阱  
  
- 将`int`值转换为`BOOL`时应特别小心。避免直接和`YES`比较    
- Objective - C中，将`BOOL`定义为`unsigned char`,这意味着除了`YES`(1)和`NO`(0)外，它还可以是其他值。*禁止将`int`直接转换(cast or convert)为`BOOL`*  
- 常见的错误包括：将数组的大小，指针值或位运算符的结果转换(cast or convert)为`BOOL`，因为该`BOOL`值的结果取决于*整型值的最后一位*  
- 将整型值转换为`BOOL`的方法：使用三元运算符返回`YES`/`NO`,或使用位运算符（&&，||，！）  
- `BOOL`，`_Bool`和`bool`之间的转换是安全的，但是`BOOL`和`Boolean`间的转换是不安全的，所以将Boolean看成整型值。  
- 在Objective-C中，只允许使用`BOOL`
