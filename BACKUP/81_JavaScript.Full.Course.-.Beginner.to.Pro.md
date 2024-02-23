# [JavaScript Full Course - Beginner to Pro](https://github.com/QiYongchuan/MyGitBlog/issues/81)

Function
why we use function?
let us reuse code

return与parameter的区别
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/0f4ec351-3a90-49d3-a059-3b29ad179989)


存储在对象中的函数，也称为方法。
比如：console是对象，console.log则是方法（function）

内置对象 Json与localStorage

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/0db54f33-2378-4d33-beb3-b4a20eda82ed)


---

**Json与JavaScript的object的区别？**
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/c716aacc-91aa-41d3-b827-17ceeaf16c48)

* 两者写法类似，注意json只能用双引号
* json里面不能写函数，而JavaScript的object可以有
* json更通用，可以被其它语言理解，但JavaScript的object只被JavaScript能理解。
* json用于计算机之间的传输信息；
* 用于存储信息
* json在JavaScript中数据类型为string

---

**如何实现Json和object之间的转换？**

通过内置对象：
JSON.stringify(object)   ==> JavaScript object 转化为JSON
JSON.parse()              ===>   将JSON    转化为  JavaScript object

```
 const product = {
      'rating': {
        'start': 4.5,
        'rate': 87
      },
      fun: function function1() {
        console.log("funtion inside object");
      },
      price: 99,
      day: '1day'
    }


 const jsonString = JSON.stringify(product)
    console.log(jsonString);
```
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/c3516188-bc7f-4405-bd36-b508717f630e)

```
    const objectProduct = JSON.parse(jsonString)
    console.log(objectProduct);
```

---

**localStorage本地存储**

* 长期存储在浏览器中 ，相比之下sessionStorage生命周期更短，一次会话结束后失效
* localStorage 只能存储字符串，如果想存储object，需要先将object转化成Json（Json在JavaScript中的类型为string）
* localStorage.setItem('score',score)  存储值
* localStorage.getItem('score)  获取值
* localStorage.removeItem('score')  删除值

---

 **null 与undefined的区别？**
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/a4a8efff-3c86-481d-9577-fe569ed11765)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/74b0d106-61eb-4d2b-861e-82b49b917ea2)
* 两者均是false
* undefined 是默认值，而null就是null

