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


---

**继承**
why ？
当两个类的属性和方法很多是相同的时候，怎么办  ==》继承，提高代码复用性 、

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/a28378b8-49ce-4ac0-b31e-dfe1cc6ae5e6)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/7ea03a29-c239-4b43-a312-f8bd0d141add)

好处：
* 扩展性提高了
* 复用性提高了

继承细节点：
* 子类继承了所有的属性和方法，但是私有属性和方法不能在子类中直接访问，只能通过公共的方法去访问。
```
 private int n4 = 4;

    public int getN4() {
        return n4;
    }

  private void Test4(){
        System.out.println("Private Base Test3...");
    }
    public void callPrivate(){  // 私有方法也可以使用公共方法调用
        Test4();
    }
```

* 创建子类对象时，必须调分类的构造器，先完成父类的初始化

>在子类创建时，子类的构造器默认调用了super（）方法：本质是调用父类的无参构造器。

*当创建子类时，无论调用子类的哪一个构造器，默认情况下总会调用父类的无参构造器；
* 如果父类没有无参构造器，就必须在子类构造器中用super指定使用父类的哪个构造器完成对父类的初始化工作，否则无法编译通过。
* 如果希望调用父类的某个构造器，可以通过super（参数列表）显式调用
* super（）在使用时，需要放在构造器的第一行，且只能放在构造器中使用
* super（）和this（)都只能放在构造器的第一行，因此无法共存在一个构造器中

java中所有类都是Objece类的子类，Object类是所有类的基类（父类）
父类构造器的调用不限于直接的父类，将会一直往上追溯到Object类（顶级父类）

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/b57017ee-630b-486e-8e6e-bf825f5590c5)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/0f1537b6-9dfd-42f3-b0d6-73dd3848d1a9)
单继承机制，只能一个父类；如果想继承C,可以先让B继承C,A就继承到了C.



---

**继承的本质**
==>逐层向上的查找关系

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/8253e05a-7782-4569-950e-3eb2e20d9c19)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/d8a54071-8057-4df1-8aba-cb43aa7f3c23)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/885d5aad-7cbf-4d3b-b77e-8ee8782692fc)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/03b44d8b-abb5-45a7-bd8e-9d1283183de7)

关键：
不要忘记了所有的构造器都有默认的super（）
super（"hhh")显示调用，并传参



---

**supper关键字**
两个用途：
* 构造器中super()
* 通过super调用父类的属性 和 方法

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/8882828e-ae8d-4be2-925f-0cf4cc377530)

 调用父类的构造器：当使用super()时，它必须是子类构造器中的第一条语句。这样做是为了确保在子类对象实例化过程中，父类的构造器首先被调用，以正确初始化继承自父类的属性。如果子类的构造器没有显式调用super()，编译器将自动插入一个无参的super()调用，前提是父类有一个无参构造器。

访问父类的成员（属性和方法）：在子类的任何方法（包括构造器）内，可以使用super.属性或super.方法名()的形式访问父类的属性和方法。这在以下几种情况下特别有用：

当子类需要覆盖（Override）父类的方法，但在新方法中仍然想要调用父类中被覆盖的方法。
当子类的字段隐藏（Hide）了父类的同名字段，但需要访问父类中被隐藏的字段。
因此，super()用于构造器中调用父类的构造器，且必须是第一行代码；而super.属性或super.方法()可用于子类的任何其他方法中调用父类的成员，不受位置限制。


为什么需要super 访问父类的方法和属性？

类中 方法调用的逻辑
* 直接调用：先在本类中寻找，如果有就调用；没有依次向父类中查找
* this.call(): 逻辑同直接调用 call（）
* super.call(): 直接在父类中查找，没有依次向上父类查找

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/99f61253-43a4-4a3d-b5ff-afe5ed1bbafc)


属性的访问逻辑：
* 直接写属性名：先在本类中查找属性，如果有直接访问；没有访问父类，向父类查找
* 通过this.属性名：同上直接访问
* 通过super.属性名：直接访问父类，其余规则一致

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/f0a4ec95-1f48-4a76-9416-26d7ff77e433)

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/0b46fbb9-cbe1-4914-a15f-908eda408be1)

