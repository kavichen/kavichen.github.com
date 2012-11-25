---
layout: post  
title: Objective-C Understand the iOS UIViewController lifecycle

---   
  
[原文](http://stackoverflow.com/questions/5562938/looking-to-understand-the-ios-uiviewcontroller-lifecycles)  
  
## Ans #1:  
  
There's nothing special you need to do in Monotouch that's different from how you would do things normally in ObjectiveC

All these commands are called automatically at the appropriate times by iOS when you load/present/hide the view controller. It's important to note that these methods are attached to UIViewController and not to UIViews themselves. You won't get any of these features just using a UIView.

There's great documentation on apple's site here: http://developer.apple.com/library/ios/#documentation/uikit/reference/UIViewController_Class/Reference/Reference.html

Putting in simply though :

ViewDidLoad - Called when you create the class and load from xib. Great for initial setup and one-time-only work

ViewWillAppear - Called right before your view appears, good for hiding/showing fields or any operations that you want to happen every time before the view is visible. Because you might be going back and forth between views, this will be called every time your view is about to appear on the screen

ViewDidAppear - Called after the view appears - great place to start an animations or the loading of external data from an API.

ViewWill/DidDisappear - Same idea as the WillAppear.

ViewDidUnload/Dispose - Available to you, but usually not necessary in Monotouch. In objective-c, this is where you do your cleanup and release of stuff, but this is handled automatically so not much you really need to do here.  
  
## Ans #2:  
![](http://ww1.sinaimg.cn/large/a74e55b4jw1dz7ayki65tj.jpg)