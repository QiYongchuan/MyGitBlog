# [Java的一些基础知识点复习](https://github.com/QiYongchuan/MyGitBlog/issues/83)

**方法的重载 overload**

定义：一个类中方法名字相同，但是参数列表不同的方法。
> 注意：重载的方法，就是不同的方法，只是名称相同而已。
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/43049d4c-3ac2-4c06-9c3a-631973c2d9a4)


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
**方法的调用机制**
* 当程序执行到方法时，会在栈中单独开一个空间（栈空间）
* 执行完毕，或者执行到return语句后，就会返回到 **调用方法的地方**
* 同理，main方法栈执行完毕之后，栈空间也会回收，整个程序退出

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/f6d6fb3a-07e1-4b87-85bc-f776e64eaa93)




**方法的传参**
* 基本数据类型传参：形参不影响实参的传递（本质上栈中main方法区与swap方法区是两个区，两者不会相互影响）
* 引用数据类型传参：传递过程传递的其实是地址，所以栈方法指向的空间和main主方法指向的空间是一致的
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/3b3a049a-b833-4856-9781-fcaf129b8274)





**可变参数**

Java中允许同一个类中多个**同名** **同功能**但是**参数个数不同**的方法，封装成一个方法。

==>对方法重载的一种优化，不用因为参数个数不同而写多个方法了
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/a287a282-f311-40a2-84ca-37850136dafb)

可以把传入的参数nums  视为数组
```
    public int getSum(int... nums) {
        System.out.println("参数的个数" + nums.length);
        int tolNums = 0;
        for (int i = 0; i < nums.length; i++) {

            tolNums += nums[i];
        }
        return tolNums;
    }
```

* 可以直接传递一个数组
* 可变参数可以和普通类型参数放在一起传参，但是必须保证可变参数放在最后
* 一个形参列表只允许出现一个可变参数，不可以多个可变参数一块。

---

**Java中的基本数据类型**


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

**数据类型转换**

* 自动类型转换：精度低的向精度高的类型转换
* 强制类型转换：精度高的向精度低的转换

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/f69b69be-cafd-4ff3-b088-954c0d227967)
```
public static void main(String[] args) {
        int num = 'a';  //   char --> int 97
        double d1 = 80;  // double -->  80.0

        System.out.println(num);
        System.out.println(d1);
    }
```
注：
1.混合多种类型时，转换为最高的类型
2.（byte,short)和char之间不会相互自动转换
3.byte,shoort,char 他们三者可以计算，计算时首先转化为int 再计算；另三种无论是单独还是混合都会提升。（精度提升到int） 

强制类型转化：
* 数据精度丢失
* 数据溢出造成不可知的数
```
int a = (int)1.9;
        System.out.println(a); //1   直接丢失了小数部分

        int n = 2000;
        byte b = (byte)n;    // 超出byte127的范围，会造成数据溢出
        System.out.println(b);   //-48
```
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/7e091bce-8b18-43b6-ba3d-ec39b6fdeb50)

**基本数据类型与String类型的转换**
* 基本数据类型转字符串：直接用+连接就可以
* String转为基本数据类型：通过基本数据类包装类调用parseXX方法
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/eb970fe4-24d1-4206-86e8-9ab31f5efbdc)
注：String转char时，是charAt(0),即转为String的第一个值。
注意：
* Sring 转化为数字时，只有String的内容是数字才可以转化，比如”123“，但是”123hi“ 或”hello"都不可以转
* 

---

OOP 面向对象编程

面向过程：适合简单、不需要协作的事务，重点关注如何执行
> 类比，如何把大象装进冰箱，1、2、3步，一步一步的执行，不需要过多的协作，一步一步就可以了

面向对象：宏观上把握，整体上分析整个系统；但具体到实现部分的操作的时候，仍然需要一步一步的考虑，也就是面向过程了。

两者是相辅相成，不可分开的：
* 宏观上：通过面向对象进行整体涉及
* 微观上：执行和处理数据，仍然是面向过程

具体概念

对象和类：类class是模板，是图纸，对象object（instance实例），对象是具体的体现，是实例。


类有三个成员：**属性（field，也称为成员变量）、方法method、构造器constructor**

属性即静态的数据，方法是动态的行为

属性（file 成员变量）：用于定义该类或该类的对象包含数据，或者说静态特征，作用范围是整个类体，在定义成员变量时可以对其初始化，如果不对其初始化，java采用默认值对其初始化。



**方法：**用于定义该类或该类实例（对象）的行为特征和功能实现的。方法是类和对象行为特征的抽象。
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


![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/02ddcb29-bb58-4501-bb9f-c5d2d61ce051)


**构造方法（构造器constructor）**
why ?
> 在创建的同时进行赋值
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/501f6357-bd91-473f-a380-b3bf9db52dbc)
如果不写，则是默认的系统指定的无参构造器，无法在创建的时候进行赋值，只能等创建完成之后，再赋值；一旦构建了有参构造器后，默认的构造器就会被覆盖了，如果想用就必须再创建一个默认的无参构造器。
```
class Person{
    String name;
    int age;
   public Person(String name1,int age1){
       System.out.println("Constructor 被调用");
        name = name1;
        age = age1;
    }
    public Person(){
        System.out.println("默认构造函数被调用");
    }
}
```

构造器用于对象的初始化，而不是创建；
> 构造方法是装修房子，而不是创建房子

* 方法名与类名相同
* 在创建对象时，系统自动调用该类的构造器完成对象的初始化。