本质：继承的本质==>向上查找，以及通过super.[属性/方法] 访问直接访问父类

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/8162ddb8-6dcf-4647-810d-d3dba70c3535)

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/4124b9c7-c4dc-4c66-acaa-207c32daec5f)


---

**方法的重写/覆盖override**

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/cf223d3c-2710-4fb7-ba51-1ef91999e0d6)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/d099f195-02c2-431f-82cc-c406c34f221e)

注意：
* 方法三要素一定要相同才是方法重写：返回值类型、名称、参数列表
* 返回类型可以是父类的子类，但是不能是父类；比如父类是object，子类可以是String
* 访问权限不能变小
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/d2b06b2d-5f0d-4103-ab74-f38b3acf2bb8)

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/00400d64-8f39-4483-b913-763d751544ad)


---

**多态polymorphic**
方法和对象具有多种形态，是面向对象的第三大特征，多态是建立在封装和继承基础之上的。
why?
当类越来越多时，传统方法，代码复用性不高，且不利于维护

1. 方法的多态：
    （方法的重写和重载就体现了多态）
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/fcd702b7-b20c-41d9-b78a-3191922e3cc4)

2.对象的多态

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/4078d508-d36f-4f47-ab00-ed073a4d557e)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/3070de66-248e-4c8b-9479-13801abea6f4)

 
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/2b82db2e-93c7-48f7-8391-bf553252c3c3)
**向上转型：**
本质：父类的引用指向了子类的对象
Animal animal = new Dog();    //animal 编译类型就是Animal，运行类型就是Dog
animal.cry()；   //运行时，执行的是子类的cry（），因为animal的运行类型就是Dog，所以cry就是Dog的cry  

 **向上转型的规则**
* 可以调用父类的所有方法（遵循访问权限）
* 但不能调用子类特有的成员
* 因为在编译阶段，能调用哪些成员是由编译类型决定的。（此时编译类型是父类，而子类特有的成员父类没有）
* 最终的运行效果看子类（运行）的具体实现，运行时，运行类型则是子类，即调用方法时，按照子类开始查找方法（即有可能子类重写了父类的方法，所以实现会不同）

```






```

**多态的向下转型**

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/8e910072-8f38-475d-a6ca-149bdd21e614)
 
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/173d9bb0-8420-442b-b4b1-c9122390a575)


**属性重写问题**
* 注意：属性区别于方法，属性没有重写
* 值，直接看编译类型，从编译类型处查找

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/db9e2168-8b1d-44ce-9456-fa8415f016cf)

第一个例子向上转型后，base.count 时，此时的编译类型是Base 父类，所以base.count直接从父类查找，即10
第二个例子，不是向上转型,sub.count 遵循属性查找规则，先找本类，有，即20


* instance of
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/f2142dd4-ae84-41d4-9fc8-d5c7be3353d1)


---

练习：
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/15c3bae3-d7ef-4d3e-9350-619d02dbc62d)

注意最后的b.display();  方法运行看运行类型，此时b的运行类型是s，所以执行s的方法，输出的是20

---

**java的动态绑定机制**
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/1cc4b926-b716-46a4-bb2f-b18d7c1794e4)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/33dd2736-e5f3-4157-bbe6-b6e5d115c561)
[详解](https://www.bilibili.com/video/BV1fh411y7R8/?p=315&spm_id_from=pageDriver&vd_source=c3c4a5db9e4d968c67a652118ea87497)

* 方法有动态绑定，方法先到运行类型里去找
* 属性没有动态绑定，属性直接就是看编译类型

**多态的应用2：多态参数**

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/451df40b-85dc-4e6e-ab04-3bb0d09d7c2e)



---

**object类详解**

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/0929bdec-81b5-4186-bce8-8decb243b738)
**equal和 == 的区别**
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/90c3402e-c81f-4600-8a13-7ba9f9640e60)
区别：
*   == 是运算符，既可以判断基本数据类型又可以判断引用数据类型，基本数据类型判断值是否相等，引用则判断地址是不是同一个
* equals 是Object类中的方法，只能判断(对象）引用类型，判断引用地址是否相同； 如果字符串调用equal，则是重写后的equal，则判断内容是否相同。
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/3850f046-7687-4ea4-b200-208a62a04af7)

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/39634941-989b-4d16-a8c6-fa25570a4a4d)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/402d6170-2463-408c-a0fc-ae0885887656)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/40a58883-c530-4355-8313-85aa94304e6d)

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/f16b59b9-3212-44e3-bfec-f35311554088)



