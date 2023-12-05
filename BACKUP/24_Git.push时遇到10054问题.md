# [Git push时遇到10054问题](https://github.com/QiYongchuan/MyGitBlog/issues/24)

问题描述：

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/748e5bbf-72a8-4898-b96b-4a2a31b8c5f8)

可能的原因：

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/cd3f9ed7-6442-474b-8e63-b699254e5424)

总结：根本原因在于网络。

解决方式：
1.之前挂梯子代理时，将局部代理换成全局代理后，解决。
2.修改一下代理：
git config --global http.sslVerify "false"

![51401a33c96a4af18f7325994d56999](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/563e5219-8bc5-4ed2-ab53-b77b21396fef)

3. 把wifi换成数据流量上网，解决。

大概还是因为网速的原因，上次出现这个问题也是在家里，连的家里的宽带，切换手机开热点后就成功push上去。在学校反而没遇到过10054的情况。
