# [SpringBoot学习笔记：RESTful应用接口](https://github.com/QiYongchuan/MyGitBlog/issues/92)

#### 什么是RESTful？ 


REST（Representational State Transfer）是一组设计原则，用于构建网络服务。RESTful服务意味着遵循这些设计原则的服务。

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/88852ba7-bf4a-474e-b180-48886926593e)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/ef022762-b68e-4b72-bd5c-0b9891372730)

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/46fcc40a-5a3c-4dd7-8c96-1360f393784d)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/edf1a8b4-712f-4355-b314-db34cbc6ece9)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/b03f92a3-70f7-4ebc-9c94-8332207d584e)




---

#### SpringBoot 实现RESTful API
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/21125fe3-bd99-49e6-974e-8c4ff6f31424)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/628d8787-0e50-4245-af88-06f15e12eb64)



#### 动态参数的获取

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/4c441a63-12e9-4572-b728-0ed6ccd6502a)

注意：两种类型的参数，
一种是通过url传过来的（比如用户的id），此时需要动态参数的获取，即使用@PathVariable获取到参数
比如获取(get） 和删除（delete）的应用场景
一种则直接通过body请求体传过来的数据，
此时直接通过实体类接受了
比如添加用户，更新用户。

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/22164fe5-d673-4202-a7b9-0d950cea4e63)
