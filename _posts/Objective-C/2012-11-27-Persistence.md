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
  
## NSString  
Path construction methods and reading/writing strings to files.  
  
	- (NSString *)stringByAppendingPathComponent:(NSString *)component;  
	- (NSString *)stringByDeletingLastPathComponent;  
	- (BOOL)writeToFile:(NSString *)path  
	        atomically:(BOOL)flag  
            encoding:(NSStringEncoding)encoding //e.g. ASCII, ISOLatin1, etc.  
            error:(NSError **)error;  
  
	- (NSString *)stringWithContentsOfFile:(NSString *)path
				  usedEncoding:(NSStringEncoding *)encoding  
				  error:(NSError **)error;  
  
### `- (NSArray *)contentsOfDirectoryAtURL:(NSURL *)url includingPropertiesForKeys:(NSArray *)keys options:(NSDirectoryEnumerationOptions)mask error:(NSError **)error
Description	
`  
Performs a shallow search of the specified directory and returns URLs for the contained items.  
  
## NSURL中的Path怎么理解？  
### - (NSString *)path  

#### Descriptio
Returns the path of a URL conforming to RFC 1808.  

#### Returns	
The path of the URL, unescaped with the stringByReplacingPercentEscapesUsingEncoding: method. If the receiver does not conform to RFC 1808, returns nil.
If this URL object contains a file URL (as determined with isFileURL), the return value of this method is suitable for input into methods of NSFileManager or NSPathUtilities. If the path has a trailing slash it is stripped.  

Per RFC 3986, the leading slash after the authority (host name and port) portion is treated as part of the path.  
  
### 什么是RFC1808  
  
RFC 1808           Relative Uniform Resource Locators          June 1995


      <scheme>://<net_loc>/<path>;<params>?<query>#<fragment>

   each of which, except <scheme>, may be absent from a particular URL.
   These components are defined as follows (a complete BNF is provided
   in Section 2.2):

      scheme ":"   ::= scheme name, as per Section 2.1 of RFC 1738 [2].

      "//" net_loc ::= network location and login information, as per
                       Section 3.1 of RFC 1738 [2].

      "/" path     ::= URL path, as per Section 3.1 of RFC 1738 [2].

      ";" params   ::= object parameters (e.g., ";type=a" as in
                       Section 3.2.2 of RFC 1738 [2]).

      "?" query    ::= query information, as per Section 3.3 of
                       RFC 1738 [2].

      "#" fragment ::= fragment identifier.

   Note that the fragment identifier (and the "#" that precedes it) is
   not considered part of the URL.  However, since it is commonly used
   within the same string context as a URL, a parser must be able to
   recognize the fragment when it is present and set it aside as part of
   the parsing process.

   The order of the components is important.  If both <params> and
   <query> are present, the <query> information must occur after the
   <params>.
  
[原文链接](http://www.w3.org/Addressing/rfc1808.txt)  
