# [issue中发帖子的图片无法显示问题](https://github.com/QiYongchuan/MyGitBlog/issues/55)

在issue中写文章，插进了图片，分享出去之后，文章可以正常显示，但是图片缺无法加载。

发给朋友测试，无论是开代理还是没开代理，图片均无法加载。

在csdn上搜相关问题时，基本上是在自己电脑端无法显示，原因是DNS污染。

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/595616e3-b773-4cde-a34d-ca130b1f02e8)
参考来源：[解决Github无法显示图片以及README无法显示图片](https://blog.csdn.net/qq_41709370/article/details/106282229)

但我的问题显示不是这个，我的是自己端可以看到（手机登录点开这个issue也能加载成功），但是朋友访问时看不到。没有尝试修改自己的host，我在想即使这种方法真的可以的话，难道需要我让朋友为了能看到图片，也得修改自己电脑的host配置嘛？

于是问了chatgpt，回答如下：

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/e16114b4-5c51-4ed7-9612-ec54f799797d)

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/49edb418-2f8a-4cd3-88ba-edbf52fe0be8)


![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/a2cf5d5c-648d-4b7b-8712-2330186ebce5)

最终问题解决，原因是之前的帖子是写在了私人仓库里，供自己记一下的，后来想创建成公开的帖子，供我朋友参考的，图省事，直接将私有仓库的issue直接全文复制过来了。但是图片是存在私有仓库的，所以无法访问到，重新传了一次就好了。

---

> 发现 https://picx.xpoet.cn/#/upload 可以使用 github 仓库当作图床，还不错~

谢谢，我研究研究，之前用hexo搞博客就是被图片问题折磨了很久，也尝试过七牛云