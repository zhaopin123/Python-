#02-变量的作用域

##1.变量的作用域
变量在程序中能使用的范围

###1.全局变量
声明在函数或者类的外部的变量都是全局变量
作用域：（从声明开始到整个py文件结束），任何位置都可以使用

###2.局部变量
声明在函数或者类的内部的变量都是局部变量
作用域：从声明开始都函数结束，任何位置都可以使用
```
a = 10

# x,y都是全局变量
for x in range(10):
    y = 10

print(x,y)

# num1 num2,a,xx都是局部变量
def func1(num1,num2):
    print(num1,num2)
    a = 11
    for xx in range(10):
        print(xx)
```
### 3.global使用

global作用是在函数中声明一个全局变量
global 变量名
变量名 = 值
```
a1 = 100

def test1():
    # a1 = 200
    # print(a1)
    global a1 #说明：全局变量
    global b1#声明全局变量
    b1 = 300
    a1 = 200

test1()
print(a1,b1)#200,300
```
### 4.nonlocal使用

nonlocal关键字只能在函数中使用
当需要在局部的局部中修改变量的值，就是要nonlocal

yufa:
nonlocal 变量名
变量名 = 值
```
def func1():
    a2 = 'abc'

    def func11():
        nonlocal a2
        a2 = 123
        print(a2)
        a3 = 111
    func11()
    print(a2)
func1()

funtion = []
for x in range(5):
    def func1(a):
        return a*x
    funtion.append(func1)

t1 = funtion[0]
t2 = funtion[2]
print(t1(2),t2(2))
 ```
#03-函数作为变量

声明函数就是声明变量，函数名就是变量名

函数名作为变量除了可以用来调用函数以外，普通变量能做的它都能做
```
 #声明类型是dict的变量b
b={}
#声明类型是function类型的变量c
c = lambda x :x*x

#声明类型是function类型的变量d
def d():
    print(1)
```
```
1.让一个变量给另一个变量赋值
list1 = [1,2,5,6]
list2 = list1
```
```
# 声明函数变量func1
def func1():
    print(1)
# 使用函数给f2赋值
f2 = func1
f2()
```
```
2.将变量作为列表元素或者字典的值
list1 =[1,2,5]
# 将list1 作为list2的第一个元素
list2 = [list1,4,5]
print(list2[0][1])
```
```
# 函数变量
def func2():
    print(2)
list2 = [func2,100]
print(list2[0]())
```
 3.作为函数的参数

将函数作为实参传递给函数2，函数2就是高阶函数（实参高阶函数）
声明整型变量a
a = 10
```
def test(x):
    print(3)
 将变量作为实参
test(a)

def func3():
    print(4)

def func4(f):
    print('函数三')

func4(func3())
```
def sort(self, key=None, reverse=False)
key - 确定排序时以什么值为标准来排序，默认情况下以列表元素值大小为标准排序
      需要传一个函数，函数需要一个参数一个返回值，参数是列表元素
reverse - 是否降序排序，默认值是None
 """
 3.1 sort
`
print(max([('z',10),('b',30),('c',20)],key = lambda x:x[1]))
`
 4.变量作为函数返回值

返回值是函数的函数，也叫高阶函数（返回值高阶函数）
```
def test1(n):
    sum1 = 1
    for x in range(1,n+1):
        sum1 *= x
    return sum1
re = test1(5) + 10

def test3(char):
 ``` 
    根据不同符号返回不同功能
    :param char: 运算符符号
    :return: 不同运算符对应功能的函数
  
```
    if char == '+':
        def sum(*args,**kwargs):
            sum1 = 0
            for item in args:
                sum1 += item
            for key in kwargs:
                sum1 += kwargs[key]
            return sum1
        return sum
    elif char == '-':
        def sub(*args):
            sub1 = args[0]
            for x in range(1,len(args)):
                sub1 -= args[x]
            return sub1
        return sub
re = test3('+')
x = re(1,56,89)
print(x)

```
#04-迭代器

##1.什么是迭代器（iter）
迭代器是序列类型，可以同时存储多个数据。取迭代器中数据只能一个一个取，而且取出
来的数据在迭代器中就不存在了

##2.迭代器中那个数据来源
a.将其他序列转换成迭代器
b.使用生成式、生成器去产生数据

### 1.将数据转换成迭代器(所有序列都能转换成迭代器)
```
iter1 = iter('acb')
print(iter1)

iter2 = iter([1,5,3,8,25])
print(iter2)

iter3 = iter({1:2,5:3})
print(iter3)
```
### 2.获取迭代器中的元素

next(迭代器)-取出迭代器中第一个元素（已经取出来的元素再也回不到迭代器中了）
```
print(next(iter1))
print(next(iter1))
print(next(iter1))
# print(next(iter1))#StopIteration 当迭代器为空时，出现异常

print(iter2.__next__())
print(next(iter2))

```
b.通过for循环取出迭代器中的每个元素(再取报错)
```
for x in iter2:
    print(x)
```
#05-生成器

生成器就是迭代器，迭代器不一定是生成器

生成器就是带有yield关键字的函数的结果
调用带有yield的关键字的函数获取到的结果就是生成器，
生成器中的元素就是yield关键字后面的值

只要函数中有yield关键字，调用函数时不会获取返回值，直接创建一个生成器
当获取生成器元素的时候，才会执行函数的函数体，执行到yield语句为止
并将yield后面的值作为结果返回，并且保存当前执行的位置。
获取下一个元素的时候就从上次结束的位置接着往下执行函数，
知道遇到yield或者函数结束为止，如果函数结束就会出现异常

生成器对应的函数，执行遇到yield的次数决定了生成器产生数据的个数
```

def func1():
    print(1)
    yield 100,544
re = func1()
print(re)
# next(re)- 执行re对应的函数体，将yield关键字后面的值作为结果
print(next(re))


def func2():
    for item in range(101):
        yield item

x = func1()
print(next(x))
```
```
# k可以不断产生斐波那契序列1,1,2,3,5,8，
def func3():
    num1 = 0
    num2 = 1
    yield num2
    while 1:
        num1 = num1 + num2
        num2 = num1 + num2
        yield num1
        yield num2
x=func3()
for _ in range(10):
    print(next(x))
```











