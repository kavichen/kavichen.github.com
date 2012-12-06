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

