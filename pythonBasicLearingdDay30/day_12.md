
# 02-.编程思想

##1.面向过程编程 - 逻辑、算法
遇到问题考虑直接把逻辑思维转换成代码解决问题

##2.函数式编程 - 函数
遇到问题就考虑是否有一个这种功能的函数

##3.面向对象编程 - 类和对象
遇到问题就考虑是否有一个对象能帮我解决这个问题



## 2.类和对象

1.定义：
类：就是有相同属性和功能的对象的集合（抽象的）
对象：类的实例（具体的）

#03-类的声明

 类：就是有相同属性和功能的对象的集合（抽象的）
 对象：类的实例（具体的）

## 1.类的声明

语法：
class 类名（父类列表）：
    类的内容

说明：
class - 声明类的关键字
类名 - 标识符，不能是关键字（要求）；
       采用驼峰式命名，并且首字母大写；
      见名知义
（父类列表） - 继承语法；可以省略，省略时相当于（objct）
类的内容 - 主要包含类的属性和方法


驼峰式命名：多个单词时，单词首字母大写来区分不同单词
            studentName
方法：声明在类中的函数就是方法

## 2.类的属性和方法
属性-指的是在类中声明的变量；分为类的字段和对象属性
方法 - 指的是类中声明的函数，分三种：对象方法、类方法、静态方法
```
#声明一个Person类
class Person:
    """人类"""
    num = 61#属性
    def eat(self):#方法
        print('人在吃饭')
```
 Person是类（类就是类型）

##3.创建对象
类名（） --> 创建类对应的对象
```
# 创建Person类的对象xiao_ming
xiao_ming = Person()
print(xiao_ming)
```

#04-对象方法

##1.什么是对象方法
直接声明在类中的并且自带一个叫self的参数的函数，

##2.对象方法的调用- 通过对象调用对象方法
对象.对象方法（）

##3.self(当前对象)
通过对象调用对象方法的时候，对象方法中的第一个参数不用传参，
系统会自动将当前对象传给self
哪个对象调用的，self就是谁

注意：当前类的对象能做的事，self都能做
```
class Person:
    """人类"""
    def sleep(self):
        #self = p1
        print('睡觉')
        self.run()

    def run(self):
        print('跑')

# 创建Person对象
p1 = Person()
p1.sleep()

```
#05-init方法和构造方法

0.魔法方法
Python类中由__开头并且__结尾的方法。魔法方法不需要调用，都是自动调用

##1.__init__方法
是对象方法
不需要自己调用，会被自动调用
一般用来对对象进行初始化的

##2.构造方法
函数名和类名一样的方法就是构造方法
当我们创建类的时候，系统会自动创建这个类的构造方法，用来创建对象
通过构造方法创建对象的时候，系统会自动调用init方法开队创建好的对象就行初始化

注意：当init方法中如果除了self以外需要别的参数，那么这些参数需要构造方法来传参
     只要调用构造方法，就会产生新的对象（想要对象，调用构造方法）

```
class Person:
    def __init__(self):
        print('init')
```

#06-对象属性

##1.什么是对象属性
声明在init函数中的变量
self.属性名 = 值
通过对象使用：对象.属性

语法：
self.变量名 = 值

说明：变量名就是属性名，变量就是对象属性


##2.什么样的属性应该声明成对象属性
如果属性的值会因为对象不一样而不一样，那么就声明成对象属性，否则就声明成类的字段


 1.所有对象属性创建时都使用一个默认值
```
class   Person:
    def __init__(self):
        # name /age 就是Person类的对象属性
        self.name = '张三'
        self.age  = 0
 # 创建对象
p1 = Person()
p2 = Person()

# 使用对象属性
p1.name = '李四'
p2.name = '123'
print(p1.name,p2.name)
```
 2.创建对象的时候就决定对象的值
```
class   Person:
    def __init__(self,name1,age1 = 1):
        # name /age 就是Person类的对象属性
        self.name = name1
        self.age  = age1

p1 = Person('小明')
p2 = Person('小红')
print(p1.name,p2.name)

p1.name = 'laowang'
print(p1.name)
```

