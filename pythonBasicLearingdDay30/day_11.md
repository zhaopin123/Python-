#02-json数据

##1.什么是json数据：
json是一种数据格式，满足json格式的数据就是json数据。
文件后缀是.json，并且文件中内容满足json格式

##2.json格式：
一个json中只有一个数据，并且这个数据时json支持的数据了类型的数据

json支持的数据类型
数字类型 - 包含所有数字，包括整数小数
字符串 - 使用双引号括起来的字符集，列如：“123” "hghji"
布尔 - true 和 false
数组 - 相当于列表，使用中括号括起来，括号里是json支持的任意类型数据
        列如：[12,"iuyg",true]
字典 - 就是字典，使用{}括起来，使用键值对。键一般是字符串，
        值是json支持的任意类型的数据
特殊值 - null （相当于None），表示空

##3.Python中有一个内置json模块，用来支持对json模块的处理：json
a.将json数据转换成Python数据
b.将Python数据转换成json数据

import json

# 1.将json数据转换成Python数据

loads(字符串)-将json格式的数据转换成Python对应的数据
注意：字符串的内容必须是json格式的数据

json         Python
数字         整型、浮点型
字符串        字符串（双引号会变成单引号）
布尔          布尔（首字母变大写）
数组          列表
字典          字典

```
py1 = json.loads('"absv"')
py2 = json.loads('[1,2,58,"cxei",null,true,{"abc":32}]')
#                [1, 2, 58, 'cxei', None, True, {'abc': 32}]
print(py1,py2)

import json
with open('data.json','r',encoding='utf-8')as f:
    py3 = json.loads(f.read())
    x = py3['data'][2]['age']
    print(x)
```
# 2.将Python数据转换成json数据

dumps(数据)-转换成内容符合json格式的字符串
注意：最终结果都是字符串

Python          json    
整型、浮点型     数字      
字符串          字符串（单引号会变双引号）    
布尔                布尔（大写变小写）
列表、元组          数组      
字典               字典
None               null"
```
js1 = json.dumps([1, 2,(1,5,8,45), 58, 'cxei', None, True, {'abc': 32}])
print(js1)  # [1, 2, [1, 5, 8, 45], 58, "cxei", null, true, {"abc": 32}]
js2 = json.dumps((1,5,7,9,5))#元组括号不能省略
print(js2)

```
添加多个学生信息：姓名年龄、电话，将数据保存到json文件中
 并且上次添加的信息不会删除
list1 = []


# 3.json文件操作相关方法

load(文件对象)- 将文件对象中的数据读出来，并转换成Python对应的数据
                （文件对象中的内容必须是json格式的数据）
dump(数据，文件对象)-将Python数据转成


```
with open('data.json','r',encoding='utf-8')as f:
    py4 = json.load(f)
    print(py4)
with open('data.json', 'w', encoding='utf-8')as f:
    json.dump(py4,f)
```

#03-异常捕获

##1.什么是异常
执行过程中出错，也叫出现异常

##2.异常捕获
让本来会出现异常的位置不出现异常，而是自己去处理异常出现的情况

##3.怎么捕获异常
1.捕获所有异常
语法：
try :
    代码段1
except:
    代码段2

执行过程：执行代码段1，如果代码段1中出现异常，不会崩溃，而是马上执行代码段2.
          如果1没有异常，不会执行2

```
try:
    print([1,2,3,4][4])
except:
    print('出现异常')
```

2.捕获指定异常
语法：
try：
    代码段1
except 错误类型名：
    代码段2
    
执行过程：执行1，当1出现指定类型的异常后执行2
```
print(int('asb'))
try:
    print(int('asb'))
except ValueError:
    print(int('123'))
```


3.同时捕获多个异常，对不同异常做出相同的反应
try：
    代码段1
except（错误类型1，错误类型2，错误类型3....）：
    代码段2

执行过程：执行1，如果出现指定异常，执行代码段2
```
try:
    print(int('nb'))
    print([1,2,5,4][6])

except(SyntaxError,ValueError,KeyError,IndexError,StopIteration,FileExistsError):
    print(123)
```

##4.同时捕获多钟类型，对不同类型做出不同反应
try：
    代码段1
except 错误类型1
    2
except 错误类型3
    3
except 错误类型
    4
    .
    .
    .
except 错误类型n
    n


##5.try-except-finally
try:
    1
except:
    2
finally:
    3
    
不管代码段1是否出现异常也不管异常是否捕获到，finally后面的代码都能执行（一般用于数据保存）


什么时候使用异常捕获：
1.明明知道某段代码可能会出现异常，但无法避免，就使用异常捕获
2.


 封装函数，获取文件中内容
 从封装角度：调用者做的事情越少越好
```
def get_file(file):
    while 1:
        try:
            with open(file,encoding='utf-8')as f:
                content = f.read()
                return content
            break
        except FileExistsError:
            print('地址错误，请重新输入')
x = get_file('a.txt')
print(x)

```
抛出异常：主动让程序出现异常

语法：
raise 错误类型 - 程序执行到raise时直接抛出异常

注意：错误类型必须是一个类，并且是Exception的子类

 输入年龄，如果不在0~100，程序就崩溃
```
x = int(input('输入0~100：'))
if 0 > x or x > 100:
    raise ValueError
```






















