#02-列表相关方法
##1.- 列表赋值

a.直接使用一个列表变量给另一个列表赋值，赋的是地址。
 赋值完之后，对其中一个列表进行操作，会影响另一个列表
b.如果赋值的时候使用切片或拷贝赋值，会产生新地址，使用新的地址赋值，
赋值之后，两个列表之间互不影响

现象1
```
list1 = [1,2,3]
list2 = list1
list2.append(100)
print(list1)#[1,2,3,100]
```

现象2
```
list1 = [1,2,3]
list2 = list1[:]
list2.append(100)
print(list1)#[1,2,3]
```

##2.列表中的方法

1.list.count(元素)-获取指定元素在列表中出现的次数
```
numbers = [1,54,6,8,6,2,6,4,6]
print(numbers.count(6))#4
```

2.list.extend(序列)-将序列中所有元素都添加到列表中
```
numbers.extend([34,57,8])
print(numbers)
```

3.list.index(元素)-获取指定元素对应的下标

注意：a.如果有多个，获取第一个
      b.元素不存在会报错
```
numbers = [1,2,3,4,5,3,5]
print(numbers.index(3))#2
#print(numbers.index(35))#ValueError: 35 is not in list
```

4.list.revers()-反向列表。倒叙
```
numbers = [1,5,8,65,4,2,4,5,6]
numbers.reverse()
print(numbers)
```

5.list.sort()-对列表升序排序
list.sort(revers=Ture)-降序

注意：1.列表元素类型一样  2.支持比较运算符
```
numbers = [1,5,8,65,4,2,4,5,6]
numbers.sort()
print(numbers)

numbers = [1,5,8,65,4,2,4,5,6]
numbers.sort(reverse=True)
print(numbers)
```

6.list.clear()-清空列表

注意：清空列表尽量用clear()
```
numbers = [1,5,8,65,4,2,4,5,6]
numbers.clear()
print(numbers)
```

7.list.copy()-将列表直接赋值产生一个新的列表。和列表切片一样
注意：这是浅拷贝
```
list1 = [1,5,8,65,4,2,4,5,6]
list2 = list1.copy()
print(list2)
```
#03-深拷贝和浅拷贝

import copy

copy.copy(对象)-浅拷贝(直接拷贝元素的值产生一个新地址)
copy.deepcopy(对象)-深拷贝（不会直接复制地址而是将地址对应的值复制产生新地址）
```
numbers1 = [1,2,3]
numbers2 = [10,20,30]
list1 = []
```
#04-元组

1.什么是元祖
元组就是不可变的列表。（有序，不可变）
有序 - 可以通过下标获取元素
不可变 - 不支持增、删、改

2.元组的字面量：通过小括号将多个元素括起来，元素之间用逗号隔开
a.只有一个元素的元组：在元素后面必须加一个逗号
b.直接将多个数据用逗号隔开，不用括号，还是表示元组
```
tuple1 = (1,True,'de',[2,3])
print(tuple1)
```
 a.
```
tuple2 = (10,)
print(tuple2)
```
b.
```
tuple3 = 1,5,'jj',9
print(tuple3)
```
c.
```
tuple4 = (10,20)
print(tuple4[1],tuple4[-2])

可以通过变量变量个数个元组个数一样来获取元组元素
x,y = tuple4
print(x,y)
```
通过在变量名前加*，获取没有*的变量获取到的元素剩下的部分，以列表形式返回
```
tuple5 = ('余婷',89,56,89,98,58)
name,*scores = tuple5
print(name,scores)  #余婷 [89, 56, 89, 98, 58]

*name,scores = tuple5
print(name,scores)#['余婷', 89, 56, 89, 98] 58
```
```
tuple1 = 1,2,3
list1 = ['aa','ed']
print(*list1)
print(*tuple1)

```
3.获取元组元素和列表一样



相关运算
+ ，*，in，not in，len(),max(),min(),tuple()



5.列表相关方法：只有列表中的count和index

#05-认识字典

1.什么是字典：
字典是可变，无序的容器类数据类型。字典的元素是键值对

2.字典的字面量：使用大括号括起来，大括号中是键值对，
多个键值对用逗号隔开
键值对：键 ：值
键 （key）- 不可变的，唯一的，一般使用字符串作为key
值 (value)- 任何类型的数据
```
dict1 = {'a':100,10:52,(10,30):'kj'}
print(dict1)
```
列表和字典不能作为key
```
#key是唯一的
dict2 = {'a':100,'a':200,'b':300}
print(dict2)#{'a': 200, 'b': 300}
```

什么时候用字典
如果要存储不同意义的数据，就使用字典
```
student = {'name':'小明','age':28,'tel':12248,'score':30}
print(student['name'])
```
#06-字典的增删改查

##1.获取字典的值

a.获取单个值
dict1[key]- 获取字典中key的值(如果key不存在会报错)
dict1.get(key)-获取字典中key的值(如果key不存在，不会报错并返回none)
None是关键字，表示没有、空的意思
```
dog1 = {'name':'旺财','age':3,'color':'黄色'}
print(dog1['name'])
print(dog1['color'])
print(dog1.get('age'))
```

a.遍历

直接遍历字典拿到的是所有的key
```
for x in dog1:
    print(x,dog1[x])
```
同时获取key和value（不建议用，性能差，内存消耗多）
```
for key,value in dog1.items():
    print(key,value)
```
##2.增（添加键值对）

dict1[key] = 值 - 当key不存在时，在字典中添加键值对
```
dict1= {'a':100}
dict1['b'] = 200
print(dict1)
```

dict1.update(序列) - 将序列中的元素转换成键值对，然后添加到字典中

注意：序列要求是能转成字典的序列，序列元素是只有两个元素的子序列
```
dict1 = {'a': 100, 'b': 200}
#当key有重名的时候，会更新原字典的key对应的值
dict1.update({'aa':56,'bb':60})
print(dict1)

dict1.update([[1,2],['a',2],(2,5)])
print(dict1)
```
##3.改（修改key的值）

dict1[key] = 值- 当key存在就修改key的值
```
dict1 = {'a': 100, 'b': 200}
dict1['a'] = 10
print(dict1)
```
## 4.删（删除键值对）

a.del dict1[key] - 删除key对应的键值对
```
person = {'name':'张三','age':30,'sex':'男'}
del person['sex']
print(person)
```
b.字典.pop(key)-取出key对应的键值对

```
person = {'name':'张三','age':30,'sex':'男'}
person.pop('age')
print(person,'age')

person = {'name':'张三','age':30,'sex':'男'}
# 取出最后一个键值对，以元组形式返回
person.popitem()
print(person)
```
#07-字典的运算和方法

1.字典不支持+和*
#1.in和not in
key in dict1 - 判断字典中是否存在指定的key
```
dict1 = {'a':2,'b':5,'c':8}
print(dict1)
```
