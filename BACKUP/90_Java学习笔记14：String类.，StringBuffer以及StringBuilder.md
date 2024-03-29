# [Java学习笔记14：String类 ，StringBuffer以及StringBuilder](https://github.com/QiYongchuan/MyGitBlog/issues/90)

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


---

#### StringBuffer 与String的区别


内存区别：
String 的值是通过常量池的，而StringBuffer 是存在堆中的数组
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/624bd8da-de8c-4c14-b250-0e27ea27ee00)

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/e25b98be-5428-48a9-97ef-c06ce60ad5a5)


![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/abf76d85-0268-43d2-a773-680f5fea4cab)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/0328d148-d65a-4698-abad-7acbbc988457)

##### String 与StringBuffer转换
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/0871cedf-1454-4a44-8d7b-2e3b683688c7)


---

#### StringBuilder

**对Stringbuffer的补充，单线程更好的使用**

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/2159ce65-f2e6-40e4-825e-1d800eb0a74e)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/8bd163c8-5dc8-43e8-9145-be046e0cf1b8)


---

####  String 与StringBuffer 、StringBuilder比较
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/f84f2f74-2d95-4b48-9048-599aea2f84cb)

效率：StringBuilder>StringBuffer> String

使用场景：

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/8c90d9d4-d0dd-424d-b237-29cea8096cef)


---

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/89b01b13-0901-41f0-8dca-0c0138eed523)