创建对象的四步：
1. 分配对象空间，并对对象成员变量初始化为0或者空
2. 执行属性值的显式初始化（即如果一开始的属性值给赋值后，就执行显示初始化，而不是默认值）
3. **执行构造方法**
4. 返回对象的地址给相关的变量

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/892c8e3a-9db9-4131-ac6c-c689aee8c229)



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

对象创建流程详解：

1. 加载类（Perseon.class）信息，只会加载一次
2. 在堆中分配内存空间（地址）
3. 在完成对象初始化
   * 3.1 默认初始化 age=0 name=null
   * 3.2 显式初始化 age=90 name=null
   * 3.3 构造器初始化 age=20，name=小倩
 4. 将对象在堆中分配到的内存地址，返回给p（p，就是对象名，也就是说是对象的引用）





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

```
 public static void main(String[] args) {
  
        People p1 = new People();
        p1.age = 10;
        People p2 = p1;
        System.out.println(p2.age);  //10
        p2.age = 20;
        System.out.println(p1.age);  //20
    }

本质：两者是同一个引用地址
```

垃圾回收：

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/84c6119e-db9a-40fa-b11b-f062fc1e9e00)
为什么  b.age 会报错？

将b设置为null，断开了b与Person对象的连接。在Java中，设置为null意味着引用不再指向任何对象，但由于a仍然指向那个对象，所以那个对象不会被垃圾回收器回收。

尝试打印b.age，但是会抛出NullPointerException，因为b已经被设置为null，不再指向任何对象。
```
System.out.println(b.age); // 抛出NullPointerException
```
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/20a75a87-f038-4adf-b019-1b956407cf99)


区分：

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/b8c15a82-e74a-44fd-b9be-e4de8894915a)

这里p=null指向空，栈中test200中的p空了，但是main中的p.age依然指向原来的地址（堆中的地址p）

---

**作用域**
变量的范围。
Java中变量一般分为：属性和成员方法中的变量，即分别是全局变量和局部变量。
* 全局变量==>类的属性（成员变量），可以在整个类体中使用
* 局部变量：出来属性之外的其它变量，作用域为定义它的代码块。
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/24202f73-54fd-4496-89c7-d477906583a2)

补充：
* 全局变量可以不赋值，此时为默认值
* 局部变量必须赋值才可以适应，因为没有默认值

区别：

* 全局变量可以被本类使用，或者被其它类使用（通过对象来调用）
* 局部变量：只能在本类中对应的方法中使用
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/6c1bb3a7-bf3e-4ec8-a9d4-f842a604373b)

修饰符:
* 全局变量前面可以加修饰符
* 局部变量不可以加修饰符


---

**this关键字**
why？
区分当前类的属性和局部变量而引入。

* 哪个对象调用，就代表哪个对象（”我的“）
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/a940ab0b-06f0-40f8-a12f-451df2c4e959)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/1734d227-043d-488e-950b-6b5f9de204d4)

```
//访问成员方法的语法  this.f
class T{
    public void f1(){
        System.out.println("f1（） 方法");
    }
    
    public void f2(){
        System.out.println("f2（） 方法");
        
        //调用本类的f1（）方法
        //第一种方式
        f1();
        //第二种方式
        this.f1();
    }
}

```

构造器中使用this
注：仅限在构造器中使用，且this要放在第一条语句
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/6ae8d7a1-1517-4558-a341-4255df979f18)

this访问属性的区别：
如果没有this时，在成员方法中访问属性时采用就近原则（即有局部变量先访问局部变量，没有时访问全局变量），但是有this时，就只访问全局变量了。
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/1fdd9a53-85f9-442a-ac54-118718eacfa4)


![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/fcc2279c-0af0-4529-9bfb-1f2c770d9c31)
答案10，9，10
涉及匿名对象，创建之后就销毁了
以及count++ 是后加加，先输出之后，后加

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/aca07fe3-b57b-4376-a9e2-f96e57002bc1)


---

**包 package**
why?
包的三大作用：
* 区分相同名字的类
* 当类很多时可以很好的管理类
* 控制访问范围

本质：创建不同的文件夹/目录，来保存文件
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/067ea62a-c286-42b8-a05b-0deb2890f9fa)

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/21793574-3003-4931-9c4f-23903123d0f9)


---

**访问修饰符**
用于控制方法和属性（成员变量）的访问权限（访问范围）。

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/3806f0b1-6879-4d4a-a745-1d82bbc4f5f2)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/7158b4d5-14df-4907-b342-8238ea888315)


* 修饰符修饰方法、属性、和类
* 只有public和默认可以修饰类


---

**封装**
面向对象的三大特征：封装、继承、多态
封装：把抽象出来的数据（属性）和对对象的操作（方法）封装在一起，数据被保护在内部，程序的其它部分只有通过被授权的操作（方法），才能对数据进行操作。

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/ec3c0ea8-02a7-4372-8129-9c7af90c1524)

如何实现？
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/1c621e9f-9b59-45e1-b9ff-cb6229b12cc4)
   
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/c2135ab4-231e-4018-993a-932cd6e7bcbc)


**构造器与setxx**

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/f6ffabaa-6810-44d9-ba1b-c6c2c5c7c2b5)
因为当只写构造器时，可以在初始化时直接赋值，这样就绕过了set设置的规则；此时如果想继续保证set的效果，就将构造器与set结合，在构造器中调用set，这样即使是初始化赋值给的值不符合要求，就无法绕过set了。
