---
layout: post  
title: Objective-C NSSortDescriptor Wiki  

---    
  
## 用来给object做基本的排序  
</br> 
## Initializing a Sort Descriptor  
### `+sortDescriptorWithKey:ascending:`  
Creates and returns an `NSSortDescriptor` with the specified key and ordering.  
`+(id)sortDescriptorWithKey(NSString *) key ascending:(BOOL)ascending`  
  
*ascending*  
	YES if the receiver specifies sorting in ascending order, otherwise NO.
