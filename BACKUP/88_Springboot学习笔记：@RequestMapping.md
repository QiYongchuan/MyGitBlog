# [Springboot学习笔记：@RequestMapping](https://github.com/QiYongchuan/MyGitBlog/issues/88)

一句话介绍：@RequestMapping就是用来做路由映射的，即在Controller中，处理url地址以及前端发送的方法，进一步转到不同的方法中进行下一步的处理。

（补充：当然不仅限于URL路径，还可以设置（可选地）请求方法（如GET、POST等）、请求参数、请求头等条件）
```
@RequestMapping(value = "/users", method = RequestMethod.GET)
public List<User> getUsers() {
    // 方法体，返回用户列表
}

@RequestMapping(value = "/users", method = RequestMethod.POST, consumes = "application/json")
public User addUser(@RequestBody User user) {
    // 方法体，添加一个新用户
}

```

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/7eb5d7e0-83fe-4354-9206-1618ee109fc8)
1.@RequestMapping  默认post、get请求均可以，可以在后面写上具体的方法，也可以直接用另一种等价的写法：
@PostMapping 和@GetMapping

2. 用实体来接受形参时：注意请求发送的形式不同：请求体（body）和URL查询参数传递数据
具体可参考 #87 

```
 @RequestMapping("/Entiy")
    public String entity( User user){
        System.out.println(user);
        return "实体类接收参数";
    }
    @RequestMapping("/Entiy2")
    // 如果前端传递的参数是json格式的，
    // 那么可以使用@RequestBody
    public String entity2(@RequestBody User user){
        System.out.println(user);
        return "实体类接收参数Json";
    }
```

3.关于传参接收以及实体

#### 多个参数自动装箱（boxing）成一个JavaBean

* 什么是javaBean：一种特殊的Java类。
  * 所有的成员变量都是私有的private的
  * 有一个不带参数的构造函数
  * 通过一组get、set函数来读取或者修改属性的值
  * 以上可以通过右键-生成-来对应生成
* 实体Bean：EntityBean
  * 跟数据库的表可以实现一一对应
  * Bean的名字，与表的名字完成相同（Emp）
  * Bean中的属性名，与表的字段名相同（empno、ename、hiredate、sal）
  * 属性的类型，与表中字段的类型兼容
  * 实体Bean的一个实例（instance）对应数据库数据表中的一条记录



* JDO：Java Data Obiect ： java与关系数据库的关系
     *  Data：数据库中的内容，永久存在数据库中的。
  * Object：JAvaBean的实例，存放在内存中。
  * 持久化操作，将内存上的东西存入到数据库中

* 装箱过程
  * Step1：读取URL请求参数列表

```http
h5?empno=11&sal=1000&hiredate=2022-2-22
```

* setp2:如果函数形参是一个JavaBean，系统会自动调用该Javabean的一组set函数，来实现属性的赋值。这个过程称为自动装箱

```java
   @ResponseBody
    @RequestMapping("h5")
    public String h5(Emp emp)
    {
        return  "<h1>"+ emp + "</h1>";
    }
```

前提是该javaBean中有相应的属性
