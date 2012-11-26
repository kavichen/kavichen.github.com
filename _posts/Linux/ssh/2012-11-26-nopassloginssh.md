---
layout: post
title: 不用密码登陆ssh

---
  
## 步骤 
1. 例如：本机为client，192.168.1.122为Server.

2. 在本机输入 `ssh-keygen -t rsa` <== 这个步骤产生Key Pair
3. 在本机输入 `cd ~/.ssh`  
4. 在本机输入 `scp id_rsa.pub pi@192.168.1.122:~/`
5. 在Server输入 `cd ~/.ssh`
6. 在Server输入 `cat ../id_rsa.pub >> authorized_keys`
7. Done
 
### 参考  
《鸟哥的Linux私房菜》