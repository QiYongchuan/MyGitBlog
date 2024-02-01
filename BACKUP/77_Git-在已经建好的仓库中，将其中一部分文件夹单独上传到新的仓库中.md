# [Git-在已经建好的仓库中，将其中一部分文件夹单独上传到新的仓库中](https://github.com/QiYongchuan/MyGitBlog/issues/77)

> 使用场景：是在cs50的学习中，创建了一个大的仓库，记录不同章节的学习代码和笔记。但遇到了一个情况是，学校的安排上：CI/CD中，单独这一块是一个仓库的。就需要将这一部分的代码单独上传到一个新的仓库了，问题是，这部分已经处于一个仓库中了，还能再新上传吗？

> 答案是，可以； 同样的场景是，大的项目中，每一个独立的小项目，对应一个独立的仓库，进行单独的版本控制。

过程其实跟**“将一个已经存在的仓库上传到你建立的仓库”**的流程是一样的。

在GitHub新建仓库：airline

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/a5cdaf9b-5db2-4a31-af55-9fd1ecb15614)


…or push an existing repository from the command line
```
git remote add origin https://github.com/QiYongchuan/airline.git
git branch -M main
git push -u origin main

```
在你的本地，找到你想上传的文件夹：
**再一次初始化仓库**
命令行中：
```
git init
```
然后
```
git remote add origin https://github.com/QiYongchuan/airline.git   //跟新建的远程仓库关联
```
注意：此时需要你再一次的git add . 和git commit

然后按流程：
```
git branch -M main
git push -u origin main
```

就可以了，实现了在原来大仓库下，新建一个小的独立仓库。

同时，你可能担心：这会不会对我原来的大仓库造成什么影响呢？ 会不会引起更多的麻烦？
完全不会。

> 对于您原来的仓库，这个操作不会有直接的影响。您将现有项目文件夹上传到新创建的仓库中，不会影响原来的仓库或其历史记录。原来的仓库将保持不变，您可以继续在原来的仓库中进行开发和维护。

>新创建的仓库将成为一个独立的仓库，其中包含您上传的项目文件夹的副本。这意味着您可以在新仓库中进行独立的开发和版本控制，而不会影响原来的仓库。

>如果您希望在原来的仓库中保留与新仓库相同的历史记录，您可以考虑使用分支或者合并操作来保持两个仓库的历史记录同步。但是，这取决于您的具体需求和项目结构。

>总的来说，将现有项目文件夹上传到新创建的仓库中，不会直接影响原来的仓库，原来的仓库将保持不变。