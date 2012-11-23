---
layout: post  
title: Objective-C UITableView Wiki  

---    
  
## Data Source  
</br>  
  
	- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section
	{
	    return [[self.sortedByCountry objectForKey:[self.sectionHeaders objectAtIndex:section]] count];
	}  
  
`numberOfRowsInSection:(NSInteger)section` 中的`section`是表示在第几个section中，它的类型是`NSInteger`。