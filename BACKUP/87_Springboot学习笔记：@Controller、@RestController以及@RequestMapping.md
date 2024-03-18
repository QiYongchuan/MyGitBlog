# [Springboot学习笔记：@Controller、@RestController以及@RequestMapping](https://github.com/QiYongchuan/MyGitBlog/issues/87)

### 1.@Controller与@RestController

涉及MVC模型：

##### MVC模型

* M：model，模型层，和数据库打交道。《==MyBatis
* V：view，视图层。用户看到的页面结果。 《== Thymeleafs模板语言/前后端分离项目中返回的数据（多是JSON)
* C：controller，控制层。实现业务逻辑：数据的处理和页面的跳转。《==Spring MVC

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/bda0a2d2-fe25-4057-b9f9-57b754b968ed)

控制器中两种注解：
##### @Controller与@RestController

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/478d0d60-2b56-4076-abf4-1a756425f494)

> 在前后端分离的项目中，后端主要往前端返回的是数据，所以用RestController，
> 而在前后端不分离的项目时，多用Controller返回的是页面，结合Thymeleaf使用的，此时是返回页面，寻找的是页面。

@Controller  是返回页面和数据的，当我们只用Controller的时候，默认是找的页面，比如下面是找hello页面了（前后端 不分离的项目）
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/087ac14c-138d-4a4f-8d55-123043e33a88)

如果想返回数据，而不是页面呢？ 
需要加上@RequestBody

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/eb42e352-fcc6-4699-82fc-0e3ab8fdd84f)

##### @RestController=@Controller和@ResponseBody的结合

当你使用@RestController注解时，Spring会自动处理你的类中的所有方法，使其返回的数据直接作为HTTP响应的正文返回给客户端，而不需要你在每个方法上单独标注@ResponseBody。

@RestController注解是@Controller和@ResponseBody的结合，这意味着它既将类标记为控制器，又表明类中的所有方法都会自动以@ResponseBody的方式处理。这使得@RestController非常适合用于构建RESTful API，其中所有的响应都是数据（如JSON或XML），而不是视图或模板页面。

这种方式简化了开发过程，因为你不需要在每个方法上重复使用@ResponseBody注解，从而让代码更加简洁和直观。总的来说，如果你的应用主要是服务于HTTP API的，使用@RestController会更方便。

前后端分离项目中，主要使用的就是:**@RestController**