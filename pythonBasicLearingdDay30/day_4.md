#02-分支结构
"""
python中分支结构只有if语句，没有switch

"""
##1.if语句
"""
a.语法
if 条件语句：
    代码段
    
b.说明：
if - 关键字
条件语句 - 任何有结果的表达式（不管结果是什么都可以）
： - 固定写法
代码段 - 和if保持一个缩进的一条或多条语句。

c.执行过程
先判断条件语句结果是否为真，如果为真就执行：后面代码段
否则不执行
注意：如果条件语句结果不是布尔，会先转成布尔再判断
    
"""
1. if后面可以写哪些语句（除了赋值语句都可以）
```
if 10:
    print('条件语句是10')

if 'abd':
    print('条件语句是abc')

if 10 > 20:
    print('条件语句是10 > 20')

# if num = 10:
num = 10
if num & 1 == 0:
    print('%d是偶数' % (num))
```
```
随机产生一个年龄值，大于是十八打印成年
import random
age = random.randint(0,100)
print(age)
if age >= 18:
    print("成年")
```
##2.if-else
"""
a.语法
if 条件语句：
    代码段1
else：
    代码段2  
    
b.执行过程
先判断条件语句是否为真，真就执行代码段1，否则执行代码段2
         
"""
```
随机产生一个整数，是奇数就打印XXX是奇数，否则打印XXX是偶数
import random
num = random.randint(0,50)
print(num)
if num & 1 == 1:
    print('%d是奇数' % (num) )
else:
    print('%d是偶数' % (num))
```
##if-elif-else
"""
语法：
if 条件语句1：
   代码段1
elif 条件语句2：
    代码段2   
elif 条件语句3：
    代码段3   
    ...
else：
    代码段4    
    
b.执行过程
先判断条件语句1是否为真，真就执行代码段1；否则判断条件语句2
是否为真，真就执行代码段2；否则判断条件语句3是否为真，
真就执行代码段3，依次类推，如果都为假，就执行else后代码段        

注意：后面判断前提是前面条件不成立
"""
```
#分数小于60不及格，60-90良好，90+优秀
score= random.randint(0,100)
#score=input(int())
print(score)
if score < 60:
    print('不及格')
elif score < 90:
    print('良好')
else:
    print('优秀')
```
##4.if嵌套
```
#如果是偶数打印偶数，否则打印奇数，
#如果偶数能被4整除，再打印4的倍数
print(num)
if num & 1 == 0:
    print('偶数')
    if num % 4 == 0:
        print('能被4整除')
else:
    print('奇数')

#if (type(num >> 2) == int):
 #   print(1)
```
```
str1 = input('请输入：')
if  ('A'<= str1[0] <= 'Z') or ('a'<= str1[0] <= 'z'):
    #str1[0].isalpha()
    print('以字母开头')
    if 'A'<= str1[0] <= 'Z':
        #str1[0].isupper()
        print('以大写字母开头')
else:
    print('不是字母开头')
```
```
trantab = str.maketrans('123','abc','7o')
str1 = '13fddoiS67dh'
print(str1.translate(trantab))
```
#03-for循环
"""
python中循环结构有两种：for循环和while循环

某个操作需要重复执行，就考虑用循环
"""
#1.for循环
"""
语法：
for 变量 in 序列 :
    循环体
    
b.说明：
for 关键字
变量 - 变量名
in - 关键字
序列 - 字符串、列表、元祖、字典、集合、迭代器、range
循环体 - 一条或多条语句（需要重复执行的代码）

c.执行过程：
让变量去序列中一个一个的取值，取完为止，每取一次执行一次循环体
(序列中元素的个数决定了循环的次数)

d.如果取到的值在循环体里不使用，命名时用_命名    
"""
```
for x in 'abc':
    print('===')
```
#2.range
"""
range(n)-产生一个数字序列，序列中内容是0 ~ n-1
range(m,n) - 产生一个数字序列，序列中内容是m ~ n-1
range(m,n,step) - 产生一个数字序列，从m开始，每次加step，直到n前

range一般用在：a需要产生指定范围的数字序列
              b.单纯的控制循环次数
"""
```
for num in range(10):
    print(num)

for num in range(5,10):
    print(num)

for num in range(0,10,2):
    print(num)
```
```
#求1+2+3...+100

sum = 0
for num in range(1,101):
    sum += num
print(sum)
```
```
#2+4+6+...+100

sum = 0
for num in range(0,101,2):
    sum += num
print(sum)
```
```
sum = 0
for num in range(101):
    if num % 2 == 0:
        sum += num
print(sum)
```
```
#统计字符串中数字字符个数
count = 0
str1 = 'sd384h7fb5'
for index in range(len(str1)):
    if '0' <= str1[index] <= '9':
        count += 1
print(count)
```
```
count = 0
for char in str1:
    if '0' <= char <= '9':
        count += 1
print(count)
```
#04-while循环

##1.while循环
"""
a.语法：
while 条件语句：
    循环体

b.说明：
while - 关键字
条件语句 - 有结果的表达式，除了赋值语句
： - 固定写法
循环体 - 一条或多条语句（会被重复执行）

c.执行过程：
先判断条件语句是否为真，真就执行循环体，再判断条件语句是否为真
真又执行循环体，直到条件语句为假，循环结束
"""
```
#1,2,3,...100
num = 1
while num <= 100:
    print(num)
    num += 1
```
```
#1+2+3..+100
sum1 = 1
num = 1
while num <= 10:
    sum1 *= num
    num += 1
print(sum1)
print(num)
```
```
#while循环取字符
str1 = 'abc123'
index = 0
while index < len(str1):
    print(str1[index])
    index += 1
```
##2.for循环和while循环的选择
"""
Python中for循环能做的，while循环都能做，反之不然

使用for循环
1.获取序列中的元素
2.循环次数确定

while循环
1.死循环
2.循环次数不确定时
"""
不断输入内容，直到输入的值为0
```
while num !='0':
    num = input('请输入：')

print('停止')
```
#05-continue和break

##1.continue
"""
continue是关键字，只能在循环中

功能：当循环执行过程中遇到continue，会结束本次循环，进入下次循环的判断
    （for循环就是变量取下一个值，while循环就是直接判断条件语句是否为真）

"""
##2.break
"""
break是一个关键字，只能写在循环体中

功能：循环中遇到break，整个循环结束
"""
##3.else
"""
语法：
while 条件语句
    循环
else：
    代码段
    
for 变量 in 序列：
    循环体
else:    
     代码段
     
执行过程：
else结构不会影响原循环的执行过程，当循环自然结束的时候就会执行else后面的代码段
循环因为遇到break而结束的时候不会执行else后面的代码段            
"""























