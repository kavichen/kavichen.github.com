---
layout: post
title: 如何为Jekyll绑定域名  

---
  
之前从来没有帮顶过域名，第一次用，在google简单搜索了一下，居然成功了。
我这里用的是 http://paomi.com 泡米网的域名管理服务。如果选用其他域名地址，原理也是一样的。  
  
## 步骤 
1. 在本地代码库里新建名为CNAME文本文件，在Terminal中输入，以为例:example.com      

		echo 'example.com' > CNAME  
	然后push    

		git add CNAME
		git commit -am "CNAME ADDED"  
		git push  

2. 登陆域名管理，在域名解析中添加  
	  
	- 主机记录：@
	- 记录类型：A
	- 线路类型：默认
	- 记录值：204.232.175.78
	- 其他：默认

### 参考  
[github:help](https://help.github.com/articles/setting-up-a-custom-domain-with-pages)  
[再谈github页面域名帮顶](http://yanping.me/cn/blog/2011/12/26/github-pages-domain-2/)  
*此步骤只适合绑定顶级域名*