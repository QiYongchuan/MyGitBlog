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

补充扩展：

* 如何在object中存储一个方法调用自己的属性呢？
* 如何将这个方法序列化存储到localstroge中呢？

对象中存储方法调用自己的属性
```
const score = {
  lose: 0,
  win: 0,
  get score() {
    return this.win - this.lose;
  }
}

调用：
 document.querySelector('#score').innerHTML = `${score.score}`;

直接object.属性名  就可以直接调用

```

对象中方法序列化存储到localstorage中：
无法实现：可以存储状态，再根据状态转换

> 要通过localStorage存储对象中的方法（例如get score()）是不直接可能的，因为localStorage只支持字符串类型的数据。当你尝试将对象序列化为字符串（使用JSON.stringify()）时，对象中的方法（包括get和set访问器属性）将不会被序列化。这意味着当你从localStorage中检索数据并反序列化（使用JSON.parse()）时，这些方法将不会被恢复。
> 
> 如果你的目标是保持score对象的状态（即win和lose属性的值），同时能够在页面加载时恢复这些值并重新应用get score()方法来计算分数，你可以采用以下步骤实现：
> 
> 序列化和存储状态：只存储对象的状态（即非函数属性），而不是整个对象。
> 
> 读取和反序列化状态：从localStorage读取状态，并使用这些状态值创建一个新的对象，该对象包含相应的方法。

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



---

**object 的auto-boxing**
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/2fa70c50-573a-4956-896f-1dd448391c30)
上述例子中，字符串也有对象的方法，这是因为JavaScript自动将字符串包裹着一个像盒子一样的对象中，来实现的。
这一过程就被称为自动装箱。

同样适用于数字类型和布尔类型，但对于null和undefined不适用
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/ab2988af-dad8-415a-9f47-b5b2dfada3fc)


---

**对象的引用  objects are references **  

* javascript中对象存储的是一个引用地址，即存储的是一个位置,而不是所有的信息。

```
  const object1 = {
      message: "hello object1",
    }

    const object2 = object1
    console.log(object1);
    console.log(object2);

    object1.message = 'hello,change'
    console.log('change 1');
    console.log(object1);
    console.log(object2);

    object2.message = 'hello,change2'
    console.log('change 2');
    console.log(object1);
    console.log(object2);
```
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/3eb4e147-c079-45c6-a8ce-f86e33c6f476)

> JavaScript 中的对象引用和赋值的知识点。在 JavaScript 中，当你将一个对象赋值给另一个变量时，**实际上是将对象的引用（内存地址）赋给了新的变量，而不是创建了一个新的对象。这意味着这两个变量实际上指向了同一个对象**，因此对其中一个变量所指向的对象进行修改，会影响到另一个变量所指向的对象。
> 
> 在这段代码中，object1 和 object2 都指向了同一个对象。当你修改 object1 的 message 属性时，object2 的 message 属性也会随之改变，因为它们实际上指向同一个对象。(也是同一个地址，所以object1===object2）
> 
> 这种行为在 JavaScript 中称为**对象引用**。如果你想要创建一个对象的独立副本，而不是引用，你需要使用深拷贝的方法来创建一个新的对象，而不是简单地将一个对象赋值给另一个变量。


** 对象的解构 **

可以直接使用快捷方式来获取，但注意{ } 里面的名称需要对应对象中的属性名称，否则无法解构。
```
  // const message = object3.message;
    const { message, price } = object3   //解构

    console.log(message);
    console.log(price);

```


---

**如何进行深拷贝，而不仅仅是复制引用呢？**

在 JavaScript 中，有几种方法可以实现深拷贝，其中包括使用对象展开运算符（spread operator）、Object.assign 方法、JSON.parse 和 JSON.stringify 方法，以及一些第三方库如 Lodash 的 _.cloneDeep 方法等。

```
// 使用对象展开运算符进行深拷贝
const originalObject = { a: 1, b: { c: 2 } };
const copiedObject = { ...originalObject };
copiedObject.b.c = 3;
console.log(originalObject); // 输出: { a: 1, b: { c: 2 } }
console.log(copiedObject); // 输出: { a: 1, b: { c: 3 } }

// 使用Object.assign方法进行深拷贝
const originalObject = { a: 1, b: { c: 2 } };
const copiedObject = Object.assign({}, originalObject);
copiedObject.b.c = 3;
console.log(originalObject); // 输出: { a: 1, b: { c: 2 } }
console.log(copiedObject); // 输出: { a: 1, b: { c: 3 } }

// 使用JSON.parse和JSON.stringify方法进行深拷贝
const originalObject = { a: 1, b: { c: 2 } };
const copiedObject = JSON.parse(JSON.stringify(originalObject));
copiedObject.b.c = 3;
console.log(originalObject); // 输出: { a: 1, b: { c: 2 } }
console.log(copiedObject); // 输出: { a: 1, b: { c: 3 } }
```