# [GitHubPoster项目折腾记录：withings-sync 依赖下载失败到网络问题](https://github.com/QiYongchuan/MyGitBlog/issues/64)

在安装过程中遇到了几个问题：
1.withings-sync 依赖的安装问题上：withings-sync 安装失败的原因是 UnicodeDecodeError，并提供了一系列可能的解决方案，最终通过手动下载、修改 setup.py 中的编码设置，并重新安装成功。  原因可能是编码方式设置问题？

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/406db6e6-ea6c-4243-9c60-fa1a0dfff20d)

2.安装成功之后，依然从远程仓库下载其余的依赖，用不上手动下载的依赖：

手动关闭了
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/bca6f36e-91e2-4858-9ed5-d3dc9cf91296)

3.但是关闭之后，遇到了有些依赖仍然需要安装，但是还没有从远程安装下来  ==>  手动pip install xxx   手动安装了几个模块


4.运行项目：

成功了，但是在运行了四次尝试换一些参数后，又一直开始报错无法生成了
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/52454f9f-69db-40b6-8554-a62325050b8f)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/6e20b5da-c4a4-4c2a-be87-74b1ab5490d7)

之后的报错信息：

无论是开梯子还是关闭梯子，均无法再连上了。

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/7b3d3fd4-5df0-4c6b-8dfd-60b22ac964df)

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/f68faebc-05dd-4eff-b5fb-61dfef2fdcc6)


5.后续：又成功了
在刚刚整理报错信息时，发现之前即使成功生成的记录里，也提示了
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/ac573b12-e5e1-4af6-89f9-89d87e953cc3)
有一个依赖没有装，但本着能跑就不动的原则没去管。
刚才一直不行，又把这个依赖装了一下，结果现在又成功了。
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/4e42463e-4bcb-420e-b37b-16583bfebb80)

后后续：并不是依赖的问题，应该是网络的原因。
在继续增加参数后，又出现了之前的问题，无论是关了梯子还是开了梯子，都是显示997或者443

解决办法：
关了虚拟环境又重新进去了一遍后，重新请求可以了，而且修改参数后再请求也可以一直连接了。
但应该不是虚拟环境的原因？

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/43c6dd95-e609-4e1d-bdd7-4600db380821)


后续考虑：如何把下载生成的图片动态插入到博客页？

---

另一方面：感受到gpt4.0带给我的信心了，本来是一开始就打算去大佬的issue区去求助的，最后让自己给搞出来了！
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/40f764e3-2b93-4c6a-9954-6009c95a3eaf)


---

![github](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/cce123e1-cd9f-4ff8-8caf-1a97c2f09e1d)
