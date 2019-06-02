#02-类方法和静态方法

类中方法有三种：对象方法，类方法，静态方法
##1.对象方法
声明在类中
有默认参数self
通过对象调用：对象.对象方法

##2.类方法
在声明前加一个@classmethod
有默认参数cls,调用时不需要给cls传参，系统会自动将调用类方法的类传给cls。
cls最终就是这个类，类可以做的事cls都可以做
通过类去调用：类.类方法（）

##3.静态方法
声明前@staticmethod
没有默认参数
通过类调用：类.静态方法

##4.对三种方法的选择
什么时候使用对象方法：
当实现函数功能需要使用对象属性是就用对象方法

什么时候使用类方法：
实现函数功能不需要使用对象属性，但是需要类的时候就使用类方法

什么时候使用静态方法：
实现函数功能不需要使用对象属性也不需要类的时候就使用静态方法
```
class Person:
    def __init__(self,name):
        self.name = name


    def eat(self,food):
        print('%schhi%s'% self.name,food)


    类方法
    @classmethod
    def destroy(cls):
        print(1)

   静态方法
    @staticmethod
    def hit_animal():
        print('ren')


Person.destroy()
Person.hit_animal()
```

# 声明一个数学类，属性：pi  功能：求圆的面积,qiu 和
```
class Math:
    pi = math.pi
    @classmethod
    def area(cls,r):
        print(cls.pi*(r**2))

    @staticmethod
    def sum1(num1,num2):
        return num1+num2

Math.area(1)
print(Math.sum1(1,5))
```

#03-私有化

##1.私有化指的是
在类中可以通过在属性名前或者方法名前加__(注意：结尾不能加__),那么这个属性或者方法就会变成私有的。
私有的属性和方法在类的外部不能使用
```
class Peerson:
    __num = 100#私有属性
    def __init__(self):
        self.name = 45

    def show(self):
        print('名字',self.name)
```

##2.私有化原理
Python中并没有真正的私有化，不能从访问权限上控制使用
只是在以__开头的名字前加‘_类名’，导致不能通过原名访问


#04-对象属性的getter和setter

如果希望在获取对象属性之前要做点别的事情，就给这个属性添加getter
如果希望在给对象属性赋值之前要做点别的事情，就给这个属性添加setter

##2.给属性添加getter
属性命名的时候，属性名前加_  ; self._age = 0
声明一个函数，函数名是属性名（不要下划线），不需要参数，要一个返回值，并且使用@property修饰。
这个函数的返回值就是获取属性的结果@property
    def age(self):
        return 年龄相关值
当需要获取属性的时候通过对象.不带下划线的属性；如 ：对象.age

##3.给对象属性添加setter
想要给对象属性添加setter，必须先给它添加getter
属性命名的时候，属性名前加_  ; self._age = 0
 声明一个函数，函数名是属性名（不要下划线），需要一个额外参数；
 使用函数前用@getter名.setter修饰
@age.setter
def age(self,value):
    self._age = value

```
class Person:
    def __init__(self,name='li'):
        self.name = name
        self._age = 0
        self.set = 'nan'

    #  这儿的age属性就是属性_age的getter方法
    @property
    def age(self):
        if self._age < 1:
            return 'yiner'
        elif self._age < 18:
            return 'weichengnian'
        else:
            return 'chengnianren'


    @age.setter
    def age(self,value):
        if not isinstance(value,int):
            print('整数')
        if not (0<=value<=100):
            print('错')
        self._age = value

p1 = Person()
# 这儿实质是在调用_age的getter方法
print(p1.age)

# 这儿实质是在调用_age的getter方法:p1.age(23)
p1.age = 23
```
```
class Time:
    def __init__(self):
        self._miao = 0

    @property
    def miao(self):
        return self._miao

    @miao.setter
    def miao(self,time):
        if int(time[0:2]) > 60 or int(time[-2:]) > 60:
            print('错误')
        else:
            t1 = int(time[0:2])*60 + int(time[-2:])
        self._miao = t1
    
       # 打印自己声明的类的对象的时候，默认打印的是：<模块名.类名 object at 对象地址>
       # 如果不希望这样，可以使用__repr__方法，打印对象的时候就会打印这个方法的返回值
         返回值必须是字符串
        
    def __repr__(self):
        return str(self.miao)


t1 = Time()
t1.miao = ('02:23')
print(t1.miao)
```

