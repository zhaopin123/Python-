#03-认识列表
1.什么是列表（list）
列表是python内置的可变并且有序的容器类的数据类型（序列）
有序：说明可以通过下标获取元素
可变;列表中元素的个数、元素的值以及元素的位置可变

2.列表的字面量：中括号括起来，有多个元素，用逗号隔开
[元素1，元素2，元素3.....]

元素：可以是任何数据类型的数据，同一个列表，不同元素的类型可以不一样

```
list1 = [10,20,'sd',[2,4]]
print(list1)

# 空列表
list2 = []
print(list2,type(list2))

# 保存一个班学生成绩
scores = [47,98,87,76,89]
```

##1.查（获取列表的元素）

a.获取单个元素
列表[下标]-获取指定下标对应的元素

列表一旦确定，列表中的每一个 元素都对应一个下标；
下标范围：0~列表长度-1；-1~-列表长度
下标不能越界
```
films = ['战狼','沉默的羔羊',4,6,8,9]
print(films[1])
```

b.获取多个元素（切片）-结果是列表
列表[开始下标：结束下标：步长]
列表[开始下标：结束下标]
```
print(films[1:5:2])
print(films[::-1])
```

c.遍历列表（将元素一个一个取出来）

```
names = ['小明','小黄','小花','小红']
#1.直接获取列表元素
for item in names:
    print(item)
#2.通过遍历下标获取元素
for index in range(len(names)):
    print(names[index])
```
##2.增（添加元素）

a.list1.append(元素)-在列表最后添加指定元素
```
films = ['战狼','沉默的羔羊',4,6,8,9]
films.append(89)
print(films)
```
```
#录入学生成绩。保存到列表
scores = []
score = input('请输入成绩:')
while score != 'end':
    scores.append(score)
    score = input('请输入成绩:')
print(scores)
```

b.列表.insert(下标，元素)-在指定的下标前插入指定的元素
```
films = ['海贼王','一人之下','火影忍者',384,6,43]
films.insert(2,'一拳超人')
print(films)
```
有一个有序序列[1,7,34,67,100].输入有个数字插入到数列中，
 要求插入后还是从小到大排
```
list1 = [1,7,34,67,100]
num = int(input('请输入：'))
for index in range(len(list1)):
    if list1[index] >= num:
        list1.insert(index,num)
        break
else:
    list1.append(num)

print(list1)
```
##3.删（删除列表元素）

a.del 列表【下标】- 删除列表中指定下标对应的元素
del - 关键字，可以删除任何内容

```
films = ['海贼王','一人之下','火影忍者',384,6,43]
del films[-2]
print(films)
```

b.列表.remove(元素) - 删除列表中指定的元素

注意：如果指定元素有多个，只删除最前面那一个
```
films.remove(43)
print(films)
```
3.列表.pop() - 取出列表中最后一个元素
列表.pop(下标) - 取出下标对应的元素
```
nums = [1,2,3,4,5,6,7,8]
del_num = nums.pop(2)
print(del_num)
print(nums)
```
有一个列表，有数字和字符串，要求将字符串全部放到另一个列表中
```
list1 = [1,'ab',303,'hello',89,9,90]
list2 = []
for n in list1:
    if isinstance(n,str):
        list2.append(n)
        list1.remove(n)
print(list1,list2)
```
## 4.改（修改列表元素的值）

列表[下标] = 新值 - 修改指定下标对应的元素为指定的值
```
list1 = [1,2,'ac',4]
list1[2] = 3
print(list1)
```
1.+

列表1 + 列表2 -将两个列表元素取出产生一个新列表

```
list1 = [2,5,4]
list2 = [568,5]
print(list1 + list2)
```
2. *

列表 * n(正整数) - 将列表中的元素重复n次，产生新列表
```
print(list1 * 3)
```
3. in 和 not in

元素 in 列表 - 判断指定元素是否在列表中

```
names = ['小明','路飞','小花']
if '路飞' in names:
    print('中奖')
```
4.

len(列表) - 获取元素个数


## 5.list

list(数据)-将其他数据转换成列表

注意：数据只能是序列
```
str1 = 'dueeu'
print(list(str1))
print(list(range(10,20)))
```
##6.max/min

max(列表) - 获取最大值
min(列表)-获取最小值
```
print(max([1,5,9,6]))
print(min(8,5,6))
```


