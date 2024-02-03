# [python中的数据类型](https://github.com/QiYongchuan/MyGitBlog/issues/79)

### python中的数据结构：

Data stractures

* list - sequences of mutable values   //列表可以改变[]
* tuple - sequence of immutable values //元组不可改变()
* set - collection of unique values    //集合不可以重复()
* dict - collection of key-value pairs  // 字典键值对{}


#### list 列表
```
# define a list of names
names = ["harry","Ron","heri","Ginny"]

```

#### dic 字典
```

# define a dic
houses = {"harry":"Gry","Draco":"Sly"}
houses['Herminoe'] = "Gry"
```

#### tuble 元组
```
coordinateX = 10.0
coordinateY = 20.0

coordinate = (10.0,20,0)

#即相当于直接可以用一个变量来代表两个变量

```

#### set 
```

#create an empty set

s = set() 

# add elements

s.add(1)
s.add(2)
s.add(3)
s.add(4)
s.add(4)

s.remove(1)
print(s)   // 234

```