---

**Hashcode**
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/7428d619-877a-4fc7-ac4d-e3cd14c99abd)

**toString**
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/e2ae77ff-d577-49d5-a483-da6e00e9fdf6)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/aa77a7a4-63eb-4aa6-8c9e-5ed352dffc38)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/23b976d2-6f70-4cdc-9e6e-9fd7ef94c951)

重写：
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/a034a6c4-8d4f-450b-87d5-3902f2c9e12b)


**finalize**

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/82ca5fc7-0d7a-4d35-9868-498e90736ab6)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/b3f8faa8-c354-4678-9535-e3f4254adf9f)

 
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/37d4afbb-d968-415f-92be-bf3c39bc4b97)


---

**类变量（静态变量）**
最大的特点就是可以被类的所有实例共享。
所有的对象都共享的空间（在堆中单独的空间），都拥有的对象

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/648463c4-8c63-42ab-85ee-d24fdd108143)

* 可以直接通过类名访问
* static 变量是同一个类所有对象共享的
* static类变量，在类加载的时候就生成了
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/02cb7c9a-fd61-4039-93f4-41757e1e9c1f)

访问： 
 类名.类变量名（推荐）
或者：对象名.类变量名

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/e42064c6-1065-4094-9c51-1152fd2c1786)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/207ea239-25eb-4426-a2d6-0392a170ae41)



---

**类方法（静态方法）**

类的方法，可被所有的成员对象共享、调用；
* 注意：静态方法只能访问 静态成员；
* 普通方法，既可以访问非静态成员，也可以访问静态成员（变量和方法）


![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/08ab4da1-e8dd-44ab-b079-57d335cf793a)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/9cbc263c-10ab-47f9-b0b2-b23c6bd6b26f)

类方法的经典使用场景：
* 如果我们希望不创建实例，也可以调用某种方法时。比如某些工具类，比如Math中的各种方法均是static
* 在开发中，某些通用的方法，比如打印一维数组，冒泡排序等

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/e2184fd4-c193-4b2a-98a2-4d9e4f3dc3d5)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/03955bcc-3372-4e0e-beaa-34b5165fe2f7)

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/7473efc2-20c9-40b3-a519-2571ed933d2b)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/87109b91-1a4f-497e-b7f3-b6a04ceac0d5)


---

**main方法**

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/ea72ee28-78e5-4088-bb08-40490445987f)
* 1.java虚拟机调用的main方法
* 2.args参数，在执行的时候传入的


![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/c58b023e-2b05-4770-a4eb-67f91a758a87)


---

**代码块**
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/7b4c94ab-5590-427c-82a0-66ba12926445)

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/a00a5bb7-3636-4a73-bad0-a7ef3c07bd3d)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/6a0bb9a1-541e-4ccf-a7ef-849c0ce0f6b2)

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/009f6c30-3b02-46ce-9d9e-4917d8c9f65b)

补充细节：静态代码块与普通代码块
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/a10104a7-0b3f-4056-9ed4-6edcff535958)

当同时有静态属性初始化和静态代码块时：
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/d6d70120-4462-40a7-b79b-d8f48f0b050f)

注意：构造器是最后执行的

当涉及继承时:  构造器内默认隐藏的两步：
* super
* 本类的普通代码块
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/70cf8b55-3b20-436b-8379-8d6dfa25232b)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/5598281b-3dbc-49d2-9791-0e644ee88b3d)

综合案例
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/1d3b7af7-5f09-4ba8-a582-0c2180ffcf3f)

1.先加载类
  1.1 加载父类的静态属性以及代码块
  1.2 再加载子类静态属性以及代码块
2.再加载对象
   2.1 执行子类的构造器super（）
       2.2 在执行子类构造器之前，隐藏了父类的super（），以及父类的普通代码块和普通属性的初始化操作，的执行
    2.3 执行完2.2，相当于执行完了子类super之前的隐藏的东西，现在 执行子类的普通代码块以及普通属性的初始化（看代码顺序了）
  2.4 再执行完子类构造器中的剩余内容

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/7f8ee305-d083-4f7f-8c49-a02f7167a7ca)


