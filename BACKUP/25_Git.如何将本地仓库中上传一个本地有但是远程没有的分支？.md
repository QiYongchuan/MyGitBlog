# [Git 如何将本地仓库中上传一个本地有但是远程没有的分支？](https://github.com/QiYongchuan/MyGitBlog/issues/25)

问题描述：

我在本地有一个仓库StydyPy，用来记录我的学习代码，我要上传到我的远程项目仓库Let’s Run中。

思路：本地有master分支，远程则是main分支，现在我要建一个StudyPy上去，一是我直接把我的master分支改名字，然后上传到远程仓库，或者我在本地新建一个StudyPy分支，然后将master分支里的内容，merge过去，再上传到远程仓库。

因为远程仓库并没有StudyPy的分支，无论哪种方法，也需要在远程新建一个分支，即原来不存在的分支。


新建-复制思路
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/d2576cda-4bf4-4c49-a6b9-26eaa66fce5d)

重命名思路：
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/6a96163c-72a7-4c8f-8580-e613cd02b486)


将本地推送到远程：

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/03061fde-2002-4a6b-8d53-02f196c3ecc4)

以上是说，当远程有仓库的时候，git push origin StudyPy 就可以；如果远程没有，那就git push -u origin StudyPy，意思是先建一个，再传过去。

当然，把本地仓库push到远程的前提是，两者建立了关联：

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/2f5d0fa8-532a-4073-8cc2-0b3c9b6ddc39)


---

#65   git远程分支：如何将本地分支与远程分支相关联

参考最新的博客：可以将本地存在但远程不存在的分支上，上传并且关联；
