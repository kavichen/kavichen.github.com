---
layout: post  
title: Objective-C NSMutableDictionary Wiki  

---   
  
## Create a NSMutableDictionary  
</br>  

### `dictionary`  
Creates and returns an empty dictionary  
  
	+(id)dictionary  
  
---  
---  
---  
## 如何在一个`NSMutableDictionary`查询`key`值是否存在   
 
	if (![sortedByCountry objectForKey:country]) {
            [sortedByCountry setObject:[NSMutableArray array] forKey:country];
        }
  
`sortedByCountry`为`NSMutableDictionary`的一个实例，查询`country`这个`key`是否存在。  
  
---