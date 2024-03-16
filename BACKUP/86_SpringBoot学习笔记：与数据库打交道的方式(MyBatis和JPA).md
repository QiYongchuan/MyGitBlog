# [SpringBoot学习笔记：与数据库打交道的方式(MyBatis和JPA)](https://github.com/QiYongchuan/MyGitBlog/issues/86)

> 之前的项目是用的Mybatis，新的项目是用到了JPA(Java Persistence API),两者均是跟数据库相关的，比较好奇两者的区别，整理部分资料。

### 为什么要用Mybatis或者JPA？

涉及到几个概念：

数据持久化和ORM
1.数据持久化：是指将内存中的数据保存到持久化存储（如数据库）中，以便数据在程序结束后仍然存在并可以再次被访问。

2.对象关系映射（ORM）：是一种在关系数据库和对象之间进行映射的技术，允许开发者使用面向对象的方式来操作数据库。ORM技术抽象了数据库操作的复杂性，开发者无需直接编写繁琐的SQL语句，即可进行数据操作。

**关系型数据库：**以ER（实体-关系）模型为基础，如MySQL、SQLServer、Oracle等。它们通过表结构（实体）、字段（属性）和表间关系（一对一、一对多、多对多）来组织数据，以及通过SQL语言进行数据的查询和操作。

*  实体：对应数据库中的表。
* 关系：表与表之间的连接，如一对一、一对多、多对多。
* 关系运算：如选择（查询特定条件的记录）和投影（选择特定列）。

**面向对象编程**：如Java、C++、Python等语言，它们通过类、对象、继承和多态等概念来组织和操作数据。

* 类：定义了对象的结构和行为。
* 继承与引用：允许类之间的关系和数据的重用。

使用ORM框架如MyBatis或JPA，可以高效地管理数据持久化过程和对象关系映射，同时降低数据库操作的复杂性。MyBatis提供了更细粒度的控制，通过手写SQL配合对象映射，适合对SQL性能和灵活性有高要求的场景。而JPA提供了一套更高层次的抽象，通过注解和JPQL（Java Persistence Query Language）来实现自动的SQL生成和查询，适合希望快速开发且不需要深入优化SQL的应用。

通过这种方式，开发者可以专注于业务逻辑的实现，而不是数据库操作的细节，提高开发效率和系统的可维护性。


### Mybatis和JPA之间的区别：

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/4e3c861f-2418-4ae3-b229-253c8a44accb)

这里我的理解是：
1.MyBatis更多的控制，尤其是可以直接写sql语句，而JPA则是封装成标准的控制方法了。
”MyBatis提供了对SQL的精细控制，而JPA则通过标准化的ORM模型来简化数据访问。“

2.分层设计：
 * JPA多一层service，实现数据库访问逻辑和业务逻辑的分开，代码结构更清楚
 * Mybatis则是访问逻辑和业务逻辑均放在Mapper层（DAO层）

### 在MVC中的体现

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/f724ece8-e56a-4fd8-8c20-8e6b5756b8e5)

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/6cb6191b-544a-4602-8e68-8ccbc4610a7e)


