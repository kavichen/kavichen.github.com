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
</br>  

# 问题  
</br>  
  
## UIViewController. viewDidLoad vs. viewWillAppear: What is the proper division of labor?    
  

[原文](http://stackoverflow.com/questions/1579550/uiviewcontroller-viewdidload-vs-viewwillappear-what-is-the-proper-division-of)  
  
viewDidLoad is things you have to do once. viewWillAppear gets called every time the view appears. You should do things that you only have to do once in viewDidLoad - like setting your UILabel texts. However, you may want to modify a specific part of the view every time the user gets to view it, e.g. the iPod application scrolls the lyrics back to the top every time you go to the "Now Playing" view.

However, when you are loading things from a server, you also have to think about latency. If you pack all of your network communication into viewDidLoad or viewWillAppear, they will be executed before the user gets to see the view - possibly resulting a short freeze of your app. It may be good idea to first show the user an unpopulated view with an activity indicator of some sort. When you are done with your networking, which may take a second or two (or may even fail - who knows?), you can populate the view with your data. Good examples on how this could be done can be seen in various twitter clients. For example, when you view the author detail page in Twitterrific, the view only says "Loading..." until the network queries have completed.