# [Java的一些基础知识点复习](https://github.com/QiYongchuan/MyGitBlog/issues/83)

**方法的重载 overload**

定义：一个类中方法名字相同，但是参数列表不同的方法。
> 注意：重载的方法，就是不同的方法，只是名称相同而已。
* 形参的数量不同
* 形参的类型不同
均可以构成方法的重载（也就是说是不同的方法）

```
    static void add(){
        
    }
    static void add(int a,int b)
    {
        System.out.println(a+b);
    }
    static void add(double a,double b)
    {
        System.out.println(a+b);
    }
```

> 当返回值不同时，但形参形同时，无法构成  
```
   static int add(int a,int b,int c){
        System.out.println(a+b+c);
        return a+b+c;
    }
    static double add(int a,int b,int c){
        System.out.println(a+b+c);
        return a+b+c;
    }
```

---

Java中的基本数据类型


byte: 8位有符号的补码整数，范围为-128到127。
short: 16位有符号的补码整数，范围为-32768到32767。
int: 32位有符号的补码整数，范围为-2^31到2^31-1。
long: 64位有符号的补码整数，范围为-2^63到2^63-1。
float: 单精度32位IEEE 754浮点数。
double: 双精度64位IEEE 754浮点数。
boolean: 逻辑类型，只能取两个值之一：true或false。
char: 单个16位Unicode字符，范围为'\u0000'到'\uffff'。

整数：byte、short、int、long
浮点数：float、double
字符：char
逻辑：boolean