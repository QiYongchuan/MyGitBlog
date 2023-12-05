# [JSP学习笔记](https://github.com/QiYongchuan/MyGitBlog/issues/2)

## 1.如何配环境
“你是免费的还是付费的？” ---如何用社区版IntelliJ IDEA创建Servlet项目

当我开始认真的读文档自己学jsp时，才想起了Javaweb课上老师面对我们各种各异的报错，重复问出的一句话：“你是免费的还是付费的？”

课上稀里糊涂的配置过去，下次上课代码出不来时，老师依然重复同样的问题。直到我现在从头开始建一个Servlet项目时，我才意识到问题的严重性：

Servlet项目本质上不能在inteilj community edit 版（也就是免费版）上创建啊！

![image](https://user-images.githubusercontent.com/105039020/233590254-3bf1549a-fc96-47f0-b867-372fa4724cd0.png)

![image](https://user-images.githubusercontent.com/105039020/233590599-46eb29ab-4878-4bd7-b6ab-bbdec202344d.png)
| 来自官网的直接否定

所以问题的本质是：免费的就是不能直接创建servlet项目，要么选择付费版的，要么选择其他编译器：比如[Eclipse](https://eclipse.org/)。 

但是总有人，因为各种原因<del>（我主要是没钱）</del>就是想用免费版的创建Servlet项目，那也没问题

![image](https://user-images.githubusercontent.com/105039020/233592842-02de5684-095e-4605-af53-3570c6194fc2.png)

英文文档没找到好的解决办法，~~真编程还得是中文，英文也就图一乐~~

找到一篇很详细的中文博客：[[IDEA Community(社区版)+maven创建Java web项目并配置Tomcat全过程](https://www.cnblogs.com/Luquan/p/12273595.html)

注意的是，在创建项目时，我的intellij 上不能直接创建meaven项目，而是左侧的Maven Archetype，右边选择时，与参考博客中不同的是只有一个webapp可选，选这个就可以，其余步骤均参考上面博客就可以。
![image](https://user-images.githubusercontent.com/105039020/233635542-533c4fcd-34e1-49a4-bd0f-c14a1f2b2f3e.png)


创建成功之后，添加selvlet类，点击运行后，经典404
检查后发现是web.xml出错，
![image](https://user-images.githubusercontent.com/105039020/233636456-4227ab0d-5e79-4c5e-a92d-a813d5ce98e7.png)

这里需要对应。

当然在实验课上也出现过很多次经典404，但当时纯属黑盒调试，重启大法换电脑，纯纯玄学调试，不知道哪里错了：）

![image](https://user-images.githubusercontent.com/105039020/233638376-82e52099-00f1-49e4-93e2-3e571d43a9b8.png)


至此，第一部分创建项目到这里结束。但似乎还不算开始，一套操作猛如虎，一看进度刚配好环境：）

---

## 2.开始第一个项目

上一条笔记主要是搭建起来了环境，但是并没有实现起功能来，搞的那个servlet也并没有用上。这一条的目标是建立一个“交互”的项目，用上servlet。

在手册中，介绍说建一个这样的项目就需要三个文件的：

> One important point to note – for any servlet program, you need 3 files – index.html file, Java class file, and web.xml file. 

一个展示的html页面，java控制逻辑的，一个是控制跳转路径的

于是按照手册，无脑复制了三个代码，如下：
![image](https://user-images.githubusercontent.com/105039020/233785004-51d62659-8f55-4b49-83e2-23d77b7d7e69.png)
![image](https://user-images.githubusercontent.com/105039020/233785032-57199109-ab6c-4cab-bc7c-c27be4381534.png)
![image](https://user-images.githubusercontent.com/105039020/233785049-b712baa6-bb87-4f16-822c-be55c07cba46.png)

问题不是很大，其中某个类没有引入爆红时，ALT+Enter 然后选择从Meaven中自动引入就可以解决。

但是还有一个比较大的问题是这些都是Java代码，但Java中各种方法的重写等等已经记得很模糊了，这部分前置知识是需要快速补一补的。<del>会很快补起来的吧，要不然debug太难受了，只能先无脑丢给GPT了</del>

实现的效果是进行了小小的交互，页面输入后，判断一下，输出一个结果。

![image](https://user-images.githubusercontent.com/105039020/233785253-44ce0b91-5a6d-42b4-80ad-201a579387ab.png)
![image](https://user-images.githubusercontent.com/105039020/233785269-73d7ac21-500d-408a-8215-bb582b87b291.png)

有些不懂，丢给GPT，得到注释：

```
package Edureka; // 定义了这个Java类的包名。这个类属于Edureka包。
import java.io.IOException;
import java.io.PrintWriter;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class Login extends HttpServlet { // 定义一个名为Login的类，继承了HttpServlet类。
    
    // 定义了一个名为doPost的方法，它接受HttpServletRequest和HttpServletResponse两个参数，并可能抛出ServletException和IOException异常。这个方法在接收到来自客户端的POST请求时被调用。
    protected void doPost(HttpServletRequest req, HttpServletResponse res) throws ServletException,IOException {
        
        PrintWriter pw = res.getWriter(); // 创建一个PrintWriter对象pw，用于向客户端输出响应。
        res.setContentType("text/html"); // 设置响应的内容类型为text/html，表示响应的内容是HTML格式的。
        
        String user = req.getParameter("userName"); // 从HTTP请求中获取名为userName的参数，并将其存储在名为user的字符串变量中。
        String pass = req.getParameter("userPassword"); // 从HTTP请求中获取名为userPassword的参数，并将其存储在名为pass的字符串变量中。
        
        if (user.equals("edureka") && pass.equals("edureka")) { // 根据user和pass的值进行用户验证。如果user和pass都等于"edureka"，则向客户端输出"Login Success...!"，否则输出"Login Failed...!"。
            pw.println("Login Success...!");
        } else {
            pw.println("Login Failed...!");
        }
        pw.close(); // 关闭PrintWriter对象pw，释放资源。
    }
}
```

解释index页面


```
<html>
<body>
<h2>Hello World! is you?</h2> <!-- 在HTML页面中显示一个标题“Hello World! is you?” -->
<form action="Login" method="post"> <!-- 定义一个表单，它的**提交地址是“Login”**，提交方式是POST -->
<table> <!-- 创建一个HTML表格 -->
<tr>
<td>Name:</td> <!-- 表格中的一行，包括一列标签“Name:” -->
<td><input type="text" name="userName"></td> <!-- 表格中的一行，包括一列用于输入文本的输入框。输入框的名称为“userName”。 -->
</tr>
<tr>
<td>Password:</td> <!-- 表格中的一行，包括一列标签“Password:” -->
<td><input type="password" name="userPassword"></td> <!-- 表格中的一行，包括一列用于输入密码的输入框。输入框的名称为“userPassword”。 -->
</tr>
</table>
<input type="submit" value="Login"> <!-- 创建一个提交按钮，用于将表单中的数据提交给服务器。**按钮的名称为“Login”**。 -->
</form>
</body>
</html>

```

解释web.xml页面
```

<!DOCTYPE web-app PUBLIC "-//Sun Microsystems, Inc.//DTD Web Application 2.3//EN"
 "http://java.sun.com/dtd/web-app_2_3.dtd" > <!-- 定义了一个DOCTYPE声明，用于指定当前XML文档使用的DTD版本。 -->

<web-app> <!-- 定义了一个web应用程序 -->
  <display-name>Archetype Created Web Application</display-name> <!-- 指定了web应用程序的显示名称 -->
  
  <servlet> <!-- 定义了一个servlet -->
    <servlet-name>Login</servlet-name> <!-- 指定servlet的名称 -->
    <servlet-class>Edureka.Login</servlet-class> <!-- 指定servlet的Java类 -->
  </servlet>
  
  <servlet-mapping> <!-- 定义了servlet的映射 -->
    <servlet-name>Login</servlet-name> <!-- 指定servlet的名称 -->
    <url-pattern>/Login</url-pattern> <!-- 指定servlet处理的URL路径 -->
  </servlet-mapping>
  
  <welcome-file-list> <!-- 定义了欢迎页面列表 -->
    <welcome-file>index.html</welcome-file> <!-- 指定了欢迎页面的文件名 -->
  </welcome-file-list>
  
</web-app>
```

![image](https://user-images.githubusercontent.com/105039020/233785713-ec41641e-f9b5-46f2-b875-4e57f3fc4a00.png)

## 根据手册，继续添加新的东西

添加一个index.html页，以及添加新的servlet和更新web.xml

![image](https://user-images.githubusercontent.com/105039020/233789026-2c6a8e90-c36b-4ad0-8892-9ba03ccf1e6c.png)
但是这里继承的类变了

```
package Edureka;

import java.io.*;
import javax.servlet.*;
public class generic extends GenericServlet{
    public void service(ServletRequest req,ServletResponse res) throws IOException,ServletException{
        res.setContentType("text/html");
        PrintWriter pwriter=res.getWriter();
        pwriter.print("<html>");
        pwriter.print("<body>");
        pwriter.print(
                        "<h2>Generic Servlet Example</h2>"
                );
        pwriter.print("Welcome to Edureka YouTube Channel");
        pwriter.print("</body>");
        pwriter.print("</html>");
    }
}

```
以及web.xml中的变化，新写一个servlet以及mapping，但是web-app标红报错，但没影响功能

```
<!DOCTYPE web-app PUBLIC
 "-//Sun Microsystems, Inc.//DTD Web Application 2.3//EN"
 "http://java.sun.com/dtd/web-app_2_3.dtd" >

<web-app>
  <display-name>Archetype Created Web Application</display-name>
  <servlet>
    <servlet-name>Login</servlet-name>
    <servlet-class>Edureka.Login</servlet-class>
  </servlet>
  <servlet-mapping>
    <servlet-name>Login</servlet-name>
    <url-pattern>/Login</url-pattern>
  </servlet-mapping>
  <welcome-file-list>
    <welcome-file>index.html</welcome-file>
  </welcome-file-list>
  <servlet>
    <servlet-name>generic</servlet-name>
    <servlet-class>Edureka.generic</servlet-class>
  </servlet>
  <servlet-mapping>
    <servlet-name>generic</servlet-name>
    <url-pattern>/welcome</url-pattern>
  </servlet-mapping>
</web-app>
```
新建的index.html页，然后注意 配置文件中有一行代码：
```
  <welcome-file-list>
    <welcome-file>index.html</welcome-file>
  </welcome-file-list>
```
![image](https://user-images.githubusercontent.com/105039020/233789345-550a19c7-efac-4d4d-8274-bb20e5e65f23.png)


实现的效果：

点击首页超链接之后跳转到欢迎页




---

## 新的内容：Servlet and JSP Tutorial: Session Tracking

为什么要用session，这是干什么的？

> Session simply means a particular interval of time. Session tracking is a technique to maintain state (data) of a user also known as session management in servlet. So, each time user requests to the server, the server treats the request as the new request.

Below figure depicts how each request from the client is considered as a new request.

![image](https://user-images.githubusercontent.com/105039020/233839349-40a266c5-83ee-43df-b33c-22d63f00c19a.png)

In order to recognize the particular user, we need session tracking. Now let’s move further and see one of the techniques of session tracking i.e. Cookies.

## Servlet and JSP Tutorial: Cookies
A cookie is a small piece of information that is persisted between the multiple client requests. A cookie has a name, a single value, and optional attributes such as a comment, path and domain qualifiers, a maximum age, and a version number.

![image](https://user-images.githubusercontent.com/105039020/233839503-5ea5f381-ac66-40b8-918d-4a7dc5c51e07.png)

In this, we add a cookie with the response from the servlet. So the cookie is stored in the cache of the browser. After that, if a request is sent by the user, a cookie is added with the request by default.

Let’s see an example of creating a cookie, adding the response and retrieving the results. Here I will be writing 2 java class files i.e MyServlet1 and MyServlet2.
新建两个类来理解




---

## 插曲 第一次用git 回退

继续写新的功能时，死活写不出来了。想把刚写的全部删掉，回到上一次的版本。 如何操作呢？ 

git log 查看上次提交的记录

![image](https://user-images.githubusercontent.com/105039020/233843054-a47e20c4-ce7b-4b93-83c1-429c06156442.png)

然后 git checkout b335e0d5f353a3c32ae9b55a84783e946082cc81 
就可以了。

但是似乎可以新建一个分支写，等等，继续尝试一下把。 

如果git checkout 出问题了，就直接强制回退了
git checkout -f b335e0d5f353a3c32ae9b55a84783e946082cc81 


**emmm，玩砸了！ 上面的没问题，成功回退回去了，但是玩了玩分支，没玩明白，再次回退失败，彻底凉凉，直接回到刚建项目的蛮荒之地了**

![image](https://user-images.githubusercontent.com/105039020/233845465-f7b579b0-022f-4fe8-adf0-4888704c8a56.png)

累了，幸亏写笔记了：）