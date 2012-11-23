---
layout: post  
title: Objective-C NSIndexPath Wiki  

---     
  
## Overview  
  
The `NSIndexPath` class represents the path to a specific node in a tree of nested array collections. This path is known as an index path.  
  
Each index in an index path represents the index into an array of children from one node in the tree to another, deeper, node. For example, the index path 1.4.3.2 specifies the path shown in Figure 1.  
  
![](http://ww3.sinaimg.cn/large/a74ecc4cjw1dz4qxddszrj.jpg)  
  
*Note: iOS adds programming interfaces to the `NSIndexPath` class of the Foundation framework to facilitate the identification of rows and sections in `UITableView` objects. The API consists of a class method and two properties. The `indexPathForRow:inSection: `method creates an `NSIndexPath` object from row and section index numbers. The properties return the row index number and the section index number from such objects. See `NSIndexPath` UIKit Additions for details.*  
  
**Example:**  
  
	- (UITableViewCell *)tableView:(UITableView *)tableView
	         cellForRowAtIndexPath:(NSIndexPath *)indexPath  
  
在这个Method中，`indexPath.section`表示Array中的第几个section，`indexPath.row`