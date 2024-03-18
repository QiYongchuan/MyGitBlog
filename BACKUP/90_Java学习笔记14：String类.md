# [Java学习笔记14：String类](https://github.com/QiYongchuan/MyGitBlog/issues/90)

#### 继承关系

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/e055865d-2ff8-41c3-913d-94e306bccefc)

说明，可以串行化，数据可以网络传输，String对象可以比较相互比较大小

本质是一个final 类型的char 数组[ ]

#### 两种创建方式的不同

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/a3c9bad4-cc97-467c-857c-71503730df20)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/e83681d6-5375-464f-b0b3-e209d74b4e6c)

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/3eb29267-14f1-48bf-8164-a21075de270c)


equal：比较值是否相等
== 比较地址是否相等

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/5ddfe772-2ddb-43c8-a547-e255d137d145)

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/af2873b3-9dfb-4866-87ab-6aa4fcf2c7c0)

注意这里的方法  String.inner  返回的是常量池的地址。


字符串的特性：
其实是创建了两个常量池对象
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/6054a501-9ab8-48c9-97f4-cd859ede7f2c)
**这里进行了优化，直接创建了一个**
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/d4028aae-1885-404e-b5e7-12aaf6a6c2ac)

**常量相加，直接在池中；变量相加，在堆中**
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/c1d47706-1087-450b-b000-9e3f6b3d40ab)

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/b4170a28-8027-4108-a04a-91c0e23da88c)


![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/f89beb90-7214-4501-8393-776355aae8c9)




---

#### String 的常用方法

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/d665c5b5-364c-4ce1-8448-132acc4bdc2e)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/d80d89ca-0869-44cf-8f99-27df55ca273b)


format 格式化字符串

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/586edf6f-a43e-49c7-aad1-da0c7694b5e0)
