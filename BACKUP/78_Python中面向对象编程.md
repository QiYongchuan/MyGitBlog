# [Python中面向对象编程](https://github.com/QiYongchuan/MyGitBlog/issues/78)

### Python中的面向对象

```
class Point():
  def __init__(self,input1,input2):
      self.x = input1
      self.y = input2


p = Point(2,8)

print(p)
print(p.x)
print(p.y)


class Flight():
   def __init__(self,capacity):
      self.capacity = capacity
      self.passagers = []

   def add_passagers(self,name):
      if not self.open_seats():
        return False
      self.passagers.append(name)
      return True 
   def open_seats(self):
      return self.capacity - len(self.passagers)
   
flight = Flight(3)

print(f"openseats is {flight.open_seats}")


names = ["harry","Ron","heri","Ginny"]

for person in names:
   success = flight.add_passagers(person)
   if success:
      print(f"successful add {person} in flight")
else:
      print(f"{person} is not add in flight")
```

面向对象：

概念：
>  * 类是对对象的抽象描述，对象是类的实例化。
> * 类定义了对象应该具有的属性和行为。

> 在面向对象编程中，类和对象之间的关系可以描述为类是对象的模板或蓝图，而对象是类的实例化。类是对一类对象的抽象描述，定义了对象应该具有的属性和行为。而对象则是类的具体实例，具体表现出类所定义的特征和行为。类可以看作是对象的集合，而对象是类的实例。对象是类的具体实例，而类则定义了对象的共同特征和行为。

扩展：
在面向对象编程中，如何通过类和对象的关系实现代码的重用和模块化？

在面向对象编程中，通过类和对象的关系可以实现代码的重用和模块化。具体来说，可以通过以下方式实现：

1. 类的定义和实例化：首先，定义一个类，该类包含了一组属性和方法，描述了某一类对象的特征和行为。然后，通过实例化该类，创建具体的对象，这样就可以重用类中定义的属性和方法。

2. 继承：通过继承，一个类可以从另一个类继承属性和方法。这样，子类就可以重用父类的代码，并且可以在此基础上进行扩展和修改，实现代码的重用和模块化。

3. 多态：多态允许不同类的对象对同一消息做出响应，这样就可以使用统一的接口来操作不同类的对象，从而实现代码的模块化和灵活性。

通过这些方式，可以将代码组织成模块化的结构，实现代码的重用和扩展。这种面向对象的设计方法有助于提高代码的可维护性和可扩展性，同时也提高了代码的复用程度。

代码实例：类的继承和多态的例子

```
# 定义一个动物类
class Animal:
    def __init__(self, name):
        self.name = name

    def make_sound(self):
        pass

# 定义一个狗类，继承自动物类
class Dog(Animal):
    def make_sound(self):
        print("汪汪汪！")

# 定义一个猫类，继承自动物类
class Cat(Animal):
    def make_sound(self):
        print("喵喵喵！")

# 多态的应用
def animal_make_sound(animal):
    animal.make_sound()

# 创建一个狗对象和一个猫对象
dog = Dog("旺财")
cat = Cat("咪咪")

# 调用多态的函数，传入不同的动物对象
animal_make_sound(dog)  # 输出：汪汪汪！
animal_make_sound(cat)  # 输出：喵喵喵！

在这个例子中，Animal类是一个基类，定义了动物的基本特征和行为。然后，Dog类和Cat类分别继承了Animal类，重写了make_sound方法，实现了多态。最后，通过animal_make_sound函数，传入不同的动物对象，实现了对不同动物对象的统一操作。

```