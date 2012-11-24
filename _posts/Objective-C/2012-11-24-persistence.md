---
layout: post  
title: Objective-C Persistence

---     

## Persistence    
</br>
  
### Property Lists  
Use `writeToURL:atomically:` and `initWithContentsOfURL:` in `NSArray` or `NSDictionary`  
Or NSUserDefaults if appropriate.  
Also `NSPropertyListSerialization` converts Property List to/from NSData.    
*atomically 的意思是，你不能写到一半就停下来*  
  
## Archiving  
  
### There is a mechanism for making ANY object graph persistent  
Not just graphs with NSArray, NSDictionary, etc. in them.
  
### For example, the view hierarchies you build in Interface Builder  
Those are obviously graphs of very complicated objects.  
  
 