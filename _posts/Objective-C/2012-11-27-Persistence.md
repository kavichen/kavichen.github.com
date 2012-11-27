---
layout: post  
title: Objective-C Persistence

---    
  
# Persistence  
</br>  
  
## Property List  
In `NSArray` `NSDictionary` or `NSUserDefaults`, we can use `writeToURL:atomically:` and `initWithContentsOfURL`  
  
`NSPropertyListSerialization` converts Property List to/from NSData.  
  
# File System  
</br>  
## How do you get the paths to these special sandbox directories?  
Use this `NSFileManager` method …    

	- (NSArray *)URLsForDirectory:(NSSearchPathDirectory)directory  //see below	inDomains:(NSSearchPathDomainMask)domainMask; //NSUserDomainMask  
  
## Notice that it returns an `NSArray` of paths (not a single path)  
Since the file system is limited in scope, there is usually only one path in the array in iOS. No user home directory, no shared system directories (for the most part),etc.  
*Thus you will almost just use `lastObject` (for simplicity)*  
  
## Examples of `NSSearchPathDirectory` values  
`NSDocumentsDirectory`,`NSCachesDirectory`,`NSAutosavedInformationDirectory`,etc.  
  
# File system  
</br>
## NSFileManager
  
	NSFileManager *manager = [[NSFileManager alloc] init];  
	- (BOOL)createDirectoryAtPath:(NSString *)path  
	withIntermediateDirectories:(BOOL)createIntermediates  
	attributes:(NSDictionary *)attributes  
	error:(NSError **)error;  
  
	- (BOOL)isReadableFileAtPath:(NSString *)path;  
	- (NSArray *)contentsOfDirectoryAtPath:(NSString *)path error:(NSError **)error;