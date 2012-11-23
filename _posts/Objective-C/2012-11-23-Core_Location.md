---
layout: post  
title: Objective-C Core Location 

---      
  
# Core Location
</br>  
  
## Basic object is `CLLocation`  
@properties:`coordinate`,`altitude`,`horizontal/verticalAccuracy`,`timestamp`,`speed`,`course`  
  
## Where is this location?  
	  
	@property (readonly) CLLocationCoordinate2D coordinate;  
	typedef {  
		CLLocationDegrees latitude; // a double  
		CLLocationDegress longitude // a double  
	}  CLLocationCoordinate2D;  
  
	@property (readonly) CLLocationDistance altitude; // meters  
  
A negative value means "below sea level".