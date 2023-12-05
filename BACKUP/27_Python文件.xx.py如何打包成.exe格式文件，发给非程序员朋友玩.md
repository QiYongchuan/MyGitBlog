# [Python文件 xx.py如何打包成.exe格式文件，发给非程序员朋友玩](https://github.com/QiYongchuan/MyGitBlog/issues/27)

前言：我花了一个上午的时间将在命令行中查询天气的接口封装成一个 Python 文件，并通过 Python 的 requests 库直接发送请求。但我想将其发送给没有 Python 编译器的朋友们使用，所以只能将 Python 打包成 exe格式的文件。在此之前，我有过打包自己python程序到exe的经验，将python画的爱心打包成exe格式程序发给朋友。

具体的过程不复杂，可以概括为以下几个步骤：1. 安装 Python 的专用打包工具 PyInstaller。  2.在命令行输入pyinstaller -F py文件路径 就完成了。  （在倒数第二行查看生成的dist文件夹，去看exe文件就可以了。

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/bbd1e960-cc22-4385-a9f0-e463c8931a65)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/785d9937-b54a-46e8-809b-a399c2c9d12f)

注意事项：
1.直接打开cmd窗口，输入命令就可以了，后面跟正确的路径就可以打包了。（我之前已经下载过打包工具了）
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/ef2b26ec-5886-4a3a-a5a4-f588046edbea)
2.打包后，点击weather.exe出现了闪退，用命令行运行后：查看到了报错信息
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/48ac40d1-a403-4efd-83f3-f7c4d36de21d)
将报错信息丢给GPT分析，得出：打包时缺少了几个依赖包，导致直接闪退了
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/d9e0c1ce-9065-4580-ae4b-075827522e39)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/ad19d36f-0ee8-464a-85f2-f24fd53dcf7a)

先是执行这一条，手动安装所需的依赖：
```
pip install chardet charset_normalizer

```
但是pip安装包出现错误：443
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/55cab05e-84ed-4998-9674-501d9e65bd8d)
轻车熟路，这次直接先关掉梯子，后重新安装，成功。

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/bbff022e-37ae-4788-b1d5-d1bf90067bc5)

再进行第二步，将缺少的依赖重新打包，这里感觉是在加上这部分后重新打包一份py到exe

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/b32ad3f9-64de-485c-8145-6747b19fb005)

此上，所有的打包工作完成，成功将写好的waether.py转成了weather.exe程序了，理论上朋友们可以在自己电脑上运行我的查询天气的程序了。




---

### Python中编码在命令行窗口中出现乱码的情况

 但问题还是出现了，乱码，乱码，编码方式不统一，让我们看到的不是同一个世界了。

理论上我想看到的是：

![84f0b9fa4844395661ca4019c30feff](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/9130abb4-c7d6-420a-b202-eac4d7db2ad8)
![0fb2c892de32e8642a38c934b108eb0](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/92e61384-3f25-454f-9fed-73191be841e4)

但在命令行中看到的是：

![990b53fd666ec3a7c2e6a6dd690bbbb](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/19aeef62-81e2-47f9-a73c-e7aa2c255dfd)
![1d6aa6ceac4af905160a91d92a5abe2](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/2369d54a-2486-44b1-9cd7-068e14197b80)

编码方式不一样，好看的效果出不来了

![e0310c23e434db1dc3b1c23d0c34b1a](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/9756d110-8f3e-4316-abe4-76e204352a32)


### 暂时留个坑先不解决了

发给朋友们，竟然没反馈，这部分先留个坑吧。

 另一个问题：挂梯子，无法查询：)，这个问题应该还是来自 
#26 Python中request发送请求时，443报错

![2db8839bc82c385922d6de1032764e3](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/44ad3924-463d-4c35-83e4-e72aef59858f)

![74d7f62ebd77cce084a25079282c7d6](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/78d8c7ef-f9e6-4570-af4f-d9151c68e667)




