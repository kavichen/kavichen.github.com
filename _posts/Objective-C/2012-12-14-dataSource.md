---
layout: post
title: Objective - C dataSource
  
---  


### 以“FlickrApp”为例子：  
  
1. 简历一个Protocol  
	  
	- `PlacesMapViewDataSource.h`  
  
	- Code  
  
		#import <Foundation/Foundation.h>
		
		@class PlacesMapViewController;
		
		@protocol PlacesMapViewDataSource
		
		-(NSArray *) placesToDisplay: (PlacesMapViewController *)sender;
		
		@end    
  
2. 将数据源所在的Class `PlacesUITableViewController.m` 中遵循`PlaceMapViewDataSource`  
   
		@interface PlacesUITableViewController() <TopPhotoTableViewControllerDataSource, PlacesMapViewDataSource>

  
3. 在数据源所在的Class `PlacesUITableViewControlle.h` 中添加  
  
		@property (nonatomic, weak) id<PlacesMapViewDataSource> dataSource;  
  
4. 将数据源所在的Class `PlacesUITableViewController.m` 中实现`placesToDisplay` 
  
		- (NSArray *)placesToDisplay:(PlacesMapViewController *)sender
		{
		    return self.places;
		} 
  
5. 在`PlacesMapViewController.m`的`viewDidLoad`中实现  
  
		self.places = [self.dataSource placesToDisplay:self];