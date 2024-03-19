# [SpringBoot学习笔记：拦截器](https://github.com/QiYongchuan/MyGitBlog/issues/91)

**拦截器（Interceptor）是用来拦截进入Controller方法之前或之后的请求的。
它们常用于日志记录、身份验证、权限检查、或者添加通用的请求或响应的头信息等场景。**

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/1bdc09ec-ce55-4cf0-9c4e-684795045958)

用的最多的是preHandle


简单使用：

1.创建拦截器

```
public class LoginInterceptor  implements HandlerInterceptor {
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        System.out.println("登录拦截器");
        return true;
         //  其中request对应的就是前端的请求
//        if (request.getSession().getAttribute("user") == null)
//            return false;
//        else if (request.getSession().getAttribute("user") != null) {
//            return true;
//        }   可根据条件来判断
    }
}
```

2.注册拦截器

```
@Configuration   //注明是配置类
public class WebConfig implements WebMvcConfigurer {
    @Override     // 添加拦截器,将我们之前写的拦截器注册，添加拦截的路径，使其生效
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(new LoginInterceptor()).addPathPatterns("/user/**");

        registry.addInterceptor(new LoginInterceptor());  //也可以不添加拦截的路径，这样默认所有的都拦截

        // 拦截之后就是调用LoginInterceptor的preHandle方法
    }
}
```

---

详细介绍

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/3f2f4cad-c230-4f32-98f3-93c2d7c014e0)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/b42e846a-2c36-4684-883f-a857746134e8)