```
class Person:
    def __init__(self,name='li'):
        self.name = name
        self._age = 0
        self.set = 'nan'

    def  __repr__(self):
        return str(self.__dict__)[1:-1]

p1 = Person()
print(p1)

```
#05-类的继承

##1.继承
python中的类支持继承，并且支持多继承
默认情况下是继承自object（object就是Python中类的基类）

什么是继承：
一个类可以继承另外一个类，继承者叫子类，被继承者叫父类。继承就是让子类直接拥有父类中的内容

可以继承哪些内容
所有属性和方法都可以继承
__slots__对应的值不会被继承
```
class Person:
    num1 = 100
    def __init__(self):
        self.name = '张三'
        self._age = 0
        self.sex = 'nan'

    def c(self):
        return 12

# Stu类继承Person类
class Stu(Person):
    pass


# 学生对象
stu1 = Stu()
# 对象属性,字段，对象方法都可以继承
print(stu1.name,stu1.num1,stu1.c())

```

#06-添加属性和方法


子类除了有父类的属性和方法外，还有自己的属性和方法

##1.在子类中添加方法
添加新的方法
直接在子类中声明其他方法;添加后子类可以用自己和父类的方法，但是父类不能用子类的方法

重写父类的方法：重新实现父类的方法
完全重写 - 覆盖父类的功能- 重新实现父类方法
部分重写，保留父类功能，添加新的功能 - 在子类中实现父类方法的时候通过super调用父类方法，
                                        再添加新的方法
注意：可以在子类的方法中，可以通过super调用父类的任何方法
super（类，对象）- 获取对象中父类的部分（要求对象是指定的类的对象）

类中方法的调用过程
通过类或者对象调用方法的时候，先看当前类中是否声明过这个方法，如果有就直接调用，
如果没有就去找父类，如果父类中也没有，再往上找，直到找到object，如果object中也没有，就会报错

注意：静态方法中不能使用super()
```
class Person:
    num1 = 100
    def __init__(self):
        self.name = '张三'
        self._age = 0
        self.sex = 'nan'

    def show_message(self):
        print(self.name,'你好啊')

class Students(Person):
    def study(self):
        print('xuexi')

    #     保留父类功能，
    def show_message(self):
        super().show_message()
        print('我要去学校')
```


##1.添加字段
直接添加新的字段

##2.添加对象属性
类的对象属性是继承父类的init方法继承下来的

如果想要保留父类的属性并添加新的属性，
需要在子类的init方法中通过super（）去调用父类的init方法

```
class Person:
    num1 = 100
    def __init__(self):
        self.name = '张三'
        self.age = 0
        self.sex = 'nan'


class Stu(Person):
    number = 152
    def __init__(self):
        super().__init__()
        self.stu_id = '101'

stu1 = Stu()
print(stu1.name)
```

 动物类。属性：年龄，颜色，类型，创建对象的时候类型和颜色必须赋值
 猫类，属性：年龄，颜色，类型，爱好，创建对象时颜色必须赋值，类型不能赋值
```
class Animal:
    def __init__(self,color,type,age=0):
        self.color = color
        self.type = type
        self.age = age

class Cat(Animal):
    def __init__(self,color,hobby='',age=0):#数量=父类属性数量+自己属性
        super().__init__(color,'cat',age)
        # self.type = 'cat'
        self.hobby = hobby

c1 = Cat(5)

```