练习题：
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/77b6950b-b437-4449-b5a5-3994f5d3c497)

注意：z在类调用时，完成静态属性和静态 代码块的加载；同时，静态代码块只执行一次；

---

**单例设计模式**

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/cce07051-057d-4c90-9430-34a0c158a721)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/27eab9d8-e404-4bb7-9fd7-10093a976058)


---

**final**  -- 常量
当不希望类被继承、或者方法被重写时
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/8df06c60-084e-4447-a078-cd7457223754)

赋值的地方有三个：
* 定义时
* 构造器中
* 代码块中

如果final修饰的属性是静态的，则初始化的位置只能是：
1.在定义时
2.在静态代码块中

不能在构造器中（因为此时static加载是在类时，而构造器则是在实例化的时候）
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/8007172e-2275-4bdc-8cdd-5d794f1127c4)


当只想要某个值，但是不需要类加载时，可以同时使用final和static
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/44c4d5a1-41f5-492f-b0c7-aad925dd7950)



---

**抽象类**
当父类有方法，但是暂时不确定时。

抽象方法，就是没有实现的方法，即没有方法体的方法
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/bec46b0b-438e-4290-8d20-aff6b3ebb5c4)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/9e8ad7dd-f16e-4bdd-89c2-1117ee791bf4)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/f6f9c72a-d271-46d7-a053-ea308abab1fb)


```
public abstract void eat()
```

细节：
* 抽象类无法被实例
* 抽象类不一定含有抽象方法，抽象方法一定必须声明抽象类
* 抽象类中可以有其它方法，不一定有抽象方法
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/6c8694e7-7635-4c9b-8b4f-ccc2b39ea6ad)

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/d85a7196-a2c3-495e-8399-c0a59f991d66)




---

**接口**
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/4bc0e144-d834-468b-8277-17863c2961ea)
在接口中抽象方法可以省略abstract

interface中可以写属性以及方法，方法只能有以下三种：
* 抽象方法
* 默认实现方法（前面需要加default）
* 静态方法

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/dd6bfe2a-170c-432c-afef-c95684ea6958)



---

**内部类**
属性、方法、构造器、代码块、内部类
嵌套在一个类中的类，被称为内部类。

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/e30a9636-b73b-4b7c-b79b-b71038c614ab)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/cfa4ab42-d249-4759-b764-fc94cacb79f1)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/7e3472e7-8487-40fc-a94b-33571b07433e)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/183277cd-d688-4ed5-a425-8bb532b44ab3)

内部类分为四类：
* 局部内部类
* 
 
1.局部内部类定义在方法中/代码块中
2.作用域在方法体里或代码中【也就是说内部类，只能在方法体中使用】
3.本质仍然是一个类 
4.可以访问外部类的所有成员，包括私有的

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/247c4e69-6b76-487a-bc93-32ee58003a5d)


**匿名内部类**

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/686d7fc5-e268-4c01-bf27-1a4e153050b3)
* 本质还是类
* 是一个内部的类
* 该类没有名字（其实有名字，但是看不到，是系统给分配的)
* 同时还是一个对象

WHY?
什么时候会需要以及产生内部类？
==>  匿名内部类是用来简化开发的，匿名其实是系统自动分配一个用户看不到的名字的内部类，用来实例化

使用场景：基于接口的内部类
1.当我们想实现一个接口的方法，但不想创建一个新的类时，
```
IA tiger =new IA(){  // 注意：这里的编译类型是IA 接口， 运行类似就是**匿名内部类**，
此时是编译器自动执行的。
 new ==>jdk底层在创建匿名内部类的时候，也同时创建了实例，并且把实例返回给了tiger
@Overwride
//实现接口的方法
}
```
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/436ffd5f-d59c-458a-85b3-ce3b143d25b4)

2.基于类的匿名内部类
即原来有一个类，如果要继承之后重写，需要新建一个类，现在可以直接使用匿名的内部类来实现
如何写？

原来new一个对象，只需要
Father father = new Father();
就可以，如何使用匿名内部类，则需要：
Father father = new Father(){};     //  注意，多了对象的{}，如果是抽象的父类，就需要重写抽象方法了

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/65fb0567-71d6-47d7-bef2-a38849661800)


匿名内部类的最佳实践：
当作实参直接传递
代码简洁高效
