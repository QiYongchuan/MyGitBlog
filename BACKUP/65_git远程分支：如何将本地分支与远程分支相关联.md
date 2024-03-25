# [git远程分支：如何将本地分支与远程分支相关联](https://github.com/QiYongchuan/MyGitBlog/issues/65)

![image](https://github.com/QiYongchuan/Algorithm-learn/assets/105039020/cb74f1ae-8bf1-4861-8d4c-5f14eb4902b0)

---

#### 本地分支与远程分支相关联

两种情况：

* 将本地的main/master分支，与新建的远程仓库中的mian分支进行关联
* 本地有一个自己建立的分支，想在远程仓库中新建一个分支，并关联


**1. 将本地master分支与远程仓库中进行关联：**

```
git branch -M main
git push -u origin main

git branch -M main

```

> 这个命令用于将当前分支重命名为main。在Git中，-M选项表示强制重命名，即使目标分支名（这里是main）已经存在也会进行重命名。这个命令不会影响远程分支，它只改变本地分支的名称。
> 
> 这个操作通常用于遵循GitHub和其他Git托管服务中的新惯例，将默认分支从master改为main，以避免使用带有奴隶制历史的术语。
> 
> git push -u origin main
> 
> git push命令用于将你的本地更改推送到远程仓库。这里的命令做了几件事情：
> 
> -u选项告诉Git不仅要推送本地的main分支到远程仓库，而且还要将本地的main分支设置为跟踪远程的main分支。跟踪关系意味着在未来的操作中，你可以更方便地从远程分支拉取（pull）更新或向远程分支推送（push）更改。
> origin是远程仓库的默认名称。当你克隆一个仓库时，Git自动将这个远程仓库命名为origin。这代表了你想要推送到的远程仓库的地址。
> main指的是你想要推送的本地分支的名称，这里表示你想要将本地的main分支推送到远程仓库。
> 总的来说，这两行命令的组合用途通常是为了将本地的主分支从master重命名为main，并且将这个改动推送到远程仓库，同时设置本地的main分支跟踪远程的main分支。


**2.将本地的分支上传到远程仓库中，并新建一个分支，并关联**

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/3070462f-ddc8-4e12-a633-086ba2e68616)


**3.将自己本地分支（非main），上传到远程的main分支**
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/cf6c42b9-3329-4a77-8a24-ea900f659427)

