# [在挂梯子的情况下pip install xx 失败以及git push失败的解决方案（443以及10087等）](https://github.com/QiYongchuan/MyGitBlog/issues/67)

这个问题算是一个长期问题了，常见的症状表现在：
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/18ed6ca2-01b1-47ff-8b2c-c9189fc4a634)

在连接梯子（VPN)之后，pip install xx，无法安装；
断开梯子之后，安装成功；

同样，在本地写完代码上传github的远程仓库时，使用git push，
连接梯子的情况下，无法push上去，
断开梯子，就可以push上去。


之前的解决的方法，就是不停的开/关梯子。

现在因为更加频繁的使用Chatgpt，开关梯子需要更加频繁了，不得不解决这个问题。

一开始，照例先问gpt，但是回答不好。（之前应该也是问过的，没解决好）

大概是因为chatgpt它老家那块的人遇不到这么复杂的网络情况吧，又是翻墙又是啥的。

所以这防火墙问题，还得去找CSDN，一搜果然有大量的案例，不愧是修建长城的国家：）

问题分两个方案解决：
**1.解决pip安装问题，**本质是因为换源之后连接国内的镜像网站，检测到有代理，连接不上；
所以解决的方法就是：设置电脑的**代理**，把换源的网站增加到表中，就设置成了不进行代理。
即：
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/6a691feb-a215-4cea-8f78-0f2c6b7790df)

这样，在命令行pip install xx  的时候，就可以愉快的下载包了，与之前每一次下载都断开梯子的原理是一样的，这次是我们手动将这个网站设置成不代理了。

> 参考：[解决开着代理情况下pip或魔搭下载失败](https://blog.csdn.net/qq_51116518/article/details/134536785)


2.解决git push 时超时问题

这个原因也是网络相关，但具体是因为挂了梯子还是没挂梯子，我现在还不是很确定。

一般是，挂梯子的时候，push不上去，提示443以及代理问题；
当断开梯子时，可以push上去。

按照之前的思路，那我直接把github的网址也加到我的电脑-代理管理中好了，直接所有的通过该网址的请求都不要走代理了，问题不就解决了？


但我们知道，一是github是国外的网址，裸连的情况下，时好时坏，也就是说，裸连情况，我们有时可以直接连上，push成功，有时也会push不成功。
二，在挂梯子的情况下，又会出现因为梯子代理的原因，也连不上。

问题解决的办法是：

查询说的是，没有设置git的全局代理，这一步是设置全局代理
`
git config --global http.proxy http://127.0.0.1:7890

git config --global https.proxy http://127.0.0.1:7890
`
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/af49f9fa-e2b9-4b8b-be07-38eb261672d8)
dui'ying
> 对应上次代理设置里你自己的端口及地址

同样，看到了之前熟悉的解决思路：

（不过在资料中讲的是，取消上面设置git 全局代理时的设置）

`
取消全局代理：
git config --global --unset http.proxy
 
git config --global --unset https.proxy

`
这跟我们上面讲到的，当梯子断开时，能成功连接到远程仓库，成功push到，似乎是做了同样的事情，断开梯子。



