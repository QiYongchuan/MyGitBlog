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
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/2dc7996c-fe8f-4f7b-af09-a08ab3a474f3)


整数：byte、short、int、long
浮点数：float、double
字符：char
逻辑：boolean

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/cf6c2442-f05b-4232-9153-c7c0ba2053f6)


基本数据类型的默认值如下：

byte: 0
short: 0
int: 0
long: 0L
float: 0.0f
double: 0.0d
boolean: false
char: '\u0000'

补充：所有的引用类型则是null

---

OOP 面向对象编程

面向过程：适合简单、不需要协作的事务，重点关注如何执行
> 类比，如何把大象装进冰箱，1、2、3步，一步一步的执行，不需要过多的协作，一步一步就可以了

面向对象：宏观上把握，整体上分析整个系统；但具体到实现部分的操作的时候，仍然需要一步一步的考虑，也就是面向过程了。

两者是相辅相成，不可分开的：
* 宏观上：通过面向对象进行整体涉及
* 微观上：执行和处理数据，仍然是面向过程

具体概念

对象和类
类class是模板，是图纸，对象object（instance实例），对象是具体的体现，是实例。


类有三个成员：**属性（field，也称为成员变量）、方法method、构造器constructor**

属性即静态的数据，方法是动态的行为

属性（file 成员变量）：用于定义该类或该类的对象包含数据，或者说静态特征，作用范围是整个类体，在定义成员变量时可以对其初始化，如果不对其初始化，java采用默认值对其初始化。



方法：用于定义该类或该类实例（对象）的行为特征和功能实现的。方法是类和对象行为特征的抽象。
因为在面向对象中，整个程序的基本单位是类，所以方法是从属于**类**和**对象**的。

```
public class Student {
    int id;
    int age;
    String name;

    public void study(){
        System.out.println("I am studying");
    }
    public void sleep(){
        System.out.println("I am sleeping");
    }

//实现一个对象，实例化一个对象，利用的是编译器自动生成构造函数 Study(){}
 public static void main(String[] args) {
        Student st1 = new Student();
        st1.id = 100;
        st1.age = 20;
        st1.name = "John";
        st1.study();
        st1.sleep();
    }
}
```

简单内存分析（帮助理解面向对象）：

图

**构造方法（构造器constructor）**
构造器用于对象的初始化，而不是创建；
> 构造方法是装修房子，而不是创建房子

创建对象的四步：
1. 分配对象空间，并对对象成员变量初始化为0或者空
2. 执行属性值的显式初始化（即如果一开始的属性值给赋值后，就执行显示初始化，而不是默认值）
3. **执行构造方法**
4. 返回对象的地址给相关的变量

构造器（构造方法）的四个要点：
* 构造器通过new 关键字调用
* 不能在构造器中使用return返回某个值；构造器有返回值，但不能定义返回的类型的（返回值的类型肯定是本类）
* 如果没有在类中定义构造器，编译器会自动定义一个无参的构造方法；如果已经定义了，就不会添加。
* 构造器的方法名必须和类名是一致的。

```
public class Point {
   double x,y;

     Point(double i, double j) {
          x = i;
          y = j;
    }
```
构造方法重载

```
public class User {
    int age;
    String name;
    int pswd;

    public User(int age, String name, int pswd)
    {
        this.age = age;
        this.name = name;
        this.pswd = pswd;
    }
    public User()
    {
    }
```


---

OOP 面向对象编程

面向过程：适合简单、不需要协作的事务，重点关注如何执行
> 类比，如何把大象装进冰箱，1、2、3步，一步一步的执行，不需要过多的协作，一步一步就可以了

面向对象：宏观上把握，整体上分析整个系统；但具体到实现部分的操作的时候，仍然需要一步一步的考虑，也就是面向过程了。

两者是相辅相成，不可分开的：
* 宏观上：通过面向对象进行整体涉及
* 微观上：执行和处理数据，仍然是面向过程

具体概念

对象和类
类class是模板，是图纸，对象object（instance实例），对象是具体的体现，是实例。


类有三个成员：**属性（field，也称为成员变量）、方法method、构造器constructor**

属性即静态的数据，方法是动态的行为

属性（file 成员变量）：用于定义该类或该类的对象包含数据，或者说静态特征，作用范围是整个类体，在定义成员变量时可以对其初始化，如果不对其初始化，java采用默认值对其初始化。



方法：用于定义该类或该类实例（对象）的行为特征和功能实现的。方法是类和对象行为特征的抽象。
因为在面向对象中，整个程序的基本单位是类，所以方法是从属于**类**和**对象**的。

```
public class Student {
    int id;
    int age;
    String name;

    public void study(){
        System.out.println("I am studying");
    }
    public void sleep(){
        System.out.println("I am sleeping");
    }

//实现一个对象，实例化一个对象，利用的是编译器自动生成构造函数 Study(){}
 public static void main(String[] args) {
        Student st1 = new Student();
        st1.id = 100;
        st1.age = 20;
        st1.name = "John";
        st1.study();
        st1.sleep();
    }
}
```

简单内存分析（帮助理解面向对象）：

图

**构造方法（构造器constructor）**
构造器用于对象的初始化，而不是创建；
> 构造方法是装修房子，而不是创建房子

创建对象的四步：
1. 分配对象空间，并对对象成员变量初始化为0或者空
2. 执行属性值的显式初始化（即如果一开始的属性值给赋值后，就执行显示初始化，而不是默认值）
3. **执行构造方法**
4. 返回对象的地址给相关的变量

构造器（构造方法）的四个要点：
* 构造器通过new 关键字调用
* 不能在构造器中使用return返回某个值；构造器有返回值，但不能定义返回的类型的（返回值的类型肯定是本类）
* 如果没有在类中定义构造器，编译器会自动定义一个无参的构造方法；如果已经定义了，就不会添加。
* 构造器的方法名必须和类名是一致的。

```
public class Point {
   double x,y;

     Point(double i, double j) {
          x = i;
          y = j;
    }
```
构造方法重载

```
public class User {
    int age;
    String name;
    int pswd;

    public User(int age, String name, int pswd)
    {
        this.age = age;
        this.name = name;
        this.pswd = pswd;
    }
    public User()
    {
    }
```


---

JVM虚拟机内存模型
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/df7b1df1-6352-437a-bb35-51a05b806e67)

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/2d5f486c-1da0-4671-832b-66a4f2633acb)
```
注意这里：
People p2 = p1   //执行的是将p1堆中的地址给了p2，

而
People p2 = new People()  则是实现了在堆中新建一个地址区

```
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/4cf5a2e7-0496-4493-91d9-ebb55e3ef8ca)

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/8145b950-bdd6-406c-a9a3-8c9098a6f479)