声明一个矩形类
```
class Rect:
    def __init__(self,len,wide):
        self.len = len
        self.wide = wide
    # 一个对象方法需不需要除了self以外的其他参数，
    # 看实现这个函数的功能需不需要其他除了属性以外的数据
    def area(self):
        return self.len *self.wide

p11 = Rect(2,5)
print(p11.area())
```
```
 声明一个point类，拥有属性x坐标和y坐标,功能：求两个点的距离
class Point:
    def __init__(self,x,y):
        self.x = x
        self.y = y

    def distans(self,other):
        return (self.x - other.x)**2 + (self.y - other.y)**2

p13 = Point(0,0)
p23 = Point(3,5)
print(p13.distans(p23))

```
#07-对象属性的增删改查
```
class Dog:
    def __init__(self,name,color,type):
        self.name = name
        self.color = color
        self.type = type
dog1 = Dog('旺财','huangse','erha')
```

## 1.查（获取指定对象指定属性的值）

获取指定对象指定属性的值
1.对象.属性 - 属性不存在报错
2.getattr(对象，属性名，默认值)- 属性不存在，返回默认值


```
print(dog1.name)
print(getattr(dog1,'color'))
print(getattr(dog1,'name','caicai'))
```
## 2.增、改

1.对象.属性 = 值
2.setattr(对象，属性名，值)
注意：属性存在时修改属性的值，不存在时添加属性

```
dog1.name = '大黄'
print(dog1.name)

setattr(dog1,'name','热狗')
print(dog1.name)
setattr(dog1,'name1','狗')
print(dog1.name1)
```
## 3.删除

1.del 对象.属性
2.delattr(对象，属性名)
```
del dog1.name1
# print(dog1.name1)
delattr(dog1,'name')
```

注意：对象属性的增删改查，都是针对指定的那个对象，对其他对象无影响


## 4.__slots__

__slots__ - 用来约束当前这个类有哪些属性
```
class Stu:
    __slots__= ('name','age','sex')

    def __init__(self,name):
        self.name=name

```
#08-类的字段和内置类属性

##1.类的字段

直接声明在类里面函数的外面的变量就是类的字段
类的字段需要通过类来使用: 类.字段 - 不管是类里面还是外面都一样

不会因为对象不同而不一样的数据就是类的字段

class Person:
    # 声明字段 number
```
    number = 61

print(Person.number)
```
## 2.内置类属性

内置属性就是类声明的时候，类中已经声明好的属性（包括类的字段和对象的属性）
```
class Dog:
    """sudcuweb"""
    type = '犬科'


    def __init__(self,name='',age='',color=''):
        self.name = name
        self.age = age
        self.color = color
```
##   l类方法
```
    @classmethod
    def shout(cls):
        print('汪汪汪')
```
##     静态方法
```
    @staticmethod
    def bite():
        print('dshc')


dog1 = Dog('小黑',3,'黑色')
```
### __name__

类.__name__ - 获取类的名字（字符串）
```
class_name = Person.__name__
print(class_name)
```
### __class__

对象.__class__ - 获取对象对应的类（结果是一个类，原来类能做的它都能做）
```
aa = Dog.__class__
print(Dog.__class__,aa)
```
### 3.__dict__

类.__dict__ - 获取当前类的所有的类的字段及其对应的值
(重点)对象.__dict__ - 将当前对象所有属性及其值转换成字典
`
print(dog1.__dict__)#{'name': '小黑', 'age': 3, 'color': '黑色'}
`
### 4.__base__

类.__bases__ - 获取当前类的父类（以元组形式返回，元组中元素就是父类）
`
print(Dog.__bases__)
`
### 5.__module__
 类.__module__ - 获取当前类所在模块的模块名
`
print(Dog.__module__)
`
### 6.__doc__

类.__doc__  - 获取当前类的说明文档
`
print(Dog.__doc__)
`













2.从生活来看类和对象
如果人是类，余大大就是一个对象
如果电脑是一个类，具体de某个电脑就是一个对象

"""